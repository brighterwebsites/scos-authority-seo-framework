# Strategic Content Operating System (SCOS)
**Version**: Two active components — `brighter-core` v4.3.0 and `site-essentials` v1.0.0
**Last Updated**: 03/04/2026
**Implementation**: WordPress MU Plugin (mid-migration from `bw_` prefix to `scos_` prefix)

---

## What It Is

SCOS is the software layer that makes the ALTC/WFB strategy frameworks 
machine-readable and executable at the content level. It sits between 
the strategic framework (ALTC/WFB) and the execution tools (WordPress, 
GSC, GA4) — connecting strategy to content to data in one integrated system.

The gap it fills: strategy normally lives in documents, disconnected from 
execution. SCOS makes strategy explicit per page (CAR) and site-wide (CAM), 
keeping AI tools calibrated and content aligned with commercial outcomes.

---

## The Four Layers

**Layer 1 — Content Architecture (Strategy)**
Defines what to create and why. The ALTC/WFB frameworks, Authority Anchors, 
Maturity Model, and Service Pathways. Lives in documentation, informs all 
other layers.

**Layer 2 — Execution (Operational Modules)**
Implements how to execute the strategy. Current modules:

- **Content Architecture** — Built and active. The core SCOS execution module. Manages per-page content classification (cluster, topic, intent, purpose, maturity), workflow tracking, and automated content analysis. Registers the CAR metabox on all public post types.
- **SEO Meta** — Built and active. Per-page SEO fields: title, description, canonical URL, robots directives, TLDR summary, and breadcrumb label. Replaces SEOPress field management. Dual-writes to SEOPress keys for compatibility.
- **Schema** — Built and active. Per-post JSON-LD input plus site-wide schema templates (Local Business, Success Stories, Product, Service). Migrated from `bw_*` option keys to `scos_site_schema_*`.
- **Social Amplification** — Built and active. YOURLS shortlink slug, Post Framing message templates, and manual Make.com webhook trigger for social post creation. Options migrated from `bw_*` to `scos_sma_*`.
- **Analytics** — Built and active. GA4 Measurement ID configuration and event seeding management. Defines the seeding status transients consumed by the GA4 seeder scripts.
- **Business Info** — Built and active. Central business identity, contact, media, and social profile data. Powers schema output, shortcodes, and Open Graph tags. Options migrating from `bw_*` to `scos_biz_*`.
- **Custom Posts** — Built and active. Optional CPTs: Customer Success Stories (`projects`), Reviews (`bw_reviews`, non-public queryable SSOT), and FAQ. Each CPT is toggled independently via settings. Reviews CPT includes full CSV import, admin columns, shortcodes, and ACF relationship field support.
- **Tweaks** — Built and active. Admin and frontend housekeeping: emoji removal, heartbeat throttle, RSD/WLW link cleanup, and miscellaneous WordPress optimisations.
- **SEO / Sitemap** — Built and active. XML sitemap generation for all public post types and images. WordPress core sitemaps are disabled; this module is the sole sitemap source.
- **CAR Data Injection** (`scos-car-injection`) — Built and active (in `brighter-core`). Injects SCOS CAR field values into page output so GA4 and AI tools can read structured strategy data from any page.
- **ALTC Legacy Taxonomies** — Built and active (in `brighter-core`). Keeps legacy `altc_strategic_lens` and `altc_topic` taxonomy slugs registered for database compatibility until data migration to `scos_content_cluster` / `scos_topic` is confirmed complete.
- **Notifications (ntfy)** — Built and active (in `brighter-core`). Server monitoring via ntfy: form submission monitoring, cron health, sitemap validity, and SMTP checks.

**Layer 3 — Intelligence (Insight Generation)**
Transforms execution data into strategic insights. Analyses content coverage, 
cannibalisation risk, maturity gaps, and authority anchor distribution.
Current status:

- **Content Analysis engine** — Built and active. Runs automatically on every post save and via batch runner on the CA Overview page. Captures word count, H2 count, image count, reading time, and internal/external link inventories per post. Analysis coverage is tracked per post type with a progress dashboard.
- **CA Strategy Overview** — Built and active. Admin dashboard showing Content Cluster definitions, per-cluster post counts, and analysis coverage statistics across all post types.
- **GA4 SCOS event seeding** — Built and active. Seeds structured GA4 event parameters (`altc_primary`, `altc_topic`, `content_maturity`) from CAR data, enabling performance analysis by cluster, topic, and maturity level.
- **Airtable CAR sync** — Built and abandonded. Bulk sync of Clusters, Topics, and Content records to Airtable in a defined order. Stores Airtable record IDs in term meta for linked record relationships.
- **Legacy content stats page** — Built and active (in `brighter-core`). Carries forward pre-refactor content statistics alongside the new CA analysis layer.
- **Cannibalization risk analysis** — Flagged as present in the legacy ALTC admin pages (now replaced by the CA module). Current status of this specific view in the new CA Overview: the cluster breakdown table is implemented; dedicated cannibalization risk analysis view has not yet been rebuilt in the new module.

**Layer 4 — Content Authority Map (CAM)**
Site-wide strategic intelligence layer. Aggregates all Content Architecture 
Records into a single strategic picture — keeping AI tools calibrated and 
identifying gaps automatically.
Current status: **Not built. No CAM module or implementation exists in the codebase.** The CA Overview page provides basic cluster and topic counts plus content analysis coverage, but this is operational status only — not a strategic authority map. CAM remains the next major build milestone.

---

## Core Components

**Content Architecture Record (CAR)**
Per-page metadata that makes strategy machine-readable. Every piece of 
content declares its strategic position — cluster, topic, maturity, intent, 
purpose, pillar, and service pathway.
Current fields implemented:

**Taxonomy naming:** Use `scos_content_cluster` and `scos_topic` for data, CAR, CLI, and MCP. Treat `scos_ca_cluster` / `scos_ca_topic` as wp-admin form and list-column labels only — not database meta keys.

*Strategy classification (per post):*
- Content Cluster — taxonomy assignment (`scos_content_cluster`)
- Primary Topic — taxonomy assignment (`scos_topic`)
- Supporting Topics — array of `scos_topic` term IDs (extra topics beyond primary)
- Pillar Page — linked pillar page relationship
- Service Pathway — linked service/product/conversion page
- Intent — search intent category (11 options: Informational, Info Problem, Info Solution, Commercial, Decision Support, Transactional Payment, Transactional Lead, Authority Trust, Navigate Hub, Policy Functional)
- Purpose — content role (13 options: Pillar, Service, Product, Conversion Hub, Conversion Event, Conversion End-Point, Success Story, Brand Authority, Supporting Topic, Content Collection, Resource Guide, Policy, Functional)
- Maturity Level — 5-point scale (Entry, Professional, Expert, Thought Leader, Industry Authority)
- Intent Goal — freetext description of the page's strategic objective

*Workflow tracking (per post):*
- Index Status — Google crawl/index state (Crawled, Discovered, Indexed, Requested, Issue, Do Not Index)
- Optimization Progress — multi-select checklist (Idea, Content, Entity Semantic Coverage, Conversion, Basic SEO, Advanced SEO, Authority Outreach, Social Amplification)
- Next Step — workflow action flag (Approved, Testing, Revise, Merge, Archive)

*Content analysis — auto-populated on save:*
- Word count, H2 count, image count, reading time, internal link count, external link count, internal link inventory, external link inventory, last analysis timestamp

*SEO meta (separate metabox, same post):*
- Meta title, meta description, breadcrumb label, TLDR summary, canonical URL, robots directives, sitemap exclusion flags

**Proof Library**
No dedicated Proof Library module exists in the codebase. Two related CPTs are present that hold proof content:

- **Reviews CPT** (`bw_reviews`) — Structured customer review data with rating, date, platform, verify URL, success outcome, customer detail, featured flag, and schema ID. CSV import supported. Shortcodes available. Queryable SSOT; no public URLs.
- **Customer Success Stories CPT** (`projects`) — Public post type with archive, supports full editor content. Used for case study / portfolio pages.

A Proof Library module that aggregates, classifies, and surfaces this proof data strategically is planned but not built.

---

## Dual Intelligence Architecture (DIA)

SCOS is designed for AI-human collaboration, not AI replacement:
- **AI handles**: Pattern recognition, gap analysis, content generation, 
  meta optimisation, performance analysis
- **Human handles**: Strategy, positioning decisions, creative direction, 
  commercial judgement

**Current DIA capability**: With WP-CLI MCP access, Claude can now read 
SCOS field data across the site and act on it — querying content by cluster, 
maturity, or intent, and writing back to SCOS fields. This makes DIA 
functional today, not theoretical.

**CAM completes DIA**: Once CAM is built, the system moves from reactive 
(Claude answers questions) to proactive (system surfaces strategic gaps 
automatically).

---

## Current Implementation Scope

- Platform: WordPress MU Plugin (two components: `brighter-core` + `site-essentials`)
- Plugin prefix: mid-migration — authoritative data uses `scos_` prefix; some legacy `bw_` keys remain with dual-write compatibility shims
- MCP / AI access: REST API at `brighter-core/v1/` authenticated via `X-Brighter-Token` header. Registered endpoints: `/posts`, `/pages`, `/faqs`, `/faqs/search`, `/faqs/export`, `/scos` (returns structured CAR data for any URL or post ID), `/social-amplification/talking-points`. WP-CLI MCP access (external, not built into the plugin) enables direct field reads and writes across the site.
- SEO module replaces: SEOPress (field management; SEOPress may still be present for frontend output during transition)
- Stack: CyberPanel + LiteSpeed + Breakdance + Cloudflare
- Airtable integration: active — Clusters, Topics, and Content records sync to Airtable with linked record IDs stored in term meta
- Prefix migration status: `site-essentials` modules use `scos_*` keys natively; `brighter-core` modules are dual-writing to both `scos_*` and `bw_*` keys; some `bw_*`-only meta remains in the Reviews CPT and legacy analysis fields

---

## Related Documentation
- `scos-framework-docs/f_001-ALTC-content-strategy-framework.md`
- `scos-framework-docs/ALTC-supporting-information.md`
- `scos-framework-docs/Terminology-Reference.md`
