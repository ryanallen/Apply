---
name: learn
description: Gather from a job post (URL, paste, or file) and follow links up to 5 levels deep. Use when user says "learn about this", "look at this", or /learn. In Claude Code and Cursor, /skills lists all.
---

# Learn

Accepts a job post as input (URL, pasted text, or file), derives starting URLs and level-0 content, then navigates recursively up to 5 levels deep. Writes findings to the project README for the Documentor (who creates job-post.md and structures the README).

## Rules

- Track all visited URLs to avoid loops
- Prefer depth-first within the focus area, breadth-first otherwise
- Extract all info, role requirements, responsibilities, application instructions, and company/benefits info
- For pages that require authentication or permissions, use Playwright in Chrome; if still inaccessible, ask the user to log in and wait for confirmation before retrying
- Summarize content when appropriate; if data is important copy it verbatim
- **Clickable links:** Every URL in the output (Sources table, Link Tree, Findings source lines) must be written as a markdown link `[title](url)`. Never output a bare URL or title-only line; always use `[title](url)` so links are clickable in the README.md.

## Inputs

1. **Input** (one or more of):
   - **Job post URL(s)** – Use as starting URLs. Primary content is the job listing.
   - **Pasted job text** – Extract URLs (company site, application link, benefits, etc.) and use as starting URLs; full text is level-0 content.
   - **File path(s)** – Read file(s), extract URLs and use as starting URLs; file content is level-0 content.
   - **Image path(s)** – Describe or extract text/URLs from image (e.g. screenshot of job post); use any URLs as starting URLs; description or extracted text is level-0 content.

**If no job post input is provided** (no URL, file, paste, or image), ask the user for one before proceeding. Do not start the process until you have at least one of these inputs.

2. **Output path** – `work/{company}/{job}/README.md` from `work/config.md`. Single README per job (see config). Documentor creates job-post.md from this output.
3. **Focus area** – Optional keywords or topics to prioritize when deciding which links to follow (e.g. benefits, team, culture, application process).

Use `work/config.md` for output path.

If no job post yet, ask for it (link, paste, or file).

## Process

### 1. Normalize Input

From the given input, produce:
- **Starting URL(s)** – Zero or more URLs to crawl. If none (only pasted text with no links), write level-0 content only to output and skip crawl.
- **Level-0 content** – Raw or summarized content from the input (job post body, pasted text, file content, image description). Include in the output for the Documentor.

### 2. Fetch Starting URLs

**Auth-gated or permission-restricted links:** Open them in Playwright using Chrome so the user's session can bypass permission walls. **If a page cannot be accessed (login wall, permission denied):** Ask the user to log in, open the URL in their browser, complete login, then tell you when done. Wait for confirmation before retrying. Do not skip without asking. Extract:
- Page title and main content
- All links (application link, company pages, benefits, team, related roles)
- Role title, level, location, requirements, responsibilities
- Application instructions and deadlines

### 3. Recursive Link Traversal

Follow links up to **5 levels deep** from each starting URL.

```
Level 0: Job post or starting URL
Level 1: Links found on starting page
Level 2: Links found on level 1 pages
Level 3: Links found on level 2 pages
Level 4: Links found on level 3 pages
```

At each level:
- Skip duplicate URLs already visited
- Track the link tree (parent -> child relationships)

### 4. Content Extraction

For each page visited, capture:
- **URL** and depth level
- **Title** and headings structure
- **Key content** (summarized, not raw HTML) – role requirements, responsibilities, benefits, company info, application steps
- **Application link** and any instructions
- **Outbound links** with context on what they reference

### 5. Output

Write to the project README (handoff to Documentor).

If level-0 content exists, include it first:

**## Level-0 (input)** – Content from job post URL, paste, file, or image:
```markdown
## Level-0 (input)

{Content or summary of user-provided job post}
```

**## Sources** – Link index with depth levels. Use markdown links so URLs are clickable (put `[Title](URL)` in the Title column):
```markdown
## Sources

| URL | Depth | Title | Parent |
|-----|-------|-------|--------|
| ... | 0     | ...   | (root) |
| ... | 1     | ...   | ...    |
```

**## Findings** – Extracted content organized by topic (e.g. requirements, responsibilities, benefits, application process):
```markdown
## Findings

### {Topic Heading}

{Summarized content}

> Source: [page title or URL](url) (depth {N})
```

**## Link Tree** – Visual map of traversal (every item must be a markdown link so it is clickable):
```markdown
## Link Tree

- [Starting Page](url)
  - [Child Page](url)
    - [Grandchild Page](url)
```
