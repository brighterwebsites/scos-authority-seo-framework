# Service Offerings - Brighter Websites

**Version:** 1.0  
**Last Updated:** December 10, 2024  
**Purpose:** Technical specification for all service definitions, pricing, scope, and system integration

---

## Table of Contents

1. [Purpose & Scope](#purpose--scope)
2. [Service Philosophy](#service-philosophy)
3. [SEO & CRO Level Definitions](#seo--cro-level-definitions)
4. [Service Component Catalogue](#service-component-catalogue)
5. [Tier Definitions](#tier-definitions)
6. [Standalone Services](#standalone-services)
7. [Service Pathways](#service-pathways)
8. [Pricing Strategy](#pricing-strategy)
9. [CAR Integration](#car-integration)
10. [System Integration Points](#system-integration-points)
11. [Proof Library Integration](#proof-library-integration)

---

## Purpose & Scope

### What This Document Defines

Single source of truth for:
- Service tier structure (Launch Fast, Grow Visibility, Scale Smarter)
- Standalone service offerings
- Pricing bands and payment structures
- Technical scope per service
- Integration with SCOS, CAR, and Proof Library

### What This Document Does NOT Define

- Proof Library mappings (see Proof Library in Airtable)
- Standard page content sections (see Page-Structure.md)
- Proposal templates (see Proposal-Templates/)
- Client-specific customizations

### Document Relationships

```
Service-Offerings.md (YOU ARE HERE)
├── References: Proof Library (Airtable)
├── References: Standard-Page-Structure.md
├── Used by: CAR schema (service_pathway field)
├── Used by: Proposal generation
└── Used by: Website service page content
```

---

## Service Philosophy

### Constraint-Based Delivery

Start with what client can support NOW, not ideal roadmap. Build foundation that enables growth.

### Digital Growth Partner Model

Ongoing relationship with compounding value, not one-and-done projects. Faster ROI → natural tier progression.

### Three-Tier Structure Rationale

- **Launch Fast** (Entry): Get online quickly, AI-ready foundation
- **Grow Visibility** (Growth): Strategic content, ALTC implementation
- **Scale Smarter** (Premium): Full automation, advanced systems

### Content Strategy

**Standard approach:** AI-assisted content creation (faster, better SEO/CRO outcomes)

**Premium charge:** Client insists on writing own content (+30% project cost)
- Rationale: Slower timeline, quality not guaranteed, post-launch fixes likely

---

## SEO & CRO Level Definitions

### SEO Levels

| Level | Description | Typical Tier | What's Included |
|-------|-------------|--------------|-----------------|
| **Level 1: Foundation** | Basic technical SEO + structure | Launch Fast | Meta tags, XML sitemap, GSC/Bing setup, schema basics (LocalBusiness, Organization), image optimization |
| **Level 2: Strategic** | ALTC implementation + competitive analysis | Grow Visibility | Level 1 + competitor analysis, persona mapping, service pathway mapping, ALTC cluster identification (1-2), advanced schema (Service, FAQ, Review), content maturity roadmap |
| **Level 3: Comprehensive** | Full WFB/ALTC audit + 12-month strategy | Scale Smarter | Level 2 + complete competitor analysis, voice gap identification, full persona mapping, ALTC cluster identification (2-3), all schema types, quiz/calculator integration, 12-month implementation roadmap |

### CRO Levels

| Level | Description | Typical Tier | What's Included |
|-------|-------------|--------------|-----------------|
| **Level 1: Best Practice** | Design + basic tracking | Launch Fast | Strategic CTA placement (3 per page), mobile-first forms, trust signals, user pathway design, basic GA4 tracking |
| **Level 2: Data-Informed** | Best practice + analytics-driven optimization | Grow Visibility | Level 1 + multiple conversion funnels by service, advanced form optimization, proof architecture, selector-based attribution, lead hierarchy tracking |
| **Level 3: Partnership** | Ongoing optimization + testing | Scale Smarter | Level 2 + 3-month partnership, A/B testing, heat mapping, session recording, monthly optimization cycles, custom dashboards |

---

## Service Component Catalogue

### Core Technical Components

| Component | Description | Tier Availability | Internal Code |
|-----------|-------------|-------------------|---------------|
| WordPress Setup | WP + Breakdance + hosting | All | TECH-SETUP |
| SCOS Basic | Performance, Business Info, Basic SEO | Launch Fast | SCOS-BASIC |
| SCOS Pro | Content Strategy, Enhanced Analytics, FAQ | Grow+, Scale+ | SCOS-PRO |
| SCOS Agency | White-label, Priority Support | Scale+ | SCOS-AGENCY |
| Performance Optimization | LiteSpeed cache, image optimization | All | TECH-PERF |
| Security & Backup | Basic security, backup config | All | TECH-SECURITY |

### Content & Strategy Components

| Component | Description | Tier Availability | Internal Code |
|-----------|-------------|-------------------|---------------|
| AI-Assisted Content | 3,000-8,000+ words depending on tier | All | CONTENT-AI |
| ALTC Fast Track | Quick audit + topic cluster roadmap | Launch Fast | ALTC-FAST |
| ALTC Strategy | Full audit, competitor/persona/service mapping | Grow+, Scale+ | ALTC-FULL |
| Blog Setup | Structure, categories, ALTC alignment | Grow+, Scale+ | CONTENT-BLOG |
| Pillar Articles | Strategic long-form content (ALTC-aligned) | Scale+ | CONTENT-PILLAR |
| Proof Integration | Case studies, testimonials, Trust Library | All (varies) | CONTENT-PROOF |
| FAQ System | Structured CPT with schema | Grow+, Scale+ | CONTENT-FAQ |

### Analytics & Tracking Components

| Component | Description | Tier Availability | Internal Code |
|-----------|-------------|-------------------|---------------|
| GA4 Basic | Basic tracking + form submissions | Launch Fast | ANALYTICS-BASIC |
| GA4 Mid-Level | Selector-based attribution + lead hierarchy | Grow Visibility | ANALYTICS-MID |
| GA4 Full | Complete custom tracking + dashboard | Scale Smarter | ANALYTICS-FULL |

### Local Visibility Components

| Component | Description | Tier Availability | Internal Code |
|-----------|-------------|-------------------|---------------|
| GMB Optimization | Profile setup + optimization | Grow+, Scale+ | LOCAL-GMB |
| Directory Submissions (10) | Australian directories | Grow Visibility | LOCAL-DIR-10 |
| Directory Submissions (15) | Comprehensive coverage | Scale Smarter | LOCAL-DIR-15 |

### Automation Components

| Component | Description | Tier Availability | Internal Code |
|-----------|-------------|-------------------|---------------|
| Social Amplification Loop | Automated content distribution | Scale+ | AUTO-SOCIAL |
| Email Automation | Email platform + workflows | Scale+ | AUTO-EMAIL |
| Custom Integrations | Booking, CRM, custom features | Add-on | DEV-CUSTOM |

---

## Tier Definitions

### Launch Fast (Entry Tier)

**Price:** $3,500 base  
**Timeline:** 2-3 weeks  
**URL:** /services/launch/

#### Technical Specifications

| Component | Specification |
|-----------|---------------|
| Pages | Up to 6 custom pages |
| Content | AI-assisted, 3,000 words total |
| Platform | WordPress + Breakdance + SCOS Basic |
| Hosting | Domain + hosting + email (first year) |
| SEO | Level 1 (Foundation) |
| CRO | Level 1 (Best Practice) |
| Analytics | GA4 basic custom tracking |
| Support | 30 days post-launch |

#### WFB Pillar Implementation

**Strong foundations in:**
- Pillar 1: Technical Foundations (Basic)
- Pillar 2: Conversion Infrastructure (Basic)
- Pillar 3: Content Strategy (ALTC Fast Track roadmap)

**Getting started with:**
- Pillar 4: Social Amplification (account setup only, no posting)

#### Target Client Profile

- New businesses needing online presence
- Website replacement required
- Budget-conscious (< $5K budget)
- Need site within 2-3 weeks

#### Natural Progression Path

Launch Fast → (3-6 months) → Grow Visibility

#### SCOS Module Requirements

- Performance module (enabled)
- Business Info module (enabled)
- Basic SEO module (enabled)
- Basic Analytics module (enabled)

---

### Grow Visibility (Growth Tier)

**Price:** $4,800 base  
**Timeline:** 3-4 weeks  
**URL:** /services/grow/

#### Technical Specifications

| Component | Specification |
|-----------|---------------|
| Pages | Up to 10 custom pages + blog |
| Content | AI-assisted, 5,000 words total |
| Platform | WordPress + Breakdance + SCOS Pro |
| Hosting | Domain + hosting + email (first year) |
| SEO | Level 2 (Strategic - ALTC implementation) |
| CRO | Level 2 (Data-Informed) |
| Analytics | GA4 mid-level (selector-based attribution) |
| Local | GMB + 10 directories |
| Support | 60 days post-launch |

#### WFB Pillar Implementation

**Strong foundations in:**
- Pillar 1: Technical Foundations (Pro)
- Pillar 2: Conversion Infrastructure (Pro)
- Pillar 3: Content Strategy (ALTC implementation)

**Getting started with:**
- Pillar 4: Social Amplification (setup, not execution)

#### Target Client Profile

- Established businesses (1-3+ years)
- Ready for strategic growth
- Have proof to leverage (testimonials, case studies)
- Competitive market requiring differentiation

#### Natural Progression Path

Grow Visibility → (6-12 months) → Scale Smarter OR Growth Partnership (ongoing)

#### SCOS Module Requirements

- All Basic modules (enabled)
- Content Strategy module (enabled)
- Enhanced Analytics module (enabled)
- FAQ System module (enabled)
- Social Amplification module (setup only)

---

### Scale Smarter (Premium Tier)

**Price:** $6,500 base  
**Timeline:** 4-6 weeks initial + 3-month partnership  
**URL:** /services/scale/

#### Technical Specifications

| Component | Specification |
|-----------|---------------|
| Pages | Unlimited pages + full blog |
| Content | AI-assisted, 8,000+ words + 3-6 pillar articles |
| Platform | WordPress + Breakdance + SCOS Pro + Agency features |
| Hosting | Domain + hosting + email (first year) |
| SEO | Level 3 (Comprehensive - full WFB/ALTC audit) |
| CRO | Level 3 (Partnership - 3 months optimization) |
| Analytics | GA4 full tracking + custom dashboard |
| Local | GMB + 15 directories |
| Automation | Choice: Email OR Social Amplification Loop |
| Support | 90 days + monthly strategy calls (during partnership) |

#### WFB Pillar Implementation

**All 5 pillars implemented:**
- Pillar 1: Technical Foundations (Pro)
- Pillar 2: Conversion Infrastructure (Pro)
- Pillar 3: Content Strategy (Full ALTC)
- Pillar 4: Social Amplification (Email OR Social - client choice)
- Pillar 5: Compounding Systems (3-month partnership focus)

#### Target Client Profile

- $500K+ revenue
- Proven product-market fit
- Ready to scale systematically
- Need infrastructure not hustle

#### Natural Progression Path

Scale Smarter (3-month partnership) → Growth Partnership (ongoing retainer)

#### SCOS Module Requirements

- All Pro modules (enabled)
- Advanced Analytics (enabled)
- Social Amplification OR Email Automation (client choice)
- CAR implementation (per post)
- CAM (site-wide intelligence)

---

## Standalone Services

### Website Design

**URL:** /services/web-design/

**Service Type:** Core offering (part of all tiers)

**Standalone Scope:** Custom WordPress website design and development

**When Sold Standalone:** Rarely - typically part of tier packages

**Related Tiers:** Launch Fast, Grow Visibility, Scale Smarter (see tier definitions for full scope)

**Key Differentiators:**
- Themeless WordPress (Breakdance builder)
- Mobile-responsive by default
- SCOS integration (tier-dependent)
- Performance-optimized (< 2s load time)

---

### Search Visibility (SEO)

**URL:** /services/seo/

**Service Type:** Ongoing retainer or tier component

**Standalone Pricing:** $1,800-$2,500/month (3-month minimum)

**Standalone Scope:**
- ALTC implementation (positioning-first methodology)
- Technical SEO foundations
- Content strategy and creation
- Local SEO (GMB optimization + directories)
- Monthly reporting and strategy calls

**Related Tiers:** 
- Grow Visibility (includes SEO Level 2)
- Scale Smarter (includes SEO Level 3)

**When Recommended Standalone:** Client has existing website needing visibility boost

---

### Conversion Design (Lead Generation/CRO)

**URL:** /services/more-leads/

**Service Type:** Ongoing retainer or tier component

**Standalone Pricing:** $1,200-$1,800/month (3-month minimum)

**Standalone Scope:**
- CRO audit (analytics, heatmaps, user flow)
- Form optimization + testing
- CTA strategy + implementation
- Trust signals enhancement
- Monthly optimization cycles

**Related Tiers:**
- All tiers include CRO (level varies)
- Scale Smarter includes CRO Level 3 (partnership)

**When Recommended Standalone:** Site has traffic but low conversions

---

### Partner Collaboration

**URL:** /services/collab-delivery/

**Service Type:** White-label or agency partnership

**Pricing:** Custom quoted (project-based or retainer)

**Scope:**
- Web design execution for agencies
- Technical implementation support
- Strategic consulting
- Ongoing partnership arrangements

**Typical Use Cases:**
- Agency needs technical implementation
- In-house team needs specialized expertise
- White-label website delivery

---

### Managed WP Hosting

**URL:** /services/managed-hosting/

**Service Type:** Ongoing hosting + maintenance

**Pricing:** $120-$150/month (Care Plan)

**Scope:**
- VPS hosting management (CyberPanel + LiteSpeed)
- Performance optimization
- Security + backups
- Email hosting
- Domain management
- Priority technical support

**Included in Tiers:** First year only (domain + hosting + email)

**After First Year:** Client chooses hosting continuation or transfers elsewhere

---

### eCommerce Website Design

**URL:** /services/ecommerce/

**Service Type:** Tier add-on or custom project

**Pricing:** Growth tier base + eCommerce add-on ($400-$2,000 depending on complexity)

**Scope:**
- WooCommerce setup OR custom quote forms (eCommerce-light)
- Product/service architecture
- Payment integration (Stripe, PayPal, invoicing)
- Inventory management (if needed)
- Order management workflows

**Typical Engagement:** Growth tier + eCommerce customization

---

### Social Amplification (SMM)

**URL:** /services/social/

**Service Type:** Automation setup or ongoing management

**Pricing:** 
- Setup: Included in Scale Smarter
- Ongoing: Part of Growth Partnership retainer

**Scope:**
- Content repurposing (blog → social platforms)
- Platform posting automation (Make.com workflows)
- YOURLS shortlinks + automated UTM parameters
- Platform-specific optimization (Facebook, LinkedIn, Twitter, Instagram, GMB)

**What's NOT Included:** Original content creation (repurposes existing website content)

---

## Service Pathways

### Customer Journey Mapping

```
Entry Point → Core Service → Growth → Scale → Retention
```

#### Pathway 1: New Business (No Website)

```
Launch Fast 
    ↓ (3-6 months, seeing results)
Grow Visibility 
    ↓ (6-12 months, scaling)
Scale Smarter 
    ↓ (ongoing)
Growth Partnership (retainer)
```

#### Pathway 2: Existing Website (Needs Improvement)

```
Free Audit + Strategy Session
    ↓
Grow Visibility (skip Launch Fast)
    ↓
Scale Smarter
    ↓
Growth Partnership
```

#### Pathway 3: Established Business (Ready to Scale)

```
ALTC Fast Track Audit ($800)
    ↓
Scale Smarter (immediate entry)
    ↓
Growth Partnership
```

### Cross-Sell Opportunities

**From Launch Fast:**
- ALTC Fast Track session (bridge to Grow)
- Blog article package (content addition)
- Care Plan (ongoing support)

**From Grow Visibility:**
- Social Amplification upgrade
- Advanced analytics implementation
- Additional ALTC clusters
- White paper development

**From Scale Smarter:**
- Additional site management
- Agency white-label partnership
- Certification platform
- Custom tool development

---

## Pricing Strategy

### Price Ranges

| Tier/Service | Starting Price | Add-On Range | Total Range |
|--------------|----------------|--------------|-------------|
| Launch Fast | $3,500 | +$200-$1,000 | $3,500-$4,500 |
| Grow Visibility | $4,800 | +$500-$2,000 | $4,800-$6,800 |
| Scale Smarter | $6,500 | +$1,000-$3,000 | $6,500-$9,500 |
| SEO (ongoing) | $1,800/mo | - | $1,800-$2,500/mo |
| CRO (ongoing) | $1,200/mo | - | $1,200-$1,800/mo |
| Managed Hosting | $120/mo | - | $120-$150/mo |

### Pricing Philosophy

- **Value-based:** Outcome focus, not hourly
- **Transparent:** Published ranges, not hidden pricing
- **Regional-appropriate:** SME budgets, not enterprise pricing
- **Payment plans available:** 50% deposit / 50% before launch
- **Full payment discount:** Save 5% paying upfront

### Payment Structure (Standard)

**Option 1: Full Payment (Recommended)**
- Pay 100% at project start
- Save 5% total project cost
- Fastest timeline

**Option 2: Milestone Payments**
- 50% deposit at project start
- 50% before launch
- Standard timeline

### Client Content Premium Charge

**If client insists on writing own content:**
- +30% project cost
- Extended timeline (depends on client delivery speed)
- Risk disclaimer: SEO/CRO outcomes not guaranteed

**Rationale:** Slower delivery, quality control issues, post-launch fixes likely

---

## CAR Integration

### service_pathway Field Values

**Allowed values for CAR schema:**

```json
"service_pathway": [
  "Launch Fast",
  "Grow Visibility", 
  "Scale Smarter",
  "Website Design",
  "Search Visibility",
  "Conversion Design",
  "Partner Collaboration",
  "Managed WP Hosting",
  "eCommerce",
  "Social Amplification"
]
```

### Content → Service Mapping

| Content Type | Primary Service | Secondary Service |
|--------------|-----------------|-------------------|
| Blog: ALTC Framework | Grow Visibility | Scale Smarter |
| Blog: AI Search Basics | Launch Fast | Grow Visibility |
| Blog: Automation Strategies | Scale Smarter | - |
| Service Page: Grow Visibility | Grow Visibility | - |
| Case Study: Guerrilla Steel | Scale Smarter | Grow Visibility |
| FAQ: Website Questions | Launch Fast | Website Design |

### CAR Example

```json
{
  "commercial": {
    "service_pathway": "Grow Visibility",
    "conversion_goal": "quote_request",
    "secondary_goal": "newsletter_signup"
  },
  "authority_proof": {
    "claims_used": [
      {
        "claim_id": "GS-AI-VOICE-OCT-2024",
        "anchor": 1,
        "weight": "primary"
      }
    ]
  }
}
```

---

## System Integration Points

### Proof Library Integration

**Service → Proof mapping stored in:** Airtable Proof Library

**Relationship:** Services table → Claims table (many-to-many)

**Query pattern:** "Show me all claims that support 'Grow Visibility' service"

**See:** Proof Library documentation in Airtable

### SCOS Module Requirements

**Stored in:** SCOS Settings Manager

**Module enablement per tier:**

| Tier | Basic Modules | Pro Modules | Agency Modules |
|------|---------------|-------------|----------------|
| Launch Fast | ✓ | - | - |
| Grow Visibility | ✓ | ✓ | - |
| Scale Smarter | ✓ | ✓ | ✓ |

**Module dependencies documented in:** SCOS Technical Overview

### Proposal Generation

**Template system:** Along (proposal delivery platform)

**Reusable sections:** Each service has template block

**Customization:** 80% templated, 20% client-specific

**See:** Proposal-Templates/ directory

### Website Service Pages

**Standard page structure:** See Standard-Page-Structure.md

**Content generation workflow:**
1. Pull service definition from this document
2. Pull proof claims from Proof Library (Airtable)
3. Apply standard page structure
4. Customize for client journey stage

---

## Proof Library Integration

**Status:** Implemented in Airtable (Production)  
**Documentation:** See [Proof Library - Airtable Implementation](proof-library-airtable-implementation.md)

### Quick Reference

**6 Tables:**
1. **Claims** (Central hub) - Atomic, verifiable proof statements
2. **Verification Artifacts** - Supporting evidence (screenshots, documents, data)
3. **Usage Tracking** - Where claims are deployed (pages, channels)
4. **ALTC Clusters** - Topic organization for authority positioning
5. **Service Pathways** - Maps claims to service offerings
6. **Progression Data** - Time-series metrics

**Key Features:**
- E-E-A-T framework integration (Experience, Expertise, Authoritativeness, Trustworthiness)
- Authority Anchor mapping (1-8)
- Automatic validation tracking (⚠️ warnings when >90 days old)
- Central hub pattern (all tables link to Claims)

**WordPress Integration:**
- Airtable → JSON → WordPress cache (pull)
- WordPress → Webhook → Airtable Usage Tracking (push)

**For complete structure, field definitions, and sample data:** See [proof-library-airtable-implementation.md](proof-library-airtable-implementation.md)

### Example: Generating "Grow Visibility" Service Page Content

**Query Proof Library (Airtable):**
```sql
SELECT * FROM Claims 
WHERE linked_service_pathway CONTAINS "Grow Visibility"
AND claim_status = "active"
AND eeat_strength = "high"
```

**Returns:**
```json
[
  {
    "claim_id": "GS-AI-VOICE-OCT-2024",
    "claim_text": "Achieved 80% AI voice share in 28 days for Guerrilla Steel",
    "proof_type": "case_study",
    "eeat_dimension": "authoritativeness",
    "eeat_strength": "high",
    "authority_anchors": [1, 4, 6],
    "linked_service_pathway": ["Grow Visibility", "Scale Smarter"],
    "verification_artifacts": ["/wp-content/uploads/proof/gs-ai-voice-oct-2024.png"]
  },
  {
    "claim_id": "ALTC-FRAMEWORK-ORIGIN-2022",
    "claim_text": "Developed ALTC Framework in 2022, validated with real results 2024",
    "proof_type": "methodology",
    "eeat_dimension": "expertise",
    "eeat_strength": "high",
    "authority_anchors": [4],
    "linked_service_pathway": ["Grow Visibility", "Scale Smarter"]
  }
]
```

**Usage in Service Page:**
- Inject claims into "Proof" section (Standard Page Structure)
- Set CAR: `service_pathway: "Grow Visibility"`
- Set CAR: `claims_used: ["GS-AI-VOICE-OCT-2024" (primary), "ALTC-FRAMEWORK-ORIGIN-2022" (secondary)]`

### Example: Proposal Generation for "Scale Smarter"

**Claude Code workflow:**
1. **Read:** `service-offerings-draft.md` (get tier definition, pricing, scope)
2. **Query:** Airtable Proof Library (get claims for "Scale Smarter")
3. **Read:** `Standard-Page-Structure.md` (get proposal structure)
4. **Generate:** Customized proposal with:
   - Service scope from this document
   - Proof claims from Airtable
   - Structure from page template
   - Client-specific customizations (20%)

---

## Version Control

**Current Version:** 1.0  
**Last Updated:** December 10, 2024  
**Next Review:** After 5 proposals using this structure

**Change Log:**
- v1.0: Initial service structure documentation
- Tier naming locked: Launch Fast, Grow Visibility, Scale Smarter
- SEO/CRO level definitions added
- Integration points with Proof Library and SCOS defined

---

**End of Technical Specification**