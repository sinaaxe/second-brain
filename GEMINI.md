You are working in a personal second brain — a knowledge management system, not a code project. Your job is to keep the wiki current, useful, and well-organized based on the raw notes the user captures.

## Folder Directory System

- `/raw` — Raw notes, links, and PDFs captured by the user.
    - `/raw/daily` — Daily journal entries and daily captures.
    - `/raw/others` — Uncategorized random captures.
- `/wiki` — Cleaned, structured, and interlinked knowledge notes in Obsidian-compatible Markdown. All pages must start with YAML frontmatter.
    - `/wiki/<dynamic-category>/` — Pages are organized into dynamic category subdirectories based on their content (e.g., `/wiki/books/`, `/wiki/programming/`, `/wiki/personal/`, `/wiki/tools/`, etc.).
- `/archive` — Historical record of processed `/raw` files. The directory structure must exactly mirror `/raw` (e.g. `/raw/daily/note.md` -> `/archive/daily/note.md`).

## Core Files

- **/wiki/index.md** (Content Catalog):
  - A structured catalog of all pages in the wiki, categorized under high-level headings dynamically determined by topic content.
  - Under each heading, pages must be listed in a Markdown table with the columns: `| Page Link | One-Line Summary | Date | Sources |`.
  - **Hard Rule**: Do NOT include images, videos, or drawings in the summary column. It must contain only text.
  - Must be updated during every ingest operation.
  - Used as the first point of entry to discover relevant files for answering questions.
- **/wiki/log.md** (Chronological Log):
  - An append-only historical log of all operations performed.
  - Each entry must start with a consistent date prefix: `[YYYY-MM-DD] <operation> | <Title/Summary>` (e.g., `ingest`, `query`, or `lint`).

## Common Operational Tasks

- **Translate Raw**: Process files in `/raw`, extract/merge information into `/wiki`, update `/wiki/index.md` and `/wiki/log.md`, and move the raw files to `/archive`.
- **Answer Questions**: Query the knowledge base (`/wiki` and `/archive`/`/raw` if needed) to answer questions about the user's past thinking, and offer to save the Q&A back to `/raw/others/`.
- **Lint Wiki**: Audit `/wiki` for orphans, broken links, contradictions, missing cross-references, missing pages, and formatting consistency, then log the results.

## Hard Rules (Strict Enforcement)

1. **Move-Only Preservation**: Never delete anything from `/raw` or `/archive`. Files in `/raw` are only moved to `/archive` after ingestion. Files in `/archive` are permanent records and must never be modified or deleted.
2. **Read-Then-Merge**: Never overwrite a `/wiki` entry blindly. Always read the existing page first and merge new findings carefully.
3. **No Blind Guessing**: If you are uncertain of a fact or connection, explicitly document your uncertainty inside the wiki page or entry instead of guessing.
4. **Task Filtering & Preservation**:
   - Obsidian tasks starting with `- [ ]` or `- [/-]` must NOT be added to `/wiki` as active checklist items. If they contain valuable knowledge, extract and integrate that knowledge, but discard the raw task structure.
   - **Do not translate, edit, or modify Obsidian tasks query blocks** (e.g., ````tasks ... ```` code blocks). Leave task query blocks exactly as they are.

## Wiki Voice & Structure

- **Tone**: Default is clear, factual, and terse.
- **Signal Preservation**: Preserve the user's unique phrasing and vocabulary if it carries personal signal or context. Avoid over-homogenizing into a neutral encyclopedia tone.
- **Structural Density**:
  - Use headings only when the note is long enough to justify sections.
  - Use bullets only when presenting a genuine list.
- **File Conventions**: One topic per file. Files must use `kebab-case.md` names.

## Out of Scope

- Modifying or editing files directly within `/raw` or `/archive` (aside from moving processed files from `/raw` to `/archive`).
