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

---

## 🚀 How to Use

1. Open `roadmap-drilldown_4.html` in any modern browser (Chrome, Edge, Firefox)
2. No server, no dependencies — it runs fully offline
3. Share the file directly or host via GitHub Pages for team access

---

## 🔄 Status

> ⚠️ **Interactive proof of concept — client-side only**

The app now does three things end-to-end:

1. **Structure** — drill-down across Strategic Theme → Program → Objective →
   Solution → Delivery Unit → Story, imported from a Jira CSV export.
2. **Interactivity** — every item can be created, edited, re-parented,
   deleted, and linked to dependencies via the ✎ / 🗑 icons and the **+ Add**
   button on each level. Edits are held in the browser's `localStorage`, so
   they survive a reload without any backend — "**⚠ Reset data**" in the
   top bar wipes local edits back to the seed dataset.
3. **Analytics behind every action** — the bottom panel has two tabs:
   **AI Analytics** (rule-based insights on the current view — ownership
   gaps, confidence clusters, team overload, dependency sequencing risk)
   and **Activity Log** (a full audit trail: who changed what, from what
   value to what, and when — filterable and exportable to CSV).

This is deliberately a no-backend POC: open the HTML file, no install, no
server, no database. That's the tradeoff for the "changing every field,
every dependency, live" experience without infrastructure — see
*Planned Direction* below for what a multi-user version would need.

---

## 🛣️ Planned Direction

- [x] Finalize portfolio structure and product hierarchy
- [x] Add drill-down navigation (portfolio → product → epic/feature level)
- [x] Interactive editing: create/edit/delete/re-parent + dependencies
- [x] Per-action activity log (client-side audit trail)
- [ ] **Configurable hierarchy** — today `LEVELS` / `LEVEL_LABELS` /
      `FIELD_DEFS` in the script are shared by everyone opening the file.
      For different people to monitor *their own* project/program/portfolio
      with their own level names and fields, this config needs to move out
      of the script and into a per-portfolio definition the app loads.
- [ ] **Real Jira sync** — today import is a one-time CSV drop. A live
      version would pull from Jira's REST/GraphQL API (or a synced export)
      so the structure reflects Jira as of right now, not as of the last export.
- [ ] **Shared, multi-user backend** — `localStorage` is per-browser. Once
      several people need to see the *same* edits and the *same* activity
      log, this needs a real datastore (e.g. a small API + Postgres, or a
      hosted backend like Supabase/Firebase) behind it, plus auth so
      "Acting as" becomes a real identity instead of a free-text field.
- [ ] Stakeholder-friendly view vs. team-level detail view
- [ ] Potential GitHub Pages deployment for easy sharing of the POC

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
**Tech:** Pure HTML/CSS/JS — no framework, no build step, no server. Edits and the activity log persist per-browser via `localStorage`.  

---

*Last updated: August 2026*
