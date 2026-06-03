# Release Notes Deliverables Framework

A three-pillar framework for automated creation, management, and publication of map product release notes at TomTom. Replaces fragmented, manual workflows with a structured, largely automated system.

**Confluence PRD:** https://tomtom.atlassian.net/wiki/spaces/MANA/pages/1818690857/Release+Notes+Deliverables+Framework
**Jira:** https://tomtom.atlassian.net/browse/OPC-16459
**Product Owner:** Tetiana Baselau

---

## What it does

The framework enables release notes content owners and release managers to produce consistent, publish-ready release notes and quality reports for map products — with ≥80% of content auto-populated from upstream systems. Customer-facing views are automatically scoped per customer based on their delivery information (e.g. CM ticket); no manual adaptation is needed.

---

## Three Pillars

| Pillar | What it covers |
|---|---|
| **Pillar 1 — Release Note Document** | Templated authoring tool for General Information, Highlights, Important Notes (incl. Lowlights), and Known Issues. Draft → In Review → Approved → Published lifecycle with mandatory sign-off. |
| **Pillar 2 — Feature Statistics Dashboard** | Automated ingestion of feature counts from ADP (Analytical Data Plane) with release-to-release delta comparison. Uncompiled and compiled (NDS.Live) map stats. CSV export. |
| **Pillar 3 — Quality Metrics Insights** | Inline quality KPI snapshot and deep-link to the Quality KPI Dashboard, auto-scoped to the product and release. Metric trend indicators vs. n-1. |

A **Cross-Pillar Automation Orchestration** layer monitors deltas from Pillars 2 and 3 and surfaces regression and improvement candidates into Pillar 1 (Highlights and Lowlights) for PM review before publication.

Any observable change that impacts released product quality — regression or considerable improvement — must be documented in the respective Release Notes section. Automation is designed to detect and surface all such changes.

---

## Key Design Principles

- **No manual data entry** — all statistics and quality metrics are auto-extracted from ADP.
- **Scale over customisation** — one framework serves all customers; customer views are scoped automatically.
- **Full automation direction** — v1 establishes the foundation; all sections must be progressively auto-generated in future phases.
- **PM retains sign-off** — automation surfaces candidates; nothing is auto-published.

---

## Files in this repo

| File | Description |
|---|---|
| `release-notes-framework-prd.md` | Local sync of the Confluence PRD (source of truth is Confluence). Regenerated after each PRD update. |
| `release-notes-framework-jira-ticket.md` | Jira Epic description for Pillar 1 & 2. |
| `release-notes-framework-jira-ticket-pillar3.md` | Jira Epic description for Pillar 3. |
| `release-notes-prd-sync.skill` | Claude Code skill — invoke with `/release-notes-prd-sync` to propagate any PRD change to all destinations: Confluence, local file, this repo, and a PR to `tomtom-internal/orbis-release-notes-service`. |

---

## Key Dependencies

| System / Person | Role |
|---|---|
| **ADP (Analytical Data Plane)** | Sole data source for all automated statistics; owned by MAA / Sasha Haber |
| **Quality KPI Dashboard** | Deep-linked from Pillar 3; must support parameterized linking by product + release |
| **Jira Quality sub-tickets** | Source for quality target values extracted at product setup |
| **Customer delivery information (CM ticket)** | Source for automatic customer view scoping (feature set + country scope) |
| **NDS.Live PM** | NDS.Live compiled map stats input for Pillar 2 |
