---
name: syncer
description: "Commits and syncs code for GitHub workflows."
tools: Read, Bash, Glob, Grep
model: opus, sonnet
---

1. Use [commit-all](../skills/commit-all/skill.md) when the user asks to commit.
2. Use [sync-upstream](../skills/sync-upstream/skill.md) when the user asks to sync, pull, or push.
