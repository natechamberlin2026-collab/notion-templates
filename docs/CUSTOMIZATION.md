# Notion Templates — Customization Guide

---

## Templates Included

| Template | File | Databases | Pages |
|----------|------|-----------|-------|
| **Second Brain (PARA)** | `second-brain/template.json` | 7 | 4 |
| **Project Tracker** | `project-tracker/template.json` | 6 | 3 |
| **Content Calendar** | `content-calendar/template.json` | 5 | 3 |
| **Client Portal** | `client-portal/template.json` | 5 | 4 |

---

## Quick Start

### 1. Import Template
1. Open Notion → Settings → Import → JSON
2. Select `template.json` from any template folder
3. Creates all databases + pages in your workspace

### 2. Duplicate for Use
1. Open created page
2. Click ⋮ → Duplicate
4. Rename → Move to your workspace

### 3. Configure Relations
Databases link via Relations. After import:
1. Open each database
2. Check Relation properties → Ensure they point to correct databases
3. Some Rollups may need refresh

---

## Second Brain (PARA Method)

### Databases
| Database | Purpose | Key Properties |
|----------|---------|----------------|
| **Inbox** | Quick capture | Type, Source, Status, Date Added |
| **Projects** | Active outcomes | Area, Status, Priority, Due Date, Progress |
| **Areas** | Ongoing standards | Standard, Health Score, Review Frequency |
| **Resources** | Reference material | Topic, Type, Source, Tags, Rating |
| **Tasks** | Actionable items | Project, Area, Status, Priority, Energy, Time |
| **Notes** | Atomic notes | Type, Topics, Source, Projects, Areas |
| **Daily Notes** | Journaling | Mood, Energy, Focus, Wins, Gratitude |

### Pages
- **Dashboard** — Linked DB views for today/this week
- **Weekly Review** — Template with prompts
- **Monthly Review** — Template with metrics
- **Project Template** — Standard project structure

### n8n Automation (`n8n-setup.md`)
6 workflows: Daily capture, Daily reminder, Weekly review, Project health, Resource cleanup, Discord notifications

---

## Project Tracker (Freelance)

### Databases
| Database | Purpose | Key Properties |
|----------|---------|----------------|
| **Clients** | Client directory | Company, Email, Platform, Status, Rating, Total Billed |
| **Projects** | Project tracking | Client, Type, Status, Rate Type, Budget, Hours, Dates |
| **Milestones** | Deliverables + payments | Project, Description, Amount, Status, Due Date |
| **Invoices** | Billing | Project, Client, Amount, Status, Platform, Due/Paid Date |
| **Tasks** | Granular work | Project, Milestone, Status, Priority, Hours, Tags |
| **Time Entries** | Hourly tracking | Project, Task, Hours, Description, Billable/Billed |

### Pages
- **Project Dashboard** — Active projects, upcoming milestones, unpaid invoices
- **New Project Wizard** — Step-by-step project setup
- **Invoice Tracker** — All invoices with status
- **Time Log** — Weekly/monthly time summaries

---

## Content Calendar

### Databases
| Database | Purpose | Key Properties |
|----------|---------|----------------|
| **Content Ideas** | Backlog | Topic, Platform, Format, Status, Priority, Target Date |
| **Content Calendar** | Scheduled posts | Content Idea, Platform, Publish Date/Time, Status, Content, Hashtags |
| **Content Metrics** | Performance | Platform, Impressions, Engagements, Rate, Clicks, Shares |
| **Content Pillars** | Strategy themes | Name, Description, Audience, Topics, Frequency, Active |
| **Repurposing Map** | Cross-platform | Original → Repurposed As, Transformation, Status |

### Pages
- **Content Dashboard** — This week, backlog, top performers, pillar balance
- **Weekly Planning** — Mon: Plan, Tue: Create, Wed: Schedule, Thu: Engage, Fri: Review
- **Monthly Review** — Top posts, pillar performance, platform growth, next themes

---

## Client Portal

### Databases (Client-Visible)
| Database | Purpose | Key Properties |
|----------|---------|----------------|
| **Projects** | Status overview | Type, Status, Progress, Dates, Description |
| **Milestones** | Deliverables | Project, Description, Status, Due Date, Deliverables, Files |
| **Deliverables** | Files/links | Milestone, Type, Status, Description, File, Link |
| **Communications** | Message log | Project, Type, From, Message, Resolved |
| **Invoices** | Payment status | Project, Amount, Status, Dates, Payment Link |

### Public Pages (Share with Client)
- **Welcome / Onboarding** — Guidelines, response times, escalation
- **Project Status Dashboard** — Live project view
- **Resources & Access** — Credentials (1Password links), repos, staging URLs
- **Meeting Notes** — Template for call notes

### Setup
1. Import template
2. Create client-specific views (filter by Client)
3. Share public pages → Copy links → Send to client
4. Client sees only their projects (via filtered views)

---

## Customization Patterns

### Add Custom Properties
1. Open database → ⋮ → Properties → New property
2. Choose type (Select, Multi-select, Date, Number, Formula, Relation, Rollup)
3. For Select/Multi-select: Define options with colors

### Create Custom Views
1. Database → ⋮ → View → New view
2. Choose: Table, Board, List, Calendar, Timeline, Gallery
3. Add filters, sorts, groups
4. Save as default or named view

### Formula Examples
```notion
// Project health score
if(prop("Due Date") < now() and prop("Status") != "Done", "🔴 Overdue",
  if(prop("Progress") == 100, "🟢 Done",
    if(prop("Progress") > 50, "🟡 On Track", "🟠 Started")))

// Days until due
dateBetween(prop("Due Date"), now(), "days")

// Invoice status
if(prop("Paid Date"), "✅ Paid",
  if(prop("Due Date") < now(), "🔴 Overdue", "🟡 Pending"))
```

### Rollup Examples
- **Client → Total Billed**: Rollup Projects → Invoices → Amount (Sum)
- **Project → Hours Logged**: Rollup Tasks → Time Entries → Hours (Sum)
- **Milestone → Files Count**: Rollup Deliverables → File (Count)

---

## Sharing with Clients

### Public Page Link
1. Page → Share → Publish → Allow duplicate as template
2. Copy link → Send to client
3. Client clicks → Duplicate to their workspace

### Filtered Database Views
1. Create view filtered by `Client = [Client Name]`
2. Share view link (Share → Copy link to view)
3. Client sees only their data

### Client Portal Access
- Share 4 public pages individually
- Or create single "Client Hub" page with linked views

---

## Maintenance

### Weekly
- [ ] Run Weekly Review page
- [ ] Check Project health (overdue, stalled)
- [ ] Review Inbox → Process to Projects/Areas/Resources

### Monthly
- [ ] Run Monthly Review page
- [ ] Archive completed Projects
- [ ] Review Resources → Archive outdated
- [ ] Update Content Pillar balance

### Quarterly
- [ ] Archive old Areas
- [ ] Review automations (n8n)
- [ ] Update templates based on learnings

---

## License

MIT — Customize, duplicate, sell, use commercially.