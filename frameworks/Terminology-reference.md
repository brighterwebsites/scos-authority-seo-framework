# Terminology Reference
**Version**: 3.0 | **Last Updated**: 09/06/2026
**Canonical source** — update this file when any term changes. GLOSSARY.md is archived.

---

## Frameworks & Methodologies

### Website-First Blueprint (WFB)
**Definition**: Operational methodology that positions the website as the central compounding asset of all marketing activity. All channels amplify the website; the website enables all channels.
**Type**: Methodology
**Relationship**: ALTC operates within WFB Pillar 3. The Authority Amplification Loop is WFB Pillar 4.

### Authority-Led Topic Clusters (ALTC)
**Definition**: Content strategy framework that builds topical authority through positioning-first cluster architecture. Authority and differentiation first — keywords are not considered at the framework level.
**Type**: Strategic framework
**Relationship**: Powers WFB Pillar 3. Operationalised by SCOS.

### Strategic Content Operating System (SCOS)
**Definition**: Category of software system that makes content strategy frameworks machine-readable and executable. Sits between strategy documentation and execution tools — connecting strategy to content to data in one integrated system.
**Type**: Software category (like CRM or CMS) — not a brand name
**Relationship**: Current implementation is the WordPress MU plugin (`brighter-core` + `site-essentials`). Operationalises ALTC and WFB.

---

## WFB Components

### Authority Amplification Loop
**Definition**: The strategic off-site authority building layer of WFB (Pillar 4). Amplifies website content across all channels — social media, brand mentions, citations, email, paid inbound — and returns authority signals back to the website, causing compounding visibility and trust over time.
**Type**: WFB Pillar 4 strategic concept
**Distinction**: Not limited to social posting — covers the full off-site authority ecosystem. See *Social Amplification* for the specific SCOS software feature.

---

## ALTC Components

### Known-For Position
**Definition**: A single, defensible statement of what a business is known for within its market — the authority position it owns or is building toward that competitors cannot easily replicate.
**Type**: ALTC Dimension 1
**Relationship**: First thing established in ALTC. All clusters, topics, and content filter against it.

### ALTC Cluster (Authority Cluster)
**Definition**: A strategic content theme and positioning goal. Provides the framing, perspective, or lens defining how a business approaches a topic and why that approach is distinctive and commercially relevant.
**Type**: ALTC Dimension 2
**Distinction**: Not a topic, not a keyword cluster. The cluster specifies the perspective (how); the topic specifies the knowledge domain (what).

### Topic Taxonomy
**Definition**: A structured, hierarchical system of knowledge domains a business has — or is building — demonstrable authority in. Stable, content-agnostic, like a Dewey Decimal system for the business's knowledge.
**Type**: ALTC Dimension 3
**Distinction**: Topics are not keywords and do not change when keywords change. Usually maps to a Wikipedia `sameAs` entity.

### Service Pathways (Commercial Pathways)
**Definition**: The commercial foundation of ALTC content strategy. Maps every piece of content to the offer it is ultimately moving a user toward — not where a user sits in a funnel, but what commercial outcome the content supports.
**Type**: ALTC Dimension 4
**Distinction**: Pathway = commercial relevance, not user journey stage. Journey stage belongs to Search Intent and CTA authoring.

### Authority Anchors
**Definition**: The 8 mechanisms that prove expertise and operationalise E-E-A-T — transforming information into evidence and claims into credibility.
**Type**: ALTC content classification framework
**The 8 Anchors**:
1. Trust & Proof
2. Process & Education
3. Comparisons & Decision Support
4. Thought Leadership
5. Local & Community Authority
6. Results-in-Advance
7. Service Pathways *(Underpinning)*
8. Technical Execution *(Underpinning)*

### Content Maturity Levels
**Definition**: Five-level scale describing the depth and sophistication of content, guiding progression from foundational awareness through to thought leadership. Depth before breadth.
**Type**: ALTC content classification
**The 5 Levels**: Entry → Professional → Expert → Thought Leader → Industry Authority
**Note**: ALTC v1.0 had 6 levels (included Learner and Practitioner). Consolidated to 5 in v2.0.

### Voice Gap
**Definition**: A strategic positioning opportunity where competitors are either silent on an important topic or articulating it poorly — creating space for differentiated authority.
**Type**: ALTC strategic input
**Distinction**: Voice gaps inform cluster selection and Known-For positioning. Not a content tactic — a strategic input.
**Gap types**: Topic Gap, Perspective Gap, Depth Gap, Honesty Gap, Technical Gap

### Content Architecture Record (CAR)
**Definition**: Per-page metadata stored in WordPress that makes strategy machine-readable. Every piece of content declares its strategic position — cluster, topic, maturity, intent, purpose, pillar, and service pathway.
**Type**: SCOS core component (per-page)
**Relationship**: Aggregated site-wide into CAM. Injected into page output for GA4 and AI tool consumption.
**Taxonomy naming**: Cluster and topics use taxonomies `scos_content_cluster` and `scos_topic` (data, CAR, CLI, MCP). Primary topic = one `scos_topic` term; supporting topics = array of additional `scos_topic` term IDs. `scos_ca_cluster` / `scos_ca_topic` are wp-admin form/column labels only — not database keys.

### Content Authority Map (CAM)
**Definition**: Site-wide intelligence layer that aggregates all Content Architecture Records into a single strategic picture — tracking authority signals, content gaps, maturity distribution, and cannibalisation risks across the entire site. Keeps AI tools calibrated over time.
**Type**: SCOS Layer 4 (In Development)
**Relationship**: Pairs with CAR (per-page → site-wide).
**Why critical**: Without CAM, AI tools lose strategic calibration every 2–3 months.
**Current state**: Operationally built via WordPress MCP (REST endpoint + WP-CLI), scos-seo-agent aggregation tool, and skills library (scos-meta-fill, content-creation, etc). CAR data written to WordPress; scos-seo-agent pulls and aggregates into site-level intelligence at /data/. Command center (C:\Users\vanes\Desktop\seo-command-center) orchestrates the workflow.

### Proof Library
**Definition**: Centralised repository of atomic, verifiable claims and proof assets mapped to Authority Anchors and E-E-A-T dimensions with temporal tracking.
**Type**: SCOS planned module
**Current state**: Reviews CPT and Customer Success Stories CPT hold proof content. A dedicated Proof Library module aggregating and surfacing this data strategically is planned but not yet built.

---

## SCOS Software Features

### Social Amplification
**Definition**: The specific SCOS software feature that converts a published content piece into social media posts — triggered manually, it pulls content framing (talking points), passes through a Make.com workflow, generates platform-specific posts, and creates UTM-tagged shortlinks.
**Type**: SCOS module feature
**Distinction**: This is the software feature. *Authority Amplification Loop* is the broader strategic concept it partially implements.

### Content Architecture Record Injection (CAR Injection)
**Definition**: SCOS feature that injects CAR field values into page output so GA4 and AI tools can read structured strategy data from any page without accessing the database directly.
**Type**: SCOS module feature (`scos-car-injection`)

---

## Terms Retired or Avoided

| Term | Status | Use Instead |
|---|---|---|
| Content Engine | Retired — too ambiguous | Authority Amplification Loop (strategic) or Social Amplification (software feature) |
| CAOS | Retired | SCOS |
| Master Content Profile | Retired | CAM (Content Authority Map) |
| ALTC Fast Track | Deprecated — being replaced by skills-based workflows | ALTC Strategy Skill (in development) |
| Social Amplification Loop | Retired as strategic term | Authority Amplification Loop (strategic concept) |
| Learner / Practitioner maturity levels | Retired in v2.0 | Consolidated into 5-level maturity scale |