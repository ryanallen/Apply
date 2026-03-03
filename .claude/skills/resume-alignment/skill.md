---
name: resume-alignment
description: Align resume content with the job post using keywords, reverse chronology, action verbs, and quantifiable results. Output goes to resume-alignment.md for Documentor to place at top of README. Use in Apply to a job flow after work research. Trigger: "resume alignment", "align resume", /resume-alignment.
---

# Resume Alignment

Read the job post and existing work (README, work-research, refs), apply alignment rules, and write the new aligned resume to `work/{company}/{job}/resume-alignment.md`. The Documentor will place this at the top of the README and remove the file.

## Rules

- Only write to resume-alignment.md. Do not modify README.md or job-post.md.
- Use only real experience and skills from source material; do not invent roles or metrics.
- Keep the resume concise (one to two pages when rendered).

## Inputs

1. **Project path** – `work/{company}/{job}/`. Use `work/config.md`. Has README.md, job-post.md, and possibly work-research.md or merged Existing work in README.
2. **Job post** – `work/{company}/{job}/job-post.md`.
3. **Resume source** – Existing resume content from work/ (READMEs in other company/job folders, work/ref/work-history/README.md, or Existing work section in current README).

If the project path or job post is missing, ask the user before proceeding.

## Alignment rules

Apply these when writing the aligned resume:

1. **Keywords:** Identify recurring nouns and skills in the job description. Insert them into your "Skills" and "Experience" sections where accurate.
2. **Reverse chronology:** List your most relevant experience first (by relevance to this role, then by date if needed).
3. **Action verbs:** Start bullet points with words like "managed," "developed," "optimized," "led," "shipped," "designed," "increased," "reduced."
4. **Quantifiable results:** Use data to show impact. Example: "Increased sales by 20%" instead of "Improved sales."

## Process

### 1. Read job post and resume source
Read job-post.md. Read the current README (Existing work, Role summary, Requirements) and any work/ READMEs or work-research content to get experience bullets, skills, and roles.

### 2. Extract job keywords and themes
From the job post, list recurring nouns, skills, and requirements. Note role level and domain.

### 3. Build aligned resume
Apply the four rules: weave in keywords, reorder experience (most relevant first), rewrite bullets with action verbs, add or keep quantifiable results. Produce a single resume document (Skills, Experience in reverse-chronological order, optional Education/Awards).

### 4. Write resume-alignment.md
Write the aligned resume to `work/{company}/{job}/resume-alignment.md`. Use clear markdown (headings, bullets). The Documentor will place this at the top of the README, add ---, then the rest of the doc. Do not add the --- yourself; do not modify the README.
