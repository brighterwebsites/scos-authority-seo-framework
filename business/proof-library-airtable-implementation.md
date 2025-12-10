# Proof Library - Airtable Implementation

**Version:** 1.0  
**Last Updated:** December 10, 2025  
**Status:** Production (Brighter Websites)  
**Related:** [Proof Library Specification](../technical/01-proof-library.md)

---

## Purpose

This document describes the **actual Airtable implementation** of the Proof Library for Brighter Websites.

**For:**
- Understanding how the spec is implemented in practice
- Sample data structure for development
- Reference when building WordPress sync integration
- Template for creating Proof Libraries for other businesses

**See also:**
- [Proof Library Specification](../technical/01-proof-library.md) - Complete technical spec
- Airtable Base: "Proof Library - Brighter Websites" (live data)

---

## Table of Contents

1. [Database Structure](#database-structure)
2. [Table Definitions](#table-definitions)
3. [Relationships](#relationships)
4. [Sample Records](#sample-records)
5. [Formulas & Automation](#formulas--automation)

---

## Database Structure

### Tables Overview

| Table | Purpose | Record Count | Primary Key |
|-------|---------|--------------|-------------|
| **Claims** | Core proof repository | ~10-50 | claim_id |
| **Verification Artifacts** | Supporting evidence | ~15-75 | verification_id |
| **Usage Tracking** | Where claims used | ~20-100+ | usage_id |
| **ALTC Clusters** | Topic organization | 4 | ID |
| **Service Pathways** | Service mapping | 10 | Name |
| **Progression Data** | Time-series metrics | ~10-50 | ID |

### Relationship Map

```
Claims (Central Hub)
├── 1:many → Verification Artifacts
├── 1:many → Usage Tracking  
├── 1:many → Progression Data
├── many:many → ALTC Clusters
└── many:many → Service Pathways
```

---

## Table Definitions

### Table 1: Claims (Core)

**Purpose:** Central repository of atomic, verifiable claims

**Fields:**

| Field Name | Type | Options/Format | Notes |
|------------|------|----------------|-------|
| claim_id | Text (Primary) | UPPERCASE-KEBAB-CASE | Unique identifier |
| claim_text | Long text | 50-150 chars | Human-readable claim |
| claim_status | Single select | active, historical, retired, validation_due | Current status |
| proof_type | Single select | case_study, testimonial, data, certification, methodology, award, publication, media_mention, partnership, metric, ugc | Categorization |
| eeat_dimension | Single select | experience, expertise, authoritativeness, trustworthiness | E-E-A-T mapping |
| eeat_strength | Single select | high, medium, low | Proof strength |
| authority_anchors | Multiple select | 1, 2, 3, 4, 5, 6 | Which anchors supported |
| original_date | Date | ISO 8601 | When claim achieved |
| review_date | Date | ISO 8601 | Last validation |
| problem_statement | Long text | Optional | Case study context |
| approach_used | Long text | Optional | Methodology used |
| outcome_summary | Long text | Required | Result achieved |
| description | Long text | Optional | Additional context |
| client_id | Single select | Links to Clients table | Which client |
| canonical_url | Text | Relative path | Authoritative source |
| days_since_review | Formula | =TODAY() - {review_date} | Auto-calculated |
| validation_warning | Formula | =IF({days_since_review} > 90, "⚠️", "✓") | Alert indicator |
| total_usage | Count | From Usage Tracking | Usage count |
| website_usage | Rollup | From Usage Tracking | Website-specific count |

**Linked Tables:**
- → Verification Artifacts (1:many)
- → Usage Tracking (1:many)
- → Progression Data (1:many)
- ↔ ALTC Clusters (many:many)
- ↔ Service Pathways (many:many)

---

### Table 2: Verification Artifacts

**Purpose:** Store supporting evidence and proof documents

**Fields:**

| Field Name | Type | Options/Format | Notes |
|------------|------|----------------|-------|
| verification_id | Autonumber (Primary) | Auto-generated | Unique ID |
| artifact_type | Single select | screenshot, document, data_export, web, user_generated | Type of proof |
| artifact_url | Text | URL or path | Location of artifact |
| format | Single select | png, pdf, csv, web, mp4, json | File format |
| access | Single select | public, authenticated, internal_only | Access level |
| description | Long text | - | What it proves |
| claim_id | Linked record | → Claims table | Parent claim |

**Relationship:**
- → Claims (many:1)

---

### Table 3: Usage Tracking

**Purpose:** Track where and how claims are deployed

**Fields:**

| Field Name | Type | Options/Format | Notes |
|------------|------|----------------|-------|
| usage_id | Autonumber (Primary) | Auto-generated | Unique ID |
| url | Text | Full or relative URL | Where used |
| type | Single select | blog_article, case_study, social_post, email, landing_page, service_page | Content type |
| anchor_used_for | Single select | 1, 2, 3, 4, 5, 6 | Which anchor |
| weight_on_page | Single select | primary, secondary, supporting | Importance |
| date_added | Date | ISO 8601 | When added |
| claim_id | Linked record | → Claims table | Parent claim |

**Relationship:**
- → Claims (many:1)

**Updated via:** WordPress webhook on post save

---

### Table 4: ALTC Clusters

**Purpose:** Organize claims into authority-driven topic clusters

**Fields:**

| Field Name | Type | Options/Format | Notes |
|------------|------|----------------|-------|
| ID | Autonumber (Primary) | Auto-generated | Cluster ID |
| ALTC_Name | Text | Title Case | Cluster name |
| Description | Long text | - | Strategy notes |
| Active/Inactive | Single select | Active, Inactive | Status |
| Date_Created | Formula | CREATED_TIME() | Auto-generated |
| Related_Claims | Linked records | ↔ Claims table | Claims in cluster |
| Claim_Count | Count | From Related_Claims | Number of claims |

**Current Clusters:**
1. AI-First SEO & Future-Proof Visibility
2. Local Lead Generation & Ballarat Authority
3. Conversion-Focused Website Design
4. Technical Foundations & Performance

**Relationship:**
- ↔ Claims (many:many)

---

### Table 5: Service Pathways

**Purpose:** Map claims to business service offerings

**Fields:**

| Field Name | Type | Options/Format | Notes |
|------------|------|----------------|-------|
| Name | Text (Primary) | Title Case | Service name |
| Description | Long text | - | Service details |
| Active | Checkbox | true/false | Currently offered? |
| Category | Single select | Pathway, Service | Type |
| URL | Text | Relative path | Service page |
| Related_Claims | Linked records | ↔ Claims table | Supporting proof |
| Claim_Count | Count | From Related_Claims | Number of claims |

**Current Pathways:**
1. Launch Fast
2. Grow Visibility
3. Scale Smarter
4. Website Design
5. Search Visibility
6. Conversion Design
7. Partner Collaboration
8. Managed WP Hosting
9. eCommerce
10. Social Amplification

**Relationship:**
- ↔ Claims (many:many)

---

### Table 6: Progression Data

**Purpose:** Time-series performance metrics supporting claims

**Fields:**

| Field Name | Type | Options/Format | Notes |
|------------|------|----------------|-------|
| ID | Autonumber (Primary) | Auto-generated | Metric ID |
| metric_name | Text | - | What's measured |
| metric_unit | Single select | percentage, count | Unit type |
| date | Date | ISO 8601 | Measurement date |
| value | Number | Decimal allowed | Metric value |
| data_source | Text | - | Data origin |
| Claims | Linked records | ↔ Claims table | Related claims |

**Relationship:**
- ↔ Claims (many:many)

---

## Relationships

### Visual Relationship Map

```
┌─────────────────────────────────────────┐
│           Claims (Central Hub)          │
│  - claim_id (Primary Key)               │
│  - All core claim data                  │
└───┬────────┬────────┬──────────┬────────┘
    │        │        │          │
    │1:many  │1:many  │1:many    │many:many
    ↓        ↓        ↓          ↓
┌────────┐ ┌──────┐ ┌────────┐ ┌──────────────┐
│Verif.  │ │Usage │ │Progr.  │ │ALTC Clusters │
│Artif.  │ │Track │ │Data    │ │              │
└────────┘ └──────┘ └────────┘ └──────┬───────┘
                                       │many:many
                                       ↓
                                ┌──────────────┐
                                │Service       │
                                │Pathways      │
                                └──────────────┘
```

### Key Relationships Explained

**Claims → Verification Artifacts (1:many)**
- One claim can have multiple proof artifacts
- Each artifact belongs to one claim
- Example: Guerrilla Steel claim has GSC screenshot + revenue PDF

**Claims → Usage Tracking (1:many)**
- One claim can be used on multiple pages/channels
- Each usage entry tracks one deployment
- Updated via WordPress webhook

**Claims → Progression Data (many:many)**
- One claim can have multiple metrics over time
- One metric can support multiple claims
- Example: "AI voice share" progression supports multiple SEO claims

**Claims ↔ ALTC Clusters (many:many)**
- One claim can belong to multiple clusters
- One cluster contains many claims
- Example: Guerrilla Steel case supports both "AI-First SEO" and "Conversion Design"

**Claims ↔ Service Pathways (many:many)**
- One claim can support multiple services
- One service has multiple supporting claims
- Example: "80% AI voice share" supports both Grow Visibility and Scale Smarter

---

## Sample Records

### Sample Claim 1: Framework Origin

```json
{
  "claim_id": "EXPERIENCE-20-YEARS",
  "claim_text": "20+ years digital experience including government and enterprise consulting",
  "claim_status": "active",
  "proof_type": "certification",
  "eeat_dimension": "expertise",
  "eeat_strength": "medium",
  "authority_anchors": [2, 4],
  "original_date": "2004-01-01",
  "review_date": "2024-12-09",
  "outcome_summary": "20+ years experience across government enterprise and SME",
  "client_id": "brighter-websites",
  "canonical_url": "/about/",
  "linked_altc": ["AI-First SEO"],
  "linked_service_pathway": ["Launch Fast", "Grow Visibility", "Scale Smarter"]
}
```

### Sample Verification Artifact

```json
{
  "verification_id": 5,
  "artifact_type": "data_export",
  "artifact_url": "/wp-content/uploads/proof/sept-2024-algorithm-data.csv",
  "format": "csv",
  "access": "public",
  "description": "Visibility data across client portfolio during September 2024 update",
  "linked_claim": "SEPT-2024-SURVIVAL"
}
```

### Sample Usage Tracking

```json
{
  "usage_id": 1,
  "url": "/case-studies/ecommerce-growth/",
  "type": "case_study",
  "anchor_used_for": 2,
  "weight_on_page": "primary",
  "date_added": "2024-12-01",
  "linked_claim": "GS-REVENUE-2024"
}
```

### Sample ALTC Cluster

```json
{
  "ID": 1,
  "ALTC_Name": "AI-First SEO",
  "Description": "Topic cluster focused on AI-driven SEO methodology and results",
  "Active_Inactive": "Active",
  "Date_Created": "2025-12-10T02:31:24Z",
  "linked_claims": [
    "ALTC-FRAMEWORK-ORIGIN-2022",
    "GS-AI-VOICE-OCT-2024",
    "EXPERIENCE-20-YEARS",
    "ALTC-VS-TRADITIONAL-SEO",
    "GS-REVENUE-2024",
    "SEPT-2024-SURVIVAL"
  ],
  "Claim_Count": 6
}
```

### Sample Service Pathway

```json
{
  "Name": "Launch Fast",
  "Description": "Rapid website development and launch service pathway",
  "Active": true,
  "Category": "Service",
  "URL": "/services/launch-fast/",
  "linked_claims": [
    "EXPERIENCE-20-YEARS",
    "REVIEW-FAST-TURNAROUND"
  ],
  "Claim_Count": 2
}
```

### Sample Progression Data

```json
{
  "ID": 1,
  "metric_name": "Client Revenue Growth",
  "metric_unit": "percentage",
  "date": "2024-10-01",
  "value": 250.5,
  "data_source": "Google Analytics + Client Reporting",
  "linked_claims": ["GS-REVENUE-2024"]
}
```

---

## Formulas & Automation

### Calculated Fields (Claims Table)

**days_since_review:**
```
=TODAY() - {review_date}
```
Shows days since last validation

**validation_warning:**
```
=IF({days_since_review} > 90, "⚠️ Review needed", "✓")
```
Visual indicator for stale claims

**total_usage:**
```
=COUNT({Usage Tracking})
```
Total times claim used across all channels

**website_usage:**
```
=COUNTIF({Usage Tracking}, {type} = "blog_article" OR {type} = "service_page")
```
Usage on website specifically

---

## Key Features

### E-E-A-T Framework Integration

**Built-in Google E-E-A-T tracking:**
- `eeat_dimension`: Maps claim to specific E-E-A-T component
- `eeat_strength`: Rates proof quality
- `proof_type`: Categorizes evidence type

**Used for:**
- Content strategy decisions
- Proof selection for articles
- Gap analysis (which E-E-A-T dimensions need more proof)

### Authority Anchors Mapping

**Multiple select field (1-8):**
- Claims tagged with which Authority Anchors they support
- Enables filtering: "Show all Trust & Proof (1) claims"
- Primary/secondary designation happens at usage time (in CAR)

### ALTC Integration

**Many-to-many relationship:**
- One claim can belong to multiple ALTC clusters
- One cluster contains multiple claims
- Lookup field shows cluster names in Claims table
- Enables cluster validation: "Do we have proof for this positioning?"

### Temporal Tracking

**Automatic validation warnings:**
- Claims older than 90 days since review → flagged
- Visual indicators (⚠️ vs ✓)
- Status changes to `validation_due` if not reviewed

---

## WordPress Sync Integration

### Export to WordPress

**Airtable → JSON → WordPress:**

1. **Export all active claims:**
   - Filter: `claim_status = "active"`
   - Format: JSON array
   - Include: All linked relationships (artifacts, ALTC, service pathways)

2. **POST to WordPress endpoint:**
   ```
   POST /wp-json/caos/v1/proof-library/sync
   ```

3. **WordPress caches locally:**
   ```php
   update_option('caos_proof_library_cache', $claims);
   ```

### Usage Webhook (WordPress → Airtable)

**When content published with claim:**

1. **WordPress sends webhook:**
   ```json
   {
     "event": "claim_used",
     "claim_id": "GS-AI-VOICE-OCT-2024",
     "url": "https://brighterwebsites.com.au/altc-framework/",
     "type": "blog_article",
     "anchor_used_for": 1,
     "weight_on_page": "primary",
     "date_added": "2025-12-10"
   }
   ```

2. **Make.com/Zapier receives webhook**

3. **Adds row to Usage Tracking table**

4. **Updates claim's usage counts** (automatic via Airtable formulas)

---

## Sample Claims in Production

### Claim: Guerrilla Steel AI Voice Share

```json
{
  "claim_id": "GS-AI-VOICE-OCT-2024",
  "claim_text": "Achieved 80% AI voice share in 28 days for Guerrilla Steel",
  "claim_status": "active",
  "proof_type": "case_study",
  "eeat_dimension": "authoritativeness",
  "eeat_strength": "high",
  "authority_anchors": [1, 4, 6],
  "original_date": "2024-10-15",
  "review_date": "2024-12-08",
  "problem_statement": "Low visibility, 1-2 jobs/month",
  "approach_used": "ALTC Framework Implementation",
  "outcome_summary": "80% AI voice share, 28 bookings in October 2024",
  "client_id": "guerrilla-steel",
  "canonical_url": "/case-studies/guerrilla-steel/#ai-voice-share",
  "linked_altc": ["AI-First SEO"],
  "linked_service_pathway": ["Grow Visibility", "Scale Smarter"],
  "verification_artifacts": [
    {
      "artifact_type": "screenshot",
      "artifact_url": "/wp-content/uploads/proof/gs-ai-voice-oct-2024.png",
      "format": "png",
      "access": "public",
      "description": "Google Search Console data showing 80% AI voice share"
    }
  ],
  "progression_data": [
    {"date": "2024-08-01", "value": 23, "metric_name": "AI voice share"},
    {"date": "2024-09-01", "value": 45, "metric_name": "AI voice share"},
    {"date": "2024-10-01", "value": 80, "metric_name": "AI voice share"}
  ]
}
```

### Claim: 20 Years Experience

```json
{
  "claim_id": "EXPERIENCE-20-YEARS",
  "claim_text": "20+ years digital experience including government and enterprise consulting",
  "claim_status": "active",
  "proof_type": "certification",
  "eeat_dimension": "expertise",
  "eeat_strength": "medium",
  "authority_anchors": [2, 4],
  "original_date": "2004-01-01",
  "review_date": "2024-12-09",
  "outcome_summary": "20+ years experience across government enterprise and SME",
  "client_id": "brighter-websites",
  "canonical_url": "/about/",
  "validation_warning": "⚠️ Review needed",
  "linked_altc": ["AI-First SEO"],
  "linked_service_pathway": ["Launch Fast", "Grow Visibility", "Scale Smarter"]
}
```

---

## Architectural Insights

### Central Hub Pattern

**Claims table is the hub:**
- All other tables link TO Claims
- Claims don't link back (except many:many)
- Single source of truth pattern
- Query from Claims outward

### Lookup Fields Strategy

**Bring data INTO Claims view:**
- ALTC cluster names (via lookup from linked records)
- Service pathway names (via lookup)
- Usage counts (via rollup)
- Verification artifact counts (via count)

**Benefit:** See all context in Claims table without opening linked records

### Formula-Driven Validation

**Automatic data quality:**
- `days_since_review` catches stale claims
- `validation_warning` visual alerts
- `Claim_Count` tracks cluster size
- All calculated automatically, no manual updates

---

## For Claude Code Development

### What This Provides

**When building WordPress CAR module, Claude Code can:**

1. **Understand structure:**
   - See actual Airtable implementation
   - Match JSON structure for sync endpoint
   - Generate compatible code

2. **Sample data:**
   - Real claim examples (not hypothetical)
   - Actual field values
   - Production data patterns

3. **Integration points:**
   - Webhook payload structure
   - JSON export format
   - Field mappings (Airtable → WordPress)

### Airtable → WordPress Field Mapping

| Airtable Field | WordPress Storage | Notes |
|----------------|-------------------|-------|
| claim_id | JSON key: `claim_id` | Exact match |
| claim_text | JSON key: `claim_text` | Exact match |
| authority_anchors | JSON array: `authority_anchors` | Convert from Airtable multiple select |
| linked_altc | JSON array: `context.altc_cluster` | Lookup to cluster names |
| linked_service_pathway | JSON string: `context.service_pathway` | First linked pathway |

---

## Version History

**v1.0 (Dec 10, 2025):**
- Initial Airtable implementation
- 6 tables created
- Formulas and relationships established
- Sample claims added
- WordPress webhook integration planned

**Next:**
- Build Make.com webhook receiver
- Test sync endpoint
- Add more sample claims
- Validate formula accuracy

---

**End of Implementation Document**

*This describes the actual Airtable implementation of the Proof Library Specification. See the technical spec for complete field definitions and integration architecture.*

