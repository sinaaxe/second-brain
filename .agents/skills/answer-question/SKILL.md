---
name: answer-question
description: Answers questions based on all files in the vault (wiki, raw, archive). If the user agrees, can save the interaction to raw folder for future translation.
---

This skill governs querying the knowledge base (the wiki, archive, and raw directories) to answer questions about the user's past thoughts, research, or content. It also allows saving the synthesized answers back into the knowledge base to facilitate compounding knowledge.

## Step-by-Step Query Pipeline

Follow these steps when asked a question:

### Step 1: Document Discovery
- Read the content-oriented index at `/wiki/index.md` first to identify candidate pages related to the user's query.
- Note any relevant categories, entity files, concept files, or source summaries.

### Step 2: Search & Retrieval
- Read the content of the candidate files from `/wiki`.
- If needed for deeper historical context or source checking, read relevant raw files from `/archive` or current files in `/raw`.

### Step 3: Synthesis & Answer Formulation
- Synthesize an answer that is clear, factual, and backed by citations.
- **Citation Format**: Reference sources using standard markdown links pointing directly to the file URI:
  `[Page Title](wiki/<dynamic-category>/<kebab-case-name>.md)` or `[Raw File Name](archive/path/to/file.md)`.
- Highlight connections, comparisons, or discrepancies found between different pages.

### Step 4: Compound Knowledge Proposing
- Present the final synthesized answer to the user.
- Propose saving this Q&A session to the raw folder for future compilation by asking the user:
  > Would you like to save this Q&A interaction to your raw folder for future translation?
- If the user agrees:
  1. Formulate a descriptive, unique kebab-case filename (e.g., `qa-<topic-name>.md`).
  2. Verify if a file with that name already exists in `/raw/others/` to avoid collisions. If it does, append an index suffix (e.g., `qa-<topic-name>-1.md`).
  3. Write the interaction to `/raw/others/qa-<topic-name>.md` using the following template:
     ```markdown
     ---
     type: qa-synthesis
     date: YYYY-MM-DD
     question: "Original user question"
     sources: ["wiki/<dynamic-category>/source-1.md"]
     ---

     # QA: Original User Question

     ## User Question
     <Question text>

     ## Synthesized Answer
     <Answer text with citations>
     ```
  4. Notify the user of the saved file location.

### Step 5: Logging the Query
- Append a query log entry at the bottom of `/wiki/log.md` using the following exact format:
  ```markdown
  [YYYY-MM-DD] query | <Short summary of the question asked>
  ```
  *(Note: Replace `YYYY-MM-DD` with the current system date).*
