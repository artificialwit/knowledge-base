# LLM Introduction

## What is LLM in simple term.
### Understands Intent – 
  - in simple language , LLM extract Intent and param value from prompt/text and response based on knowledge in human language other than just field and value. for example - user says,
    -   I need to book a flight from New York to London on March 10.
    -   Schedule a sales report for last quarter and email it to John.
  - It figures out what the user wants from the text (e.g., "Book a flight" or "Generate a report").
  - Extracts Parameters (Entities) – It pulls out key details from the text (e.g., "New York to London," "March 10," or "Sales Report for Q1").
  - Generates a Response – It replies in natural human language, using its stored knowledge and understanding of context.
  - Unlike a traditional system that just maps fields to values, an LLM can infer meaning, handle complex queries, and respond intelligently based on its training data.
  - For example:
    - User Input: "Schedule a sales report for last quarter and email it to John."
    - LLM Interpretation:
      - Intent: Generate & Send Report
      - Parameters:
        - Report Type: Sales
        - Timeframe: Last Quarter
        - Recipient: John
      - Response: "Your sales report for the last quarter has been scheduled and will be emailed to John."
    #### This makes it more dynamic than a simple form-based input system. 🚀

## Why Bot (AI Agent)
  - Satya Nadella on the Future of SaaS, How 2025 is the year of Agents, Advice for Indian Engineers
    - https://www.youtube.com/watch?v=GuqAUv4UKXo
## Type of Integration
- API Call
- Text to SQL query run

## Premise of LLM Model to be used
- Cloud
  - OpenAI
    - https://cookbook.openai.com/examples/how_to_call_functions_with_chat_models
  - Groq
    - https://groq.com/
  - Google
    - https://aistudio.google.com/
  - LangChain
    - https://www.langchain.com/
- On-Prem
  - Llama

## Online Agent Development Platform
  - Botpress
    - Botpress channel for learning https://www.youtube.com/@Botpress
    - https://botpress.com
    - https://app.botpress.cloud
    - https://studio.botpress.cloud
    - https://botpress.com/integrations/charts
  - https://n8n.io/
  - Agno
      https://www.agno.com/ --- phidata.com
  - LangChain
    - https://www.langchain.com/langgraph

## User Interface framework Streamlit- Awesome
  -- https://streamlit.io/
  - https://www.youtube.com/watch?v=D0D4Pa22iG0&t=41s
  - https://streamlit.io/generative-ai

## Links
- AI Agent Architecture
  -  https://www.youtube.com/watch?v=FEU6-Il8jjw 
- Building AI Agent from Scratch
  - https://www.youtube.com/watch?v=vUYnRGotTbo
  - https://www.youtube.com/watch?v=kRR1K3q5nlg
- What is Agentic AI? Important For GEN AI In 2025
  - https://www.youtube.com/watch?v=xOS0BhhdUbo
- Making API Calls in Botpress (for beginners!)
  - https://www.youtube.com/watch?v=h148bna9VIw
- Piecode
  - https://www.youtube.com/watch?v=erUfLIi9OFM
- https://www.youtube.com/watch?v=ZtltjSjFPDg

## Available Roles in OpenAI Chat API
### Role	Description
  - "system"	Provides instructions & context for the assistant. Sets behavior, style, and rules.
  - "user"	Represents the user's input (questions, commands, requests).
  - "assistant"	Represents the AI's response based on knowledge & context.
  - "tool" (or "function")	Used when the assistant calls an external function or tool.
  - "data"	Represents output from a tool (e.g., API response, database query).
### Exmaple
```json
[
    {"role": "system", "content": "You are a helpful AI assistant specialized in tech support."},
    {"role": "user", "content": "How do I reset my password?"},
    {"role": "assistant", "content": "You can reset your password by clicking 'Forgot Password' on the login page."},
    {"role": "user", "content": "Can you show me the steps?"},
    {"role": "assistant", "content": "Sure! Step 1: Go to the login page..."},
    {"role": "tool", "name": "get_user_info", "content": "Fetching user details..."},
    {"role": "data", "content": "User email: user@example.com, Last login: 2 days ago"}
]
```

