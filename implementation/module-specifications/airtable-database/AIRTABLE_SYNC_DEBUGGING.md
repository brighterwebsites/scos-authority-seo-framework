# Airtable Sync Debugging Guide
**Last Updated**: 2025-12-19  
**Issue**: Only posts and news syncing, not pages/kb/folio

---

## Airtable Rate Limits

### Rate Limits by Plan

| Plan | Rate Limit | Notes |
|------|------------|-------|
| Free | 5 requests/second | 1,200 requests/minute |
| Plus | 5 requests/second | 1,200 requests/minute |
| Pro | 10 requests/second | 2,400 requests/minute |
| Enterprise | Custom | Contact Airtable |

**What happens when limit hit**:
- HTTP 429 status code
- Error: "Rate limit exceeded"
- Retry after: Usually 1-2 seconds

### Current Protection

**Rate limiting protection added**:
- ✅ 5-second cooldown between syncs per post
- ✅ Logs rate limit errors (429 status)
- ✅ Prevents rapid-fire updates

---

## Why Only Posts/News Working?

### Possible Causes

**1. Post Type Registration**
- CPTs might not be registered when hook fires
- Check: Are `kb`, `folio` registered before `save_post` hook?

**2. Post Status**
- Only `publish` status syncs
- Check: Are pages/kb/folio actually published?

**3. Silent Errors**
- API errors not being logged
- Check: Error log for `[Airtable Sync]` messages

**4. Field Validation**
- Airtable rejecting certain field values
- Check: API response body for validation errors

---

## Debugging Steps

### Step 1: Check Error Logs

**View WordPress error log**:
```bash
# On server
tail -f /path/to/wp-content/debug.log

# Or check error_log location
# Usually: /var/log/php-errors.log or wp-content/debug.log
```

**Look for**:
```
[Airtable Sync] SUCCESS: Post 123 (post) synced to Airtable
[Airtable Sync] SUCCESS: Post 456 (news) synced to Airtable
[Airtable Sync] skipped: Post 789 (page) type "page" not in allowed list
[Airtable Sync] ERROR for post 101 (kb): ...
```

### Step 2: Test Each Post Type Manually

**Add this temporary debug function**:

```php
// Add to temp-drop-in-end-point-airtable.php (temporary)
add_action('admin_notices', function() {
    if (isset($_GET['test_airtable_sync'])) {
        $post_id = intval($_GET['test_airtable_sync']);
        $post = get_post($post_id);
        
        if (!$post) {
            echo '<div class="notice notice-error"><p>Post not found</p></div>';
            return;
        }
        
        echo '<div class="notice notice-info"><p>';
        echo 'Post ID: ' . $post_id . '<br>';
        echo 'Post Type: ' . $post->post_type . '<br>';
        echo 'Post Status: ' . $post->post_status . '<br>';
        echo 'Allowed Types: ' . implode(', ', ['post', 'page', 'kb', 'news', 'folio']) . '<br>';
        echo 'Is Allowed: ' . (in_array($post->post_type, ['post', 'page', 'kb', 'news', 'folio'], true) ? 'YES' : 'NO') . '<br>';
        echo '</p></div>';
        
        // Trigger sync manually
        sync_car_to_airtable($post_id, $post, true);
    }
});
```

**Then test**:
```
https://yourdomain.com/wp-admin/?test_airtable_sync=123
```

### Step 3: Check Airtable API Response

**Add detailed logging** (temporary):

```php
// In sync_car_to_airtable(), after API call
$response_body = wp_remote_retrieve_body($response);
error_log('[Airtable Debug] Full response: ' . print_r([
    'status' => wp_remote_retrieve_response_code($response),
    'headers' => wp_remote_retrieve_headers($response),
    'body' => json_decode($response_body, true)
], true));
```

### Step 4: Verify Post Types Exist

**Check registered post types**:
```php
// Add to functions.php temporarily
add_action('admin_footer', function() {
    if (current_user_can('manage_options')) {
        $post_types = get_post_types(['public' => true], 'objects');
        echo '<script>console.log("Registered Post Types:", ' . json_encode(array_keys($post_types)) . ');</script>';
    }
});
```

---

## Common Issues & Fixes

### Issue 1: Post Type Not Registered

**Symptom**: Log shows "type not in allowed list" even though it's in array

**Fix**: Ensure CPTs registered before `save_post` hook:
```php
// In your CPT registration file
add_action('init', 'register_my_cpt', 10);

// Then register sync hook AFTER CPTs
add_action('init', function() {
    add_action('save_post', 'sync_car_to_airtable', 10, 3);
}, 20); // Higher priority = runs after CPT registration
```

### Issue 2: Airtable Field Validation Error

**Symptom**: 422 status code, "Invalid field value"

**Fix**: Check field values match Airtable options exactly:
- Maturity Level: Must match dropdown options exactly
- Content Intent: Must match dropdown options exactly
- Case-sensitive!

**Debug**:
```php
// Log what we're sending
error_log('[Airtable Debug] Sending data: ' . json_encode($airtable_data, JSON_PRETTY_PRINT));
```

### Issue 3: Rate Limit Hit

**Symptom**: 429 status code, "Rate limit exceeded"

**Fix**: 
- Already handled with 5-second cooldown
- If still happening, increase cooldown:
```php
if ($last_sync && ($now - $last_sync) < 10) { // 10 seconds instead of 5
```

### Issue 4: Empty Field Values

**Symptom**: Some fields missing in Airtable

**Fix**: Check `array_filter` isn't removing valid empty values:
```php
// Current: Removes 0, '', null
// If you need to send empty strings, adjust:
$airtable_data = array_filter($airtable_data, function($value) {
    return $value !== null; // Only remove null, keep 0 and ''
});
```

---

## Testing Checklist

**For each post type**:

- [ ] **Post exists**: `get_post($post_id)` returns object
- [ ] **Post type registered**: Shows in `get_post_types()`
- [ ] **Post published**: `$post->post_status === 'publish'`
- [ ] **In allowed list**: Post type in `$allowed_post_types` array
- [ ] **Not autosave**: `DOING_AUTOSAVE` not defined
- [ ] **Not revision**: `wp_is_post_revision()` returns false
- [ ] **API call succeeds**: Status 200 or 201
- [ ] **Record created**: Check Airtable for new record
- [ ] **Record ID stored**: `_airtable_record_id` meta exists

---

## Quick Debug Command

**Add this WP-CLI command** (if you have WP-CLI):

```php
// wp-content/mu-plugins/debug-airtable.php
WP_CLI::add_command('airtable sync-test', function($args) {
    $post_id = intval($args[0] ?? 0);
    if (!$post_id) {
        WP_CLI::error('Usage: wp airtable sync-test <post_id>');
    }
    
    $post = get_post($post_id);
    if (!$post) {
        WP_CLI::error("Post {$post_id} not found");
    }
    
    WP_CLI::log("Testing sync for post {$post_id} ({$post->post_type})");
    sync_car_to_airtable($post_id, $post, true);
    WP_CLI::success('Sync attempted - check error log');
});
```

**Usage**:
```bash
wp airtable sync-test 123
```

---

## What to Check Right Now

1. **Error Log**: Look for `[Airtable Sync]` messages
2. **Post Status**: Are pages/kb/folio actually published?
3. **Post Type Names**: Are they exactly `'page'`, `'kb'`, `'folio'`? (case-sensitive)
4. **Airtable Base**: Check if records are being created but in wrong table/view
5. **API Token**: Is it valid? (Check Airtable account)

---

## Next Steps

1. ✅ Check error log for `[Airtable Sync]` messages
2. ✅ Verify post types are published (not draft)
3. ✅ Test one page/kb/folio manually
4. ✅ Check Airtable for any records (might be in different view)
5. ✅ Verify API token hasn't expired

**Most likely cause**: Post status not `'publish'` or post type name mismatch (case-sensitive!)

---

_Last updated: 2025-12-19_

