## Postgre SQL basic
### Environment variable settings
  - System Variables
    - Variable Name: PGHOME
    - Vairable Valule:  C:\Program Files\PostgreSQL\17\bin
  - Command
    - use pgxnclient inplace of pgxn 
## Entesions
  - *Make* is also must be installed to run the make file 
  - Make sure your have installed C++ tools, from microsoft visual studio installer, these must be below
  - Below command is not working , but have for future reference
    -  pgxnclient install --pg_config "C:\Program Files\PostgreSQL\17\bin\pg_config.exe" vector 
  - Now follow the window steps
    - https://github.com/pgvector/pgvector
### HTTP Extension for API call from database
  - Download windows zip from site or if stored locally
  - Copy and Paste the into the Postgre insatlled directories (C:\Program Files\PostgreSQL\17\):
    - DLL File (http.dll) → PostgreSQL dll Directory
    - bin file in bin folder of PostgreSQL
    - C:\Program Files\PostgreSQL\<version>\share\extension\
    - SQL Files (http--*.sql, http.control) → PostgreSQL extension Directory
    - And Install SSL if, SSL is not working then disbale the SSL with below command
    ``` sql

      SELECT http_set_curlopt('CURLOPT_SSL_VERIFYPEER', 'false');
      SELECT http_set_curlopt('CURLOPT_SSL_VERIFYHOST', 'false');


      WITH api_response AS (
          SELECT content::jsonb AS json_data
          FROM http_get('https://api-staging.assetinfinity.io/api/public/OrganizationDetails?company=dev')
      )
      SELECT
          json_data->'data'->0->>'apiUrl' AS api_url,
          json_data->'data'->0->>'fileApiUrl' AS file_api_url,
          json_data->'data'->0->>'companyName' AS company_name,
          json_data->'data'->0->>'expiryDate' AS expiry_date,
          json_data->'data'->0->>'webAppTitle' AS web_app_title,
          json_data->'data'->0->>'fabIcon' AS fab_icon
      FROM api_response;
      ```
  - create extension if not exists vector
  - 
## installlation from website and default
  - https://www.enterprisedb.com/postgresql-tutorial-resources-training-1?uuid=69f95902-b451-4735-b7e4-1b62209d4dfd&campaignId=postgres_rc_17
  - after insatllation search in windows as PgAdmin to run the Postgre Console, it is just like SQL Server managament Studio
  - We have command from also for PostgreSQL, that is SQL Shell (pgsql)
  - defaults
    - default connection/server is localhost,
    - default database created is postgres
    - default user of that database is postgres
    - default password would be same as we entered on installation time
    - Default schema is public just like dbo in MS SQL. all table, procedure etc. must be a part of a schema, just like MS SQL
      
### Language
  - **just PL/SQL, in postgre it calls PL/pgSQL**. It allows users to write functions, triggers, and procedural code within the database using control structures like loops, conditions, and error handling
  - **PL/Python – Allows writing functions in Python.**
## Extension installation
  - visit https://pgxn.org/
  - search your extension and install
### Common Command
  - SELECT datname FROM pg_database
  - SERIAL data type for Auto increment
  - currval('index_name_of_table')
  - nextval('index_name_of_table') , it store in table as default formula to get the next auto number in case of insert
  - LIMIT 5 , to get top 5 rows from select command, it must be last command
  - Use CONCAT(firstName, LastName) , to concatinate two string, it is better way
  - Use CONCAT_WS(' ', firstName, LastName) , to concatinate two string with seperator, it is better way
### References
- https://www.youtube.com/watch?v=cnzka7kF5Zk
