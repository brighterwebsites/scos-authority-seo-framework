# Airtable Quick Fix - 422 Error
**Issue**: `INVALID_VALUE_FOR_COLUMN: Value is not an array of record IDs`  
**Date**: 2025-12-19

---

## The Problem

Airtable is rejecting the sync because **Linked Record** fields expect arrays of record IDs, but we're sending strings (term names).

**Error**:
```
Status 422: {"error":{"type":"INVALID_VALUE_FOR_COLUMN","message":"Value is not an array of record IDs."}}
```

---

## Quick Fix: Change Airtable Fields to Text

**Easiest solution** (recommended for testing):

1. **In Airtable**:
   - Go to your "Content" table
   - Click on "ALTC Cluster" field header
   - Change field type: **Linked Record** → **Single line text**
   - Click on "Topics" field header  
   - Change field type: **Linked Record** → **Single line text**

2. **Result**:
   - ✅ Sync will work immediately
   - ✅ Term names will appear as text
   - ✅ You can still filter/search by cluster/topic
   - ⚠️ No automatic linking (but that's fine for testing)

3. **Later** (when ready for production):
   - Set up proper linked records with record IDs
   - Or keep as text if that works for your workflow

---

## Alternative: Remove Linked Record Fields Temporarily

**If you can't change field types**:

The code now automatically retries without linked record fields if it gets a 422 error. So you can:

1. **Leave fields as Linked Records** in Airtable
2. **Code will skip them** on retry
3. **Other fields will sync** successfully

**To manually exclude them**, edit the code:

```php
// Comment out these lines:
// 'ALTC Cluster' => $altc_term ? $altc_term->name : '',
// 'Topics' => $topic_term ? $topic_term->name : '',
```

---

## REST API Warning (Non-Critical)

**Warning**:
```
Use rest_authentication_errors instead. The REST API can no longer be completely disabled
```

**What it means**:
- ⚠️ Just a deprecation notice (not an error)
- ✅ Won't break functionality
- ✅ Can be ignored for now

**To fix** (if you want):
- Update any plugins/themes using old REST API filters
- Or ignore it - WordPress will handle it automatically

---

## Testing After Fix

1. **Change Airtable fields to Text** (recommended)
2. **Update a post** in WordPress
3. **Check error log** - should see:
   ```
   [Airtable Sync] SUCCESS: Post 123 (post) synced to Airtable
   ```
4. **Check Airtable** - record should appear with ALTC Cluster and Topics as text

---

## Why This Happens

**Linked Records in Airtable**:
- Expect: `["recXXXXXXXXX", "recYYYYYYYYY"]` (array of record IDs)
- We're sending: `"AI Citation Infrastructure"` (string)

**Text Fields in Airtable**:
- Accept: `"AI Citation Infrastructure"` (string)
- ✅ Works perfectly for our use case

**For Proto-CAM Testing**:
- Text fields are actually **better** for now
- Easier to filter/search
- No need to maintain record ID mappings
- Can always upgrade to linked records later

---

## Next Steps

1. ✅ **Change Airtable fields to Text** (2 minutes)
2. ✅ **Test sync** - should work immediately
3. ✅ **Continue proto-CAM testing**
4. 📋 **Upgrade to linked records later** (if needed)

---

**Status**: ✅ Quick fix available - change fields to Text type in Airtable

---

_Last updated: 2025-12-19_

