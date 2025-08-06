
# Telegram Assistant Workflow

A powerful n8n workflow that creates an intelligent Telegram bot assistant capable of managing your emails, calendar events, tasks, and contacts through natural language conversations.

![Telegram Assistant Banner](https://raw.githubusercontent.com/MajorAbdullah/Telegram-Assistant/main/image.png)

# Problem Statement

Managing emails, calendar events, tasks, and contacts across multiple platforms can be time-consuming and inefficient, especially when switching between apps or devices. Users need a unified, conversational interface to streamline daily productivity tasks and access information quickly.

## Solution

Telegram Assistant is an n8n-powered workflow that transforms your Telegram bot into a smart personal assistant. It integrates Gmail, Google Calendar, Baserow, and AI models to provide seamless, conversational access to your emails, events, tasks, and contacts—all from within Telegram, using both text and voice commands.

## Features

- 🤖 **AI-Powered Conversations**: Uses OpenAI's GPT model with conversation memory
- 📧 **Email Management**: Fetch and summarize unread Gmail messages
- 📅 **Calendar Integration**: Access Google Calendar events and scheduling
- ✅ **Task Management**: Query and manage tasks via Baserow database
- 👥 **Contact Management**: Access contact information from Baserow
- 🎤 **Voice Message Support**: Transcribe voice messages using Google Gemini
- 💭 **Context Memory**: Maintains conversation context per user session

## Prerequisites

### Required Services & Accounts

- [n8n](https://n8n.io/) workflow automation platform
- [Telegram Bot](https://core.telegram.org/bots#creating-a-new-bot) - Create via @BotFather
- [OpenAI API](https://openai.com/api/) account
- [Google Cloud Platform](https://cloud.google.com/) account with:
  - Gmail API enabled
  - Google Calendar API enabled
  - Google Gemini API access
- [Baserow](https://baserow.io/) account with databases for tasks and contacts

### Required n8n Nodes

- `n8n-nodes-base.telegramTrigger`
- `n8n-nodes-base.telegram`
- `@n8n/n8n-nodes-langchain.agent`
- `@n8n/n8n-nodes-langchain.lmChatOpenAi`
- `@n8n/n8n-nodes-langchain.memoryBufferWindow`
- `n8n-nodes-base.googleCalendarTool`
- `n8n-nodes-base.gmailTool`
- `n8n-nodes-base.baserowTool`
- `@n8n/n8n-nodes-langchain.googleGemini`

## Setup Instructions

### 1. Telegram Bot Configuration

1. Create a new bot via [@BotFather](https://t.me/botfather)
2. Save the bot token for n8n configuration
3. Add the Telegram API credentials in n8n

### 2. Google Services Setup

1. Create a Google Cloud Project
2. Enable Gmail and Calendar APIs
3. Create service account credentials
4. Configure Google API credentials in n8n

### 3. OpenAI Configuration

1. Sign up for OpenAI API access
2. Generate an API key
3. Add OpenAI credentials in n8n

### 4. Baserow Database Setup

Create two databases in Baserow:

#### Tasks Database 

- Set up your task management structure
- Note the database ID (146496) and table ID

#### Contacts Database 

- Create fields for contact information (emails, phone numbers)
- Note the table ID for configuration

### 5. Workflow Configuration

1. Import the workflow JSON into your n8n instance
2. Update the following parameters:
   - **Google Calendar**: Replace your email
   - **Baserow Tools**: Update database and table IDs to match your setup
   - **Credentials**: Configure all service credentials

## Usage

### Text Commands

Send text messages to your bot for various operations:

```
"What emails did I receive today?"
"Show me my calendar for tomorrow"
"What tasks do I have pending?"
"Find contact information for John"
```

### Voice Messages

- Send voice messages to the bot
- The workflow will automatically transcribe using Google Gemini
- Process the transcribed text through the AI assistant

### Supported Queries

#### Email Management

- "Check my unread emails"
- "Summarize emails from today"
- "Any important emails since yesterday?"

#### Calendar Operations

- "What's my schedule for today?"
- "Do I have any meetings tomorrow?"
- "Show me next week's appointments"

#### Task Management

- "What tasks are due today?"
- "Show me all pending tasks"
- "Any urgent tasks?"

#### Contact Lookup

- "Find email for [contact name]"
- "Get phone number for [contact name]"
- "Show contact details for [name]"

## Workflow Components

### Core Nodes

- **Listen for incoming events**: Telegram webhook trigger
- **Voice or Text**: Processes incoming messages
- **Good Bot**: Main AI agent with system instructions
- **Telegram**: Sends responses back to users

### AI Tools

- **Google Calendar**: Fetches calendar events
- **Get Email**: Retrieves Gmail messages
- **Tasks**: Baserow task management
- **Contacts**: Baserow contact database

### AI Components

- **OpenAI Chat Model**: Primary language model
- **Window Buffer Memory**: Maintains conversation context
- **Transcribe a recording**: Google Gemini voice transcription

## System Instructions

The AI assistant operates with the following guidelines:

- Filters out promotional emails when fetching messages
- Assumes "today" when no date is specified
- Provides detailed email summaries with sender, date, subject, and content
- Focuses on relevant calendar events based on user queries
- Uses current date context for intelligent responses

## Security Considerations

- Store all API keys securely in n8n credentials
- Use service accounts for Google API access
- Limit bot access to authorized users
- Regular credential rotation recommended
- Monitor workflow execution logs

## Troubleshooting

### Common Issues

1. **Voice transcription fails**: Verify Google Gemini API credentials
2. **Calendar not loading**: Check Google Calendar API permissions
3. **Email fetch errors**: Ensure Gmail API is enabled and authenticated
4. **Memory not working**: Verify session key configuration

### Debug Tips

- Check n8n execution logs for detailed error messages
- Test individual nodes to isolate issues
- Verify API quotas and rate limits
- Ensure webhook URLs are accessible

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Support

For issues and questions:

- Check the [n8n documentation](https://docs.n8n.io/)
- Review API documentation for integrated services
- Open an issue in this repository

---

**Note**: Remember to update all placeholder values (emails, database IDs, credentials) with your actual configuration before deploying.
