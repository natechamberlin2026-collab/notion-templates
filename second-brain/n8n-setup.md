# n8n Setup for Notion Second Brain

## Prerequisites

- n8n instance (self-hosted or n8n.cloud)
- Notion API integration
- Discord webhook (optional, for notifications)
- Google Calendar (optional, for review reminders)

## Notion API Setup

1. Go to https://www.notion.so/my-integrations
2. Create new integration: "Second Brain Automation"
3. Copy the **Internal Integration Token**
4. Share your databases/pages with the integration:
   - Open each database → `...` → `Add connections` → Select your integration

## n8n Credentials

In n8n, create these credentials:

### Notion API
- **Authentication**: Access Token
- **Access Token**: Your Notion integration token

### Discord Webhook
- **Webhook URL**: Your Discord channel webhook URL

### Google Calendar OAuth2
- Follow n8n Google Calendar setup

## Workflows to Import

Import these workflow JSON files from the `../n8n-workflows/` directory:

1. `notion-discord/workflow.json` - Notion → Discord notifications
2. `notion-sheets/workflow.json` - Notion → Google Sheets sync

## Environment Variables

Create these in n8n (Settings → Environment Variables):

```
NOTION_DATABASE_INBOX_ID=your_inbox_database_id
NOTION_DATABASE_PROJECTS_ID=your_projects_database_id
NOTION_DATABASE_AREAS_ID=your_areas_database_id
NOTION_DATABASE_RESOURCES_ID=your_resources_database_id
NOTION_DATABASE_TASKS_ID=your_tasks_database_id
NOTION_DATABASE_NOTES_ID=your_notes_database_id
NOTION_DATABASE_DAILY_ID=your_daily_notes_database_id

DISCORD_WEBHOOK_URL=your_discord_webhook_url
DISCORD_NOTIFICATION_CHANNEL_ID=your_channel_id

GOOGLE_SHEETS_ID=your_sheets_id
```

## Finding Database IDs

Open a database in Notion → URL looks like:
`https://www.notion.so/workspace/Database_Name-<DATABASE_ID>?v=...`

The DATABASE_ID is the 32-char string after the last `-` and before `?v=`

## Workflow: Daily Review Reminder

Create a new workflow:

1. **Cron Trigger** - Every day at 21:00 (9 PM)
2. **Notion: Query Database** - Tasks database
   - Filter: `Due Date` = Today AND `Status` != Done
3. **Function Node** - Format message
4. **Discord: Send Message** - To your DMs or channel

## Workflow: Weekly Review Generator

1. **Cron Trigger** - Every Sunday at 10:00
2. **Notion: Create Page** - In Daily Notes database
   - Parent: Weekly Reviews page
   - Template: Use Weekly Review template
   - Properties: Date = This week's Monday

## Workflow: Project Health Check

1. **Cron Trigger** - Every Monday at 09:00
2. **Notion: Query Database** - Projects database
   - Filter: `Status` = Active AND `Last Updated` > 14 days ago
3. **Function Node** - Create alert message for stalled projects
4. **Discord: Send Message** - To notifications channel

## Testing

1. Run each workflow manually first
2. Check Notion for created/updated pages
3. Check Discord for notifications
4. Enable workflows once verified

## Troubleshooting

- **401 Unauthorized**: Check Notion token and database sharing
- **404 Not Found**: Verify database IDs are correct
- **Rate Limited**: Add delays between Notion operations
- **No Results**: Check filter syntax and property names

## Security Notes

- Never commit credentials to git
- Use n8n's built-in credential storage
- Rotate Notion token periodically
- Limit integration access to only needed databases