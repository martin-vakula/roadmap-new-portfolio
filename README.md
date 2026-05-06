# Roadmap Drilldown — XDR Platform Vision

An interactive roadmap visualization with drill-down navigation across six hierarchy levels: Strategic Theme → Programs → Objectives → Solutions → Delivery Units → Stories.

## Features

- Drill-down navigation through roadmap hierarchy
- Quarter and sprint timeline views
- Dark/light theme toggle
- AI analytics panel with insights
- CSV import for JIRA Epics + Stories
- Configurable horizon (quarter range)

## Getting started

```bash
npm run dev
```

Then open http://localhost:3000/roadmap-drilldown_4.html

## GitHub Codespaces

Open this repo in Codespaces — the dev server starts automatically on port 3000 and the browser opens the app.

## CSV Import

Click **Import Epics+Stories CSV** to load JIRA exports. Expected columns:

| Column | Accepted names |
|--------|---------------|
| Issue type | `Issue Type`, `Type`, `IssueType` |
| Summary | `Summary`, `Name`, `Title` |
| Key | `Issue Key`, `Key`, `IssueKey` |
| Parent epic | `Parent Epic`, `Epic Link`, `Parent`, `Parent Key` |
| Assignee | `Assignee`, `Owner`, `Assigned To` |
| Status | `Status` |
| Story points | `Story Points`, `Points`, `SP` |
| Sprint | `Sprint`, `Iteration` |
