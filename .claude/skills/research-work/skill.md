---
name: research-work
description: Research all existing work/ (READMEs, refs) and output findings for the Documentor to merge into the current job's README. Use after the job post is documented in Apply to a job flow. Trigger: "research work", "existing work", /research-work.
---

# Research Work

Read all content under `work/` (past applications, refs, work history) and write structured findings to `work/{company}/{job}/work-research.md`. The Documentor then merges this into the project README.

## Inputs

1. **Project path** – `work/{company}/{job}/` (the current job you are applying to). Output goes here.
2. **Work root** – `work/` (read from here). Use `work/config.md` paths table; also scan for all `work/{company}/{job}/` and `work/ref/work-history/` folders.

If project path is missing, ask the user before proceeding.

## Process

### 1. List work paths
Read `work/config.md`. Find every folder under `work/` that contains README.md: each `work/{company}/{job}/` and `work/ref/work-history/`. Skip the current project path (so you do not re-read the job you are documenting).

### 2. Read each README and optional job-post
For each path, read README.md (and job-post.md if present). Capture:
- **Past applications:** company, job/role, and a short summary or key points from each README (resume/cover letter content, role focus).
- **Work history:** from `work/ref/work-history/README.md`, key roles, dates, and highlights.
- **Relevant experience:** bullets or themes that may align with the current job (skills, domains, metrics).

### 3. Write work-research.md
Create `work/{company}/{job}/work-research.md` with structured markdown:

- **Existing applications** – Table or list: Company | Job | Key points (from each README).
- **Work history summary** – Condensed from ref/work-history (roles, timeline, highlights).
- **Relevant experience** – Themes or bullets from past READMEs that match the current job post (requirements, domain, level).

Use clear headings (H2). No placeholder or made-up rows. The Documentor will merge this into the README and remove work-research.md.

## Rules

- Only read from work/. Do not invent paths; use config and actual folder structure.
- Skip the current project folder when listing (avoid circular content).
- Write only to work-research.md in the project path. Do not modify other READMEs.
