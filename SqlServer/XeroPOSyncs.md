### Complex JSON to get and insert data into a table

```sql

ALTER PROC dbo.usp_SyncXeroPurchaseOrders
AS

BEGIN


    DECLARE @ProviderId INT,
            @RequestUrl NVARCHAR(MAX) = N'',
            @SupportUserId INT = 3,
            @AzureTenantId NVARCHAR(100) = N'',
            @AccessToken NVARCHAR(MAX) = N'',
            @Headers NVARCHAR(MAX) = N'',
            @ResponseData NVARCHAR(MAX) = N'',
            @SessionId NVARCHAR(50) = NEWID();

    SELECT @ProviderId = CAST(Provider AS INT),
           @AzureTenantId = AzureTenantId
    FROM dbo.AzureAdClientCredentials (NOLOCK)
    WHERE IsAction = 1;


    IF @ProviderId = 3 --'Xero'        
    BEGIN
        BEGIN TRY
            -- Refresh Access token first               

            IF OBJECT_ID('tempdb..#AccessCred') IS NOT NULL
                DROP TABLE #AccessCred;

            CREATE TABLE #AccessCred
            (
                AccessToken NVARCHAR(MAX) NULL,
                RefreshToken NVARCHAR(MAX) NULL,
                ModifiedDate DATETIME NULL
            );

            INSERT INTO #AccessCred
            (
                AccessToken,
                RefreshToken,
                ModifiedDate
            )
            EXEC dbo.usp_GetRefreshOAuthToken @ProviderId = @ProviderId;

            SELECT @AccessToken = AccessToken
            FROM #AccessCred;

            SET @Headers = N'Authorization: Bearer ' + @AccessToken + N';xero-tenant-id:' + @AzureTenantId;
            SET @RequestUrl = N'https://api.xero.com/api.xro/2.0/PurchaseOrders';

            SELECT @ResponseData = databaselog.dbo.GetHttpDataHeaders(@RequestUrl, @Headers);

            --PRINT @ResponseData;

            -- Insert the PurchaseOrders
            INSERT INTO XeroPurchaseOrders
            (
                PurchaseOrderID,
                SessionId,
                PurchaseOrderNumber,
                PoDate,
                DeliveryDate,
                DeliveryAddress,
                AttentionTo,
                Telephone,
                DeliveryInstructions,
                HasErrors,
                IsDiscounted,
                Reference,
                PoType,
                CurrencyRate,
                CurrencyCode,
                ContactName,
                BrandingThemeID,
                PoStatus,
                LineAmountTypes,
                SubTotal,
                TotalTax,
                Total,
                HasAttachments
            )
            SELECT p.PurchaseOrderID,
                   @SessionId,
                   p.PurchaseOrderNumber,
                   CONVERT(DATETIME, p.DateString),
                   CONVERT(DATETIME, p.DeliveryDateString),
                   p.DeliveryAddress,
                   p.AttentionTo,
                   p.Telephone,
                   p.DeliveryInstructions,
                   p.HasErrors,
                   p.IsDiscounted,
                   p.Reference,
                   p.PoType,
                   p.CurrencyRate,
                   p.CurrencyCode,
                   JSON_VALUE(p.Contact, '$.Name'),
                   p.BrandingThemeID,
                   p.PoStatus,
                   p.LineAmountTypes,
                   p.SubTotal,
                   p.TotalTax,
                   p.Total,
                   p.HasAttachments
            FROM
                OPENJSON(@ResponseData, '$.PurchaseOrders')
                WITH
                (
                    PurchaseOrderID UNIQUEIDENTIFIER '$.PurchaseOrderID',
                    PurchaseOrderNumber NVARCHAR(255) '$.PurchaseOrderNumber',
                    DateString NVARCHAR(255) '$.DateString',
                    DeliveryDateString NVARCHAR(255) '$.DeliveryDateString',
                    DeliveryAddress NVARCHAR(MAX) '$.DeliveryAddress',
                    AttentionTo NVARCHAR(255) '$.AttentionTo',
                    Telephone NVARCHAR(255) '$.Telephone',
                    DeliveryInstructions NVARCHAR(MAX) '$.DeliveryInstructions',
                    HasErrors BIT '$.HasErrors',
                    IsDiscounted BIT '$.IsDiscounted',
                    Reference NVARCHAR(255) '$.Reference',
                    PoType NVARCHAR(255) '$.Type',
                    CurrencyRate DECIMAL(18, 10) '$.CurrencyRate',
                    CurrencyCode NVARCHAR(255) '$.CurrencyCode',
                    Contact NVARCHAR(MAX) '$.Contact' AS JSON,
                    BrandingThemeID UNIQUEIDENTIFIER '$.BrandingThemeID',
                    PoStatus NVARCHAR(255) '$.Status',
                    LineAmountTypes NVARCHAR(255) '$.LineAmountTypes',
                    SubTotal DECIMAL(18, 2) '$.SubTotal',
                    TotalTax DECIMAL(18, 2) '$.TotalTax',
                    Total DECIMAL(18, 2) '$.Total',
                    HasAttachments BIT '$.HasAttachments'
                ) AS p;

            INSERT INTO XeroPoLineItems
            (
                LineItemID,
                SessionId,
                PurchaseOrderID,
                ItemCode,
                Description,
                UnitAmount,
                TaxType,
                TaxAmount,
                LineAmount,
                AccountCode,
                Quantity
            )
            SELECT li.LineItemID,
                   @SessionId,
                   po.PurchaseOrderID,
                   li.ItemCode,
                   li.Description,
                   li.UnitAmount,
                   li.TaxType,
                   li.TaxAmount,
                   li.LineAmount,
                   li.AccountCode,
                   li.Quantity
            FROM
                OPENJSON(@ResponseData, '$.PurchaseOrders')
                WITH
                (
                    PurchaseOrderID UNIQUEIDENTIFIER '$.PurchaseOrderID',
                    LineItems NVARCHAR(MAX) '$.LineItems' AS JSON
                ) AS po
                CROSS APPLY
                OPENJSON(po.LineItems)
                WITH
                (
                    LineItemID UNIQUEIDENTIFIER '$.LineItemID',
                    ItemCode NVARCHAR(255) '$.ItemCode',
                    Description NVARCHAR(MAX) '$.Description',
                    UnitAmount DECIMAL(18, 4) '$.UnitAmount',
                    TaxType NVARCHAR(255) '$.TaxType',
                    TaxAmount DECIMAL(18, 2) '$.TaxAmount',
                    LineAmount DECIMAL(18, 2) '$.LineAmount',
                    AccountCode NVARCHAR(255) '$.AccountCode',
                    Quantity DECIMAL(18, 4) '$.Quantity'
                ) AS li;


        END TRY
        BEGIN CATCH

            -- Log Failed case    

            IF @@TRANCOUNT > 0
                ROLLBACK TRAN;
            EXEC dbo.PrcThrowErrorMessage;
        END CATCH;

    END;


END;

```
