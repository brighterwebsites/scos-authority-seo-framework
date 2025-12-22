# Airtable Field Mapping Reference
**Last Updated**: 2025-12-19  
**Status**: Ready for Implementation  
**Related File**: `temp-drop-in-end-point-airtable.php`

---

## WordPress → Airtable Field Mapping

### Basic Post Info

| Airtable Field | WordPress Source | Type | Notes |
|----------------|------------------|------|-------|
| Post ID | `$post_id` | Number | Primary key |
| Title | `$post->post_title` | Text | Post title |
| URL | `get_permalink($post_id)` | Text | Full URL |
| Published Date | `get_the_date('Y-m-d')` | Date | ISO format |
| Last Modified Date | `get_the_modified_date('Y-m-d')` | Date | ISO format |

---

### ALTC Strategy Fields

| Airtable Field | WordPress Meta Key | Type | Options/Notes |
|----------------|-------------------|------|---------------|
| Maturity Level | `bw_cont_maturity` | Single Select | Export, Professional, Thought Leader, etc. |
| Content Intent | `bw_intent` | Single Select | Information, Commercial, etc. (11 types) |
| Content Purpose | `bw_purpose` | Single Select | Pillar, Supporting, Authority, etc. (12 types) |
| ALTC Cluster | `bw_primary_altc_id` | Linked Record | Taxonomy: `altc_strategic_lens` |
| Topics | `bw_primary_topic_id` | Linked Record | Taxonomy: `altc_topic` |

**Content Intent Options** (from code):
- Information
- Information Problem
- Information Solution
- Commercial
- Commercial Decision Support
- (+ 6 more - see `bw_cs_intent_options()` in `bw-content-strategy.php`)

**Content Purpose Options** (from code):
- Pillar
- Supporting
- Authority
- Case Study
- Resource Guide
- Service Page
- Product Page
- (+ 5 more - see `bw_cs_purpose_options()` in `bw-content-strategy.php`)

---

### Content Analysis

| Airtable Field | WordPress Meta Key | Type | Notes |
|----------------|-------------------|------|-------|
| Internal Links Out | `bw_internal_link_count` | Number | Count of outbound internal links |
| Internal Links In | N/A | Number | Currently 0 - needs calculation |
| Word Count | `bw_word_count` | Number | Content only (no headers/footers) |

---

### Optimization & Status

| Airtable Field | WordPress Meta Key | Type | Options/Notes |
|----------------|-------------------|------|---------------|
| Optimization Status | `_brt_opt_status` | Single Select | 14 states (see below) |
| Index Status | `bw_index_status` | Text | 5 states (see below) |

**Optimization Status Options** (14 states):
- Content
- SEO Basic
- Conversion
- Repurpose
- (+ 10 more - see `bw_cs_opt_status_options()` in `bw-content-strategy.php`)

**Index Status Options** (5 states):
- See `bw_cs_index_status_options()` in `bw-content-strategy.php`

---

### Content Fields

| Airtable Field | WordPress Source | Type | Notes |
|----------------|------------------|------|-------|
| TLDR | `field_689df9726f48c` (ACF) | Long Text | ACF custom field |
| Excerpt | `$post->post_excerpt` | Long Text | Auto-generated if empty (55 words) |
| MetaTitle | `_yoast_wpseo_title` OR `_seopress_titles_title` | Text | SEO meta title |
| Meta Description | `_yoast_wpseo_metadesc` OR `_seopress_titles_desc` | Long Text | SEO meta description |
| BreadCrumbs | `bw_breadcrumbs` | Long Text | Short title for YOURLS |
| Content Notes | `bw_notes` | Long Text | ALTC/Content strategy notes |

---

### Relationships

| Airtable Field | WordPress Meta Key | Type | Notes |
|----------------|-------------------|------|-------|
| Pillar Article | `bw_pillar_page_id` | Text | Post title of related pillar |
| Category | WordPress category | Single Select | First category name |

---

## Important Implementation Notes

### 1. Linked Records (ALTC Cluster, Topics)

**Current Implementation**:
- Sends term names as strings
- Example: "AI Citation Infrastructure", "Schema Optimization"

**For True Airtable Linked Records**, you need ONE of:

**Option A: Store Airtable Record IDs in WordPress**
```php
// Store Airtable record ID in term meta
update_term_meta($term_id, 'airtable_record_id', 'recXXXXXXXXXXX');

// Then send as array of record IDs
'ALTC Cluster' => [get_term_meta($primary_altc_id, 'airtable_record_id', true)],
'Topics' => [get_term_meta($primary_topic_id, 'airtable_record_id', true)],
```

**Option B: Use Airtable Typecast**
```php
// Add typecast parameter to API call
$response = wp_remote_post('https://api.airtable.com/v0/appOqcQR79umbJJGP/Content?typecast=true', [
    // ... rest of config
]);
```
This auto-creates linked records by name if they don't exist.

---

### 2. Internal Links In (Backlinks)

Currently set to `0`. To calculate:

```php
/**
 * Count internal backlinks to this post
 */
function get_internal_backlinks_count($post_id) {
    global $wpdb;
    
    $permalink = get_permalink($post_id);
    $domain = parse_url($permalink, PHP_URL_HOST);
    
    // Search post content for links to this post
    $count = $wpdb->get_var($wpdb->prepare("
        SELECT COUNT(DISTINCT p.ID) 
        FROM {$wpdb->posts} p
        WHERE p.post_status = 'publish'
        AND p.post_content LIKE %s
        AND p.ID != %d
    ", '%' . $wpdb->esc_like($permalink) . '%', $post_id));
    
    return (int) $count;
}

// Then use:
'Internal Links In' => get_internal_backlinks_count($post_id),
```

**⚠️ Warning**: This query can be slow on large sites. Consider:
- Caching results
- Background processing
- Incremental updates

---

### 3. Duplicate Record Prevention

**Current Implementation**: Creates NEW record each save

**To UPDATE existing records instead**:

```php
// 1. Check if record exists
$existing_record = get_post_meta($post_id, 'airtable_record_id', true);

if ($existing_record) {
    // 2. Use PATCH to update
    $response = wp_remote_request(
        'https://api.airtable.com/v0/appOqcQR79umbJJGP/Content/' . $existing_record,
        [
            'method' => 'PATCH',
            'headers' => [
                'Authorization' => 'Bearer YOUR_TOKEN',
                'Content-Type' => 'application/json'
            ],
            'body' => json_encode(['fields' => $airtable_data])
        ]
    );
} else {
    // 3. Create new record (POST)
    $response = wp_remote_post(/* ... */);
    
    // 4. Store Airtable record ID for future updates
    if (!is_wp_error($response)) {
        $body = json_decode(wp_remote_retrieve_body($response), true);
        if (isset($body['id'])) {
            update_post_meta($post_id, 'airtable_record_id', $body['id']);
        }
    }
}
```

---

### 4. Field Type Validation

**Airtable is strict about field types**:

| Type | WordPress | Airtable Requirement |
|------|-----------|---------------------|
| Number | String "123" | Integer 123 |
| Date | "2025-12-19" | ISO format: "2025-12-19" ✅ |
| Checkbox | "yes" | Boolean true |
| Select | Any string | Must match option exactly |

**Current code handles**:
- ✅ Numbers cast to `(int)`
- ✅ Dates in ISO format
- ✅ Empty values filtered out
- ⚠️ Select options - ensure exact match with Airtable

---

### 5. Error Handling & Logging

**Current Implementation**:
```php
if (is_wp_error($response)) {
    error_log('Airtable sync error: ' . $response->get_error_message());
}
```

**Enhanced Error Handling**:
```php
if (is_wp_error($response)) {
    error_log(sprintf(
        'Airtable sync error for post %d: %s',
        $post_id,
        $response->get_error_message()
    ));
    return;
}

$status_code = wp_remote_retrieve_response_code($response);
$body = wp_remote_retrieve_body($response);

if ($status_code !== 200 && $status_code !== 201) {
    error_log(sprintf(
        'Airtable API error for post %d: Status %d, Response: %s',
        $post_id,
        $status_code,
        $body
    ));
}
```

---

## Testing Checklist

Before deploying:

- [ ] **API Token Valid**: Test API call in Postman/Insomnia
- [ ] **Field Names Match**: Verify Airtable field names (case-sensitive!)
- [ ] **Select Options Match**: Maturity Level, Intent, Purpose values exist in Airtable
- [ ] **Linked Records Work**: Test ALTC Cluster and Topics linking
- [ ] **Duplicate Prevention**: Verify updates vs. creates
- [ ] **Error Logging**: Check error_log for failed syncs
- [ ] **Performance**: Test on large content library (consider async)

---

## Webhook Return Sync (Airtable → WordPress)

The script includes a placeholder for bidirectional sync:

```javascript
// Airtable automation script (lines 46-62)
fetch('https://brighterwebsites.com.au/wp-json/scos/v1/sync-car', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json',
        'Authorization': 'Bearer YOUR_WP_API_KEY'
    },
    body: JSON.stringify({
        post_id: record.getCellValue('Post ID'),
        car_updates: {
            maturity_level: record.getCellValue('Maturity Level'),
            priority: record.getCellValue('Priority')
        }
    })
});
```

**To implement**:
1. Register REST endpoint: `/wp-json/scos/v1/sync-car`
2. Validate webhook signature
3. Update WordPress post meta from Airtable data
4. Prevent infinite loop (WP → Airtable → WP)

---

## Related Documentation

- **CAR Schema**: `brighter-frameworks-docs/technical/02-CAR-schema.md`
- **Technical Architecture**: `TECHNICAL_ARCHITECTURE.md` (lines 494-544)
- **Module Reference**: `MODULE_REFERENCE.md` - Content Architecture Module
- **Content Strategy Fields**: `brighter-core/includes/bw-content-strategy.php`

---

**Next Steps**:
1. ✅ Field mapping complete
2. 🔄 Test with single post
3. 📋 Implement duplicate prevention
4. 📋 Add backlinks calculation
5. 📋 Set up bidirectional sync

---

_Last updated: 2025-12-19_

