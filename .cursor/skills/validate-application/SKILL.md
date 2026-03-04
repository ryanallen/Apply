---
name: validate-application
description: After step 6 in Apply to a job, validate the README and resume against all rules. On failure, Strategist diagnoses fix and Documentor applies; repeat until pass. Trigger: "validate", "validation", /validate-application.
---

# Validate Application

Run after step 6. Check README against all applicable rules (learn, document-findings, resume-alignment). PASS or FAIL with validation-report.md; on FAIL, Strategist diagnoses fix and Documentor applies, then re-validate until PASS.

## Inputs

1. **Project path** – `work/{company}/{job}/` from `work/config.md`.
2. **README** – `work/{company}/{job}/README.md` (cover letter at very top, then ---, then resume, then ---, then TOC and sections).

## Output

- **PASS** – All checks below pass. Report "Validation passed."
- **FAIL** – One or more checks failed. Write `work/{company}/{job}/validation-report.md` with failed check numbers and short description. Do not modify README. Coordinator runs Strategist → Documentor → re-validate.

## Checks (every rule)

Run these in order. If a check fails, add it to the failure list and continue.

### Years of experience and resume cutoff

1. **Years documented:** README has a section **⏱ Years of experience required** (or equivalent) with one clear line stating the job's experience requirement (e.g. "Total: 12+ years. Leadership: 5+ years." or "Not specified."). If missing or empty, fail.
2. **Resume experience cutoff:** The resume (the block between the first `---` and the second `---`, or before the first `---` if no cover letter) does not show significantly more years of experience than the job asks for. Compute the earliest start year that should appear (e.g. if job asks 12+ years, roles should start no earlier than ~12–15 years ago). If the resume lists roles starting more than that window back, fail.

### Document-findings rules

3. **No absolute paths:** No link in the README uses an absolute filesystem path; all links are relative or external URLs.
4. **No invented data:** No placeholder, TBD, example names/dates, or made-up content in any section (Deliverables, tables, etc.). Only real data from source material.
5. **Sources preserved:** README has a **🔗 Sources** section with a table; each URL is a markdown link `[title](url)`.
6. **Link tree preserved:** README has a **🌐 Link tree** section; each item is a markdown link `[title](url)`.
7. **TOC complete:** After the second `---` (the one that follows the resume), the table of contents links to every H2 and H3 in the document. No section is missing from the TOC.
8. **Emoji in headings:** Every H2 and H3 below the second `---` has an emoji in the heading text.
9. **Job post in README:** README has **📄 Job post (full copy)** section with the full job listing content.
10. **Structure:** README starts with cover letter (if present), then first `---`, then resume, then second `---`, then H1 title and TOC and sections.

### Resume-alignment rules (resume and cover letter at top)

11. **Keywords:** Resume Skills and Experience reflect recurring nouns/skills from the job post where accurate. Cover letter (if present) references role and company and key fit.
12. **Reverse chronology:** Experience is listed most recent first (by date).
13. **Action verbs:** Resume bullets start with action verbs (e.g. led, designed, shipped, increased).
14. **Quantifiable results:** At least some resume bullets include numbers or measurable impact where the source material supports it.
15. **Experience cutoff:** Resume includes only roles within the job's years-of-experience window (see check 2).

### Learn rules (as reflected in README)

16. **Clickable links:** Every URL in Sources and Link tree is written as `[title](url)`. No bare URLs or title-only lines in those sections.

## On failure

Write validation-report.md (failed check numbers and what is wrong). Report FAIL. Coordinator runs Strategist → Documentor → re-validate until PASS (see Output and Process).

## Process

1. Read config for project path; read README.
2. Run each check; collect failures.
3. No failures → report PASS. Any failures → write validation-report.md, report FAIL.
