---
name: translate-raw
description: Translates raw notes and links in the /raw folder into structured, interlinked wiki pages in the /wiki folder, updates index.md and log.md, and moves the ingested raw files to /archive.
---

This skill governs the ingestion and processing of raw captures (notes, web clips, drafts) from the `/raw` directory into the structured, Obsidian-compatible `/wiki` directory.

## Ingest Workflow

Follow these steps precisely for each file in `/raw`:

### 1. File Discovery
Scan the `/raw` folder (including `/raw/daily` and `/raw/others`) for unprocessed files. Process them one at a time.

### 2. Read and Merge
- Read the content of the target raw file.
- Identify the core concepts, entities, or topics.
- Check the existing `/wiki` directory (using the `/wiki/index.md` catalog or a search tool) to see if pages for these topics already exist.
- **Hard Rule**: Never overwrite a `/wiki` entry blindly. If a page exists, read its contents first, then merge the new information cleanly.

### 3. Wiki Page Structure & Voice
- All pages must start with YAML frontmatter containing metadata (e.g., `title`, `date`, `tags`, `source`).
- **File Naming**: Use one topic per file, and name files using `kebab-case.md`.
- **Tone**: Keep it clear, factual, and terse.
- **Preservation**: Preserve the user's specific phrasing if it carries signal.
- **Formatting**:
  - Use headings only when the entry is long enough to need them.
  - Use bullets only when the content is genuinely a list.
  - **Tasks**: Do NOT add Obsidian tasks that start with `- [ ]` or `- [/-]` to the wiki as tasks. If they contain valuable knowledge or links, extract and add that knowledge to the wiki, but discard the raw checkbox task structure.

### 4. Index and Log Updates
- **Update `/wiki/index.md`**: On every ingest, update the catalog index. List the page under its appropriate category (entities, concepts, sources, etc.) with:
  - A markdown link to the file.
  - A one-line summary.
  - Metadata (e.g., date of ingest, source count).
- **Append to `/wiki/log.md`**: Add an append-only entry to the log with a consistent prefix. Use the current date:
  ```markdown
  ## [YYYY-MM-DD] ingest | <Title/Topic Name>
  ```

### 5. Archiving Processed Files
- Once the content is successfully integrated into the `/wiki` and logged:
  - Create the corresponding destination subdirectory under `/archive` if it does not already exist.
  - Move the raw file to `/archive` while preserving the exact relative path structure.
  - **Hard Rule**: Never delete anything from `/raw` or `/archive`. Move files only.
  
  *Example Command to execute:*
  ```bash
  # For a file raw/daily/my-note.md:
  mkdir -p "archive/daily" && mv "raw/daily/my-note.md" "archive/daily/my-note.md"
  ```
