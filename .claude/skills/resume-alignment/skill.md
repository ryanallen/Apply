---
name: resume-alignment
description: Align resume and cover letter to the job post (keywords, reverse chronology, action verbs, quantifiable results, experience cutoff). Before building, ask user for any more info (e.g. people at company). Output: resume-alignment.md and cover-letter.md for Documentor. Trigger: "resume alignment", "align resume", /resume-alignment.
---

# Resume Alignment

Read job post and existing work from README; ask user for any more info; apply alignment rules; write resume-alignment.md and cover-letter.md. Documentor places cover letter at top, then ---, then resume, then ---, then rest.

## Rules

- Only write to resume-alignment.md and cover-letter.md. Do not modify README.md.
- Use only real experience and skills from source material; do not invent roles or metrics.
- Keep the resume concise (one to two pages when rendered). Keep the cover letter to one page when rendered.

## Inputs

1. **Project path** – `work/{company}/{job}/`. Use `work/config.md`. Has README.md (including Job post section and possibly merged Existing work).
2. **Job post** – Full job post lives in the README in the **📄 Job post (full copy)** section (or Level-0 / job post content in learn output).
3. **Resume source** – Existing resume content from work/ (READMEs in other company/job folders, work/ref/work-history/README.md, or Existing work section in current README).

If the project path or job post content in README is missing, ask the user before proceeding.

## Alignment rules

Apply these when writing the aligned resume and cover letter:

1. **Keywords:** Identify recurring nouns and skills in the job description. Insert them into your "Skills" and "Experience" sections and into the cover letter where accurate.
2. **Reverse chronology:** List your most relevant experience first (by relevance to this role, then by date if needed).
3. **Action verbs:** Start bullet points with words like "managed," "developed," "optimized," "led," "shipped," "designed," "increased," "reduced."
4. **Quantifiable results:** Use data to show impact. Example: "Increased sales by 20%" instead of "Improved sales."
5. **Experience cutoff:** Use the job's years of experience (from README section "Years of experience required" or job post). Include only roles within that window (e.g. if 12+ years, show roughly the last 12 to 15 years). Omit or aggregate older experience so the resume does not show far more years than the job asks for.
6. **Cover letter:** Align to the job (role, company, key requirements). Weave in any user-provided additional info (e.g. people at the company, prior collaboration). One page; clear opening, body, and close.

## Process

### 1. Read job post and resume source
Read the README: **⏱ Years of experience required** section (or Role summary / Job post) for the job's experience years. Read Job post (full copy) section or Role summary and Requirements for job context. Read Existing work, and any work/ READMEs or work-research content, for experience bullets, skills, and roles.

### 2. Ask for additional info (before building)
**Ask the user:** Do you have any more info to add? (e.g. people you know at the company, someone you worked with who now works there, other relevant experience.) Wait for their response. If they provide anything, use it when building the resume and cover letter.

### 3. Extract job keywords and themes
From the job post, list recurring nouns, skills, and requirements. Note role level and domain. **Note the experience cutoff year:** from "Years of experience required" compute the earliest start year to include (e.g. 12 years back from today).

### 4. Build aligned resume
Apply the five resume rules: weave in keywords, reorder experience (most relevant first), rewrite bullets with action verbs, add or keep quantifiable results, and cut off experience at the appropriate year. Produce a single resume document (Skills, Experience in reverse-chronological order within the cutoff window, optional Education/Awards).

### 5. Build aligned cover letter
One-page cover letter aligned to the job: role and company, why the candidate is a fit, 1–2 concrete ties to the job. Incorporate any additional info the user provided (e.g. people at the company, prior collaboration). Clear opening, body, and sign-off.

### 6. Write resume-alignment.md and cover-letter.md
Write resume to `work/{company}/{job}/resume-alignment.md`, cover letter to `work/{company}/{job}/cover-letter.md`. Documentor merges: cover letter at top, ---, resume, ---, rest. Do not add --- or modify README.
