Project report

Tools used
- ChatGPT — step-by-step guidance and troubleshooting suggestions
- Supabase — database 
- n8n — workflow backend / automation engine
- Telegram Bot API — used via direct HTTP requests for sending inline keyboards
- https://r.jina.ai/ - extract text blocks from a website

Challenges and solutions
- Inline keyboards with the n8n Telegram node: the built-in Telegram node ignores inline keyboards even when the JSON payload is correct. To work around this, I used an HTTP Request node to call the Telegram Bot API directly.
- Bot token availability in n8n Cloud: the Telegram API requires the bot token in the request URL. When the workflow is hosted in n8n Cloud, using local `.env` variables are not available (so the token is just hardcoded in the workflow node).
- Single entrypoint and payload normalization: initially I implemented two triggers (one for messages/commands and one for callback queries). Before publishing I realized the workflow should have a single entrypoint. Since `message` and `callback_query` telegram events have different payload formats, I refactored the workflow to normalize incoming events at the trigger and handle both event types through the same entry node.

Database structure
5 tables: 
users
quizes (one row - one question)
quiz_sessions(keeps current question number and score)
quiz_attemts (user answers)
learning_materials (website data)

n8n Workflow
Telegram Learning Bot Workflow _final_tokens_cut.json - downloaded final published workflow, all tokens and auth data removed