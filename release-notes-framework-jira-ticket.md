# Release Notes Deliverables Framework — Pillar 1 & 2

**Summary:** Build Release Notes Deliverables Framework — Templated Authoring + Feature Statistics Dashboard

PRD: [Release Notes Deliverables Framework](https://tomtom.atlassian.net/wiki/spaces/MANA/pages/1818690857/Release+Notes+Deliverables+Framework)

---

## Background

Creating a release note for TomTom map products today takes several days of manual data gathering, cross-team coordination, and document assembly — with no enforced structure and inconsistent output. This ticket covers the first two pillars of the framework that replace this process. Pillar 3 (Quality Metrics Insights) is tracked in a separate ticket.

Full automation of all release note sections is the required long-term direction. v1 establishes the authoring foundation; future phases must progressively auto-generate all sections until manual authoring is no longer needed.

---

## Pillar 1 — Release Note Document

A template-enforced authoring tool covering four sections: **General Information**, **Highlights**, **Important Notes**, and **Known Issues**. See PRD Section 5 for the full section breakdown and mapping from the current LM document structure.

**Document lifecycle:** `Draft → In Review → Approved → Published`

Publication is **blocked** until all validation gates pass:
1. Every expected statistic has a numeric value (incl. `0`) or explicit `N/A` — no blanks
2. Every statistic record contains all required fields: `name`, `feature`, `country`, `unit`, `value`
3. All automation-generated candidates in Highlights and Lowlights explicitly confirmed or dismissed by the PM/content owner

**Key requirements:**
- Rich text editor (tables, lists, links); versioned drafts with change history and author attribution
- Role-based access: creators (edit) / consumers (read-only)
- Export to PDF
- Automation for General Information, Highlights, and Known Issues via Jira API or equivalent — approach to be defined by the engineering team. **Future direction (required): all sections must be auto-generated; PM/content owner role shifts to review and approval only**
- **Cross-pillar automation surfaces Highlights candidates (positive deltas above threshold) and Lowlights candidates (negative deltas above threshold) from Pillar 2**
- Automation candidates clearly marked as "auto-generated"; must be reviewed and confirmed or dismissed before publication — not auto-published

---

## Pillar 2 — Feature Statistics Dashboard

Automated ingestion and delta comparison of feature counts from the **Analytical Data Plane (ADP)** — no manual data entry.

**Sub-components:**
- **Uncompiled Map Stats** — feature counts and release-to-release deltas for raw map data
- **Compiled Map Stats (NDS.Live)** — primary consumer-facing stats: layer stats, road class statistics (FRC/ARC/PRC in km), feature statistics (attribute km or feature count), and Compilation Report. Details for the NDS.Live section TBD with Dennis van Nooij
- **Release Selector** — any past release as the delta baseline

**Data model:** each record requires `name`, `feature`, `country`, `unit`, `value`. Deltas are derived by the system.

**Value state rules:**
- `0` = pipeline ran, result was zero
- `N/A` = measurement not executed for this release
- Blank/unmarked values must be **rejected at ingestion**

**Key requirements:**
- Stats auto-extracted from ADP; NDS.Live stats shown as primary, uncompiled as drill-down/diagnostic
- Visual delta indicators (up/down/unchanged); distinct `N/A` indicator
- CSV export
- Delta outputs feed the Cross-Pillar Automation layer
- Customer-facing dashboard view automatically scoped to the contracted feature set and country scope sourced from customer delivery information (e.g. CM ticket); no manual adaptation required per release

---

## Cross-Pillar Automation Orchestration (Pillar 2 → Pillar 1)

Feature statistics deltas automatically trigger automation that surfaces Highlights and Lowlights candidates in Pillar 1.

**Regression Detection (Negative Deltas → Lowlights):**
- Negative delta vs. n-1 exceeding the configured regression threshold → auto-generates a Lowlight candidate
- Each candidate includes: statistic name, delta value (absolute + %), and a reason template
- PM must confirm or dismiss each candidate before publication; automation does **not** auto-publish

**Improvement Detection (Positive Deltas → Highlights):**
- Positive delta vs. n-1 exceeding the configured "considerable improvement" threshold → auto-generates a Highlights candidate
- Each candidate includes: statistic name, delta value (absolute + %), and a reason template
- PM must review and incorporate or dismiss each candidate before publication

**Configuration:**
- Thresholds configurable per map product and per metric (e.g., feature count ±5%, coverage ±2%); defined collaboratively by **Map Experts and content PMs** during product setup
- Each product team can opt-in per metric

**Edge Cases:**
- `N/A` statistic values are skipped (no delta computable)
- Missing or `N/A` n-1 value → delta computation skipped
- No n-1 release (first-ever release) → regression detection disabled

---

## Acceptance Criteria

- [ ] Document moves through full `Draft → In Review → Approved → Published` lifecycle with mandatory sign-off
- [ ] Publication blocked with actionable errors if any validation gate fails (including automation candidate review)
- [ ] Feature stats auto-populated from ADP; `0` and `N/A` rendered distinctly; CSV export works
- [ ] Delta indicators (absolute + %) shown for all stats vs. selected baseline release
- [ ] All content changes logged with user + timestamp
- [ ] Published view accessible via stable, versioned URL (read-only)
- [ ] PDF export functional for Pillar 1 documents
- [ ] Automation detects feature statistic regressions above threshold and surfaces Lowlight candidates in authoring UI
- [ ] Automation detects feature statistic improvements above threshold and surfaces Highlights candidates in authoring UI
- [ ] Automation candidates clearly marked as "auto-generated" and distinct from manually authored content
- [ ] Publication blocked until PM explicitly confirms or dismisses all automation candidates
- [ ] Threshold configuration per product accessible and documented (to be finalized during technical design)

---

## Follow-up Actions

### Onboarding & Guidance Page

**Owner:** Engineering team + Process Owner
**Trigger:** Before Beta release; finalized before GA.

Create a dedicated onboarding and guidance page covering all user types of the framework. Structured per persona so each group finds exactly what they need.

**Required coverage:**

| Persona | Content to cover |
|---|---|
| **PM / Content Owner** | How to create and edit a release note; Draft → Published lifecycle; how to review, confirm, and dismiss automation candidates; publication checklist and common blockers |
| **Release Manager** | Dashboard completion tracking; sign-off step; publication blocker resolution |
| **Map Expert** | How to configure quality metrics, measurement descriptions, and target values at product setup; how to set and adjust thresholds; how automation alerting works |
| **Technical Program Manager** | Release selector for cross-release delta comparison; reading and exporting stats reports; interpreting automation candidate outputs |
| **External Customer** | Navigating the published dashboard; reading feature statistics and delta indicators; exporting data (PDF, CSV) |

Must include: step-by-step workflows per persona, annotated screenshots, glossary (e.g., `N/A` vs `0`, automation candidates, Lowlights vs Known Issues), and FAQ per role.

---

### Transition Timeline Plan

**Owner:** Process Owner
**Trigger:** Drafted during Beta; finalized before GA cutover.

Create a structured plan for switching from the current manual release notes process to the new framework across all map products and related artifacts.

**Required content:**

| Element | Description |
|---|---|
| **Current state baseline** | Document existing manual process per map product: tools, people, time per step, pain points |
| **Transition milestones** | Go/no-go gates per product aligned with Section 11 delivery phases: Beta onboarding, parallel running, full cutover, legacy decommission |
| **Parallel running period** | Window where old and new processes run in parallel; criteria for full cutover |
| **Cutover criteria per map product** | All pillars functional, onboarding complete, at least one release published end-to-end via the new framework |
| **Legacy process decommission** | Steps to retire manual processes, spreadsheets, and ad-hoc data flows; communication to affected teams |
| **Customer communication plan** | How and when external customers are informed about the new format and dashboard |
| **Rollback plan** | Conditions for reverting to manual process during transition and steps to do so without disrupting a release |
