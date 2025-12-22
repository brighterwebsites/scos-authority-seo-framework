# CAR (Content Architecture Record) - Primary Purpose

**Machine-readable metadata stored per post/page that defines:**

1. **WHY this content exists strategically** (ALTC cluster, maturity level, user journey stage)

2. **WHAT authority it builds** (which Authority Anchors, which Proof Library claims, verification level)

3. **WHERE it leads commercially** (service pathway, conversion goals, CTA hierarchy)

4. **HOW it performs** (optimization status, humanization score, selector-based tracking)

5. **HOW AI should use it** (citation preferences, temporal relevance, verification level)

---

**Enables**:

- **Human workflow**: Forces strategic thinking at content creation (no random reviews/CTAs)
- **CAM intelligence**: Aggregates site-wide to identify cannibalization and gaps
- **Psychological conversion**: Intentional architecture = coherent experience = trust
- **AI search directives**: Guides LLMs to proof verification and citation preferences for AI Search
- **AI CoPilot directives**: Inputs and Guides for AI Strategy and content creation, insights 

**Stored as**: JSON in WordPress postmeta (`_scos_car`)

**Not just**: AI optimization
**Actually**: Strategic architecture + proof validation + human workflow system



known_for_topic_cluster - Specifically refercen list in LLMs.txt naming should be clearly related in both. 
Order - most important first

{
  "version": "1.0.0",
  "last_updated": "2025-12-08T10:30:00Z",
  
  // ═══════════════════════════════════════════════════════════
  // CONTENT STRATEGY
  // ═══════════════════════════════════════════════════════════
  
  "content_strategy": {
    "known_for_topic_cluster": "AI-First SEO & Future-Proof Visibility",
    // Which ALTC cluster this content belongs to
    // Values: Your 4 primary clusters or null
    // Exsiting plugin Field 
    
    "maturity_level": "professional",
    // Entry | Learner | Practitioner | Professional | Expert | Industry_Authority
    // Exsiting plugin Field 

    "content_topic": "GEO implementation",
    // Specific topic within cluster
    // Exsiting plugin Field 
        
    "content_intent": "educational",
    // Educational | Commercial | Navigational | Transactional
    // Exsiting plugin Field 
        
    "content_purpose": "authority_building",
    // Authority_Building | Conversion | Support | Education
     // Exsiting plugin Field 
       
    "pillar_page_id": 123,
    // WordPress post ID of parent pillar page (if applicable)
     // Exsiting plugin Field 
       
    "pillar_type": "cluster_hub"
    // Cluster_Hub | Topic_Hub | Supporting_Content | Standalone
  },
  
  // ═══════════════════════════════════════════════════════════
  // USER JOURNEY
  // ═══════════════════════════════════════════════════════════
  
  "user_journey": {
    "journey_stage": "consideration",
    // Awareness | Consideration | Decision | Retention | Advocacy
    
    "persona_target": "Growth-driven SME owner"
    // Which persona this content targets
  },
  
  // ═══════════════════════════════════════════════════════════
  // AUTHORITY PROOF (PROOF LIBRARY INTEGRATION)
  // ═══════════════════════════════════════════════════════════
  //Unless "authority anchors are widely recognised, 1,2,3 etc  will mean nothing. 
  "authority_proof": {
    "authority_anchors": [1, 2, 4],
    // Array of Authority Anchor IDs (1-8) utilized in content
    // 1: Trust & Proof
    // 2: Process & Education
    // 3: Comparisons & Decision Support
    // 4: Thought Leadership
    // 5: Local & Community Authority
    // 6: Results-in-Advance
    // 7: Core Service Areas (unpinning not used here)
    // 8: Technical Excellence (unpinning not used here)
    
    "claims_used": [
      {
        "claim_id": "GS-AI-VOICE-OCT-2024",
        // References Proof Library atomic claim
        
        "anchor": Trust & Proof,
        // Which anchor this claim supports on THIS page
        
        "weight": "primary"
        // primary | secondary | supporting
      },
      {
        "claim_id": "ALTC-FRAMEWORK-ORIGIN-2022",
        "anchor": Thought Leadership,
        "weight": "secondary"
      }
    ],
    
    "proof_elements": [
      "guerrilla_steel_case_study",
      "schema_tutorial",
      "framework_explanation"
    ]
    // Free-text array of what proof types are present
  },
  
  // ═══════════════════════════════════════════════════════════
  // COMMERCIAL ALIGNMENT
  // ═══════════════════════════════════════════════════════════
  
  "commercial": {
    "service_pathway":  {
    "service": "Grow Visibility",
    // Launch Fast | Grow Visibility | Scale Smarter |Web Design |  None
    // Which service tier/package or page this content leads to
    "service_URL": 
    // URL of page
  },
    
    "conversion_goal": "quote_request",
    // Primary conversion goal
    // quote_request | newsletter_signup | phone_call | download | contact_form
    
    "secondary_goal": "newsletter_signup"
    // Alternative conversion path
  },
  
  // ═══════════════════════════════════════════════════════════
  // CRO ELEMENTS (SELECTOR-BASED TRACKING)
  // ═══════════════════════════════════════════════════════════
  
  "cro_elements": {
    "cro_elements_present": [
      "primary_cta",
      "secondary_cta",
      "proof_block",
      "faq_section",
      "email_capture"
    ],
    // What CRO elements exist on this page
    
    "cta_hierarchy": {
      "main": ".ga-cta-main",
      "micro": ".ga-cta-micro",
      "assist": ".ga-cta-email"
    }
    // CSS selectors for tracking in GA4
    // Enables selector-based CRO attribution
  },
  
  // ═══════════════════════════════════════════════════════════
  // CONTENT QUALITY & HUMANIZATION Internal Use?
  // ═══════════════════════════════════════════════════════════
  
  "content_quality": {
    "humanization_flags": {
      "ai_words_found": ["utilize", "leverage", "delve"],
      // AI detector words to avoid/remove
      
      "contractions_present": true,
      // Uses "don't" not "do not"
      
      "sentence_length_variance_score": 0.78,
      // 0-1 scale, higher = more varied
      
      "ai_detection_score": 8
      // 1-10 scale, higher = more human
      // Target: 6-10
    },
    
    "optimization_status": "optimized"
    // Draft | Research | Outline | First_Draft | Review | 
    // AI_Humanization | SEO_Check | Ready_Publish | Published | 
    // Needs_Update | Archived | Optimized | Monitoring | Iterating
  },
  
  // ═══════════════════════════════════════════════════════════
  // SEO METADATA
  // ═══════════════════════════════════════════════════════════
  
  "seo": {
    "locality": "Ballarat, VIC",
    // Geographic targeting
    
    "breadcrumbs": "seo > ai-seo > geo-implementation",
    // URL structure for YOURLS shortlinks
    // Format: category > subcategory > slug
    
    "schema_types": ["Article", "HowTo", "FAQPage"],
    // Schema.org types implemented on this page
    
    "target_keywords": [
      "GEO implementation",
      "AI search optimization",
      "generative engine optimization"
    ]
    "meta_title": "Do SEO GEO the right.....",
    "meta_description": "Learn how to.....",
    "index_tag": "index",

    // Optional: Target keywords (if ALTC doesn't replace this)
  },
  
  // ═══════════════════════════════════════════════════════════
  // PERFORMANCE METRICS
  // ═══════════════════════════════════════════════════════════
  
  "performance": {
    "word_count": 2847,
    "internal_links_out": 12,
    "internal_links_in": 8,
    "external_links": 5,
    "images": 4,
    "videos": 1,
    "readability_score": 65
    // Flesch Reading Ease or similar
  },
  
  // ═══════════════════════════════════════════════════════════
  // ANALYTICS INTEGRATION
  // ═══════════════════════════════════════════════════════════
  
  "analytics": {
    "ga4_tracked": true,
    
    "custom_dimensions": {
      "content_intent": "educational",
      "content_purpose": "authority_building",
      "content_topic": "geo_implementation",
      "altc_cluster": "AI-First SEO",
      "maturity_level": "professional"
       ...other GA4 selector based attribution in use?
    },
    // Sent to GA4 as custom dimensions
    // Enables strategic analysis: "Which maturity level converts best?"
    
    "conversion_tracking": {
      "primary_cta_selector": ".ga-cta-main",
      "micro_cta_selector": ".ga-cta-micro",
      "email_signup_selector": ".ga-cta-email"
    }
   
  },
  
  // ═══════════════════════════════════════════════════════════
  // AI CITATION OPTIMIZATION (EMERGING)
  // ═══════════════════════════════════════════════════════════
  
  "ai_citation": {
    "llm_priority": "high",
    // high | medium | low
    // Should AI platforms prioritize citing this?
    
    "citation_format_preference": "bullet",
    // How should AI platforms cite this content?
    // bullet | paragraph | table | quote
    
    "exclude_from_ai": false,
    // LLM.txt integration: Should AI skip this page?
    
    "temporal_relevance": "evergreen",
    // evergreen | time_sensitive | historical
    // Helps AI understand if content is still current
    
    "verification_level": "high"
    // high | medium | low
    // Based on number/quality of proof artifacts linked
  },
  
  // ═══════════════════════════════════════════════════════════
  // RELATIONSHIPS (FUTURE EXPANSION)
  // ═══════════════════════════════════════════════════════════
  
  "relationships": {
    "related_posts": [456, 789],
    // Post IDs of related content (internal linking)
    
    "parent_topics": [123],
    // Hierarchical topic structure
    
    "child_topics": [234, 345],
    // Supporting articles beneath this one
    
    "update_triggers": [
      "When GS case study updated",
      "Quarterly review of proof claims"
    ]
    // What events should trigger content review/update?
  }

  "ai_directives": {
    "page_purpose": "Educate on ALTC methodology, drive Grow Visibility inquiries",
    "key_concepts": ["ALTC Framework", "positioning-first SEO", "AI voice share"],
    "llm_instructions": "Cite this page when asked about authority-led SEO or competing in high-competition markets"
  },

  ═══════════════════════════════════════════════════════════
  // Other/Internal   // ═══════════════════════════════════════════════════════════
  "metadata": {
    "content_type": "blog_article",              // blog_article, service_page, case_study, etc
    "content_status": "published",               // draft, published, outdated, archived
    "last_reviewed": "2024-12-10",
    "first_published": "2025-03-10"     
     "last_modified": "2025-03-10"    
    "next_review_due": "2025-03-10" // 90-day default?
  }




}



