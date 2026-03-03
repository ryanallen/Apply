# Apply

An autonomous agent and modular skill set designed to automate job applications.

## How to use

1. Get this repo: use the template button above to create your copy (or clone/download).
2. Open the folder as a project in your editor (Cursor, Claude Code, Codex, etc.).
3. Ask the assistant to help you apply to a job. It will ask for company and job name, then for the job post (URL, paste, or file), and run the workflow.

---

## 🤖 Agents and their skills

Call a skill by saying its trigger phrase or typing /skill-name. In Claude Code and Cursor, /skills lists all. Skills live under `.claude/skills/` in a kebab-case folder with a file named `skill.md`.

### 🧭 Coordinator
Orchestrates researcher, documentor, and strategist for the Apply to a job flow: learn job post, document, research work/, document (merge work research), strategist resume alignment, document (final resume at top of README). See [coordinator](.claude/agents/coordinator.md).

### 📝 Documentor
- **document-findings**: Take research output and produce structured markdown with mermaid diagrams; places final resume at top of README when present, then ---, then TOC and sections with emoji headers. "write up", "document", /document-findings.
- **update-ticket**: Post a comment on a Jira ticket with link to project deliverables. "update ticket", "Jira", /update-ticket.

### 🔍 Researcher
- **learn**: Gather from a job post (URL, paste, or file) and follow links up to 5 levels deep; Documentor creates job-post.md and structures the README. "learn about this", "look at this", /learn.
- **research-work**: Research all existing work/ (READMEs, refs) and write work-research.md for Documentor to merge into the current job's README. "research work", "existing work", /research-work.

### 🎯 Strategist
- **resume-alignment**: Align resume to job post (keywords, reverse chronology, action verbs, quantifiable results); writes resume-alignment.md for Documentor. "resume alignment", "align resume", /resume-alignment.

### 🔄 Syncer
- **commit-all**: Stage all and create a commit with derived message. "commit", "commit all", /commit-all. Does not push.
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
│       ├── commit-all/skill.md
│       ├── sync-upstream/skill.md
│       └── update-ticket/skill.md
├── work/
│   ├── config.md
│   └── {company}/{job}/
│       ├── README.md
│       └── job-post.md
├── package.json
└── README.md
```
