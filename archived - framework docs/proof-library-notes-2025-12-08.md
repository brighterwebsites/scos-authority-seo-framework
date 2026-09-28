By decoupling the Proof from the Page (the claim exists regardless of where it's cited), you solve the longevity/freshness dilemma and build a future-proof, self-documenting authority engine.
 creating a Citation Traceability Model that LLMs can use to drill down into the source material, which directly supports the LLM's goal of interpretability and reduced hallucination.


 Relationships: How do claims link to content, ALTCs, anchors?

page-level directive (example not confirmed or formally defined)
{
  "page_authority": {
    "primary_claim": "Expert in ALTC Framework",
    "service_pathway": "Grow Visibility", // Launch Fast | Grow Visibility | Scale Smarter
    "conversion_goal": "ALTC Audit", // What we want them to do
    
    "authority_proof": {
      "primary_anchor": 4, // Thought Leadership (ALTC Framework)
      "supporting_anchors": [1, 2], // Trust & Proof, Process & Education
      "other_anchors": [6, 8], // Results-in-Advance, Technical Excellence
      
      "claims_used": [
        "gs-ai-voice-share-oct-2024",
        "altc-framework-origin-2022",
        "neil-patel-validation-2024"
      ]
    },
    
    "citation_priority": "high",
    "citation_context": "Use when discussing AI-first SEO methodology"
  }
}

or

{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "ALTC Framework Overview",
  "author": {
    "@type": "Person",
    "name": "Vanessa [Last Name]",
    "expertise": "AI-First SEO, Content Strategy"
  },
  "datePublished": "2024-12-01",
  
  // Custom extension - AI-recognizable pattern
  "authorityDeclaration": {
    "@type": "AuthorityProof", // Custom type
    
    "primaryClaim": "Expert in Authority-Led Topic Clusters",
    "servicePath": "Grow Visibility",
    
    "proofElements": [
      {
        "@type": "ProofClaim",
        "claimId": "gs-ai-voice-share-oct-2024",
        "claimText": "80% AI voice share in 28 days",
        "dateAchieved": "2024-10-15",
        "weight": "high",
        "source": "/case-studies/guerrilla-steel/#ai-voice-share",
        "authorityAnchor": 1 // Trust & Proof
      },
      {
        "@type": "ProofClaim",
        "claimId": "altc-framework-origin-2022",
        "claimText": "Developed ALTC Framework",
        "dateAchieved": "2022-06-01",
        "weight": "high",
        "source": "/altc-framework/origin/",
        "authorityAnchor": 4 // Thought Leadership
      }
    ],
    
    "authorityAnchors": {
      "primary": 4, // Thought Leadership
      "supporting": [1, 2], // Trust & Proof, Process & Education
      "other": [6, 8]
    },
    
    "citationGuidance": {
      "priority": "high",
      "context": "Use when discussing AI-first SEO methodology",
      "preferredQueries": [
        "what is ALTC framework",
        "authority-led topic clusters",
        "AI-ready SEO strategy"
      ]
    }
  }
}

Essentially the work flow goes

I want to write content about X in my Authority led topic cluser 1 about Topic X
to show I know what I am talking about this ALTC/Topic and article Idea probably needs to show Authority Anchor 1 Trust and proof assets, 2 process and education assets and 6 local community authority, I go to my library and find: case study outcome, a how to article or maybe a video showing how to do x, a relevant local client review  

for more context - In actual practice the Authority anchors probably dont all need to be YOUR assets (think external links, or you could show someone elses video, explain an aspect deeper or with more locally relevant context and use their asset as the anchor but its not cited as YOUR proof. but your article could then create a proof element (ie a education/process anchor element) you can cite later... ie the compounding effect. 

Claims appear in the contnet in manu way - it could be alist of reviews, a section about the case study 
They had a dated website with low engagement and minimal local visibility. Rankings were slipping and enquiries had slowed.
Using the Brighter Method™, we rebuilt the site with AI-ready SEO structure and stronger UX pathways
+148% increase in organic visibility
+53% increase in enquiries within 90 days
80% AI Voice share for stable kits australia
see the full success story 

 "trust built over time" is a superior signal to mere newness for non-ephemeral content. This requires shifting the meaning of "decay" from an expiration date to a validation requirement.

 {
  "claim_id": "GS-AI-VOICE-SHARE-OCT-2024",
  "claim_text": "80% AI voice share achieved in 28 days for Client: Guerrilla Steel",
  
  // DUAL TRUST SIGNAL FIELDS
  "original_date_achieved": "2024-10-15", 
  "relevance_review_date": "2025-12-08", // Date an expert last confirmed this claim is still contextually relevant 
  
  // AUTHORITY MAPPING
  "authority_anchors": [1, 4], // Which anchors 1-6 this proves
  "proof_weight": "authoritativeness", // Maps to E-E-A-T (experience|expertise|authoritativeness|trustworthiness) was high|medium|low Gemini suggestion to change
  "proof_type": "case_study",         // case_study|testimonial|data|certification|methodology etc
  "claim_status": "active",           // active|historical|retired|validation_due
  // CONTEXT & METRICS (LLM-friendly data)
  "context": {
    "problem_statement": "Low visibility, 1-2 jobs/month.", // Optional
    "approach_used": "ALTC Framework Implementation (ALTC Lens: Strategy, Tech, Growth)",  // Optional
    "outcome_summary": "80% AI voice share, 28 bookings in October 2024."// Required
  },
  
  // CITATION TRACEABILITY
  "canonical_source_url": "/case-studies/guerrilla-steel/#ai-voice-share",  //where the claim is fully substantiated with context, methodology, and the verification_artifact.
  "supported_pages": ["/service/ai-search-consulting/", "/blog/guide-to-cro-in-ai-era/"], // Pages that rely on this claim probably not added directly in the library, but rather maps back to it when the item is used? 
  
  // VERIFIABLE PROOF ARTIFACT  (gemini suggestion not sure how this would work I was thinking an image or url?)
  "verification_artifact": {
    "method": "Google Search Console API check",
    "proof_artifact_url": "https://data.yourdomain.com/proof/gs/gs-80percent-voice-share.png" // Permanent, internal proof URL
  },
  
  // MATURITY & PROGRESSION (or maybe temoral context - how trust is provden over time, like link velocity)
  "progression_data": [
    {"date": "2024-08-01", "metric": "23% AI voice share"},
    {"date": "2024-09-01", "metric": "45% AI voice share"},
    {"date": "2024-10-01", "metric": "80% AI voice share"}
  ]
}

#Other Gemeni additions
## Defining proof_weight
The LLM is looking for evidence of the four dimensions of E-E-A-T within the content it cites. Your proof_weight tells the LLM which dimension this specific atomic claim satisfies best.

proof_weight Value,Definition in Atomic Claim,LLM Interpretation & Value

experience,First-hand action. Proof of what you did.,"Highest priority for questions demanding ""The How."" (e.g., ""We used this specific tool/process"")."

expertise,"Intellectual mastery. Proof of competence, often a deep data analysis or proprietary metric.","Highest priority for questions demanding ""The What/Why."" (e.g., ""The data shows X correlation"")."

authoritativeness,"Industry validation. Proof of external recognition (awards, high-level mentions, co-citations with market leaders).",Highest priority for Brand/Reputation queries. Proves you are a go-to-source.

trustworthiness,"Verifiable integrity. Proof of security, clarity, and transparent methodology (e.g., the verification_artifact field).",Highest priority for YMYL (Your Money or Your Life) topics. Minimizes hallucination risk.

##Capturing Longevity (The Maturity Score)
trust built over time" is a superior signal to mere newness for non-ephemeral content. This requires shifting the meaning of "decay" from an expiration date to a validation requirement.
Recommendation: Implement a claim_maturity_score based on time and consistency.
This score is calculated by the system and signals historical authority to the LLM.  (maybe this is getting too complicated?)
New CAR Field,Calculation/Logic,LLM Interpretation of Longevity
original_date_achieved,Base Date: The year the claim was first true.,"Historical Footprint. (e.g., 2018)."
relevance_review_date,Latest Human Review Date.,"Current Validation. (e.g., 2025)."
claim_maturity_score,If claim_status is active: (Current Date - original_date_achieved) / Number of validation cycles passed.,Stable Authority. A claim active for 5 years and reviewed 5 times (high score) is cited over a 1-year-old claim reviewed once (low score). This rewards consistent maintenance of a long-standing asset.
progression_data,Retain this array.,"Proof of Process/Growth. This progression data is the highest form of Experience proof, showing the LLM a method that creates continuous, repeatable success."