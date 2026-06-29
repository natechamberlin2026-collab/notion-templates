# Notion "Second Brain" Template

A comprehensive personal knowledge management system built in Notion, following the PARA method (Projects, Areas, Resources, Archives) with automation via n8n.

## 📁 Structure

```
Second Brain/
├── 🎯 Projects (Active)
│   ├── Project Dashboard
│   ├── Project Templates
│   └── Project Archive
├── 📂 Areas (Ongoing Responsibilities)
│   ├── Health & Fitness
│   ├── Finance
│   ├── Career
│   ├── Relationships
│   └── Home
├── 📚 Resources (Reference Material)
│   ├── Notes & Learning
│   ├── Templates
│   ├── References
│   └── Inspiration
├── 🗄️ Archives (Completed/Inactive)
│   ├── Completed Projects
│   └── Inactive Areas
└── ⚙️ System
    ├── Inbox (Quick Capture)
    ├── Daily Notes
    ├── Weekly Reviews
    ├── Monthly Reviews
    ├── Yearly Reviews
    └── Templates
```

## 🚀 Quick Start

1. **Duplicate the template** to your Notion workspace
2. **Set up n8n automation** (see `n8n-setup.md`)
3. **Configure integrations**: 
   - Notion API token
   - Discord webhook (for notifications)
   - Google Calendar (for review reminders)
4. **Run the setup script** to create databases and relations

## 📊 Databases

### Inbox
Quick capture for anything - tasks, ideas, notes, links
- **Properties**: Title, Type (Task/Note/Link/Idea), Source, Status, Date Added

### Projects
Active projects with clear outcomes and deadlines
- **Properties**: Name, Area, Status, Priority, Due Date, Progress, Related Areas, Notes

### Areas
Ongoing responsibilities with standards
- **Properties**: Name, Standard, Current Projects, Last Review, Health Score

### Resources
Reference material organized by topic
- **Properties**: Title, Topic, Type, Source, Tags, Rating, Date Added

### Tasks
Actionable items linked to Projects or Areas
- **Properties**: Name, Project, Area, Status, Priority, Due Date, Energy, Time Estimate, Dependencies

### Notes
Atomic notes linked to Resources, Projects, or Areas
- **Properties**: Title, Type, Topics, Source, Projects, Areas, Status

### Daily Notes
Daily journaling and planning
- **Properties**: Date, Mood, Energy, Focus, Wins, Challenges, Gratitude, Notes

## 🤖 n8n Automations Included

1. **Daily Capture → Inbox** - Forward emails, messages to Notion Inbox
2. **Daily Review Reminder** - 9 PM notification with today's tasks
3. **Weekly Review Generator** - Auto-create weekly review template every Sunday
4. **Project Health Check** - Weekly scan for stalled projects
5. **Resource Cleanup** - Monthly prompt to review/archive old resources
6. **Notion → Discord** - Send project updates to Discord channel

## 🔧 Customization

- Add/remove Areas based on your life
- Modify Project statuses to match your workflow
- Adjust Task energy levels (High/Medium/Low)
- Create custom templates for recurring project types

## 📝 License

MIT - Use freely for personal or commercial projects