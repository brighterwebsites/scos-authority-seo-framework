# Airtable ↔ WordPress Sync Setup Guide
**Last Updated**: 2025-12-19  
**Status**: Ready for Testing  
**Purpose**: Proto-CAM layer for strategic insights testing

---

## What This Does

Uses Airtable as a middle layer (proto-CAM) to:
- ✅ Sync CAR data from WordPress → Airtable automatically
- ✅ Edit content strategy in Airtable (easier than WP admin)
- ✅ Sync changes back to WordPress via webhook
- ✅ Test strategic insights & calibration workflows
- ✅ Validate CAR requirements before Phase 4 implementation

**Think of it as**: Airtable = CAM prototype for testing content strategy workflows

---

## 1. WordPress → Airtable Sync (Automatic)

### What Gets Synced

**Every time you publish/update a post or page**:
- ✅ Basic info (Title, URL, dates)
- ✅ ALTC strategy (Cluster, Topic, Maturity, Intent, Purpose)
- ✅ Content analysis (Word count, links)
- ✅ Optimization status
- ✅ Content fields (TLDR, Excerpt, Meta, Notes)

### Post Types Synced

**Current configuration**:
```php
$allowed_post_types = ['post', 'page', 'kb', 'news'];
```

**To add more CPTs**, edit line 9:
```php
$allowed_post_types = ['post', 'page', 'kb', 'news', 'your_cpt'];
```

### What Doesn't Sync

- ❌ Media/attachments (images, PDFs)
- ❌ Drafts (only published content)
- ❌ Revisions
- ❌ Autosaves

---

## 2. Duplicate Prevention

### How It Works

1. **First time**: Post syncs → Creates Airtable record → Stores record ID in `_airtable_record_id` post meta
2. **Updates**: Checks for record ID → Found? PATCH update → Not found? POST new record
3. **If deleted in Airtable**: Detects 404 → Removes stored ID → Creates new record next time

### Manual Reset

To force re-sync a post:
```php
// In WordPress, delete the stored Airtable ID
delete_post_meta($post_id, '_airtable_record_id');
// Next save will create new Airtable record
```

---

## 3. Airtable → WordPress Sync (Webhook)

### Setup Steps

#### Step 1: Generate Secret Token

**Generate a strong token**:
```bash
# On Mac/Linux
openssl rand -base64 32

# Or use online generator:
# https://www.random.org/strings/
```

**Example token**: `Bearer xK8mP2nV9qR4tY7wE3sA6fD1gH5jL0cN`

#### Step 2: Update WordPress Code

**Edit `temp-drop-in-end-point-airtable.php` line 156**:
```php
$expected_token = 'Bearer YOUR_SECRET_TOKEN_HERE'; // Change this!
```

**Replace with your generated token**:
```php
$expected_token = 'Bearer xK8mP2nV9qR4tY7wE3sA6fD1gH5jL0cN';
```

#### Step 3: Create Airtable Automation

**In Airtable**:
1. Go to Automations
2. Click "Create automation"
3. **Trigger**: "When record updated"
   - Select table: "Content"
   - Optional: Add condition (e.g., only when specific field changes)
4. **Action**: "Run script"
5. **Paste this code**:

```javascript
let config = input.config();
let record = config.record;

// Your WordPress site URL
const wpUrl = 'https://brighterwebsites.com.au/wp-json/scos/v1/sync-car';

// IMPORTANT: Match this token with your WordPress code
const authToken = 'Bearer xK8mP2nV9qR4tY7wE3sA6fD1gH5jL0cN';

// Prepare data to send
const payload = {
    post_id: record.getCellValue('Post ID'),
    car_updates: {
        maturity_level: record.getCellValueAsString('Maturity Level'),
        content_intent: record.getCellValueAsString('Content Intent'),
        content_purpose: record.getCellValueAsString('Content Purpose'),
        optimization_status: record.getCellValueAsString('Optimization Status'),
        content_notes: record.getCellValueAsString('Content Notes'),
        breadcrumbs: record.getCellValueAsString('BreadCrumbs')
    },
    post_updates: {
        excerpt: record.getCellValueAsString('Excerpt')
    }
};

// Send webhook to WordPress
let response = await fetch(wpUrl, {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json',
        'Authorization': authToken
    },
    body: JSON.stringify(payload)
});

if (response.ok) {
    let result = await response.json();
    console.log('✅ Synced to WordPress:', result);
} else {
    let error = await response.text();
    console.error('❌ Sync failed:', response.status, error);
    throw new Error(`Sync failed: ${response.status}`);
}
```

6. **Test**: Click "Test" button in Airtable
7. **Turn on**: Enable the automation

---

## 4. What You Can Edit in Airtable

### Safe to Edit (Syncs Back to WordPress)

**ALTC Strategy**:
- ✅ Maturity Level
- ✅ Content Intent
- ✅ Content Purpose
- ✅ Optimization Status
- ✅ Index Status
- ✅ Content Notes
- ✅ BreadCrumbs

**Content**:
- ✅ Excerpt
- ✅ TLDR (if you add it to sync script)
- ✅ Meta Description (if you add it to sync script)

### Don't Edit (Won't Sync or Will Break)

**Generated Fields**:
- ❌ Post ID (breaks link to WordPress)
- ❌ URL (WordPress controls this)
- ❌ Published Date (WordPress controls this)
- ❌ Word Count (auto-calculated)
- ❌ Internal/External Links (auto-calculated)

**Read-Only**:
- ❌ Title (edit in WordPress)
- ❌ Category (edit in WordPress)

---

## 5. Testing Workflow

### Test WordPress → Airtable

1. **Create/edit a post** in WordPress
2. **Publish** (or update if already published)
3. **Check Airtable** - should see new/updated record
4. **Verify** Post ID and Title match
5. **Check** all strategy fields populated

### Test Airtable → WordPress

1. **Find a synced record** in Airtable
2. **Edit Maturity Level** (or other synced field)
3. **Check WordPress** post meta
4. **Verify** field updated correctly
5. **Check Airtable automation log** for success/errors

---

## 6. Troubleshooting

### WordPress → Airtable Not Working

**Check error_log**:
```bash
# On your server
tail -f /path/to/error_log
```

**Common issues**:
- API token expired/invalid
- Post type not in allowed list
- Network timeout (increase timeout value)
- Airtable field names don't match exactly (case-sensitive!)

**Debug**:
```php
// Add to sync_car_to_airtable() function
error_log('Syncing post ' . $post_id . ': ' . $post->post_title);
error_log('Post type: ' . $post->post_type);
error_log('Response: ' . wp_remote_retrieve_body($response));
```

### Airtable → WordPress Not Working

**Check Airtable automation log**:
- Click on automation → "Run history"
- Look for errors in console output

**Common issues**:
1. **401 Unauthorized**: Token doesn't match
   - Check `$expected_token` in WordPress
   - Check `authToken` in Airtable script
2. **404 Not Found**: Wrong WordPress URL
   - Verify: `https://yourdomain.com/wp-json/scos/v1/sync-car`
   - Test in browser (should return 404 or auth error, not 500)
3. **400 Bad Request**: Missing Post ID
   - Check Post ID field exists and has value in Airtable
4. **Infinite loop**: WordPress updates trigger Airtable, which triggers WordPress...
   - Script prevents this with `remove_action('save_post')`
   - But verify: Check timestamps in both systems

### Test REST Endpoint

**Direct test** (using curl):
```bash
curl -X POST https://yourdomain.com/wp-json/scos/v1/sync-car \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_SECRET_TOKEN" \
  -d '{
    "post_id": 123,
    "car_updates": {
      "maturity_level": "expert"
    }
  }'
```

**Expected response**:
```json
{
  "success": true,
  "post_id": 123,
  "updated_fields": ["maturity_level"],
  "message": "Updated 1 fields for post 123"
}
```

---

## 7. Proto-CAM Testing Workflows

### Workflow 1: Content Gap Analysis

**In Airtable**:
1. Create view: "By ALTC Cluster"
2. Group by: Maturity Level
3. **Insight**: See which maturity levels are missing per cluster
4. **Action**: Plan content to fill gaps

### Workflow 2: Optimization Pipeline

**In Airtable**:
1. Create view: "Optimization Queue"
2. Filter: Optimization Status = "Content" OR "SEO Basic"
3. Sort by: Word Count (asc) - start with short content
4. **Action**: Update optimization status as you work
5. **Syncs back to WordPress** automatically

### Workflow 3: Strategic Pivot Testing

**Scenario**: Test moving content between clusters

**In Airtable**:
1. Create view: "Cluster Rebalancing"
2. Change ALTC Cluster links
3. Update Content Purpose
4. **Insight**: See if content naturally groups differently
5. **Then**: Implement changes in WordPress when confident

### Workflow 4: GPT Content Planning

**Use Airtable as GPT context**:
1. Export filtered view as CSV
2. Upload to ChatGPT
3. Prompt: "Analyze this content strategy. What's missing?"
4. GPT sees: Clusters, topics, maturity distribution
5. **Output**: Strategic recommendations
6. **Implement**: Back in Airtable → Syncs to WordPress

---

## 8. Security Recommendations

### For Testing (Current Setup)

✅ **Bearer token** - Simple, adequate for testing
✅ **HTTPS** - WordPress must use HTTPS
⚠️ **Token in code** - Don't commit to public repo

### For Production (Recommended)

**Option 1: Environment Variables**
```php
$expected_token = getenv('AIRTABLE_WEBHOOK_SECRET');
```

**Option 2: Airtable IP Whitelist**
```php
// Uncomment in verify_airtable_webhook()
$allowed_ips = [
    '18.211.123.71',
    '18.205.245.195',
    '3.216.137.75',
    '3.218.143.118',
];
```

**Option 3: Both**
- Token validation + IP whitelist = Maximum security

---

## 9. Field Mapping Reference

### Editable in Airtable (Syncs to WordPress)

| Airtable Field | WordPress Meta Key | Notes |
|----------------|-------------------|-------|
| Maturity Level | `bw_cont_maturity` | Single select |
| Content Intent | `bw_intent` | Single select |
| Content Purpose | `bw_purpose` | Single select |
| Optimization Status | `_brt_opt_status` | Single select |
| Index Status | `bw_index_status` | Text |
| Content Notes | `bw_notes` | Long text |
| BreadCrumbs | `bw_breadcrumbs` | Text |
| Excerpt | `post_excerpt` | Long text |
| TLDR | `field_689df9726f48c` | ACF field |

### To Add More Fields

**Edit Airtable automation script**:
```javascript
car_updates: {
    maturity_level: record.getCellValueAsString('Maturity Level'),
    // Add your field here:
    pillar_article: record.getCellValue('Pillar Article'),
    index_status: record.getCellValueAsString('Index Status')
}
```

**Edit WordPress webhook handler** (line 196):
```php
$field_map = [
    'maturity_level' => 'bw_cont_maturity',
    // Add your field here:
    'pillar_article' => 'bw_pillar_page_id',
    'index_status' => 'bw_index_status'
];
```

---

## 10. Next Steps

### Immediate (Start Testing)
1. ✅ Publish a test post → Check Airtable
2. ✅ Edit in Airtable → Check WordPress
3. ✅ Create Airtable views for gap analysis
4. ✅ Test content planning workflows

### Short-term (Refine Proto-CAM)
- [ ] Add calculated fields in Airtable (e.g., "Days since last update")
- [ ] Create dashboards for strategic insights
- [ ] Test with GPT for recommendations
- [ ] Document CAR requirements from learnings

### Long-term (Phase 4 Implementation)
- [ ] Build native CAM system based on Airtable learnings
- [ ] Migrate insights/workflows to WordPress
- [ ] Phase out Airtable or keep as external integration

---

## Related Documentation

- **Field Mapping**: `AIRTABLE_FIELD_MAPPING.md`
- **CAR Schema**: `brighter-frameworks-docs/technical/02-CAR-schema.md`
- **CAM Structure**: `brighter-frameworks-docs/technical/03-CAM-structure.md`
- **Module Reference**: `MODULE_REFERENCE.md` - Content Architecture Module

---

**Status**: ✅ Ready for proto-CAM testing!

Test the sync, build some views, and see what strategic insights emerge. This will inform Phase 4 CAM requirements. 🚀

---

_Last updated: 2025-12-19_

