You are working in a personal second brain — a knowledge management system, not a code project. Your job is to keep the wiki current, useful, and well-organized based on the raw notes the user captures.

## Folders

- `/raw` — anything I capture: notes, PDFs, links
    - `/raw/daily` this is where I store my daily notes.
    - `/raw/others` any other random notes will be stores here.
- `/wiki` — clean notes written by you all in Obsidian-compatible markdown. All pages should start with YAML frontmatter. 
- `/archive` — processed `/raw` files land here so I can see what's been handled. Keep the folder structured the same as the `/raw` folder.

## Files

**/wiki/index.md** is content-oriented. It's a catalog of everything in the wiki — each page listed with a one-line summary, and metadata like date or source count. Organized by category (entities, concepts, sources, etc.). You update it on every ingest. When answering a query, the LLM reads the index first to find relevant pages, then drills into them.

**/wiki/log.md** is chronological. It's an append-only record of what happened and when — ingests, queries, lint passes. Each entry starts with a consistent prefix, for example `## [2026-04-02] ingest | Article Title`.

## Common Tasks

- **Translate raw** → run the prompt in translate skill against `/raw`.
- **Answer questions** → read `/wiki` and `/archive` to answer ad-hoc questions about my own past thinking.
- **Lint wiki** → periodically health-check the wiki. Look for: contradictions between pages, stale claims that newer sources have superseded, orphan pages with no inbound links, important concepts mentioned but lacking their own page, missing cross-references, data gaps that could be filled with a web search. The LLM is good at suggesting new questions to investigate and new sources to look for.

## Hard Rules

1. **Never delete** anything from `/raw` or `/archive`. Move only, never delete.
2. **Never overwrite** a `/wiki` entry blindly. Always read it first, then merge.
3. **Never modify** `/archive` after a file lands there — it is a permanent record.
4. **When uncertain, log it in the entry** rather than guessing.
5. **Add Tasks To Wiki** Obsidian tasks that start with `- [ ]` or `- [/-]` should not be added to the wiki as tasks. If they have links or knowledge that can be used for wiki, add them to the wiki.

## Wiki Voice and Structure

- Default tone: clear, factual, terse.
- Preserve my own phrasing when it carries signal — don't sand everything into neutral encyclopedia tone.
- Headings only when the entry is long enough to need them.
- Bullets only when the content is genuinely a list.
- One topic per file. Kebab-case filenames.

## Out of Scope

- Editing files in `/raw` or `/archive`.

