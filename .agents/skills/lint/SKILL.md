---
name: lint-wiki
description: Performs a health-check of the wiki pages, identifying contradictions, stale claims, orphan pages, broken links, missing cross-references, data gaps, and cleaning up formatting.
---

This skill governs the health-checking and maintenance of the `/wiki` directory. It scans the wiki files to ensure high quality, internal consistency, and discoverability.

## Step-by-Step Audit Pipeline

Follow these steps to perform a wiki audit:

### Step 1: Cataloging and Link-Map Building
- Read the content of all markdown files in `/wiki` (including `index.md`).
- Build an internal link map tracking:
  - Every link target (file paths and anchors).
  - Every inbound link to each file.

### Step 2: Running Audit Checks
Scan the link map and files for the following issues:
1. **Orphan Pages**: Identify pages that have no incoming links from *any* page in the `/wiki` directory (including `index.md`). 
   - *Note*: If a page has at least one inbound link from `/wiki/index.md` or any other page, it is NOT considered an orphan.
2. **Broken Links**: Find internal links that point to files or headings/anchors that do not exist.
   - Look for target files that might have been renamed or have a close typographic match.
3. **Contradictions & Stale Claims**: Audit contents for logical contradictions, or claims that have been superseded by newer sources or entries.
4. **Missing Cross-References**: Look for pages that mention important concepts or entities that already have dedicated files in `/wiki` but are not currently linked in the text.
5. **Missing Pages**: Find important concepts or entities that are frequently mentioned across multiple pages but do not yet have their own page in the wiki.
6. **Formatting Inconsistencies & Markdown Issues**: Ensure all files start with correct YAML frontmatter, use `kebab-case.md` names, and conform to the default clear, factual, and terse tone. Check for and fix any markdown syntax issues, including misaligned, broken, or poorly formatted markdown tables (in `index.md` or any other wiki pages). Verify that no media assets (images, videos, drawings, etc.) are present in the `/wiki/index.md` tables' summary columns, and verify index tables are well-formed.
7. **Categorization & Directory Audit**:
   - Verify that every wiki page is stored in its correct category subdirectory under `/wiki/` (e.g. `/wiki/<dynamic-category>/<kebab-case-name>.md`).
   - Check if any individual page has evolved and needs to be moved/recategorized based on its current content.
   - Perform a high-level taxonomy review to check if the entire wiki's folder and table classification structure needs a global reorganization (e.g. merging similar categories or defining new ones to group files better). Propose folder movements and index table updates for any reorganization.

### Step 3: Reporting Format
Generate the audit report using the following structure:
```markdown
# Wiki Audit Report - [YYYY-MM-DD]

## 1. Summary of Issues Found
- **Orphan Pages**: [None / List of files]
- **Broken Links**: [None / List of source files and broken targets]
- **Contradictions & Stale Claims**: [None / Description of issues]
- **Missing Cross-References**: [None / List of pages and suggested links]
- **Missing Pages / Concepts**: [None / List of suggested new pages]
- **Formatting & Index Media Issues**: [None / List of formatting issues]
- **Categorization & Taxonomy Reorgs**: [None / List of files needing recategorization or taxonomy suggestions]

## 2. Proposed Remedies & Action Plan
- **Automated Fixes (Ready to Execute)**: [e.g., Simple typo fixes, inserting cross-references to existing pages]
- **Requires User Review**: [e.g., Resolving contradictions, page recategorizations, global taxonomy restructuring]
```

### Step 4: Proposing & Executing Fixes
- Offer to fix simple or obvious formatting/link errors automatically.
- For complex fixes (such as resolving contradictions or writing new concept pages), present the proposed remedies to the user for approval.

### Step 5: Logging
- Append an entry to `/wiki/log.md` with the lint activity. Use the current date:
  ```markdown
  [YYYY-MM-DD] lint | <Brief summary of findings and fixes performed>
  ```
