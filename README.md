# Studio

Agent workflows for design capture, research, and strategic analysis.

---

## ⚙️ Setup

Say "setup", "install", or type `/setup`. The [setup skill](.claude/skills/setup/SKILL.md) runs the standard steps (show hidden files, project config). After that, quit the terminal and relaunch, then run `/mcp` in the chat and complete OAuth for Figma and Atlassian.

Custom setup: `.claude/skills/setup/custom/SKILL.md`. The Installer runs the [Customizer](.claude/agents/Customizer.md) agent, which runs that file.

---

## 🤖 Agents and their skills

Call a skill by saying its trigger phrase or typing /skill-name. In Claude Code and Cursor, /skills lists all. Skills live under an assistant config folder (this repo uses `.claude/skills/`), where each skill must live in a kebab-case folder with a file named `SKILL.md` (e.g. `.claude/skills/commit-all/SKILL.md`).

### 🧭 Coordinator
Orchestrates Researcher, Documentor, and Strategist for the full pipeline: learn, document, analyze, audit, propose, update ticket. No skill of its own. See [Coordinator](.claude/agents/Coordinator.md).

### 🔧 Customizer
Runs `.claude/skills/setup/custom/SKILL.md` after the Installer (local overrides, install_scope). See [Customizer](.claude/agents/Customizer.md).

### 🎨 Designer
- **capture-webpage**: Capture a live webpage as a Figma design. "capture page", "to Figma", /capture-webpage. Give webpage URL and Figma file URL.
- **generate-figma**: Generate or update a Figma design by calling the Figma Console MCP with target file details. "generate Figma", "generate design", /generate-figma.

### 📝 Documentor
- **document-findings**: Take research output and produce structured markdown with mermaid diagrams. "write up", "document", /document-findings.
- **update-ticket**: Post a comment on a Jira ticket with link to project deliverables. "update ticket", "Jira", /update-ticket.

### 📦 Installer
- **setup**: Run the standard Studio setup steps (show hidden files, project config). "setup", "install", /setup. Then quit terminal, relaunch, run /mcp and complete OAuth for Figma and Atlassian.

### 🔍 Researcher
- **learn**: Gather from any input (ticket, URL(s), text, file(s), image(s)) and follow links up to 5 levels deep; Documentor then structures the output. "learn about this", "look at this", /learn.
- **analyze-figma**: Analyze a Figma link and produce a structured report. General link = full file; specific link (with node-id) = deep analysis from that node. "analyze Figma", "Figma audit", /analyze-figma. Give Figma design URL.

### 🎯 Strategist
- **analyze-root-cause**: Analyze findings with Five Whys, identify root causes and propose solutions. "why broken", "find cause", /analyze-root-cause.

### 🔄 Syncer
- **commit-all**: Stage all and create a commit with derived message. "commit", "commit all", /commit-all. Does not push.
- **sync-upstream**: Sync from upstream main, push to origin. "sync", "pull", /sync-upstream.

<details>
<summary>📌 Using a working repo with this as upstream</summary>

For a working repo that pulls from this repo (ryanallen/Studio) as upstream.

**Add upstream.** In the working repo:

```bash
git remote add upstream https://github.com/ryanallen/Studio.git
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
Studio/
├── AGENTS.md
├── CLAUDE.md -> AGENTS.md
├── .claude/
│   ├── settings.json
│   ├── agents/
│   │   ├── Coordinator.md
│   │   ├── Designer.md
│   │   ├── Documentor.md
│   │   ├── Researcher.md
│   │   ├── Strategist.md
│   │   ├── Syncer.md
│   │   ├── Installer.md
│   │   └── Customizer.md (runs .claude/skills/setup/custom/SKILL.md)
│   └── skills/
│       ├── learn/SKILL.md
│       ├── document-findings/SKILL.md
│       ├── analyze-root-cause/SKILL.md
│       ├── analyze-figma/SKILL.md
│       ├── setup/
│       │   ├── SKILL.md
│       │   └── custom/
│       │       └── SKILL.md
│       ├── commit-all/SKILL.md
│       ├── sync-upstream/SKILL.md
│       ├── update-ticket/SKILL.md
│       ├── generate-figma/SKILL.md
│       └── capture-webpage/
│           ├── SKILL.md
│           └── scripts/capture.js
├── work/
│   ├── config.md
│   └── {team}/{space}/{project}/
│       └── README.md
├── package.json
└── README.md
```
