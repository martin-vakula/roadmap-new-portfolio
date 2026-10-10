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
| `epic-hierarchy.html` | v2: Objective → Solution Increment → Epic → Stories. Default **Outline** (folded tree, chips for dependencies) + Board views (solid = Solves, dotted = Relates, columns = PI) |
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

**Start with the Outline view (default).** It shows the same hierarchy as a folded tree – one line per item, no arrows:

- **Show down to** Objective / Solution Increment / Epic / Work items – start at the top and open only what you need. Click ▸/▾ to fold one branch.
- **One line = status, rolled-up progress, when, flags.** Objective and SI lines roll up their epics (forecast end vs. Objective due date, % done).
- **Dependencies and relations are chips on the line instead of arrows:** `⛔ blocked by X`, `→ blocks Y`, `↔ relates`, `↺ also SOLINC-n` (epic shared by several SIs). Click a chip to jump to that line; the side panel shows details and lets you edit links / PI.
- **Closed epics fold into one line** ("7 closed epics") so history does not bury current work; empty SIs fold into one line too.
- **"only what needs attention"** keeps just the branches with something late, on hold, blocked/blocking, or an SI without epics.
- Epics linked straight to an Objective (no SI) sit in *"Epics not assigned to a Solution Increment"*.
- The grouped *Issues to resolve* panel lists each problem once (e.g. "8 epics end after objective …") instead of once per epic.

**Right-hand panel:** drag its left edge to make it wider or narrower (double-click the edge to reset), hide it with **Hide ✕** / **Panel ⇥** to give the list the full width, fold each section by clicking its header, or use **Expand all / Collapse all**. Width, hidden state and folded sections are remembered in this browser.

The two **Board** views (PI columns, arrows, what-if drag & drop) are still there for planning conversations.

Importer notes (real JIRA "all fields" exports): the *Objectives Panel* / *Requirements Panel* columns are read as child lists (Objective → epics, Epic → stories/tasks); an epic that *solves* an SI counts as part of that SI; with several Fix Version columns the latest PI wins (`PI85A` / `PI86plan` → PI85 / PI86); *Implemented* counts as done; RAG / priority columns holding junk are ignored (re-point them in the Data mapping panel if the export has shifted headers).

Open `epic-hierarchy.html` → **Import JIRA CSV** (or **Load sample**).

**Model**: Objective ← *Solves* ← Solution Increment (SI) ← *Relates to* ← Epic (lives in a Delivery Unit = Jira project) → Stories.
Many-to-many on both links: an SI can feed several Objectives, an epic can serve several SIs (shown under each, joined by a dotted line).

- **By Solution Increment** view: Objective banner (status, RAG, priority, due, forecast end) → SI rows → epic cards in PI columns. **By Delivery Unit** view: rows = Jira projects.
- **Calendar**: sprints are 2 weeks (sprint 292 = 1 Oct 2026), PI85 = sprints 291–298; editable in the side panel. SI timing is derived from its epics; epic timing from its stories' sprints (or the whole PI if moved / no stories).
- **Epic dependencies** are not in JIRA yet: add "blocks" links on an epic, *Save in browser* (re-applied on every import) or export/import as CSV. A real `Blocks` link in the JIRA CSV is read too.
- **Critical path** = longest chain of dependencies with ≤ 1 sprint of slack, compared with the Objective due dates.
- Flags: epic/SI ends after Objective due, SI without epics, Objective without SI, dependency overlap.
- **Data mapping panel**: columns, link-type meanings (solves / relates / blocks / depends / ignore), issue-type levels, priority direction and Delivery Unit source are auto-detected and can all be overridden in the app. Click an SI row header to add/remove its Objective and epic links by hand.
- Simulation: drag epic to another PI, add/remove links, ▲▼ objective priority, auto-resolve. **Reset scenario** = back to imported data; **Clear all** = empty dashboard.

**Import formats**: JIRA *Export → Word* (`.doc`, which is HTML inside) and re-saved `.docx` are read directly, as is CSV. `sample-jira-export.doc` shows the shape. In the Word export the links come as text in a *Linked Issues* column ("relates to KEY", "is solved by KEY" …); the wording → meaning table in the Data mapping panel is editable. Binary Word 97-2003 and JIRA XML are not supported.

CSV columns (one file, all issue types): Issue key, Issue Type, Summary, Status, Assignee, PI, Story Points, Sprint (repeated), Epic Link, RAG Status,
Objective Manager, Global Priority, Due date, and Outward/Inward issue link (Solves / Relates / Blocks) columns. Optional `Project` column (else taken from the key prefix).
