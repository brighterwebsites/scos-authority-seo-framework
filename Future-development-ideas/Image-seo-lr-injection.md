
Since you have **Claude CLI** on your desktop and a highly structured **SCOS**, you are actually in a better position than 99% of photographers. You don't need to wait for Adobe to build a "Brand Voice" feature—you can build a bridge between Lightroom's file system and your Claude MCP today.

In 2026, the "back door" is simply the fact that Lightroom Classic stores its metadata in **Sidecar XMP files** or the **Catalog SQLite database**.

### The "SCOS-Lightroom Bridge" Concept
Instead of manual entry, you can use a CLI-based workflow where Claude "looks" at your export folder, reads your SCOS strategy docs, and writes the metadata back to the images before they ever hit WordPress.

#### 1. The "Vision-to-Meta" Workflow
Since Claude 3.5/4 (2026 models) has elite vision capabilities, your CLI can perform a "Contextual Injection":
1.  **Export:** You export your "Job" from Lightroom to a local folder.
2.  **Analyze:** You run a Claude CLI command: `claude analyze-images ./exports --intent "Commercial" --cluster "Running Gear"`.
3.  **Process:** Claude opens the image, sees the blue shoes, cross-references your **SCOS Brand Voice** (stored in your Layer 1 docs), and generates:
    * **Alt Text:** Brand-aligned and descriptive.
    * **Caption:** Story-driven for your "Success Stories" CPT.
    * **Keywords:** Entity-heavy for 2026 SEO.
4.  **Write:** Use a tool like `exiftool` (via CLI) to inject that text directly into the image's IPTC fields.

#### 2. Using "PhotoTag.ai" or "Excire" as a Middleman
If you want a more "packaged" solution within Lightroom:
* **PhotoTag.ai (2026 Plugin):** This is the current leader for AI metadata in LR. It can batch-generate Titles/Captions/Keywords.
* **The SCOS Hack:** You can feed PhotoTag.ai a "Custom Context" prompt. Paste your **SCOS Intent Definitions** into its settings. This forces the AI to categorize images using your specific strategic lenses (e.g., "Maturity: Expert" or "Intent: Transactional").

---

### Implementation: The "SCOS Image Prep" Script
Since you’re comfortable with a "Software Layer," you could add an `scos-image-prep` utility to your system. 



**How the script would work:**
```bash
# Example CLI command for your SCOS desktop bridge
scos-prep --folder "./Job-202-BlueShoes" --voice "Authoritative" --target-page "blue-shoe-review"
```
1.  **Fetch Context:** The script hits your `brighter-core/v1/scos` endpoint to get the "Intent Goal" and "Primary Topic" for the `blue-shoe-review` page.
2.  **Vision Pass:** Claude scans the folder.
3.  **Metadata Injection:** It writes the Title, Alt, and Caption to the images.
4.  **Upload:** When you upload to WP, **Media Library Assistant** picks up these perfectly optimized, brand-aligned strings and populates your site.

### Why this is better than "Native" AI:
Adobe’s AI is "General Purpose." It will tell you it's a "shoe on a road." Your **SCOS-Claude Bridge** will tell the world it’s a *"High-durability [Topic] solution for professional athletes [Maturity] looking for pavement-tested reliability [Intent]."*

**Would you like me to draft a prompt for your Claude CLI that you can use to test this "Vision-to-IPTC" logic on a single image?**