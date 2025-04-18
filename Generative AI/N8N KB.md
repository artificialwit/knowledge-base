### Controls used in 8n8

1. ## Triggers
    - Manually - For Testing purpose specially 
    - On Webhook call
    - Run Any Other App like Bamboo HR, Asana, Microsoft Dynamic CRM etc.
    - On A Schedule
    - On form submission - We can create form using n8n
    - Whenn executed by another workflow
    - On Chat Message
    - #### Others
        - Email Trigger
        - Error Trigger
        - Local File Trigger
        - n8n Trigger
        - SSE (Server side event) Trigger
  
2. ## Credentials Account
   - ### Database
       - Postgres
       - Sqlite
       - Supabase
   - ### Language Model - Link with Language Models
       - OpenAI
       - Azure
       - Ollama
   - ### Cloud Account
        - #### Google
            - Google Drive Account (Oauth2 API)
            - Google Calendar Account  (Oauth2 API)
            - etc.
        - #### WhatsApp
            - WhatsApp API
            - WhatsApp OAuth
        - #### Microsoft
            - Drive OAuth2 API
  
3. ## Tools
   - Postgres Tool
2. ## Data Transformation
   - Code  - Run custom javasript or python code
   - Date & Time - Manipulate date and time values
   - Edit Fields (set) - Modify, Add Or Remove item fields
   - If - Route Item two different branches (true/false)
   - Switch - Route item depending on defined expression or rules
   - Filter - remove items matching a condition
   - Loop Over Items (Split in batches) - Split data into batches and iterate over each batch
   - Limit - restrict the number of rows
   - Remove Duplicate - Remove duplicate rows
   - Split Out - Turn a list inside items into seperate items
   - Aggregate - Combine a field from many items into a list in a single item
   - Merge - Merge data of multiple streams once data from both is available
   - Summarize - Sum , Count, Max , Min, etc. accross items
   - Crypto - Provide Crypto graphic utinilies
   - Rename Keys - update item field names
   - Sort - Change Items order
   - Compare Datasets - Compare tow inputs for datasets
   - Execute sub-workflow - Call other n8n workflow
   - Stop and Error - Throw an error in workflow
   - Wait - Wait before continue with execution
3. ## File Handling
   - Convert to file - Convert json data to a binary data
   - Extract From File - Convert Binary data to JSON
   - Edit Image - Edit an image like blur, resize, and adding border and text
   - HTML  - Work with HTML
   - Markdown - Convert data between Markdown and HTML
   - XML - Convert data from and to XML
   - Compression - Compress and decopress files
   - ## Google
       - Google Ads
       - Google Chat
       - Google Docs
       - Google Books
       - Google Drive
           - File Copy , Downlaod , Create , Move , Share , Update , Upload
           - Folder Create, Delete , Share
       - Google Task
       - Google Sheets
       - Google Slides
       - Google Calendar
       - Google Contact
       - Google Analytics
       - Google Translate
       - Google Prospective
       - Google Cloud Storage
       - Google Cloud Firestore
       - Google Workspace Admin
       - Google Business Profile
       - Google Cloud Natural Language
       - Google Cloud Realtime Database
       -  ### Google Tools
           - Google Drive Tool
           - Google Sheet Tool
           - Google Calendar Tool
           - Google SerpAPI - Google Search etc.
3. ## Chat Model (Language Models)
   - Groq Chat Model
   - Ollama Chat Model
   - OpenAI Chat Model
   - Deepseek Chat Model
   - xAI Grok Chat Model
   - Anthropic Chat Model
   - OpenRouter Chat Model
   - AWS Bedrock Chat Model
   - Azure OpenAI Chat Model
   - Google Gemini Chat Model
   - Google Vertex Chat Model
   - Mistral Cloud Chat Model
5. ## Chat Memory
   - Simple Chat Memory (Sqlite)
   - Postgres Chat Memory - Store chat hisotory in postgres sql
   - MongoDB Chat Memory - Store chat hisotory in mongodb collection
   - Redis Chat Memory
   - Xata
   - Zep
### Reference
- How I Built JARVIS with No Code (Tutorial w/ Lovable, ElevenLabs, n8n)
  -   https://www.youtube.com/watch?v=KUvSzvFeZls
-   How to Use Claude to INSTANTLY Build & Replicate Any n8n Agents
  -  https://www.youtube.com/watch?v=JM0y9JKopc0
