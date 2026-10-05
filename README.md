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

**Model**: Objective ← *Solves* ← Solution Increment (SI) ← *Relates to* ← Epic (lives in a Delivery Unit = Jira project) → Stories.
Many-to-many on both links: an SI can feed several Objectives, an epic can serve several SIs (shown under each, joined by a dotted line).

- **By Solution Increment** view: Objective banner (status, RAG, priority, due, forecast end) → SI rows → epic cards in PI columns. **By Delivery Unit** view: rows = Jira projects.
- **Calendar**: sprints are 2 weeks (sprint 292 = 1 Oct 2026), PI85 = sprints 291–298; editable in the side panel. SI timing is derived from its epics; epic timing from its stories' sprints (or the whole PI if moved / no stories).
- **Epic dependencies** are not in JIRA yet: add "blocks" links on an epic, *Save in browser* (re-applied on every import) or export/import as CSV. A real `Blocks` link in the JIRA CSV is read too.
- **Critical path** = longest chain of dependencies with ≤ 1 sprint of slack, compared with the Objective due dates.
- Flags: epic/SI ends after Objective due, SI without epics, Objective without SI, dependency overlap.
- Simulation: drag epic to another PI, add/remove links, ▲▼ objective priority, auto-resolve. **Reset scenario** = back to imported data; **Clear all** = empty dashboard.

JIRA export (one CSV, all issue types): Issue key, Issue Type, Summary, Status, Assignee, PI, Story Points, Sprint (repeated), Epic Link, RAG Status,
Objective Manager, Global Priority, Due date, and Outward/Inward issue link (Solves / Relates / Blocks) columns. Optional `Project` column (else taken from the key prefix).
