# MOR_PLAN: XML COMPENDIUM

## MISSION
Build decentralized repository of structural XML layouts for MorBlogger Theme Editor. 
Decouple bone (structure) from skin (CSS). 
Make complex Blogger layouts copy-pasteable.
Kill monolithic template bloat.

## ARCHITECTURE
Rust is the brain. XML is the bone.
Blogger XML is traditionally a monolithic nightmare. We slice it into isolated files: headers, footers, sidebars, main content grids.
XML files MUST be DOM-agnostic. No hardcoded user data.
XML files MUST use standard `<b:section>` tags to generate native Blogger widget sockets.
XML files MUST use exact double-brace tokens for data binding.

## THE TOKEN LEDGER
If an XML module requires dynamic data from the MorBlogger UI, use these exact tokens. Do not invent new ones. `xml_generator.rs` will fail to parse unknown tokens.

### Site Identity
* `{{SITE_TITLE}}` : Raw text of site name
* `{{SITE_TITLE_ATTR}}` : Escaped text for alt/aria attributes
* `{{SITE_HOME_URL_ATTR}}` : Escaped URL to blog root
* `{{HEADER_LOGO_URL_ATTR}}` : Escaped URL to uploaded logo

### Functional
* `{{SEARCH_ACTION_URL_ATTR}}` : Escaped URL for search form target
* `{{LEFT_PANEL_OPEN_LABEL}}` : Aria label for left dock toggle
* `{{RIGHT_PANEL_OPEN_LABEL}}` : Aria label for right dock toggle

## DIRECTORY STRUCTURE
* `headers/` : Top navigation, logos, global search.
* `footers/` : Bottom navigation, copyright, system widgets.
* `main_layouts/` : Core post loops, masonry grids, magazine grids.
* `sidebars/` : Left/right column sockets.
* `css_snippets/` : Pure CSS structural overrides (e.g., hijacking list logic into buttons).

## CURRENT INVENTORY (Phase 1 Complete)
1. `headers/mor_search_plus_bell_header.xml`
2. `footers/mor_three_col_links_plus_audio_player_footer.xml`
3. `css_snippets/mor_two_column_button_grid_for_labels_and_archives.css`

## NEXT OBJECTIVES (Phase 2)
1. **Extract Masonry Grid:** Rip out CSS grid logic for the main blog loop. Convert standard vertical post stream into Pinterest-style masonry cards.
2. **Extract Magazine Layout:** Build a `main_layout` module with a featured post banner on top and a 3-column grid below.
3. **Build Sticky Sidebar Module:** Extract CSS/XML required to make a right-aligned `<b:section>` stick to the viewport while scrolling.
4. **Standardize Pagination:** Build a universal `next/prev` and `home` button XML block that replaces the ugly default Blogger pager.

## RULES FOR SUBMISSION
1. One file, one job.
2. File names must be literal and exact. Describe the structure, not the vibe.
3. All UI strings must be tokenized.
4. Provide standard `<b:section id="..." showaddelement='yes'>` sockets so users can drag-and-drop widgets natively.