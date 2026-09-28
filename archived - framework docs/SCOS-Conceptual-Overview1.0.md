# Strategic Content Operating System (SCOS)
**Conceptual Framework - Vendor Neutral**

**Version**: 1.0  
**Last Updated**: December 16, 2024  
**Document Type**: Category Definition & Conceptual Architecture

---

## What This Document Is

This document defines **Strategic Content Operating System (SCOS)** as a **category of software system**, not a specific product. Think of this relationship:

- **CRM** = Category → **Salesforce/Hubspot** = Implementations
- **SCOS** = Category → **[Specific Products]** = Implementations

**Purpose**: Establish the conceptual framework, core components, and architectural patterns that define an SCOS, independent of any specific implementation.

**→ For implementation details**: See product-specific architecture documentation

---

## Executive Summary

### What is an SCOS?

**Strategic Content Operating System (SCOS)** is a category of software system that **operationalizes content strategy frameworks** through integrated execution, intelligence, and autonomous alignment layers.

Unlike traditional content tools (CMS, SEO platforms, analytics), an SCOS maintains **strategic alignment over time** by making strategy machine-readable and keeping all execution tools calibrated with strategic intent.

### The Gap SCOS Fills

**Traditional content tools are siloed**:
- **CMS**: Manages content publishing (WordPress, Contentful, etc.)
- **SEO Platforms**: Optimize pages (SEMrush, Ahrefs, etc.)
- **Analytics**: Track performance (Google Analytics, etc.)
- **CRO Tools**: Improve conversion (Optimizely, VWO, etc.)

**The Problem**: None maintain strategic alignment. Strategy exists in documents and spreadsheets, disconnected from execution. AI tools lose calibration every 2-3 months.

**SCOS Solution**: Makes strategy machine-readable at the content level, maintains site-wide strategic intelligence, and autonomously keeps all tools aligned with strategic intent.

---

## Core Principles

### What Makes Software an SCOS?

To be considered a Strategic Content Operating System, software must:

1. **Make content strategy machine-readable** (Content Architecture Record pattern)
2. **Maintain site-wide strategic intelligence** (Content Authority Map pattern)
3. **Keep AI tools calibrated automatically** (temporal consistency tracking)
4. **Integrate across four layers**: Strategy → Execution → Intelligence → Brain
5. **Enable autonomous AI agent workflows** (MCP-ready or equivalent)
6. **Connect content to commercial outcomes** (every piece has purpose)
7. **Track authority proof mechanisms** (E-E-A-T operationalization)
8. **Support maturity progression** (depth before breadth)

If software lacks these characteristics, it's a content tool, not a content operating system.

---

## The Four-Layer Architecture

SCOS operates on a four-layer architectural model where each layer serves a distinct purpose:

### Layer 1: Content Architecture (Strategic Framework)

**Purpose**: Defines **what** to create and **why**

**Components**:
- **Content Strategy Framework**: Positioning-first content strategy (e.g., ALTC, SLTC, or similar)
- **Marketing Methodology**: Website-centric marketing philosophy (e.g., WFB or similar)
- **Authority Mechanisms**: Proof systems (e.g., 8 Authority Anchors or equivalent E-E-A-T operationalization)
- **Maturity Model**: Content depth progression (e.g., 6-level maturity map or equivalent)
- **Service Pathways**: Commercial alignment structure

**Nature**: Strategic frameworks, not executable code. Lives in documentation and informs all other layers.

**Key Principle**: Strategy must be explicitly defined and documented before execution begins.

---

### Layer 2: Execution Layer (Operational Tools)

**Purpose**: Implements **how** to execute the strategy

**Core Functional Modules**:

**Content Strategy Module**:
- Content architecture tracking
- Strategic positioning management
- Content optimization workflow
- Content Architecture Record (CAR) generation

**SEO Module**:
- Technical SEO (sitemaps, robots.txt, canonicals)
- On-page optimization (meta, schema, structured data)
- AI-ready markup (LLMs.txt or equivalent)
- SEO performance tracking

**Analytics Module**:
- Custom event tracking
- Enhanced conversion tracking
- Content performance attribution
- Strategic dimension tracking

**Social Amplification Module**:
- Multi-platform content distribution
- Shortlink integration with UTM automation
- AI-powered content adaptation
- Platform-specific optimization

**Proof Library Module**:
- Atomic proof element storage
- Temporal tracking (proof validity over time)
- Cross-content proof reference system
- Authority validation

**Business Information Module**:
- Single source of truth for business data
- Schema integration (Local Business, Organization, etc.)
- Cross-platform data consistency

**FAQ/Knowledge Base Module**:
- Structured Q&A management
- AI training data export
- Schema markup (FAQ, Speakable, etc.)

**External Integrations**:
- AI Content Generators (strategic content creation)
- AI Strategy Tools (rapid positioning analysis)
- Marketing Automation Platforms (distribution workflows)
- Analytics Platforms (performance tracking)

**Key Innovations**:
- **Content Architecture Record (CAR)** per content piece (strategy made explicit)
- **MCP-first design** (AI agent-ready architecture)
- **Modular architecture** (components can be enabled/disabled)

---

### Layer 3: Intelligence Layer (Insight Generation)

**Purpose**: Transforms execution data into strategic **insights**

**Core Analytics Components**:

**Content Intelligence**:
- Topic saturation analysis (coverage by cluster)
- Cannibalization detection (competing content identification)
- Content gap analysis (missing strategic content)
- Maturity distribution tracking (depth assessment)

**Authority Intelligence**:
- Authority Anchor coverage analysis (proof mechanism utilization)
- E-E-A-T signal strength tracking
- Proof element effectiveness measurement
- Citation and mention tracking

**Performance Intelligence**:
- Content-to-conversion attribution (which content drives outcomes)
- Service pathway effectiveness (commercial alignment strength)
- User journey mapping (content → decision → conversion)
- ROI attribution (content value measurement)

**Strategic Alignment Intelligence**:
- Content-to-strategy alignment scoring
- AI tool calibration status
- Strategic drift detection
- Content velocity and trend analysis

**Data Sources**:
- Content Architecture Records (CAR) from all content
- Analytics platform events
- Internal linking structure analysis
- Content optimization status
- Proof Library temporal data

**Key Principle**: Analysis runs once, stores results, and triggers re-analysis only when:
- Content modified since last analysis
- Analysis hasn't run in X time period
- Strategic framework updated

---

### Layer 4: Content Authority Map (CAM) - The Brain

**Purpose**: Site-wide strategic intelligence layer that **keeps all AI tools calibrated** and maintains strategic alignment

**What CAM Tracks**:

**Strategic Inventory**:
- Which content clusters exist
- Maturity distribution per cluster
- Topic saturation index (high/medium/low coverage)
- Content count and velocity trends

**Authority Mapping**:
- Authority mechanism distribution across all content
- Proof element inventory and freshness
- E-E-A-T signal strength site-wide
- Citation and validation status

**Commercial Alignment**:
- Content-to-service pathway mapping
- Conversion goal distribution
- Service pathway coverage gaps
- Commercial intent balance

**Performance Intelligence**:
- Which content contributes to offline sales
- Content lifecycle status (published → updated → archived)
- Internal linking maturity
- Cannibalization risk assessment

**AI Tool Calibration**:
- Last calibration timestamps per tool
- Strategic drift detection
- Refresh requirements
- Tool-specific context needs

**Why CAM is Critical**:
Without Layer 4, AI tools drift and lose calibration every 2-3 months. CAM maintains alignment across all execution layers by:
- Aggregating all Content Architecture Records site-wide
- Providing strategic context to AI tools
- Tracking what content exists vs. what's needed
- Identifying gaps and opportunities automatically
- Maintaining consistency across all tools

**CAM Structure** (Conceptual Schema):
```json
{
  "site_id": "example-site",
  "last_updated": "2025-12-04T10:30:00Z",
  "strategic_clusters": [
    {
      "cluster_id": "strategic-positioning-cluster-1",
      "maturity_distribution": {
        "entry": 3,
        "learner": 5,
        "practitioner": 4,
        "professional": 8,
        "expert": 2,
        "industry_authority": 0
      },
      "authority_mechanisms_used": [1, 2, 4, 6, 8],
      "service_pathways": ["primary-service", "secondary-service"],
      "content_count": 22,
      "last_content_added": "2025-11-15",
      "next_maturity_target": "expert",
      "gap_analysis": "Need 3 more expert-level pieces before expanding width"
    }
  ],
  "topic_saturation": {
    "high": ["topic-1", "topic-2"],
    "medium": ["topic-3", "topic-4"],
    "low": ["topic-5", "topic-6"]
  },
  "cannibalization_risks": [
    {
      "topic": "competing-topic",
      "content_pieces": ["id-123", "id-456"],
      "risk_level": "medium",
      "recommendation": "Consolidate or differentiate"
    }
  ],
  "ai_tool_calibration": {
    "content_generator_last_updated": "2025-12-01",
    "strategy_tool_last_updated": "2025-11-28",
    "needs_refresh": false
  },
  "content_velocity": {
    "pieces_per_month": 4,
    "trend": "stable"
  }
}
```

**Integration Points**:
- **AI Content Generators**: Read CAM before generating to avoid duplication
- **AI Strategy Tools**: Use CAM to identify strategic gaps
- **Analytics Modules**: Feed performance data back to CAM
- **Content Modules**: Update CAM when content is published/modified

---

## Core Components (Detailed)

### Content Architecture Record (CAR)

**What it is**: Per-content metadata that explicitly defines each piece's strategic position within the SCOS.

**Why it matters**: Makes implicit strategy explicit and machine-readable. Every piece of content declares what it's supposed to do strategically.

**Conceptual CAR Schema**:
```json
{
  "version": "1.0.0",
  "last_updated": "2025-12-04T10:30:00Z",
  
  "content_strategy": {
    "strategic_cluster": "cluster-name",
    "maturity_level": "professional",
    "content_topic": "specific-topic",
    "content_intent": "educational",
    "content_purpose": "authority_building",
    "pillar_relationship": "cluster_hub | topic_hub | supporting | standalone"
  },
  
  "user_journey": {
    "journey_stage": "awareness | consideration | decision | retention | advocacy",
    "persona_target": "target-persona"
  },
  
  "authority_proof": {
    "authority_mechanisms": [1, 2, 4],
    "proof_elements": ["case-study-ref", "data-ref", "testimonial-ref"]
  },
  
  "commercial": {
    "service_pathway": "target-service",
    "conversion_goal": "primary-action",
    "secondary_goal": "fallback-action"
  },
  
  "cro_elements": {
    "elements_present": ["primary_cta", "secondary_cta", "proof_block"],
    "cta_hierarchy": {
      "main": "selector-for-main-cta",
      "micro": "selector-for-micro-cta",
      "assist": "selector-for-assist-cta"
    }
  },
  
  "content_quality": {
    "optimization_status": "draft | research | outline | optimized | published",
    "humanization_score": 8,
    "last_optimized": "2025-12-04"
  },
  
  "seo": {
    "locality": "geographic-target",
    "breadcrumbs": "category > subcategory > topic",
    "schema_types": ["Article", "HowTo", "FAQPage"]
  },
  
  "analytics": {
    "tracked": true,
    "custom_dimensions": {
      "content_intent": "educational",
      "content_purpose": "authority_building"
    }
  }
}
```

**Key Fields**:
- **Strategic Cluster**: Which strategic content cluster this belongs to
- **Maturity Level**: Entry → Learner → Practitioner → Professional → Expert → Industry Authority
- **Authority Mechanisms**: Which proof mechanisms (1-8) are utilized
- **Service Pathway**: Which commercial outcome this leads toward
- **Journey Stage**: Where in buyer journey this content serves
- **Proof Elements**: References to specific proof (case studies, data, testimonials)

**Implementation Notes**: 
- Can be stored as JSON metadata, database records, or structured files
- Must be accessible to both human editors and AI tools
- Should update automatically on content changes
- Must integrate with CAM (Layer 4) for site-wide intelligence

---

### Content Authority Map (CAM)

**What it is**: Site-wide aggregation of all Content Architecture Records providing strategic intelligence and AI tool calibration.

**Why it matters**: Without CAM, AI tools lose strategic context over time and begin generating content that:
- Duplicates existing content
- Misaligns with strategic positioning
- Ignores maturity progression principles
- Breaks commercial pathways

**Key Functions**:

**1. Strategic Inventory Management**
- Tracks all existing content by cluster
- Maps maturity distribution
- Identifies saturation levels
- Flags gaps and opportunities

**2. Authority Proof Tracking**
- Which proof mechanisms are underutilized
- Where proof elements are concentrated
- Temporal proof validity (claims age over time)
- Citation and validation status

**3. Commercial Alignment**
- Service pathway coverage analysis
- Conversion goal distribution
- Content → service mapping strength
- Orphaned content detection

**4. AI Tool Calibration**
- Provides strategic context to AI generators
- Prevents content duplication
- Maintains positioning consistency
- Tracks when tools need recalibration

**5. Performance Attribution**
- Which content drives conversions
- Content lifecycle effectiveness
- ROI per content cluster
- Strategic ROI validation

**Update Frequency**:
- Real-time: Content publication/modification triggers CAM update
- Scheduled: Performance data aggregation (daily/weekly)
- On-demand: AI tool calibration requests
- Manual: Strategic framework updates

---

### Proof Library

**What it is**: Centralized repository of atomic, verifiable proof elements with temporal tracking.

**Why it matters**: Traditional content management loses track of proof over time. Case studies become outdated, statistics age, testimonials lose relevance. Proof Library tracks:
- When proof was created
- When proof should be refreshed
- Where proof is referenced
- Proof element freshness/validity

**Conceptual Proof Record**:
```json
{
  "proof_id": "unique-identifier",
  "proof_type": "case_study | testimonial | data_point | certification | award",
  "title": "Human-readable title",
  "description": "What this proves",
  "created_date": "2024-01-15",
  "valid_until": "2025-01-15",
  "freshness_status": "fresh | aging | stale | expired",
  "authority_mechanism": 1,
  "referenced_in": ["content-id-1", "content-id-2"],
  "proof_data": {
    "metric": "80% AI voice share",
    "timeframe": "28 days",
    "context": "Guerrilla Steel case study",
    "outcome": "Q3 revenue matched entire H1"
  },
  "refresh_required": false,
  "last_validated": "2024-12-01"
}
```

**Integration Points**:
- **CAR**: Content references specific proof elements
- **CAM**: Tracks proof distribution and freshness site-wide
- **AI Tools**: Access proof library when generating content
- **External Systems**: Can sync with CRM, project management tools

---

## Dual Intelligence Architecture (DIA)

**Conceptual Innovation**: SCOS builds on Dual Intelligence Architecture (DIA), an emerging concept where:
- **AI handles**: Pattern recognition and analysis
- **Humans handle**: Strategy and creativity
- **Both work in tandem**, not isolation

### How SCOS Implements DIA

**1. Content Architecture Record (CAR) = Machine-readable strategy**
- **DIA concept**: AI analyzes content to understand purpose
- **SCOS innovation**: Content **declares** its own strategic purpose explicitly
- **Result**: AI doesn't guess - it knows

**2. Content Authority Map (CAM) = Temporal consistency tracking**
- **DIA concept**: Human provides strategy once
- **SCOS innovation**: System maintains strategic alignment over time automatically
- **Result**: Strategy doesn't drift as humans move on

**3. Proof Library = Atomic authority validation**
- **DIA concept**: AI finds patterns in successful content
- **SCOS innovation**: Explicit proof references AI can verify and track temporally
- **Result**: AI knows which proof is valid, fresh, and appropriate

**The DIA Advantage**: Traditional AI tools operate blindly - they don't know what content already exists, what strategy drives decisions, or which proof is still valid. SCOS makes this explicit, enabling true AI-human collaboration.

---

## MCP-First Design Principles

**Model Context Protocol (MCP)** or equivalent AI agent integration protocols enable autonomous AI workflows. SCOS should be designed MCP-first (or equivalent) from the start.

### Core Principle: Separate Interface from Business Logic

**Traditional Architecture** (MCP retrofit required):
```
AI Tool → Custom API → Business Logic
```
Later adding MCP requires duplicating business logic.

**MCP-First Architecture** (extensible):
```
Business Logic (pure)
├── REST API Layer → Calls business logic
├── MCP Tool Layer → Calls same business logic
└── Web UI Layer → Calls same business logic
```

**Key Principle**: Business logic is interface-agnostic. Any interface (REST, MCP, UI, CLI) calls the same core logic.

### Future MCP Tools (Conceptual)

**Content Strategy**:
- `get_content_inventory()` - List publishable content
- `analyze_content()` - Run strategic analysis
- `get_strategic_gaps()` - Identify missing content

**Content Generation**:
- `generate_content()` - Create strategically aligned content
- `update_content()` - Refresh existing content
- `validate_content()` - Check strategic alignment

**Proof Management**:
- `get_proof_library()` - Access proof elements
- `validate_proof()` - Check proof freshness
- `suggest_proof()` - Recommend proof for content

**Analytics**:
- `get_performance_report()` - Content performance data
- `get_conversion_attribution()` - Lead/sale attribution
- `get_strategic_roi()` - Content strategy ROI

**AI Calibration**:
- `get_site_strategy()` - Current strategic state (CAM)
- `update_calibration()` - Refresh AI tool context
- `detect_drift()` - Identify strategic misalignment

---

## SCOS vs Traditional Content Tools

| Aspect | Traditional CMS | SEO Platform | Analytics | SCOS |
|--------|----------------|--------------|-----------|------|
| **Purpose** | Content publishing | Keyword optimization | Performance tracking | Strategic alignment |
| **Strategy Layer** | ❌ Documents/spreadsheets | ❌ Implicit in keywords | ❌ External | ✅ Machine-readable (CAR) |
| **Site-wide Intelligence** | ❌ No strategic view | ⚠️ Keyword tracking only | ⚠️ Traffic metrics only | ✅ Strategic context (CAM) |
| **AI Tool Calibration** | ❌ Not applicable | ❌ Loses context | ❌ Data only | ✅ Automatic temporal tracking |
| **Content Purpose** | ⚠️ Tags/categories | ⚠️ Target keywords | ❌ Not tracked | ✅ Explicit per piece (CAR) |
| **Proof Tracking** | ❌ No system | ❌ Not tracked | ❌ Not tracked | ✅ Temporal validation |
| **Commercial Alignment** | ⚠️ Manual links | ❌ Not tracked | ⚠️ Goal tracking only | ✅ Service pathway mapping |
| **Authority Progression** | ❌ No system | ⚠️ Keyword difficulty | ❌ Not tracked | ✅ Maturity model |
| **AI Agent Ready** | ❌ No | ❌ No | ❌ No | ✅ MCP-first design |

**Key Differentiator**: SCOS maintains strategic alignment over time. Traditional tools execute tactics but lose strategic context.

---

## Integration Patterns

### Core Integration Requirements

**1. Content Creation Tools**
- **Integration Type**: Bidirectional
- **Data Flow**: CAR metadata ↔ Content editor
- **Purpose**: Content declares strategic purpose during creation

**2. AI Content Generators**
- **Integration Type**: Bidirectional with CAM
- **Data Flow**: CAM strategic context → AI → CAR-compliant content
- **Purpose**: AI generates strategically aligned content, updates CAM

**3. Analytics Platforms**
- **Integration Type**: Bidirectional
- **Data Flow**: CAR dimensions → Analytics | Performance data → CAM
- **Purpose**: Track content performance with strategic context

**4. Marketing Automation**
- **Integration Type**: Outbound
- **Data Flow**: CAR metadata → Distribution workflows
- **Purpose**: Content distributed with strategic context preserved

**5. Proof Management Systems**
- **Integration Type**: Bidirectional
- **Data Flow**: Proof Library ↔ CAR references | Proof freshness → CAM
- **Purpose**: Track proof utilization and validity

**6. CRM/Sales Systems**
- **Integration Type**: Inbound
- **Data Flow**: Conversion events → CAM → Attribution
- **Purpose**: Connect content to commercial outcomes

### API Requirements (Conceptual)

**Strategic Context API**:
- `GET /strategic-context` - Retrieve CAM for AI calibration
- `GET /content/:id/strategic-position` - Retrieve CAR for specific content
- `POST /content/:id/strategic-position` - Update CAR metadata

**Content Intelligence API**:
- `GET /content-gaps` - Identify missing strategic content
- `GET /cannibalization-risks` - Detect competing content
- `GET /maturity-distribution` - Assess content depth

**Proof Management API**:
- `GET /proof-library` - Access all proof elements
- `GET /proof/:id/freshness` - Check proof validity
- `POST /proof/:id/refresh` - Update proof timestamp

**Performance Attribution API**:
- `GET /content/:id/performance` - Retrieve content performance
- `GET /service-pathway/:id/attribution` - Service pathway ROI
- `GET /strategic-roi` - Overall content strategy ROI

---

## Implementation Considerations

### Technical Requirements

**Storage**:
- Structured data store for CAR (JSON, database, or equivalent)
- Site-wide data store for CAM (can be aggregated or cached)
- Proof Library database with temporal tracking
- Performance data integration

**Performance**:
- CAR read/write must be fast (< 100ms)
- CAM aggregation should be cached (update on content change)
- Intelligence Layer analysis runs once, stores results
- Proof Library queries must be optimized

**Scalability**:
- System must handle 1000s of content pieces
- CAM aggregation must scale efficiently
- AI tool calibration must be responsive
- Analytics integration must handle high volume

**Security**:
- CAR metadata may contain strategic IP
- CAM provides competitive intelligence
- Proof Library contains proprietary data
- API access must be authenticated and authorized

---

## Maturity Progression Model

**Core Principle**: Depth before breadth. Build authority in one area before expanding.

**The 6 Maturity Levels**:
1. **Entry** - Basic educational content, awareness stage
2. **Learner** - How-to guides, consideration stage
3. **Practitioner** - Tactical implementation, decision stage
4. **Professional** - Advanced strategy, retention stage *(Checkpoint: can expand horizontally)*
5. **Expert** - Original frameworks, thought leadership, advocacy stage
6. **Industry Authority** - Setting standards, widely cited, market leadership

**Maturity Rules**:
- Never expand to new clusters until reaching Professional (Level 4) in current cluster
- Track maturity distribution in CAM
- AI tools should respect maturity progression when generating content
- Content strategy should prioritize depth over breadth

---

## Authority Mechanism Framework

**Purpose**: Operationalize E-E-A-T (Experience, Expertise, Authoritativeness, Trustworthiness) through specific, measurable proof mechanisms.

**Conceptual Authority Mechanisms** (8 standard):

1. **Trust & Proof** - Converts claims into verifiable evidence
2. **Process & Education** - Makes expertise visible through teaching
3. **Comparisons & Decision Support** - Clarifies choices, builds confidence
4. **Thought Leadership** - Establishes original frameworks
5. **Local & Community Authority** - Demonstrates geographic trust
6. **Results-in-Advance** - Proves helpfulness before purchase
7. **Core Service Areas** (Underpinning) - Commercial alignment principle
8. **Technology Infrastructure Excellence** (Underpinning) - Technical execution standard

**Implementation**: Each piece of content should utilize 1-3 authority mechanisms, tracked in CAR. CAM tracks distribution site-wide to ensure balanced proof across all content.

---

## Conclusion

**Strategic Content Operating System (SCOS)** represents a fundamental category shift from "collection of content tools" to "integrated operating system for content strategy."

### What Makes SCOS Different

**Traditional Approach**:
```
Strategy (document) → Tools (disconnected) → Execution → Hope for results
```

**SCOS Approach**:
```
Strategy (machine-readable) → System (integrated) → Execution (aligned) → Intelligence (feedback) → Brain (maintains alignment)
```

### The Four-Layer Guarantee

1. **Layer 1**: Strategy is clearly defined and documented
2. **Layer 2**: Execution is connected to strategy (via CAR)
3. **Layer 3**: Data generates strategic insights (not just metrics)
4. **Layer 4**: Intelligence maintains alignment over time (via CAM)

### Core Innovations

- **Content Architecture Record (CAR)**: Makes strategy machine-readable at content level
- **Content Authority Map (CAM)**: Aggregates strategy into site-wide intelligence
- **Dual Intelligence Architecture (DIA)**: AI and humans work in tandem
- **MCP-First Design**: AI agents can operate autonomously
- **Temporal Proof Tracking**: Authority doesn't age invisibly
- **Maturity Progression**: Depth before breadth prevents thin authority

### This is Not Just Software

SCOS is a category of system that transforms how content-driven businesses operate. It's the operating system layer that sits between content strategy frameworks (like ALTC/WFB) and execution tools (like WordPress/analytics).

**Just as CRM transformed how businesses manage relationships, SCOS transforms how businesses manage content strategy.**

---

## Implementations

**Current Known Implementations**:
- WordPress-based SCOS implementation → See specific product documentation

**Future Potential Implementations**:
- Shopify/e-commerce platforms
- Webflow/no-code platforms
- Standalone SaaS
- Agency management systems
- Custom enterprise solutions

**→ For implementation-specific details**: See product architecture documentation

---

## Related Documentation

**Strategic Frameworks**:
- Website-First Blueprint (WFB) Methodology
- ALTC Framework Definitions
- ALTC Origin Story

**Implementation Examples**:
- WordPress SCOS Implementation Architecture
- Proprietary Terminology Reference
- AI-First Implementation Reference

**Technical References**:
- CAR Schema Specification
- CAM Structure Specification
- Proof Library Technical Specification
- LLMs.txt Format Specification

---

**Document Version**: 1.0  
**Document Type**: Category Definition  
**Maintenance**: Update when conceptual framework evolves (not when implementations change)  
**Next Review**: Quarterly or when significant conceptual evolution occurs
