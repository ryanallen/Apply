---
name: research-work
description: Research all existing work/ (READMEs, refs) and output findings for the Documentor to merge into the current job's README. Use after the job post is documented in Apply to a job flow. Trigger: "research work", "existing work", /research-work.
---

# Research Work

Read all content under `work/` (past applications, refs, work history) and write structured findings to `work/{company}/{job}/work-research.md`. The Documentor then merges this into the project README.

## Rules

- Only read from work/. Do not invent paths; use config and actual folder structure.
- Skip the current project folder when listing (avoid circular content).
- Write only to work-research.md in the project path. Do not modify other READMEs.

## Inputs

1. **Project path** – `work/{company}/{job}/` from `work/config.md`. Output goes here. If a folder for that company/job already exists and the user might mean a different role, offer the choice: update that one or create a new job folder (do not ask them to type). If they choose new, add the new company/job to config and use it.
2. **Work root** – `work/`. **Enumerate every folder and file under work/** (directory listing or equivalent). Scan all `work/{company}/{job}/` and `work/ref/work-history/` folders that contain README.md. Do not rely on a single path; use the full enumerated list.

**If there is no work to research** (no READMEs under work/ other than the current project, or work/ is effectively empty): ask the user to provide files, links, or pasted data about their work history or past applications. Alternatively, offer plan mode. Do not write an empty work-research.md; wait for input or plan mode.

## Process

### 1. Enumerate work paths
**List every folder and file under `work/`** (e.g. via directory listing or glob). Do not rely on a single path or config alone. From that list:
- Identify every `work/{company}/{job}/` and `work/ref/work-history/` folder that contains README.md.
- Note any other files in each folder (e.g. cover-letter.md, resume-alignment.md, work-research.md).
- Skip the current project path (so you do not re-read the job you are documenting). **If no work paths remain** (nothing to research), ask for files/links/paste or offer plan mode as above; do not proceed to write work-research.md.

### 2. Read each README and optional job-post
For **each** path from step 1, read README.md. Capture:
- **Past applications:** company, job/role, and a short summary or key points from each README (resume/cover letter content, role focus).
- **Work history:** from `work/ref/work-history/README.md`, key roles, dates, and highlights.
- **Relevant experience:** bullets or themes that may align with the current job (skills, domains, metrics).

### 3. Write work-research.md
Create `work/{company}/{job}/work-research.md` with structured markdown:

- **Existing applications** – Table or list: Company | Job | Key points (from each README).
- **Work history summary** – Condensed from ref/work-history (roles, timeline, highlights).
- **Relevant experience** – Themes or bullets from past READMEs that match the current job post (requirements, domain, level).

Use clear headings (H2). No placeholder or made-up rows. The Documentor will merge this into the README and remove work-research.md.

### 4. Optional additional info
At the end, offer the user the option to provide any additional info relevant to the application. If they provide it, add it to work-research.md (e.g. a section "Additional info (user-provided)") so the Documentor merge will include it in the README.
