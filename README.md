# Apply

An autonomous agent and modular skill set designed to automate job applications.

## How to use

1. Get this repo: [Use this template](https://github.com/ryanallen/Apply/generate) to create your copy (or clone/download).
2. Open the folder as a project in your editor (Cursor, Claude Code, Codex, etc.).
3. Ask the assistant to help you apply to a job. Share the job link, paste the listing, or upload a file or screenshot. The assistant infers the company and role from that and runs the workflow.

You can give the system different resumes or past application examples (paste, files, or links). They are cataloged in `work/` and used to align the next application. If `work/` is empty, the assistant asks for input or plans with you.

---

## 🤖 Agents and their skills

Call a skill by saying its trigger phrase or typing /skill-name. In Claude Code and Cursor, /skills lists all. Skills live under `.claude/skills/` in a kebab-case folder with a file named `skill.md`.

### 🧭 Coordinator
Orchestrates researcher, documentor, strategist, and validator for the Apply to a job flow: learn job post (including years of experience), document, research work/, document (merge), ask user for any more info then strategist resume and cover letter alignment, document (cover letter at top, ---, resume, ---, rest), then validate; if validation fails, strategist diagnoses fix and documentor updates until pass. See [coordinator](.claude/agents/coordinator.md).

### 📝 Documentor
- **document-findings**: Take research output and produce structured markdown with mermaid diagrams; places cover letter at very top when present, then ---, then resume, then ---, then TOC and sections with emoji headers. "write up", "document", /document-findings.
- **update-ticket**: Post a comment on a Jira ticket with link to project deliverables. "update ticket", "Jira", /update-ticket.

### 🔍 Researcher
- **learn**: Gather from a job post (URL, paste, or file) and follow links up to 5 levels deep; explicitly extract years of experience required; Documentor structures README (full job post in README). "learn about this", "look at this", /learn.
- **research-work**: Research all existing work/ (READMEs, refs) and write work-research.md for Documentor to merge into the current job's README. "research work", "existing work", /research-work.

### 🎯 Strategist
- **resume-alignment**: Align resume and cover letter to job post (keywords, reverse chronology, action verbs, quantifiable results, experience cutoff); before building, ask user for any more info (e.g. people at company). Writes resume-alignment.md and cover-letter.md for Documentor. "resume alignment", "align resume", /resume-alignment.

### ✅ Validator
- **validate-application**: After step 6, validate README and resume against all rules (years documented, experience cutoff, document-findings and resume-alignment rules). On FAIL, Strategist diagnoses fix and Documentor applies; repeat until PASS. "validate", "validation", /validate-application.

### 🔄 Syncer
- **save**: Stage all and create a commit with derived message. "save", "commit", /save. Does not push.
- **sync-upstream**: Sync from upstream main, push to origin. "sync", "pull", /sync-upstream.

<details>
<summary>📌 Using a working repo with this as upstream</summary>

For a working repo that pulls from this repo (ryanallen/Apply) as upstream.

**Add upstream.** In the working repo:

```bash
git remote add upstream https://github.com/ryanallen/Apply.git
git fetch upstream
```

Pull with `git pull upstream main` (or say "sync", "pull", or /sync-upstream).

**Keep local config from being overwritten.** If you change `work/config.md` in the working repo and don't want pull to overwrite it:

```bash
git update-index --skip-worktree work/config.md
```

To allow upstream to update it again: `git update-index --no-skip-worktree work/config.md`.

</details>

---

## 📁 Repo Structure

```
Apply/
├── agents.md
├── claude.md -> agents.md
├── .claude/
│   ├── settings.json
│   ├── agents/
│   │   ├── coordinator.md
│   │   ├── documentor.md
│   │   ├── researcher.md
│   │   ├── strategist.md
│   │   └── syncer.md
│   └── skills/
│       ├── learn/skill.md
│       ├── research-work/skill.md
│       ├── document-findings/skill.md
│       ├── resume-alignment/skill.md
│       ├── validate-application/skill.md
│       ├── save/skill.md
│       ├── sync-upstream/skill.md
│       └── update-ticket/skill.md
├── work/
│   ├── config.md
│   └── {company}/{job}/
│       └── README.md
├── package.json
└── README.md
```
