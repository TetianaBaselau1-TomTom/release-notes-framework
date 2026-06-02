# Release Notes Deliverables Framework — PRD

**Author:** Tetiana Baselau
**Status:** Draft v1.0
**Confluence (source of truth):** https://tomtom.atlassian.net/wiki/spaces/MANA/pages/1818690857/Release+Notes+Deliverables+Framework
**Related Jira:** https://tomtom.atlassian.net/browse/OPC-16459

> This file is kept in sync with the Confluence PRD. Do not edit it directly — update the Confluence page and regenerate.

---

> _Last Confluence sync: v39 (2026-05-28). The Document content reflects LM Release notes structure as of 4/27/2026; later LM document modifications are not taken into account._

| **Reviewers / Stakeholders** | **Status** |
| --- | --- |
| @Ioanna Kostara (LM content owner/PM) |  |
| @Raquel Rosa (RM/LM content owner/PM) |  |
| @Marta Olek-Przydatek (MapEx team) |  |
| @Daniela Leon (TPM) |  |
| @Engin Erkan (TPM) |  |
| @Anna Cywinska (TPM) |  |
| @Stefanie Gysels (RM) |  |
| @Ashwini Raskar (EM) |  |
| @Tomasz Szambor  (EM) |  |
| @Jakob Coppens (Pillar 1-2) |  |
| @Jacek Bleja (Pillar 1-2) |  |
| @Oleksandr Kozak Kozak (Pillar 3) |  |

---

## Product Brief

|  |  |
| --- | --- |
| **What** | An internal/external dashboard and tooling framework that enables release notes content owners and release managers to create, configure, and publish structured release notes and quality reports for map products — ready to be exposed directly to external customers with minimal additional effort. **The framework is designed to serve all customers across TomTom's map product lines. Core release note content is standardised per product line; the customer-facing dashboard is automatically scoped per customer based on their delivery information (e.g. CM ticket) — no manual adaptation is needed.** |
| **Who** | **Internal (creators):** Release notes content owners (PMs), release managers, Map Experts, and Technical Program Managers.  **External (consumers):** Customers of TomTom's map products — Road Model and Lane Model maps — who rely on release notes as a key input for integration and their products development. |
| **Why now** | The current process is heavily manual, error-prone, and not scalable as the number of map product releases grows. Assembly of a single release note requires gathering data from multiple disconnected sources by hand, leading to delays and inconsistencies. Customer feedback consistently points to release notes that carry limited or irrelevant information — lacking clarity on geo scope and feature coverage, and missing quality insights altogether. Addressing this now protects both internal efficiency and external customer trust at a point of growth. |
| **Outcomes** | **Efficiency:** ≥70% reduction in end-to-end time to produce a complete, publish-ready release note.  **Quality & completeness:** 100% of required sections filled at the time of publication;  ≥80% of structured content (stats, metrics) auto-populated with no manual data entry.  **Customer trust & usage:** Measurable improvement in customer satisfaction with release notes (baseline survey to be established); ≥50% reduction in ad-hoc post-release data requests from customers. |
| **Scope (v1)** | Templated release note document authoring (general information, highlights, known issues, important notes) with draft→review→publish workflow; feature statistics dashboard for uncompiled and compiled map outputs (NDS.live and other formats) with release-to-release delta comparison; link to the quality metrics dashboard; export to PDF for the release notes document, CSV files for the feature statistics/deltas; **cross-pillar automation that surfaces significant statistical and quality metric deltas as highlights or lowlights**; **automatic customer-specific view scoping derived from customer delivery information (e.g. CM ticket)**. |
| **Out of scope** | Automated push-publishing to external customer portals; **per-customer branding or white-labeling** (per-customer view scoping is automatic and derived from delivery information — no manual adaptation or separate implementations); support for non-map product lines; mobile-optimized consumer interface; per-KPI-route measurement breakdown (may be reconsidered if data becomes available in ADP for inclusion in Pillar 3). |
| **Timeline** | Discovery & design   Pillar 1: Document MVP  Pillar 2: Feature Stats MVP Pillar 3: Quality Metrics MVP  Integration & end-to-end testing Beta with 1-2 customers  General availability  _(See Section 11 for full timeline details.)_ |

---

## Executive Summary

The Release Notes Deliverables Framework replaces a fragmented, manual release notes process with a structured internal platform purpose-built for TomTom's map products. Today, creating a single release note can take several days of manual data gathering, cross-team coordination, and document assembly — with no enforced structure and inconsistent output quality.

The framework introduces three integrated pillars: a **templated document authoring tool** (general information, highlights, known issues, important notes), an **automated feature statistics dashboard** (uncompiled and compiled map stats with delta comparison), and a **quality metrics gateway** (linking to the Quality KPI system with an inline summary). A **cross-pillar automation orchestration** layer analyzes deltas from Pillars 2 and 3, automatically surfacing candidates for Highlights (positive deltas) and Lowlights (regressions) in Pillar 1 based on configurable thresholds. Together, these pillars enable release notes creators to produce consistent, complete, publish-ready deliverables with ≥80% of content auto-populated from upstream systems.

**The framework serves all customers and is built to scale across product lines.** Core release note content is standardised per product line. Customer-facing views are automatically scoped in the background based on customer delivery information (e.g. CM ticket) — no manual adaptation is needed and no separate implementations are required.

**Full automation across all release note sections — including narrative content — is the required long-term direction.** v1 establishes the automation foundation; future phases must progressively automate every remaining section until manual authoring is no longer required.

**Key targets:** ≥70% reduction in release note production time; 100% section completeness at publication; ≥50% reduction in ad-hoc post-release data requests from customers. General availability is targeted at TBD.

---

## 1. Overview

The Release Notes Deliverables Framework is an internal platform designed to streamline the creation, management, and distribution of map product release notes and associated quality reports. It replaces fragmented, manual workflows with a structured, largely automated system — enabling release notes creators and content owners to produce consistent, high-quality deliverables with minimal manual effort.

The framework is built to serve all customers across TomTom's map product lines through a single implementation. Core content is standardised per product line. Customer-facing views are automatically scoped in the background based on the customer's delivery information (e.g. CM ticket) — reflecting their contracted feature set and country scope without any manual adaptation.

---

## 2. Problem Statement

### Current State (Today)

Today, release notes for map products are assembled manually through a multi-step process involving several disconnected tools and teams. Content owners gather feature statistics from raw data pipeline outputs (typically files or spreadsheets shared ad hoc), quality metrics from the Quality KPI dashboard (accessed separately), and written inputs from engineering and product teams — each through separate channels and with no standardized handoff. These inputs are then manually consolidated into a Confluence page or document, reviewed informally, and distributed to customers.

The assembly process typically spans several days and involves significant back-and-forth between teams. There is no enforced document structure, resulting in variability in completeness and format across releases. Version control is informal, change history is not preserved, and there is no audit trail for edits made during the assembly process. The absence of a single source of truth makes it difficult to ensure consistency or to onboard new contributors quickly.

### Key Pain Points

Today, creating release notes for map products involves significant manual effort spread across multiple tools and teams. Content owners must gather feature statistics, quality metrics, and documentation inputs independently, assemble them into documents by hand, and ensure consistency across releases. This process is slow, error-prone, and difficult to scale. Consumers of release notes — external customers relying on this content for integration decisions — receive deliverables that may lack consistency or completeness, undermining trust in the product.

There is no single source of truth or standardized structure for release notes deliverables. The framework aims to fix this.

---

## 3. Goals & Objectives

**Primary goals:**

* Enable release notes creators and content owners to produce structured, complete release note deliverables with minimal manual effort.
* Automate or semi-automate the aggregation of feature statistics, quality metrics, and document sections.
* Establish a consistent, reusable structure for all map product release notes.
* Provide consumers (external customers) with a clear, reliable, and machine-readable output they can use as input for map product integration.
* **Automatically surface significant statistical and quality metric changes (both regressions and improvements) as candidates for Highlights or Lowlights, reducing manual review effort.**
* **Any observable change that impacts released product quality — whether a regression or a considerable improvement — must be documented in the respective Release Notes section. Automation must be planned to systematically detect and surface such changes, reducing reliance on manual discovery and preventing quality signals from being missed.**
* **Enable Map Experts to shift from manual quality artifact production and reporting to automated generation, comparison, and alerting — reducing time spent on data collection and population tasks.**
* **Serve all customers through a single scalable framework — core release note content is standardised per product line; customer-facing views are automatically scoped per customer based on their delivery information (e.g. CM ticket), with no manual adaptation required.**
* **Establish full automation as the long-term direction for all release note sections — including narrative content (general information, highlights, important notes, known issues). v1 automation covers statistics, quality metrics, and delta-based candidates; all remaining sections must be progressively automated in future phases until manual authoring is no longer required.**

**Non-goals (out of scope for v1):**

* Automated publishing to external customer portals (can be considered in a future phase).
* Real-time map data processing or feature computation — the framework consumes pre-computed statistics.
* Per-customer branding or white-labeling — customer view scoping is automatic and derived from delivery information, not visual customisation.
* Support for non-map product lines.
* Per-KPI-route measurement breakdown — may be reconsidered if data becomes available in ADP and the KPI route data needs to remain in the release notes long-term (Pillar 3 future scope).

_(See also: Out of Scope in Product Brief above.)_

---

## 4. User Personas

### Group 1 — Creators & Owners (Internal)

These users produce and manage the release notes deliverables. See https://tomtom.atlassian.net/wiki/spaces/MANA/pages/1910047018 for the details.

| Persona | Role | Primary Need |
| --- | --- | --- |
| **Release Notes Creator / PM / Content Owner** | Writes and assembles release note documents; owns the narrative and feature highlights | Easy editing of highlights, important notes, and known issues within a consistent template; automated surfacing of significant changes to reduce manual review |
| **Release Manager** | Oversees the end-to-end release process | Status visibility, sign-off workflow, completeness checks |
| **Map Expert** | Working with quality artifacts: producing, analyzing, reporting, investigating the issues | Automation of the quality artifacts generation, comparison, alarming, results population |
| **Technical Program Manager** | Coordinates cross-functional release activities | Dashboard overview, delta reports vs. previous releases; automated insights on significant changes, communication with the customers |

### Group 2 — Consumers (External)

These users receive and act on the release notes.

| Persona | Role | Primary Need |
| --- | --- | --- |
| **External Customer (Map Product User)** | Integrates TomTom map data into their product | Clear scope, feature deltas, quality signal, known issues — automatically scoped to their contracted feature set and country scope |

### Key Stakeholders

| Stakeholder | Role | Involvement |
| --- | --- | --- |
| **Tetiana Baselau** | Product Owner / Author | Accountable for product definition, prioritization, and delivery |
| **Content PMs** | Creators and owners of release notes content; accountable for map quality and quality metrics values | Primary authors of release note narratives; responsible for content accuracy, quality metrics sign-off, and completeness of map quality reporting |
| **Release Managers** | Process owners | Key input on workflow requirements; primary internal beta users |
| **Map Experts** | Owners of the several quality artefacts execution, analysis and results population into the release notes | Owners of the several quality artefacts execution, analysis and results population into the release notes |
| **Map Product Engineering Leads** | Technical counterparts | Own upstream data pipelines and API contracts |
| **Technical Program Managers** | Cross-functional coordinators | Consumers of delta reports; stakeholders in dashboard design |
| **Customer Success / External Customers** | End consumers | Input on output format, content completeness, and quality signals |
| **VS Teams /MAA** | Owners of Quality KPI system / Owner of the quality frameworks and platforms | Enable metrics integration; define KPI availability and API contract |

---

## 5. Product Structure & Key Features

The Release Notes Dashboard is built around **three pillars** plus a **cross-pillar automation orchestration layer**:

---

### Mapping: LM Document Sections → Framework

The table below shows how each section from the current LM release notes structure (as defined in the [LM map: Generalized Structure + Guidelines](https://tomtom.atlassian.net/wiki/spaces/MANA/pages/1677164558)) is addressed in this framework.

| LM Document Section (current) | Framework Pillar | How it's addressed |
| --- | --- | --- |
| **Important Note** | Pillar 1 — General Information | Sub-section |
| **Executive Summary** | Pillar 1 — General Information | Sub-section |
| **Scope** | Pillar 1 — General Information | Sub-section |
| **Delivery Content** | Pillar 1 — General Information | Sub-section |
| **Lane Model Map Metadata** | Pillar 1 — General Information | Sub-section |
| **LM Basemap — Primer version per geography** | Pillar 1 — General Information | Temporary sub-section; to be removed when no longer operationally relevant |
| **Lowlights** | Pillar 1 — Important Notes | Dedicated section (release-specific regressions, distinct from ongoing Known Issues) |
| **Other LM Features** (from Remarks) | Pillar 1 — Important Notes | Optional sub-section |
| **Cariad Routes Specific** (from Remarks) | Pillar 1 — Important Notes | Optional sub-section |
| **Metric Retirement** | Pillar 1 — Important Notes | Optional sub-section |
| **Remarks** (methodology / measurement notes) | Pillar 1 — Important Notes | Sub-section |
| **What's New** | Pillar 1 — Highlights | Included |
| **Improvements & Fixes** | Pillar 1 — Highlights | Included |
| **Known Issues** | Pillar 1 — Known Issues | Dedicated section |
| **Measurements** (LM Basemap Coverage, Cohesion Checks, Lane Divider Thematic Accuracy, Lane Divider Relative Positional Accuracy) | Pillar 3 — Quality Metrics Insights | Auto-populated from ADP |
| **Measurement descriptions** (per-metric methodology definitions) | Pillar 3 — Quality Metrics Insights | Static content, configured per product; surfaced when KPI dashboard becomes available |
| **Feature aggregates / counts** (uncompiled map) | Pillar 2 — Uncompiled Map Stats | Auto-populated from ADP |
| **NDS.Live Statistics** | Pillar 2 — Compiled Map Stats | Auto-populated from ADP |
| **NDS.Live Compilation Report** | Pillar 2 — Compiled Map Stats | Sub-component, Will be skipped in the future |
| **Per-KPI-route measurement breakdown** | Out of scope (v1) | May be reconsidered if data available in ADP for Pillar 3 |
| **Appendix / Glossary** | Not in scope | Skipped in the automation framework |

---

### Pillar 1 — Release Note Document

The core deliverable: a structured document covering the release's essential information.

**General requirements:**

* Templated structure that enforces section completeness before publication.
* Rich text editing with support for links, tables, and structured lists (still tbd).
* Versioned drafts with change history and author attribution.
* Document lifecycle: **Draft → In Review → Approved → Published (to be checked with a team)**, with a mandatory sign-off step before publication.
* Ability to export the document to PDF for downstream consumption.

**Future direction (required):** All sections of the Release Note document — including all narrative content — must be auto-generated in future phases. In v1, automation covers statistics, quality metrics, and delta-based candidates for Highlights and Lowlights. Progressive automation of General Information, Highlights, Important Notes, and Known Issues is required in subsequent phases until manual authoring is no longer needed.

---

#### Section: General information

Covers the contextual and administrative information for the release. Contains the following sub-sections:

* **Important Note** — Release type (weekly/monthly), date, and an overview of what the document contains (which sections are included, where attachments live).
* **Executive Summary** — A short narrative summary of the release: what was delivered, the key quality outcomes, any regressions under investigation, and what to expect next. Authored by the PM/content owner.
* **Scope** — Geographic coverage for this release (countries/regions included, any geography-specific notes).
* **Delivery Content** — Delivery format (e.g., NDS.Live endpoint), full features list, API endpoint to access the data, and reference to specifications.
* **Lane Model Map Metadata** — Build branch, version reference, LM basemap revisionID, binding layer revision. _(Temporary sub-section to support the development phase; intended to be removed once no longer operationally relevant.)_
* **LM Basemap — Primer version per geography** — Primer version used per geography and region (e.g., DEU NW: v0.9, NE: v0.10, SWE: v0.12). _(Temporary sub-section; to be removed when primer versioning is stable and no longer customer-relevant.)_

**Automation & data extraction:** Jira Automation or other tooling — to be defined by the engineering team. **Future direction (required): all General Information sub-sections must be auto-populated in future phases.**

---

#### Section: Highlights

New features, notable improvements, and resolved issues introduced in this release. Contains:

* **What's New** — Anything newly introduced in the product (new features, geographies, datasets, capabilities). If nothing is new, explicitly states "n/a".
* **Improvements & Fixes** — Enhancements and resolved issues, tagged with `[FIX]`, `[IMPROVE]`, or `[NEW]`. May be split into sub-sections by component (LM Basemap, Other LM Features, Cariad Routes Specific).

Content is authored and curated by the PM/content owner in v1; automation surfaces candidates for review — it does not publish them directly. **Future direction (required): all Highlights content must be auto-generated; the PM/content owner role shifts to review and approval only.**

**Automation & data extraction:**

Any considerable improvement in released product quality must be documented in this section. Automation must be planned to detect and surface such improvements, ensuring no significant positive change is missed.

* Jira Automation or other tooling — to be defined by the engineering team.
* **Cross-Pillar Automation:** The system automatically identifies feature statistics (Pillar 2) and quality metrics (Pillar 3) with **positive deltas** that exceed the configured "considerable improvement" threshold (to be defined during technical design) and surfaces them as candidates for Highlights. Candidates are presented to the PM/content owner for review and incorporation; automation does not auto-publish.

---

#### Section: Important Notes

A dedicated section for release-specific contextual information that does not fit Highlights or Known Issues. The following sub-sections are supported; all are **optional** except Lowlights:

* **Lowlights** _(required)_ — Quality regressions identified in this specific release, with quantified impact (e.g., %, count), root cause status, and expected fix timeline. Distinct from Known Issues (which are persistent, ongoing defects) and from Highlights (which are improvements). Each item should include: what regressed, by how much, what is under investigation, and ETA for resolution.
* **Other LM Features** _(optional)_ — Feature-specific limitations, caveats, or notes that affect interpretation of the release but are not bugs (e.g., coverage limited to motorways, features in early automation phase, upcoming removals).
* **Cariad Routes Specific** _(optional)_ — Notes and context specific to Cariad KPI routes (e.g., manual moderation focus areas, customer-route-specific known behaviours). May be extended to other named customers.
* **Metric Retirement** _(optional)_ — Advance notice of metrics or document sections being deprecated in upcoming releases, including the replacement metric or approach and the target release week.
* **Remarks** _(optional)_ — Measurement methodology notes and caveats that affect interpretation of the data (e.g., "all measurements are based on pre-NDS.live compilation", denominator definitions, known data behaviour quirks). Not a defect list — these are contextual notes.

**Automation & data extraction:**

Any quality regression in released product quality must be documented in Lowlights. Automation must be planned to detect and surface such regressions, ensuring no significant quality deterioration goes undocumented before publication.

* Manual authoring only for non-Lowlights sub-sections in v1. **Future direction (required): all Important Notes sub-sections must be auto-generated in future phases.**
* **Cross-Pillar Automation:** The system automatically identifies feature statistics (Pillar 2) and quality metrics (Pillar 3) with **negative deltas** (regressions) that exceed the configured threshold (to be defined during technical design) and surfaces them as candidates for Lowlights. Each candidate includes the observed metric/statistic, the delta value, and reasoning (e.g., "Lane Divider Coverage regressed by 2.1% vs. n-1"). Candidates are presented to the PM/content owner for review; they must confirm and provide additional context (root cause, ETA for fix) before publication.

---

#### Section: Known Issues

Key known issues, limitations, and remarks relevant to the release. Contains:

* **Known issues list** — Defects grouped by component (LM Basemap, Other LM Features, Cariad Routes Specific, Other). Each item includes: description, cause (if known), impact, and expected fix timeline. New items are tagged `[NEW]`.

Supports manual entry and structured tagging (severity, affected area, workaround).

**Automation & data extraction:** Jira Automation or other tooling — to be defined by the engineering team. **Future direction (required): Known Issues must be fully auto-populated from Jira in future phases.**

---

#### Cross-Section Workflow Automation

Jira Automation or other tooling — to be defined by the engineering team.

---

### Pillar 2 — Feature Statistics

Comparative feature statistics across map compilation outputs, giving customers and creators a clear quantitative view of what changed.

**Preferred data source: Analytical Data Plane (ADP).** Feature statistics — both uncompiled and compiled — must be automatically extracted from ADP as the authoritative, centrally governed source. ADP provides the structured, release-scoped datasets needed to populate statistics without any manual extraction or data entry.

**Sub-components:**

* **Uncompiled Map Stats** — Feature counts and deltas for the raw/uncompiled map data (e.g., road segments, POIs, addresses). Supports comparison against any previously selected release.
* **Compiled Map Stats** — Feature counts and deltas for compiled map formats (NDS.live or other format targets). Same comparison capability as uncompiled stats.

    * Other parts - to be added by @Dennis van Nooij
    
* **Release Selector** — Users can pick any past release as the baseline for delta computation.

**Requirements: - might be extended for the NDS.live part by** @Dennis van Nooij

* Stats are automatically extracted from ADP; no manual entry of numbers.
* Each statistic data point must include the following required fields: **name**, **feature**, **country**, **unit**, and **value**. All other fields (e.g., deltas, percentages) are derived and calculated by the system.
* **Value states:** A statistic value of **0** means the pipeline ran and the result was zero. A value of **N/A** means the measurement was not executed for this release (e.g., pipeline not run, ground truth not yet available). These two states are distinct and must be surfaced differently in the UI. N/A does not block publication but must be displayed with a clear status indicator.
* Every expected statistic must have either a numeric value (including 0) or an explicit N/A state. Unmarked / blank values are not permitted.
* Deltas are computed and displayed as both absolute values and percentages.
* Visual indicators (up/down/unchanged) for quick at-a-glance interpretation.
* Configurable feature categories to match the map product's taxonomy.
* Export as table (CSV / spreadsheet) for customer use.
* **The statistics view is automatically scoped per customer based on their delivery information (e.g. CM ticket) — customers see only the features and countries relevant to their contracted scope. No manual adaptation is needed; scoping happens in the background.**
* For a NDS.Live map, the Compiled Map stats are the stats which represents the map the customer sees. The user interface should reflect that :

    * NDS.Live stats are the primary source of information
    * Uncompiled map stats can be used
    
        * To do root cause analysis when NDS.Live stats are different
        * To see which features are in the uncompiled map and might appear in the compiled map later
        
    
* NDS.Live stats contain 4 different sections

    * Layer stats, listing the layers which are compiled, the version and the size
    * Road Class statistics
    
        * For FRC, ARC and PRC, list the nr of kms
        
    * Feature statistics
    
        * For attributes, list the nr of km's with that attribute
        * For features (like Traffic lights), list the count
        
    

---

### Pillar 3 — Quality Metrics Insights

A gateway to the quality story of the release, providing customers with the confidence signals they need.

**Preferred data source: Analytical Data Place (ADP).** Quality metrics must be automatically extracted from ADP, which serves as the central store for map quality KPIs across products and releases. ADP enables consistent, release-scoped metric retrieval without reliance on manual exports or point-in-time snapshots.

**Sub-components:**

* **Link to Quality KPI Dashboard** — Deep link into the existing quality KPIs dashboard, scoped to the specific map product and release.
* **Key Metrics Summary** — A curated, embedded snapshot of the most critical quality measurements surfaced inline (e.g., LM basemap coverage, Lane divider thematic accuracy, Lane Divider Relative Positional Accuracy).
* **Metric Trend Indicators** — Visual indicators showing whether key metrics improved, regressed, or held steady vs. the previous release.
* **Measurement Descriptions** — Static, per-metric methodology definitions (e.g., how LM Basemap Coverage is calculated, what Cohesion Checks measure, denominator definitions). These are configured once per product setup and do not change release-to-release. Surfaced within the KPI dashboard view once it becomes available.

**Requirements:**

* Metrics snapshot is automatically extracted from ADP; no manual data entry.
* Dashboard link is automatically scoped to the correct product and release version.
* Configurable: each product team can define which KPIs surface in the inline summary.
* Measurement descriptions, quality target values, and KPI configurations are maintained by **Map Experts** at product setup time; they are not edited per release.
* Automation alerting for quality metric regressions (cross-pillar) is configurable by **Map Experts** per product and per metric.
* If ADP or the Quality KPI dashboard is unavailable or data is pending, the section gracefully degrades with a status indicator.
* **Value states for metrics follow the same rule as Pillar 2:** 0 = pipeline ran, result was zero; N/A = measurement not executed (e.g., ground truth not available for a geography). N/A must be displayed with a clear indicator and does not block publication.
* **Quality metrics linked to specific features must reference the corresponding Jira CM tickets and Quality sub-tickets (Quality Measures, Target, Results) for full traceability and context.**
* **Quality target values (e.g., target coverage %, target accuracy %) must be extracted from Jira Quality sub-tickets during product setup. The system uses these target values to compute variance, status indicators (on-track / at-risk / regressed vs. target), and to drive regression detection thresholds in cross-pillar automation.** This provides a single source of truth for quality expectations across the framework.

---

### Cross-Pillar Automation Orchestration

**Any observable change that impacts released product quality — whether a regression or a considerable improvement — must be documented in the respective Release Notes section. Automation must be planned to systematically detect and surface such changes. This orchestration layer is the primary mechanism for ensuring quality changes are automatically identified and surfaced for PM/content owner review before publication.**

A dedicated orchestration layer monitors deltas in Pillars 2 (Feature Statistics) and 3 (Quality Metrics) and automatically surfaces significant changes as candidates for Pillar 1 (Highlights and Lowlights).

**Regression Detection (Negative Deltas → Lowlights):**

* When a feature statistic (compiled or uncompiled) or quality metric shows a **negative delta vs. n-1 that exceeds the configured regression threshold**, the system automatically generates a Lowlight candidate.
* Each candidate includes: metric/statistic name, delta value (absolute + %), delta direction (down), and optionally a reason template (e.g., "Lane Divider Coverage decreased by 2.1% vs. n-1 release").
* Candidates are presented to the PM/content owner in the Lowlights section for review, confirmation, and enrichment (root cause, ETA for fix).
* Automation does not auto-publish Lowlights; they must be explicitly confirmed by the content owner before publication.

**Improvement Detection (Positive Deltas → Highlights):**

* When a feature statistic (compiled or uncompiled) or quality metric shows a **positive delta vs. n-1 that exceeds the configured "considerable improvement" threshold**, the system automatically generates a Highlights candidate.
* Each candidate includes: metric/statistic name, delta value (absolute + %), delta direction (up), and optional reason template.
* Candidates are presented to the PM/content owner in the Highlights section for review and incorporation.
* Automation does not auto-publish Highlights; they must be explicitly reviewed and incorporated by the content owner before publication.

**Configuration & Thresholds:**

* Regression and improvement thresholds are configurable per map product (e.g., feature count: ±5%, coverage metric: ±2%).
* Thresholds are defined collaboratively by **Map Experts and content PMs** during product setup (Discovery phase) and can be adjusted if data patterns change.
* Each product team can define which statistics and metrics trigger automation (opt-in per metric).
* **For quality metrics, regression thresholds may be derived from or aligned with target values defined in Jira Quality sub-tickets** (e.g., if target coverage is 95%, a regression threshold of -2% means any delta below -2% from n-1 triggers a lowlight candidate).

**Edge Cases & Constraints:**

* If a statistic/metric value is `N/A`, it is **not** eligible for delta analysis; the automation skips it.
* If n-1 value is `N/A` or does not exist, no delta can be computed; the automation skips it.
* If n-1 release does not exist in the system (edge case: first-ever release), regression detection is disabled, but improvement detection may still surface candidates.
* Automation logic is to be fully specified in the technical design phase (e.g., which statistics are analyzed by default, how thresholds are stored and retrieved).

---

## 6. Functional Requirements

### 6.1 Dashboard & Navigation

* A single dashboard view aggregates all three pillars for a given release.
* Users can switch between releases using a release selector (dropdown or search).
* Dashboard shows completion status per pillar (e.g., "Document: Draft | Stats: Complete | Quality: Pending").
* Role-based views: creators see editable panels with automation suggestions; consumers see a read-only published view.
* Map Experts have access to quality metrics configuration panels (measurement descriptions, target values, automation thresholds) within the dashboard.
* **Customer-specific views are applied automatically in the background — the system derives each customer's feature set and country scope from their delivery information (e.g. CM ticket) and scopes the dashboard accordingly. No manual setup per release is required once the customer's delivery information source is linked.**

### 6.2 Automation & Integration

* **Any observable change that impacts released product quality — regression or considerable improvement — must be documented in the respective Release Notes section. Automation is required to systematically detect and surface such changes, ensuring comprehensive quality coverage without reliance on manual discovery.**
* Feature statistics and quality metrics are automatically extracted from ADP via API or scheduled job.
* The system supports light configuration per map product (e.g., which features to track, which KPIs to display, regression/improvement thresholds) — no per-release manual configuration needed after initial product setup.
* Where data is unavailable, the system surfaces clear status indicators rather than empty or misleading content.
* **Cross-pillar automation continuously monitors statistics and metrics deltas, surfacing regression and improvement candidates to the PM/content owner for review before publication.**
* **Quality target values and KPI metadata are extracted from Jira Quality sub-tickets and configured at product setup time, enabling the system to compute status vs. target and derive threshold recommendations for regression/improvement detection.**

### 6.3 Authoring & Workflow

* All human-authored content (general information, highlights, important notes, known issues) is editable via a rich text interface in v1.
* Documents follow a **Draft → In Review → Approved → Published** lifecycle with a mandatory sign-off step before publication.
* Change history is preserved per release.
* Comments and annotations are supported for internal review.
* Automation candidates (Highlights and Lowlights from Pillars 2 & 3 deltas) are surfaced inline within the authoring interface, clearly marked as "auto-generated candidates" to distinguish from manually authored content.
* Map Experts contribute to quality-related sections (Pillar 3 configuration, measurement descriptions, Lowlights investigation context) and are involved in the review step for quality-driven automation candidates.

### 6.4 Consumer-Facing Output

* Published release notes are accessible via a stable, versioned URL.
* Export formats: PDF for the release notes document; CSV for feature statistics and deltas.
* The document structure is consistent across releases, enabling customers to reliably parse and compare across versions.
* **Customer-facing output is automatically scoped to each customer's contracted feature set and country scope — no manual adaptation is needed. The system derives the customer's scope from their delivery information source (e.g. CM ticket) and applies the filtering in the background. The underlying content and statistics are consistent per product line; scoping is transparent to the customer.**

#### Dashboard Publication Requirements

For a product release to be eligible for display in the external TomTom dashboard, it must satisfy all of the following conditions before publication is permitted:

1. **Complete statistics** — Every expected statistic has either a numeric value (including 0) or an explicit N/A state. The distinction matters: **0** means the pipeline ran and the result was zero; **N/A** means the measurement was not executed for this release (e.g., ground truth not yet available, pipeline not run). N/A values are permitted and do not block publication, but must be surfaced with a clear status indicator. Blank / unmarked values are not permitted and do block publication.
2. **Previous version present** — The previous version (n-1) exists in the system. _(Edge case: handling of the very first release to be confirmed — see Open Questions.)_
3. **Statistics data completeness** — Each statistic record includes all required fields: **name**, **feature**, **country**, **unit**, and **value** (or explicit N/A). Derived fields are calculated by the system and are not required as inputs.
4. **Automation Candidate Review** — Any automation-generated candidates in Highlights and Lowlights must be explicitly confirmed or dismissed by the PM/content owner; implicit acceptance is not permitted.

The framework must validate these conditions and surface a clear, actionable status indicator if any requirement is unmet — blocking publication until resolved.

---

## 7. Non-Functional Requirements

* **Performance:** Dashboard loads within 3 seconds; statistics and metrics render within 5 seconds of data availability; automation candidate detection runs asynchronously within 10 seconds of data ingestion.
* **Reliability:** System availability ≥ 99.5% during business hours. Degraded mode (cached last-known data) when upstream systems are unavailable.
* **Scalability:** Supports multiple concurrent map products, parallel release cycles, and multiple customers per product line without configuration conflicts; automation runs independently per product. Customer-specific view scoping is automatic and derived from delivery information — it does not require separate data pipelines or product instances.
* **Security:** Access to the creation/editing interface is restricted to authenticated internal users. Consumer-facing view is accessible based on customer access controls; customer-specific view scoping is enforced automatically based on the linked delivery information source.
* **Auditability:** All changes to authored content, automation candidate decisions (accept/reject), and configuration are logged with user and timestamp.
* **Accessibility:** Consumer-facing output meets WCAG 2.1 AA standards.

---

## 8. User Stories

* As a **Release Notes Creator**, I want sections of the release note to be auto-populated from upstream data, so I spend my time on narrative rather than data gathering.
* As a **PM / Content Owner**, I want to write and edit highlights, important notes, and known issues in a structured template, so the output is consistent across releases.
* As a **Release Manager**, I want to see a dashboard showing which sections are complete and which are pending, so I can manage the release readiness.
* As a **Technical Program Manager**, I want to compare feature stats between any two releases, so I can quickly report on what changed.
* As a **PM / Content Owner**, I want to document release-specific regressions (lowlights) in a dedicated section, so customers can clearly distinguish between new regressions and ongoing known issues.
* **As a PM / Content Owner, I want the system to automatically flag significant feature statistic and quality metric changes (vs. n-1) so I don't miss important quality signals to communicate to customers.**
* **As a PM / Content Owner, I want to review and confirm automation-generated Highlights and Lowlights candidates before publishing, so I retain control over narrative while saving time on data discovery.**
* **As a Map Expert, I want quality artifact generation and delta comparison to be automated, so I can focus on analysis and root cause investigation rather than manual data collection.**
* **As a Map Expert, I want to be automatically alerted when quality metrics show significant regressions vs. n-1, so I can investigate issues promptly before publication.**
* **As a Map Expert, I want quality results to be automatically populated into the release notes, so I don't need to manually transcribe findings into documents.**
* As an **External Customer**, I want the release notes dashboard to be automatically scoped to my contracted features and countries, so I see only the data relevant to my integration without any manual setup.
* As an **External Customer**, I want a reliable, consistently structured release note with clear scope, stats, and quality signal, so I can confidently integrate the new map data into my product.

---

## 9. Success Metrics

| Metric | Target |
| --- | --- |
| Time to produce a complete release note | Reduced by ≥ 70% vs. current manual process |
| % of release note sections auto-populated | ≥ 80% of content requires no manual data entry |
| Release note completeness at go-live | 100% of required sections filled before publication |
| Customer satisfaction with release note quality | Improvement vs. baseline (survey-based) |
| Reduction in ad-hoc data requests from customers post-release | ≥ 50% reduction |
| **% of significant statistical/quality metric changes (regressions + improvements) surfaced by automation** | **≥ 90% coverage (measured post-GA)** |
| **Manual effort to review automation candidates** | **≤ 10% of total release note creation time** |
| **Time Map Experts spend on manual quality artifact production and population per release** | **Reduced by ≥ 70% vs. current process** |
| **Manual effort required to scope the dashboard per customer per release** | **0 — customer view scoping is fully automatic, derived from delivery information** |

---

## 10. Assumptions & Dependencies

**Assumptions:**

* Feature statistics and quality metrics are pre-computed and available in ADP; this framework extracts and displays them — it does not compute them.
* The Quality KPI dashboard already exists and supports parameterized linking.
* A release is uniquely identified by product + version + date.
* v1 focuses on internal tooling; external consumer access uses a read-only published view.
* For all releases except the first, the previous version (n-1) exists in the system and can be resolved automatically by the framework.
* Measurement descriptions (per-metric methodology definitions) are static and do not require per-release updates; they are configured once at product setup.
* Per-KPI-route measurements are not available in ADP for v1; this scope may be revisited if data availability changes.
* Regression and improvement thresholds are stable per product; they can be refined post-GA if needed.
* **Jira Quality sub-tickets contain target values and KPI metadata (Quality Measures, Target, Results) in a structured, machine-readable format that the system can parse during product setup.**
* **Customer delivery information (e.g. CM ticket) contains the customer's contracted feature set and country scope in a structured, machine-readable format that the system can parse to automatically derive the customer's dashboard view. No per-release manual adaptation is required once the delivery information source is linked.**

**Dependencies:**

| Dependency | Owner | Risk if Unavailable |
| --- | --- | --- |
| Analytical Data Plane (ADP) | MAA/ @Sasha Haber | Pillars 2 and 3 cannot be auto-populated; cross-pillar automation cannot function |
| Quality KPI dashboard (parameterized deep-link) | MAA / @Oleksandr Kozak Kozak , @Ruth Martin Marco | Pillar 3 reduced to a static link; inline metrics unavailable; quality metric regression/improvement candidates not surfaced |
| Release metadata source (Jira or equivalent) | Engineering / TPMs | Release selector and versioning depend on authoritative release IDs |
| PDF export infrastructure | Rudolph team / @Ashwini Raskar , @Tomasz Szambor | PDF export for the Pillar 1 deliverable unavailable |
| Jira API (fix versions, issue fields, automation rules) | Engineering / Jira admin | General Information, Highlights, Important Notes, and Known Issues auto-population and workflow triggers cannot function |
| **Jira Quality sub-tickets (structured target values and KPI metadata)** | **Value streams (content owners)** | **Quality metrics cannot be configured with target values; variance computation and regression threshold derivation unavailable; cross-pillar automation accuracy degraded** |
| **Customer delivery information source (e.g. CM ticket) — structured feature set and country scope** | **TBD (to be confirmed in Discovery)** | **Automatic customer view scoping cannot function; manual adaptation would be required as fallback** |

---

## 11. Rough Timeline

| Phase | Scope | Target |
| --- | --- | --- |
| **Discovery & Design** | Finalize data contracts, API specs, UX wireframes; **define regression/improvement thresholds per product; design cross-pillar automation logic; validate Jira Quality sub-ticket structure and API access; validate customer delivery information source (CM ticket structure and API access) for automatic view scoping** |  |
| **MVP — Pillar 1** | Release note document template + authoring workflow |  |
| **MVP — Pillar 2** | Feature statistics ingestion + delta view |  |
| **MVP — Pillar 3** | Quality metrics link + inline KPI snapshot; **extract and configure target values from Jira** |  |
| **Cross-Pillar Automation** | Implement delta monitoring; surface regression/improvement candidates in Highlights/Lowlights |  |
| **Integration & Testing** | End-to-end testing with real release cycle; test automation accuracy and threshold effectiveness; **validate automatic customer view scoping with at least one customer** |  |
| **Beta Release** | Internal rollout to one map product team; validate automation candidate quality and PM/content owner workflow |  |
| **GA** | Full rollout across map product teams |  |

---

## 12. Risks & Mitigations

| Risk | Likelihood | Impact | Mitigation |
| --- | --- | --- | --- |
| ADP data unavailable or not yet scoped to release level | Medium | High | Validate ADP data availability and release-scoping capability in Discovery (Wks 1–3); design graceful degradation |
| Upstream API contracts change during development | Medium | High | Define and lock API contracts during Discovery; use versioned endpoints |
| Quality KPI system does not support parameterized deep-linking | Medium | High | Validate deep-link capability as a Discovery gate (Wk 1–2); degrade gracefully to static link if needed |
| Low adoption by release notes creators — perceived as added process overhead | Medium | Medium | Involve key users in beta (Wk 15); ensure the tool reduces rather than adds effort; provide onboarding materials |
| Scope creep toward external customer portal features | Medium | Medium | Maintain a locked v1 scope; log deferred requests in a backlog; enforce "Out of Scope" list at prioritization reviews |
| Data quality issues in ADP surface in the dashboard | Low | High | Surface data confidence / freshness indicators in the UI; allow authorized manual override with full audit trail |
| Timeline slippage due to API integration complexity | Medium | Medium | De-risk API integrations in Wks 1–3; prioritize API contract sign-off before Pillar 2/3 development begins |
| Release blocked from dashboard publication due to unmet data contract requirements | Medium | High | Build pre-publication validation checklist into the authoring workflow; surface blockers early in Draft stage |
| Jira data quality — issues not consistently labelled or linked to fix versions | Medium | Medium | Define Jira issue hygiene standards as part of the release process; validate completeness before release cutoff |
| N/A vs 0 misclassification in upstream data | Medium | Medium | Enforce explicit state declaration (numeric value or N/A) at data ingestion; reject blank/unmarked values at the pipeline boundary |
| **Automation thresholds poorly calibrated — too many false positives or false negatives** | **Medium** | **Medium** | **Define thresholds collaboratively with content PMs in Discovery; run threshold sensitivity analysis in beta; allow per-product refinement post-GA** |
| **Automation candidates are ignored or dismissed by content owners** | **Medium** | **Medium** | **Beta with real release cycles to validate UX and workflow; ensure automation saves time vs. manual discovery; collect PM feedback post-GA** |
| **Jira Quality sub-ticket structure inconsistent or target values not machine-readable** | **Medium** | **Medium** | **Validate Jira structure as a Discovery gate; define standard field schema for Quality Measures, Target, Results; document parsing rules in technical design** |
| **Map Experts not engaged in Discovery — threshold and KPI configuration requirements poorly defined** | **Medium** | **High** | **Involve Map Experts in Discovery workshops; validate quality artifact definitions and target values against real release data before MVP** |
| **Customer delivery information (CM ticket) not structured or accessible enough to derive view scoping automatically** | **Medium** | **High** | **Validate CM ticket structure and API access as a Discovery gate; define required fields for feature set and country scope; fall back to manual linking only if automation is not feasible** |

---

## Open Questions

1. How is the **very first release** handled for the n-1 validation check and delta computation?
2. What is the exact ADP API contract for feature statistics and quality metrics (release-scoped queries)?
3. Does the Quality KPI dashboard today support parameterized deep-linking by product + release?
4. What Jira fields/fix-version schema should drive the auto-population of Highlights and Known Issues?
5. Details of NDS.Live Compiled Map stats sections — to be provided by @Dennis van Nooij.
6. **What regression and improvement thresholds should be configured per map product (e.g., feature count ±5%, coverage ±2%)?**
7. **Should thresholds be uniform across statistics/metrics, or customizable per metric?**
8. **How should automation handle statistics/metrics that are new in this release (no n-1 baseline)? Should they be flagged separately?**
9. **What is the exact schema and field structure for target values and KPI metadata in Jira Quality sub-tickets (Quality Measures, Target, Results)?**
10. **Can target values from Jira Quality sub-tickets be reliably extracted via Jira API? What is the field access path?**
11. **What is the exact structure of the customer delivery information source (e.g. CM ticket)? Which fields define the customer's contracted feature set and country scope, and are they accessible via API for automatic view scoping?**

---

## 13. Follow-up Actions

### 13.1 Onboarding & Guidance Page

**Owner:** Engineering team + Process Owner  
**Trigger:** To be created before Beta release; finalized before GA.

Create a dedicated onboarding and guidance page covering all user types of the Release Notes Deliverables Framework. The page must be structured per persona so each group can find exactly what they need without reading content intended for others.

**Required coverage per persona:**

| Persona | Content to cover |
| --- | --- |
| **Release Notes Creator / PM / Content Owner** | How to create and edit a release note document; how to work with the Draft → Published lifecycle; how to review, confirm, and dismiss automation candidates in Highlights and Lowlights; how to fill each section (General Information, Highlights, Important Notes, Known Issues); publication checklist and common blockers |
| **Release Manager** | How to use the dashboard to track completion status across pillars; how to manage the sign-off step; what the publication blockers mean and how to resolve them |
| **Map Expert** | How to configure quality metrics, measurement descriptions, and target values at product setup; how to set and adjust regression/improvement thresholds; how to contribute Lowlights investigation context; how automation alerting works and when to act on it |
| **Technical Program Manager** | How to use the release selector for cross-release delta comparison; how to read and export feature statistics and quality metric reports; how to interpret automation candidate outputs |
| **External Customer** | How to navigate the published release notes dashboard; how to read feature statistics and delta indicators automatically scoped to their contracted scope; how to interpret quality metric trend indicators and the KPI dashboard link; how to export data (PDF, CSV) |

The onboarding page should include: step-by-step workflows per persona, annotated screenshots of key UI areas, a glossary of framework-specific terms (e.g., `N/A` vs `0`, automation candidates, Lowlights vs Known Issues), and an FAQ section addressing the most common questions per role.

---

### 13.2 Transition Timeline Plan

**Owner:** Process Owner  
**Trigger:** To be drafted during Beta; finalized before GA cutover.

Create a structured transition plan for switching from the current manual release notes process to the new framework-based approach across all map products and related artifacts. The plan must cover both the internal production process and the customer-facing output.

**Required content:**

| Element | Description |
| --- | --- |
| **Current state baseline** | Document the existing manual process per map product: tools used, people involved, time per step, known pain points. Serves as the baseline for measuring transition success. |
| **Transition milestones** | Define clear go/no-go gates for each product switching to the new framework, aligned with the Pillar delivery timeline (Section 11): Beta onboarding, parallel running period, full cutover, legacy process decommission. |
| **Parallel running period** | Define the window during which both the old and new processes run in parallel for validation. Specify which releases are produced via the new framework first (typically lower-risk / lower-frequency releases), and the criteria for full cutover. |
| **Cutover criteria per map product** | Conditions that must be met before a product team fully switches: all pillars functional for that product, onboarding completed for all relevant personas, at least one release successfully published end-to-end via the new framework. |
| **Legacy process decommission** | Steps to retire manual processes, spreadsheets, and ad-hoc data flows once cutover is complete. Includes communication to affected teams and customers about the change. |
| **Customer communication plan** | How and when external customers are informed about the new release notes format and dashboard — including confirmation that their view will be automatically scoped to their contracted features and countries with no action required on their side. |
| **Rollback plan** | Conditions under which a product team reverts to the manual process during transition, and the steps to do so without disrupting a release. |
