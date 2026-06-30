---
name: answer-question
description: Answers questions based on all files in the vault (wiki, raw, archive). If the user agrees, can save the interaction to raw folder for future translation.
---

This skill governs querying the knowledge base (the wiki, archive, and raw directories) to answer questions about the user's past thoughts, research, or content. It also allows saving the synthesized answers back into the knowledge base to facilitate compounding knowledge.

## Query Workflow

Follow these steps when asked a question:

### 1. Document Discovery
- Read the content-oriented index at `/wiki/index.md` first to identify candidate pages related to the user's query.
- Note any relevant categories, entity files, concept files, or source summaries.

### 2. Search & Retrieval
- Read the content of the candidate files from `/wiki`.
- If needed for deeper context or source checking, read relevant historical raw files from `/archive` or current files in `/raw`.

### 3. Synthesis & Answer Formulation
- Synthesize an answer that is clear, factual, and backed by citations (links to the source wiki/archive pages).
- Highlight connections or comparisons found between different pages.

### 4. Compound Knowledge Proposing
- Output the generated answer to the user.
- **Save Prompt**: Propose saving this Q&A synthesis back into the vault by asking:
  > Would you like to save this Q&A interaction to your raw folder for future translation?
- If the user agrees:
  - Formulate a descriptive, kebab-case filename (e.g., `/raw/others/qa-<topic-name>.md`).
  - Write the conversation's question and answer into that file.
  - Let the user know the file has been created and will be processed during the next translate run.

### 5. Log the Query
- Append an entry to `/wiki/log.md` with the query activity. Use the current date:
  ```markdown
  ## [YYYY-MM-DD] query | <Short summary of the question asked>
  ```
