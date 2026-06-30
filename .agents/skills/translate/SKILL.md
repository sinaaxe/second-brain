---
name: translate-raw
description: Translates raw notes and links in the /raw folder into structured, interlinked wiki pages in the /wiki folder, updates index.md and log.md, and moves the ingested raw files to /archive.
---

This skill governs the ingestion and processing of raw captures (notes, web clips, drafts) from the `/raw` directory into the structured, Obsidian-compatible `/wiki` directory.

## Step-by-Step Ingest Pipeline

Follow these steps precisely for each file in `/raw`:

### Step 1: File Discovery
- Recursively scan `/raw` (including `/raw/daily` and `/raw/others`) to list all raw files.
- Process files sequentially, one at a time, to avoid merge conflicts and index corruption.

### Step 2: Read & Match
- Read the content of the raw file.
- **Topic Extraction**: Be aware that raw files, and daily notes in particular, often contain multiple unrelated topics. Identify and extract each distinct concept, entity, or topic.
- **Topic Routing**: It is critical that you separate these different topics and route/merge each topic to its correct, corresponding wiki page (adhering to the "one topic per file" rule). Do not bundle unrelated topics onto a single page.
- Search `/wiki/index.md` or scan `/wiki` to see if pages for each of these topics already exist.

### Step 3: Read-Then-Merge
- **Hard Rule**: Never overwrite a `/wiki` entry blindly.
- If a wiki page already exists for a topic:
  1. Read the existing page's contents.
  2. Merge the new information cleanly, resolving any contradictions or redundancies.
  3. If you find conflicting facts and are uncertain, document the uncertainty directly in the content (e.g., noting "Source A claims X, but Source B claims Y").
- If the page does not exist, prepare to create it as a new file.

### Step 4: Wiki Page Formatting & Conventions
Ensure every page meets the following standards:
1. **YAML Frontmatter**: Every file must start with a YAML frontmatter block containing:
   ```yaml
   ---
   title: "Page Title"
   date: YYYY-MM-DD
   tags: [tag1, tag2]
   source: "relative/path/to/original/raw/file"
   ---
   ```
2. **File Naming**: Name files in `kebab-case.md` matching the topic (e.g., `neural-networks.md`).
3. **Tone & Style**: Use a clear, factual, and terse tone. Preserve the user's specific phrasing if it carries personal signal or context.
4. **Structural Rules**:
   - Use headings only if the document is long enough to require sub-sections.
   - Use bullets only when presenting a genuine list.
5. **Task Filtering**:
   - Checkboxes/tasks starting with `- [ ]` or `- [/-]` must NOT be copied into the wiki. Extract the underlying knowledge/links and write them as standard markdown text, but discard the task format.
   - **Do not translate, edit, or modify Obsidian tasks query blocks** (e.g., ````tasks ... ```` code blocks). Keep them completely unchanged.

### Step 5: Index and Log Updates
- **Update `/wiki/index.md`**: Add or update the page entry under its corresponding category (e.g., Entities, Concepts, Sources). The entry must follow this format:
  ```markdown
  - [Page Title](file:///home/sina/Code/second-brain/wiki/kebab-case-name.md) — A one-line summary of the topic. | Date: YYYY-MM-DD | Sources: N
  ```
- **Append to `/wiki/log.md`**: Append a new log entry at the bottom of the file following this exact format:
  ```markdown
  ## [YYYY-MM-DD] ingest | <Title/Topic Name>
  ```
  *(Note: Replace `YYYY-MM-DD` with the current system date).*

### Step 6: Archiving
- Replicate the parent directory structure of the raw file under `/archive` (e.g., if processing `raw/daily/note.md`, ensure `archive/daily` exists).
- Move the processed raw file to `/archive` using terminal commands to ensure safety.
- **Hard Rule**: Never delete files from `/raw` or `/archive`. Move files only.

*Example execution command:*
```bash
mkdir -p "archive/daily" && mv "raw/daily/my-note.md" "archive/daily/my-note.md"
```
