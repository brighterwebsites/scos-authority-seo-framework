# Airtable Field Mapping Reference (Updated)

**Last Updated**: 2026-01-19
**Status**: Updated to match current `$airtable_data` output
**Related File**: `temp-drop-in-end-point-airtable.php`

---

## WordPress → Airtable Field Mapping

### 1) Basic Post Info

| Airtable Field     | WordPress Source                           | Type                 | Notes                                                         |
| ------------------ | ------------------------------------------ | -------------------- | ------------------------------------------------------------- |
| Post ID            | `$post_id`                                 | Number               | Primary key (WP post ID)                                      |
| Title              | `$post->post_title`                        | Text                 | Post/page title                                               |
| URL                | `get_permalink($post_id)`                  | Text                 | Full canonical permalink                                      |
| Published Date     | `get_the_date('Y-m-d', $post_id)`          | Date                 | ISO date                                                      |
| Last Modified Date | `get_the_modified_date('Y-m-d', $post_id)` | Date                 | ISO date                                                      |
| PostType           | `$post->post_type`                         | Text / Single Select | You may want Single Select later (`post`, `page`, `kb`, etc.) |
| PublishedStatus    | `$post->post_status`                       | Text / Single Select | Currently `publish` only (because you gate it)                |

---

### 2) Category / Taxonomy

| Airtable Field | WordPress Source                                                   | Type          | Notes                    |
| -------------- | ------------------------------------------------------------------ | ------------- | ------------------------ |
| Category       | `wp_get_post_categories($post_id, ['fields' => 'names'])[0] ?? ''` | Single Select | First category name only |

> If you later want multiple categories, change to array or join text.

---

### 3) Content Fields

| Airtable Field | WordPress Source                                                       | Type      | Notes                              |
| -------------- | ---------------------------------------------------------------------- | --------- | ---------------------------------- |
| TLDR           | `get_post_meta($post_id, 'bw_tldr', true)`                             | Long Text | Updated from old ACF field mapping |
| Excerpt        | `$post->post_excerpt ?: wp_trim_words($post->post_content, 55, '...')` | Long Text | Auto-generated fallback            |

---

### 4) ALTC Strategy Fields

> **Important:** In the current implementation these are **sent as text** (term names), not linked record IDs.

| Airtable Field  | WordPress Source                                    | Type          | Notes                                                         |
| --------------- | --------------------------------------------------- | ------------- | ------------------------------------------------------------- |
| ALTC Cluster    | `$altc_name`                                        | Text          | Derived from taxonomy term name (`altc_strategic_lens`)       |
| Topics          | `$topic_name`                                       | Text          | Derived from taxonomy term name (`altc_topic`)                |
| Maturity Level  | `get_post_meta($post_id, 'bw_cont_maturity', true)` | Single Select | Must match Airtable option exactly                            |
| Content Intent  | `get_post_meta($post_id, 'bw_intent', true)`        | Single Select | Must match Airtable option exactly                            |
| Content Purpose | `get_post_meta($post_id, 'bw_purpose', true)`       | Single Select | Must match Airtable option exactly                            |
| Intent Goal   | `get_post_meta($post_id, 'bw_altc_notes', true)`    | Long Text     | **Updated key** (was previously `bw_notes` in your older doc) |

---

### 5) Relationships

| Airtable Field  | WordPress Source                          | Type | Notes                                      |
| --------------- | ----------------------------------------- | ---- | ------------------------------------------ |
| Pillar          | `bw_pillar_page_id → get_the_title()`     | Text | Stores the *title* of the pillar post      |
| Service Pathway | `bw_service_pathway_ID → get_the_title()` | Text | Stores the *title* of related pathway post |

> If you want these as **Linked Records** in Airtable later, you’ll need to store Airtable record IDs (or query Airtable by Post ID).

---

### 6) Workflow / Planning

| Airtable Field     | WordPress Source                                | Type                     | Notes                                                                          |
| ------------------ | ----------------------------------------------- | ------------------------ | ------------------------------------------------------------------------------ |
| Workflow Next Step | `get_post_meta($post_id, 'content_plan', true)` | Text / Single Select     | Consider making this Single Select if it’s a controlled set                    |
| Workflow Progress  | `get_workflow_stage_as_list($post_id)`          | Multi Select / Long Text | Depends what the function returns (list vs string). Marking as function-backed |

---

### 7) Content Analysis Metrics

| Airtable Field     | WordPress Source                                                    | Type   | Notes                                                      |
| ------------------ | ------------------------------------------------------------------- | ------ | ---------------------------------------------------------- |
| Internal Links Count    | `(int) get_post_meta($post_id, 'bw_internal_link_count', true)`     | Number | Count of outbound internal links                           |
| External Links Count |
| Word Count         | `(int) get_post_meta($post_id, 'bw_word_count', true)`              | Number | Content length                                             |
| H2 Count           | `(int) get_post_meta($post_id, 'bw_h2_count', true)`                | Number | Heading structure                                          |
| Image Count        | `(int) get_post_meta($post_id, 'bw_image_count', true)`             | Number | Image count                                                |
| Analysed Date      | `substr(get_post_meta($post_id, '_bw_last_analyzed', true), 0, 10)` | Date   | Extracted from MySQL datetime                              |

---

### 8) Link Arrays (Function-backed)

| Airtable Field             | WordPress Source                       | Type | Notes                                                    |
| -------------------------- | -------------------------------------- | ---- | -------------------------------------------------------- |
| Internal Links | `get_internal_links_as_ids($post_id)`  | Text | Function-backed “array” (currently comma-separated IDs)  |
| External Links    | `get_external_links_as_urls($post_id)` | Text | Function-backed “array” (currently comma-separated URLs) |

---

### 9) SEO / Indexing Fields

| Airtable Field   | WordPress Source                                              | Type                 | Notes                                          |
| ---------------- | ------------------------------------------------------------- | -------------------- | ---------------------------------------------- |
| IndexTagSet      | `get_post_meta($post_id, '_seopress_robots_index', true)`     | Text / Checkbox      | SEOPress robot meta Yes/Blank) |
| Canonical        | `get_post_meta($post_id, '_seopress_robots_canonical', true)` | URL                 | SEOPress |
| MetaTitle        | `_yoast_wpseo_title` OR `_seopress_titles_title`              | Text                 | Fallback logic retained                        |
| Meta Description | `_yoast_wpseo_metadesc` OR `_seopress_titles_desc`            | Long Text            | Fallback logic retained                        |
| Short Link       | `get_post_meta($post_id, '_bw_breadcrumb', true)`             | Text                 | Your shortlink/breadcrumb text value           |
| Breadcrumbs      | `get_post_meta($post_id, 'bw_breadcrumb_schema', true)`       | Long Text            | Text    |
| Index Status     | `get_post_meta($post_id, 'bw_index_status', true)`            | Text / Single Select | Your internal 5-state index status             |

---

## Important Implementation Notes (Updated)

### 1) Linked Records (ALTC Cluster, Topics)

**Current Implementation**: sends **term names as text** (`$altc_name`, `$topic_name`).

If you want **true Airtable Linked Records**, you still need one of:

* **Store Airtable record IDs in WP term meta**, then send as `['recXXXX']`
* or `typecast=true` (but only if you’re sending strings into a linked-record field and Airtable is set up to typecast-create)

> Right now: your mapping doc should reflect that Airtable fields for **ALTC Cluster / Topics are Text**, not Linked Records.

---

### 2) Field Type Strictness

Your new mappings introduce more “controlled vocab” fields:

* **Maturity Level / Intent / Purpose** (Single Select)
* **Workflow Next Step** (is Single Select)
* **Workflow Progress** (Multi Select needs to return an array)

If Airtable is set to single select and WP sends a value not in options, Airtable will reject the record (422).
