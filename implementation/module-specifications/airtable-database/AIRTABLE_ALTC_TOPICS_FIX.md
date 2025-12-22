# ALTC Cluster & Topics Sync Fix
**Date**: 2025-12-19  
**Issue**: ALTC Cluster and Topics not syncing to Airtable

---

## The Problem

1. **Custom dropdowns** save term IDs to `bw_primary_altc_id` and `bw_primary_topic_id`
2. **These don't sync** with WordPress taxonomies automatically
3. **Term retrieval** was failing silently
4. **Airtable fields** were Linked Record type (needed arrays, got strings)

---

## The Fix

### 1. Better Term Retrieval ✅

**Now tries multiple methods**:
1. Get term from meta field ID (`bw_primary_altc_id`)
2. **Fallback**: Get terms directly from post taxonomies
3. Handles errors gracefully

**Code**:
```php
// Method 1: From meta field (custom dropdown)
$primary_altc_id = get_post_meta($post_id, 'bw_primary_altc_id', true);
if ($primary_altc_id) {
    $altc_term = get_term($primary_altc_id, 'altc_strategic_lens');
    $altc_name = $altc_term->name;
}

// Method 2: Fallback to taxonomy (if meta empty)
if (empty($altc_name)) {
    $altc_terms = wp_get_post_terms($post_id, 'altc_strategic_lens', ['fields' => 'names']);
    $altc_name = $altc_terms[0] ?? '';
}
```

### 2. Always Send as Text ✅

**Changed**:
- Removed retry logic that stripped ALTC/Topics
- Always sends term names as text strings
- No more "record IDs" errors

### 3. Post ID as Mapping Key ✅

**Already working**:
- Post ID is primary key in Airtable
- Maps WordPress post → Airtable record
- No need to store Airtable IDs in WordPress

---

## What You Need to Do

### Step 1: Verify Airtable Field Types

**In Airtable "Content" table**:
- ✅ **ALTC Cluster** field type: **Single line text** (NOT Linked Record)
- ✅ **Topics** field type: **Single line text** (NOT Linked Record)

**If still Linked Record**:
1. Click field header → Change field type → Single line text
2. Existing linked records will convert to text (term names)

### Step 2: Test Sync

1. **Edit a post** with ALTC Cluster/Topic set
2. **Save/Update** the post
3. **Check error log** - should see:
   ```
   [Airtable Sync] SUCCESS: Post 123 (post) synced to Airtable
   ```
4. **Check Airtable** - ALTC Cluster and Topics should appear as text

### Step 3: Verify Data

**In Airtable, check**:
- ✅ Post ID matches WordPress post ID
- ✅ ALTC Cluster shows term name (e.g., "AI-First & Future-Proof SEO")
- ✅ Topics shows term name (e.g., "AI Citation Strategy")

---

## How It Works Now

### WordPress → Airtable Flow

1. **Post saved** in WordPress
2. **Get ALTC Cluster**:
   - Try: `bw_primary_altc_id` meta field → get term name
   - Fallback: `altc_strategic_lens` taxonomy → get first term name
3. **Get Topic**:
   - Try: `bw_primary_topic_id` meta field → get term name
   - Fallback: `altc_topic` taxonomy → get first term name
4. **Send to Airtable**:
   - Post ID as key
   - ALTC Cluster as text
   - Topics as text
   - All other fields

### Mapping

**WordPress** → **Airtable**
- Post ID → Post ID (primary key)
- Term name → ALTC Cluster (text)
- Term name → Topics (text)

**No bidirectional sync needed** - Post ID is the mapping key.

---

## Troubleshooting

### ALTC/Topics Still Empty

**Check**:
1. **Post has ALTC/Topic set?**
   - Check meta box in WordPress
   - Check `bw_primary_altc_id` and `bw_primary_topic_id` meta values
2. **Terms exist?**
   - Check taxonomies: `altc_strategic_lens` and `altc_topic`
   - Verify terms aren't deleted
3. **Error log**:
   - Look for `[Airtable Sync]` messages
   - Check for term retrieval errors

**Debug code** (add temporarily):
```php
error_log('ALTC ID: ' . $primary_altc_id);
error_log('ALTC Name: ' . $altc_name);
error_log('Topic ID: ' . $primary_topic_id);
error_log('Topic Name: ' . $topic_name);
```

### Still Getting 422 Errors

**If error says "record IDs"**:
- Airtable field is still Linked Record type
- Change to Text type in Airtable

**If error says "invalid value"**:
- Field value doesn't match Airtable dropdown options
- Check exact spelling/case of term names

**If error says "missing required"**:
- Required field is empty
- Check if Post ID field is required in Airtable

---

## Future: Sync Taxonomy Checkboxes

**Current limitation**:
- Custom dropdowns (`bw_primary_altc_id`) don't sync with taxonomy checkboxes
- If you check boxes in taxonomy sidebar, they don't update meta fields

**Future fix** (if needed):
```php
// Sync taxonomy → meta fields on save
add_action('save_post', function($post_id) {
    $altc_terms = wp_get_post_terms($post_id, 'altc_strategic_lens', ['fields' => 'ids']);
    if (!empty($altc_terms)) {
        update_post_meta($post_id, 'bw_primary_altc_id', $altc_terms[0]);
    }
    
    $topic_terms = wp_get_post_terms($post_id, 'altc_topic', ['fields' => 'ids']);
    if (!empty($topic_terms)) {
        update_post_meta($post_id, 'bw_primary_topic_id', $topic_terms[0]);
    }
}, 5); // Before Airtable sync (priority 10)
```

**For now**: Use the custom dropdowns in meta box - they work fine.

---

## Summary

✅ **Fixed**: Better term retrieval with fallbacks  
✅ **Fixed**: Always sends as text (no linked record errors)  
✅ **Fixed**: Post ID as mapping key (no need for Airtable IDs in WP)  
✅ **Ready**: Test sync with ALTC/Topics

**Next**: Change Airtable fields to Text type, test sync, verify data appears.

---

_Last updated: 2025-12-19_

