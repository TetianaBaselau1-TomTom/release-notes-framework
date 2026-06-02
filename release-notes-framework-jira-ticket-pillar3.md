# Release Notes Deliverables Framework — Pillar 3

**Summary:** Build Release Notes Deliverables Framework — Quality Metrics Insights

PRD: [Release Notes Deliverables Framework](https://tomtom.atlassian.net/wiki/spaces/MANA/pages/1818690857/Release+Notes+Deliverables+Framework)

Related ticket: Release Notes Deliverables Framework — Pillar 1 & 2

---

## Background

As part of the Release Notes Deliverables Framework, Pillar 3 provides customers with the quality story of each map product release — surfacing key KPI metrics inline and linking to the full Quality KPI dashboard. This replaces the current manual process of copying metrics from separate tools into release documents. Pillars 1 and 2 (document authoring and feature statistics) are tracked in a separate ticket.

Full automation of all release note sections is the required long-term direction. Pillar 3 is fully automated from v1; its delta outputs also drive progressive automation of Pillar 1 narrative sections in future phases.

---

## Pillar 3 — Quality Metrics Insights

A gateway to quality data for a given release, embedded within the release notes dashboard.

**Data source: Analytical Data Plane (ADP)** — metrics must be auto-extracted from ADP. No manual data entry.

**Sub-components:**
- **Deep-link to Quality KPI Dashboard** — auto-scoped to the specific map product and release version
- **Inline Key Metrics Summary** — embedded snapshot of critical quality measurements (e.g., LM Basemap Coverage, Lane Divider Thematic Accuracy, Lane Divider Relative Positional Accuracy)
- **Metric Trend Indicators** — visual signal showing whether each metric improved, regressed, or held steady vs. n-1 release
- **Measurement Descriptions** — static, per-metric methodology definitions; configured once per product at setup, not edited per release

**Key requirements:**
- Metrics auto-extracted from ADP; no manual entry
- Dashboard deep-link automatically scoped by product + release — **must be validated as a Discovery gate** (Week 1–2); if not supported, degrade gracefully to a static link
- Customer-facing view automatically scoped to contracted feature set and country scope from customer delivery information (e.g. CM ticket); no manual adaptation required per release
- Configurable per product: which KPIs appear in the inline summary
- Measurement descriptions, quality target values, and KPI configurations are maintained by **Map Experts** at product setup time; they are not edited per release
- Automation alerting for quality metric regressions (cross-pillar) is configurable by **Map Experts** per product and per metric
- Graceful degradation with a clear status indicator when ADP or the KPI dashboard is unavailable
- Value state rules (same as Pillar 2):
  - `0` = pipeline ran, result was zero
  - `N/A` = measurement not executed (e.g., ground truth unavailable); does not block publication but must be displayed with a clear indicator
  - Blank values not permitted
- **Quality metrics linked to specific features must reference the corresponding Jira CM tickets and Quality sub-tickets (Quality Measures, Target, Results) for full traceability**
- **Quality target values must be extracted from Jira Quality sub-tickets during product setup. The system uses these to compute variance, status indicators (on-track / at-risk / regressed vs. target), and regression detection thresholds for cross-pillar automation**

---

## Cross-Pillar Automation Orchestration (Pillar 3 → Pillar 1)

Quality metrics deltas automatically trigger automation that surfaces Highlights and Lowlights candidates in Pillar 1 (same pattern as Pillar 2).

**Regression Detection (Negative Deltas → Lowlights):**
- Negative delta vs. n-1 exceeding the configured regression threshold → auto-generates a Lowlight candidate
- Each candidate includes: metric name, delta value (absolute + %), and a reason template (e.g., "Lane Divider Coverage decreased by 1.8% vs. n-1")
- PM must confirm or dismiss each candidate before publication

**Improvement Detection (Positive Deltas → Highlights):**
- Positive delta vs. n-1 exceeding the configured "considerable improvement" threshold → auto-generates a Highlights candidate
- Each candidate includes: metric name, delta value (absolute + %), and a reason template (e.g., "LM Basemap Coverage improved by 1.2% vs. n-1")
- PM must review and incorporate or dismiss each candidate before publication

**Configuration:**
- Thresholds configurable per map product and per metric (e.g., coverage ±2%, accuracy ±3%); defined collaboratively by **Map Experts and content PMs** during product setup
- Each product team can opt-in per metric
- For quality metrics, regression thresholds may be derived from or aligned with target values from Jira Quality sub-tickets

**Edge Cases:**
- `N/A` metric values are skipped (no delta computable)
- Missing or `N/A` n-1 value → delta computation skipped
- No n-1 release (first-ever release) → regression detection disabled

---

## Acceptance Criteria

- [ ] Quality KPI dashboard deep-link auto-scoped to the correct product and release version
- [ ] Inline metrics snapshot renders with values from ADP; `0` and `N/A` displayed distinctly
- [ ] Trend indicators (improved / regressed / stable) shown vs. n-1 release for each metric
- [ ] Configurable per product: which KPIs appear in the inline summary
- [ ] Section degrades gracefully with a status indicator when ADP or KPI dashboard is unavailable
- [ ] Measurement descriptions static, configured at product setup, and surfaced correctly in the UI
- [ ] Quality target values extracted from Jira Quality sub-tickets at setup; variance and status indicators computed correctly
- [ ] Jira CM and Quality sub-ticket links present per metric where applicable
- [ ] Automation detects quality metric regressions above threshold and surfaces Lowlight candidates in authoring UI (Pillar 1)
- [ ] Automation detects quality metric improvements above threshold and surfaces Highlights candidates in authoring UI (Pillar 1)
- [ ] Automation candidates clearly marked as "auto-generated" and distinct from manually authored content
- [ ] Publication blocked until PM explicitly confirms or dismisses all automation candidates
- [ ] Threshold configuration per product and per metric accessible and documented (to be finalized during technical design)

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
| **Transition milestones** | Go/no-go gates per product aligned with pillar delivery phases: Beta onboarding, parallel running, full cutover, legacy decommission |
| **Parallel running period** | Window where old and new processes run in parallel; criteria for full cutover |
| **Cutover criteria per map product** | All pillars functional, onboarding complete, at least one release published end-to-end via the new framework |
| **Legacy process decommission** | Steps to retire manual processes, spreadsheets, and ad-hoc data flows; communication to affected teams |
| **Customer communication plan** | How and when external customers are informed about the new format and dashboard |
| **Rollback plan** | Conditions for reverting to manual process during transition and steps to do so without disrupting a release |
