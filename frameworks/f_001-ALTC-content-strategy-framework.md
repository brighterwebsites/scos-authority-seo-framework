# ALTC Content Strategy Framework
**Version**: 4.0 | **Last Updated**: 2026-05-10
**Scope**: Universal — applies to all ALTC businesses regardless of industry
**Primary AI Target**: Claude (Chat, Desktop, CLI) | Compatible: ChatGPT, Cursor

---

## Purpose

This document defines the strategic logic of the Authority-Led Topic Cluster (ALTC) framework. It covers the three-layer hierarchy, cluster anatomy, maturity levels, authority anchors, bridge content, and proof integration principles.

This is a concepts-and-logic document. It does not contain business-specific clusters, topics, or proof assets. Those are held in the business-specific ALTC strategy document (e.g. `bw-altc-strategy.md`) or accessed directly from the SCOS taxonomy in WordPress.

**For Claude Code**: Use precise terminology from this document. Do not infer meaning from general SEO knowledge — these terms have specific definitions that differ from industry convention. This is a definitions reference, not a procedural guide. Procedural skills are referenced separately where relevant.

---

## The Three-Layer Hierarchy

ALTC content strategy operates across three distinct layers. The Known-For Position governs everything beneath it. Clusters and the Topic Taxonomy both derive from it — but they are independent of each other. They connect only at the page level, through assignment.

```
              Known-For Position
                      ↓
        ┌─────────────────────────────┐
        ↓                             ↓
  ALTC Clusters               Topic Taxonomy
  (strategic lens)            (subject areas)
        └──────────┐  ┌───────────────┘
                   ↓  ↓
                  Page / Content
             (cluster assigned + topic assigned)
```

Clusters and topics do not have a parent-child relationship with each other. A page holds both assignments simultaneously. That is the only place the connection exists.

Work top-down when planning strategy. Work bottom-up when checking alignment of existing content.

---

## Layer 1: Known-For Position

The Known-For Position is the single, defensible statement of what a business is known for within its market. It is the strategic lens that filters every content, positioning, and messaging decision beneath it.

It is derived from the intersection of four inputs:
- What the business does (service and product mapping)
- What the business genuinely does differently (USP)
- Where the market voice gap is (competitor research and unmet positioning)
- Who the target audience is and what they need to hear to trust the business enough to act (ICA)

**What it is not:**
- A keyword, tagline, motto, or mission statement
- Written for search engines or for business plans
- Negotiable — every cluster and every piece of content either reinforces it or dilutes it

The Known-For Position is established first. If it hasn't been defined, no other ALTC work is valid.

---

## Layer 2: ALTC Clusters

### Definition

An ALTC Cluster is a strategic content theme — a framing lens that groups related knowledge domains together under a shared positioning goal. It defines how a business approaches a set of related topics and why that approach is distinctive and commercially relevant.

A business typically operates 1–3 clusters. Each cluster supports a different facet of the Known-For Position.

### What Makes a Valid Cluster

A cluster is not a topic, a keyword group, or a collection of articles. It is defined by five properties:

| Property | Definition |
|----------|-----------|
| **Positioning Goal** | The specific authority position this cluster builds toward, in support of the Known-For Position |
| **Voice Gap** | The specific gap in the market — in content, perspective, or framing — that this cluster fills |
| **Commercial Purpose** | The service pathway it supports and the commercial outcome it drives |
| **Audience** | Who the cluster speaks to, across both the visitor journey and the customer lifetime journey |
| **Maturity Goal** | The authority maturity level this cluster is building toward |

All five must be defined before content is assigned to a cluster.

### Cluster Assignment Logic

Content is assigned to a cluster based on the **framing and angle** applied to a topic — not the topic itself. The same topic can belong to different clusters within the same business, or across different businesses, depending on perspective, audience, and intent.

Keywords are not considered at the cluster level. Topics and clusters are assigned independently at the page level — topics do not belong to clusters, and clusters do not contain topics.

### Where to Access Cluster and Topic Data

**Taxonomy slugs (data, CAR, CLI, MCP):** `scos_content_cluster`, `scos_topic`

**AI with WordPress MCP/WP-CLI access:**
- Per post: one cluster term (`scos_content_cluster`); one primary topic term (`scos_topic`); supporting topics as an array of additional `scos_topic` term IDs (extra topics beyond primary)
- Cluster taxonomy admin: `/edit-tags.php?taxonomy=scos_content_cluster`
- Topic taxonomy admin: `/edit-tags.php?taxonomy=scos_topic`


**AI without WordPress access:**
- Cluster and topic data are held in the business-specific ALTC strategy document (e.g. `\business-name\strategy\202-authority-content-strategy.md`)

---

## Layer 3: Topic Taxonomy and Page-Level Assignment

### Topic Taxonomy

The Topic Taxonomy is a list of subject areas that exist independently of clusters. Topics are not children of clusters. They are not organised by cluster, grouped under clusters, or derived from clusters. They exist in their own right as a separate taxonomy.

A topic is a specific subject area — a domain of knowledge the business covers. The Topic Taxonomy for a business is defined in the business-specific ALTC strategy document or accessed directly from WordPress via the `scos_topic` taxonomy.

As topical authority  maturity growns topics may have Heriarchical relationships to one another. An early stage topical authority  maturity likely has a fully flat strucurtre

### How Topics and Clusters Connect

Topics and clusters are both assigned at the **page level**. A page receives:
- One cluster assignment (`scos_content_cluster`) — the strategic framing lens
- One primary topic assignment (`scos_topic`) — the dominant subject area
- Supporting topics (optional) — array of additional `scos_topic` term IDs beyond the primary

The relationship between a topic and a cluster exists only because both are assigned to the same page. It is never inferred from taxonomy structure, content grouping, or hierarchy. The page is the connection point — not the taxonomy.

This means:
- The same topic can appear across multiple clusters — the cluster assignment determines the framing, not the topic
- A cluster does not define which topics belong to it — the page assignments do
- Topics are never mapped to clusters in advance as a planning structure

### Content Assignment Checklist

Before writing any piece of content, confirm all assignments are resolved:

- [ ] Cluster identified and confirmed against Known-For Position (`scos_content_cluster`)
- [ ] Primary topic identified from the Topic Taxonomy (`scos_topic`, assigned independently of cluster)
- [ ] Supporting topics confirmed if applicable (array of additional `scos_topic` term IDs)
- [ ] Maturity level confirmed
- [ ] Authority Anchors selected (1–3)
- [ ] Service pathway confirmed (which money page does this lead toward)
---

## Maturity Levels

Every piece of content targets one maturity level. The level determines depth, assumed audience knowledge, and the type of authority the content builds.

| Level | What It Covers | Authority Built |
|-------|---------------|-----------------|
| **Entry** | Foundational concepts, introductory guides, practical basics | Accessibility and trust — the business is approachable and clear |
| **Professional** | Tactical implementation, process-based decision making, hands-on application | Competence and credibility — the business knows how to execute |
| **Expert** | Advanced strategy, proven methods, expert-level execution | Differentiation — the business has done this at depth |
| **Thought Leader** | Original frameworks, new knowledge creation, proprietary methodology | Category ownership — the business is defining the approach |
| **Industry Authority** | Standard-setting content; widely cited; market leadership position | Market authority — the business is the reference point others cite |

**Maturity progression:**
Clusters build upward over time. Entry content creates the audience entry point. Each level above it compounds on what exists below. A cluster without Entry content has no foundation. A cluster that never reaches Thought Leader or Industry Authority has no authority ceiling — it remains competent but not cited.

Do not attempt to publish at Thought Leader or Industry Authority maturity before the lower levels are established and evidenced. The upper levels require the lower levels to exist as internal link foundations and proof scaffolding.

---

## Authority Anchors

Authority Anchors are the six mechanisms through which content proves authority. Each piece of content should draw on 1–3 anchors. The anchor defines what kind of proof is needed — the proof sources listed below are where to find or draw from that proof, not a prescription for what content format to produce.

Anchor selection depends on the maturity level, the cluster goal, and what proof assets exist.

### Anchor 1: Trust and Proof
**What it does:** Demonstrates results through evidence — specific, named, measurable outcomes.
**Proof sources:** Existing case studies, recorded client metrics, before/after data, algorithm performance records, revenue outcomes, client testimonials.
**Use when:** Building credibility with a sceptical audience; content is at Professional or Expert maturity; specific named proof exists to draw from.

### Anchor 2: Process and Education
**What it does:** Builds competence authority by showing how something works — methodologies, systems, implementation steps.
**Proof sources:** The business's own documented processes, real implementation records, methodology documentation, behind-the-scenes workflow detail, technical knowledge the business holds.
**Use when:** Audience is in learning or evaluation mode; the business's differentiation is its method; Entry or Professional maturity level.

### Anchor 3: Comparisons and Decision Support
**What it does:** Builds trust by helping the audience make better decisions — honestly, without pressure.
**Proof sources:** Real trade-off experience from client work, honest criteria the business uses internally, data or outcomes that inform the comparison, market knowledge that justifies positions taken.
**Use when:** Audience is evaluating options; the business wins on differentiation rather than price; Professional maturity level.

### Anchor 4: Thought Leadership
**What it does:** Establishes category ownership through original frameworks, named methodologies, and positions the business as the standard-setter.
**Proof sources:** The business's own proprietary frameworks and named methodologies, original observations from client work, reframed industry data, positions the business has earned the right to hold through demonstrated results.
**Use when:** The business has a genuinely differentiated methodology or point of view; Thought Leader or Industry Authority maturity; building AI citation authority.

### Anchor 5: Local and Community Authority
**What it does:** Builds trust through geographic and community specificity — proving the business understands its local market.
**Proof sources:** Named local or regional client outcomes, geographic-specific market observations, community involvement records, local data or patterns the business has observed firsthand.
**Use when:** The business serves a defined geographic market; local trust is a conversion factor; competitors lack regional specificity.

### Anchor 6: Results-in-Advance
**What it does:** Reduces friction at the entry point of a service pathway by giving the audience something immediately useful — a no-cost, no-commitment experience of the business's value.
**Proof sources:** This anchor is not sourced from existing content — it requires a tangible deliverable: a working tool, a downloadable resource, a free audit, a checklist, a diagnostic assessment, a free trial or access offer.
**Important distinction:** Anchor 6 is not a content type — it is a content accompaniment. It sits alongside written content as a low-friction entry point to a service pathway. It is not informational page text, and it is not proof of results someone else achieved (that is Anchor 1).
**Use when:** The service has a high consideration barrier; the audience needs to experience value before committing; the cluster's commercial goal is retainer or project conversion.

### Anchor 7 and 8: 
are  underpinning anchors that do not surface through conent on the page but are 


---

## Bridge Content

Bridge content is a page assigned to more than one cluster simultaneously. It is valid — but only once a content strategy is mature enough to support it.

The rule: both sides of the bridge must exist before the bridge is built. Bridge content is typically long-form pillar content that links to established supporting content within each cluster it spans. Creating bridge content before that supporting content exists produces an unsupported structure.

As a guide: do not introduce bridge content until Expert or Thought Leader level content within each relevant cluster outnumbers Entry and Professional content combined.

Bridge content mechanics are documented separately when relevant to the engagement.

---

## Proof Integration Principles

Proof is what separates ALTC content from generic content. These principles apply universally — the specific proof assets are held in the business-specific documents.

### Cite Naturally, Not Mechanically

❌ Mechanical: `According to our case study, [Client] achieved [metric].`
✅ Natural: `[Client] hit [metric] in [timeframe] — and the reason wasn't [common assumption], it was [actual reason].`

The citation earns its place by connecting the proof to the argument. Proof cited in isolation is just a claim with a name attached.

### Connect Proof to Framework

Every proof point should answer: **why did this happen?**

Stating what happened builds credibility. Explaining why it happened — and connecting that explanation to the methodology — builds authority. The cause-and-effect relationship is what makes content citable by AI systems and persuasive to high-intent readers.

### Proof Types by Anchor

| Anchor | Where the Proof Comes From |
|--------|---------------------------|
| Trust and Proof | Named client outcomes, specific metrics with timeframes, performance records |
| Process and Education | The business's own documented methods, real implementation detail, technical knowledge |
| Comparisons | Real trade-off experience, internally held criteria, market knowledge earned through client work |
| Thought Leadership | Proprietary frameworks, original observations, earned positions backed by demonstrated results |
| Local and Community | Named local clients, geographic-specific data, firsthand regional market observations |
| Results-in-Advance | The deliverable itself — a working tool, audit, resource, or access offer |

---

## What This Document Does Not Cover

- Business-specific cluster definitions, names, and positioning goals → `[business]-altc-strategy.md`
- Business-specific topics and topic taxonomy → `[business]-altc-strategy.md`
- Business-specific proof assets (case studies, metrics, client names) → `[business]-altc-strategy.md` or WordPress MCP
- Step-by-step content generation workflow → `content-creation-skill.md`
- Prose mechanics and AI detection rules → `humanisation-rules.md`
- Business-specific voice, vocabulary, and tone → `[business]-brand-voice.md`
- Post-generation meta and image tasks → `pre-publish-skill.md`
