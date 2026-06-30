---
name: lint-wiki
description: Performs a health-check of the wiki pages, identifying contradictions, stale claims, orphan pages, broken links, missing cross-references, data gaps, and cleaning up formatting.
---

This skill governs the health-checking and maintenance of the `/wiki` directory. It scans the wiki files to ensure high quality, internal consistency, and discoverability.

## Audit Workflow

Follow these steps to perform a wiki audit:

### 1. Catalog and Index Verification
- Load all wiki pages and build a map of internal links (outgoing and incoming).
- Scan the wiki files for the following issues:
  - **Orphan Pages**: Identify pages that have no incoming links from *any* other page in the `/wiki` directory (including `index.md`). If a page is linked in `index.md` or any other page, it is NOT considered an orphan.
  - **Broken Links**: Find internal links that point to files or headings that do not exist. Propose to either fix the links (if the target file was renamed or has a similar name) or remove the broken links.
  - **Contradictions & Stale Claims**: Analyze pages for logical contradictions, or claims that have been superseded by newer sources or entries.
  - **Missing Cross-References**: Look for pages that mention important concepts or entities that already have their own dedicated files but are not currently linked.
  - **Missing Pages**: Find important concepts or entities that are frequently mentioned across multiple pages but do not yet have their own page in the wiki. Propose creating them.
  - **Formatting Inconsistencies**: Ensure all files start with proper YAML frontmatter and conform to the default clear, factual, and terse tone.

### 2. Reporting & Remediation
- Present a detailed report of findings categorized by the issue types above.
- For simple or obvious issues (such as fixing a typo in a link, adding a missing cross-reference to an existing page, or minor formatting issues), offer to fix them automatically.
- For complex issues (such as resolving contradictions or creating new concept pages), present the recommended action plan to the user for confirmation.

### 3. Log the Pass
- Append an entry to `/wiki/log.md` with the lint activity. Use the current date:
  ```markdown
  ## [YYYY-MM-DD] lint | <Summary of findings and fixes performed>
  ```
