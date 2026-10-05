# Roadmap-mockup
# 🗺️ Product Roadmap — New Portfolio

> Browser-based interactive roadmap visualization for ESET's new product portfolio.  
> Designed for everyone involved in product delivery — from C-suite to development teams.

---

## 🎯 Purpose

This tool provides a unified view of product roadmaps across the new portfolio structure.  
The goal is a single visual layer that communicates delivery plans clearly — regardless of the audience's technical level.

---

## 📁 Files

| File | Description |
|------|-------------|
| `roadmap-drilldown_4.html` | Main app — open directly in browser, no install needed |
| `epic-dependencies.html` | Epic dependency map + what-if simulation (import JIRA CSV export) |
| `sample-epics.csv` | Sample Monetization epics in JIRA CSV export format |
| `epic-hierarchy.html` | v2: Objective → Solution Increment → Epic → Stories view (solid = Solves, dotted = Relates, columns = PI) |
| `sample-hierarchy.csv` | Illustrative sample modelled on ESET-138 / SOLINC / DU_EPP structure |

---

## 🚀 How to Use

1. Open `roadmap-drilldown_4.html` in any modern browser (Chrome, Edge, Firefox)
2. No server, no dependencies — it runs fully offline
3. Share the file directly or host via GitHub Pages for team access

---

## 🔄 Status

> ⚠️ **Work in progress — early prototype**

This is the first HTML draft exploring layout and structure.  
Expect frequent changes to design, data structure, and interactions.

---

## 🛣️ Planned Direction

- [ ] Finalize portfolio structure and product hierarchy
- [ ] Add drill-down navigation (portfolio → product → epic/feature level)
- [ ] Make data-driven (separate data file instead of hardcoded values)
- [ ] Stakeholder-friendly view vs. team-level detail view
- [ ] Potential GitHub Pages deployment for easy sharing

---

## 👥 Target Audience

| Role | What they need from this tool |
|------|-------------------------------|
| C-suite | High-level portfolio overview, delivery confidence |
| Program Managers | Cross-product dependencies, timeline alignment |
| Scrum Masters / Teams | Feature-level detail, sprint context |

---

## 🧭 Context

**Owner:** Martin Vakula  
**Program:** ESET XDR & New Product Portfolio  
**Tech:** Pure HTML/CSS/JS — no framework, no build step  

---

*Last updated: May 2026*

---

## 🔗 Epic Dependency Map

Open `epic-dependencies.html`, click **Import JIRA CSV** (or **Load sample**).

**JIRA export** (Filter → Export → CSV, all fields), e.g. `issuetype = Epic AND fixVersion in (...)`.
Needed columns: Issue key, Summary, Status, Priority, Team/Component, Fix Version (increment), and the
*Outward/Inward issue link (Blocks / Depends)* columns (repeated per link – all are read).

**Reading it:** columns = increments, rows = teams. Green arrow = blocker earlier, amber = same increment, red = violation.
Click an epic to trace its chain; drag it to another column or change priority/dependencies in the side panel
to simulate. *Auto-resolve* pushes dependents later; *Reset scenario* returns to baseline; *Export scenario CSV* saves the what-if.
Nothing is written back to JIRA.

---

## 🧭 Epic Hierarchy Map (v2)

Open `epic-hierarchy.html` → **Import JIRA CSV** (or **Load sample**).

- **Objective banner**: status, RAG, owner/manager, Global Priority, due date, % done (roll-up from stories). ▲▼ reorder objectives to simulate priority.
- **Rows** = Solution Increments (epic ↔ SOLINC "relates to"), **columns** = PI (3 months each), **cards** = epics with progress from their stories.
- **Lines**: solid = *Solves* (strong, coloured by PI order), dotted = *Relates to* (weak).
- Epics inherit the objective from the epic they solve; epics due after their objective are flagged **late vs obj**.
- Click an epic: trace chain + stories grouped by sprint in the side panel. Drag to another PI to simulate.
- **Reset scenario** = back to imported data; **Clear all** = empty dashboard for a new upload.

One JIRA CSV with all issue types works. Needed columns: Issue key, Issue Type, Summary, Status, Assignee, PI, Due date, Story Points,
Sprint (repeated), Epic Link, RAG Status, Objective Manager, Global Priority, and Outward/Inward issue link (Solves / Relates).
