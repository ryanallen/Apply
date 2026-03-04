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
3. **Resume source** – Existing resume content from work/ (READMEs in other company/job folders, work/ref/work-history/README.md, or Existing work section in current README). For format matching, also read work/README.md **Career summary (narrative)** and any **Resume/cover format** note in Existing work when present.

If the project path or job post content in README is missing, ask the user before proceeding.

## Alignment rules

Apply these when writing the aligned resume and cover letter:

1. **Keywords:** Identify recurring nouns and skills in the job description. Insert them into your "Skills" and "Experience" sections and into the cover letter where accurate.
2. **Reverse chronology:** List your most relevant experience first (by relevance to this role, then by date if needed).
3. **Action verbs:** Start bullet points with words like "managed," "developed," "optimized," "led," "shipped," "designed," "increased," "reduced."
4. **Quantifiable results:** Use data to show impact. Example: "Increased sales by 20%" instead of "Improved sales."
5. **Experience cutoff:** Use the job's years of experience (from README section "Years of experience required" or job post). Include only roles within that window (e.g. if 12+ years, show roughly the last 12 to 15 years). Omit or aggregate older experience so the resume does not show far more years than the job asks for.
6. **Cover letter:** Align to the job (role, company, key requirements). Weave in any user-provided additional info (e.g. people at the company, prior collaboration). One page; clear opening, body, and close. Use the **cover letter output format** (structure below).

## Process

### 1. Read job post and resume source
Read the README: **⏱ Years of experience required** section (or Role summary / Job post) for the job's experience years. Read Job post (full copy) section or Role summary and Requirements for job context. Read Existing work, and any work/ READMEs or work-research content, for experience bullets, skills, and roles.

### 1b. Infer candidate format (match my formats)
Read **Existing work** in the current README and, if available, work/README.md **Career summary (narrative)** and any **Resume/cover format** subsection in Existing work. Note the candidate's usual: resume sections and order (e.g. Skills, then Experience in reverse chronology), bullet style (e.g. action verb + metric), cover letter length and structure (e.g. one page, opening/body/close). Note which roles and metrics in the narrative are most relevant to the current job post (e.g. fintech vs EdTech) so you can prioritize them when building. When building the aligned resume and cover letter (steps 4–5), preserve this structure so the output matches the candidate's other applications.

### 2. Ask for additional info (before building)
**Ask the user:** Do you have any more info to add? (e.g. people you know at the company, someone you worked with who now works there, other relevant experience.) Wait for their response. If they provide anything, use it when building the resume and cover letter.

### 3. Extract job keywords and themes
From the job post, list recurring nouns, skills, and requirements. Note role level and domain. **Note the experience cutoff year:** from "Years of experience required" compute the earliest start year to include (e.g. 12 years back from today).

### 4. Build aligned resume
Apply the five resume rules: weave in keywords, reorder experience (most relevant first), rewrite bullets with action verbs, add or keep quantifiable results, and cut off experience at the appropriate year. **Match the candidate's format** from step 1b (sections, order, bullet style). Output the resume in the **standard copy-paste format** (step 6): H1 name and title, H2 contact, # SKILLS as a plain list (one skill phrase per line; no backticks), # EXPERIENCE with ## **Company** *— Role*, date line, bullets as plain text (no backticks), # AWARDS as plain text. Produce a single resume document ready for Documentor to place and user to copy-paste into Google Docs.

### 5. Build aligned cover letter
One-page cover letter aligned to the job: role and company, why the candidate is a fit, 1–2 concrete ties to the job. **Match the candidate's usual cover structure** from step 1b (length, opening/body/close). Use the **cover letter output format** below. Incorporate any additional info the user provided (e.g. people at the company, prior collaboration). Clear opening, body, and sign-off.

### 6. Write resume-alignment.md and cover-letter.md
Write resume to `work/{company}/{job}/resume-alignment.md`, cover letter to `work/{company}/{job}/cover-letter.md`. **Resume output must use the standard copy-paste format** (see below) so the Documentor can place it unchanged and the user can copy-paste the resume block into Google Docs for PDF. Documentor merges: cover letter at top, ---, resume, ---, rest. Do not add --- or modify README.

#### Resume output format (copy-paste to Google Docs)
Use this structure. **Do not use backticks or code formatting** in the resume body; use plain text and markdown headings/emphasis only.

- Line 1: `# {Full Name} – {Title}` (H1)
- Line 2: `## [**{Portfolio URL}**](url) – [email](mailto:email) – phone` (H2)
- `# SKILLS` (H1, all caps); then one skill phrase per line as a **plain list** (no backticks). Maximum 8 skills; each phrase max 40 characters.
- `# EXPERIENCE` (H1, all caps); one intro sentence (plain text); then per role: `## **Company** *— Role Title*` (H2), date line (plain, e.g. 2018 – Current), bullets as `- ` plain text (no backticks)
- `# AWARDS` (H1, all caps); one line plain text (no backticks)

No emoji in the resume. Use this format so the user can copy-paste the resume from the README into Google Docs unchanged.

#### Cover letter output format
Structure the cover letter as follows. Use the candidate's real name, portfolio, email, and phone from resume source or Existing work; do not invent contact info.

1. **Header (top):** Full name (bold). On the next line: portfolio URL (link), then contact on one line: email and phone separated by a vertical bar or comma (e.g. `email | phone`).
2. **Date:** Current date when generating (e.g. March 3, 2026). On its own line.
3. **Recipient:** One line, bold. Use a relevant salutation such as "Hiring Team", "Hiring Manager", "Recruiting Team", or "Dear Hiring Manager" depending on what the job post or application instructions suggest. No invented names.
4. **Message body:** Two to four short paragraphs (opening with role/company, experience and fit, why this role, close).
5. **Closing line:** One word or short phrase, e.g. "Sincerely," or "Best," or "Best regards,". Professionally appropriate to the type of role and industry.
6. **Signature:** Applicant's full name (bold) on the line after the closing.

Output cover-letter.md in plain text or markdown so the header, date, recipient, body, closing, and signature are clearly separated and copy-paste friendly. Preserve any **bold** for name and recipient if using markdown.
