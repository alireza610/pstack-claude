---
name: setup-pstack
description: Configure which models pstack uses per role. Writes ~/.claude/pstack-models.md, which the skills read to override their defaults. Use for /setup-pstack, "configure pstack models", "pstack budget", or changing pstack's model choices.
---

# Setup pstack

Write `~/.claude/pstack-models.md`, the file pstack's skills read to set the model per role.

## Steps

### 1. Models you can choose

Claude Code's `Agent` tool takes the aliases `opus`, `sonnet`, and `haiku`. `inherit-parent` and `auto` mean the role runs on the parent chat model (omit `model`). Reasoning effort is not set per role here. It follows the session's `/effort` setting.

### 2. Load current state

The default role-to-model mapping is the file shape in step 4. If `~/.claude/pstack-models.md` already exists, read it and treat its `# budget` line and role values as the current choices. Drop a line whose role is not in step 4.

### 3. Budget, map, and confirm

**(a) Ask for a budget** with AskUserQuestion. Name the current budget when the file records one.

- `large — opus for judgment, sonnet for code` (the defaults)
- `max — opus everywhere`
- `small — sonnet for judgment, haiku for routine code`
- `inherit — every role on the chat model`

**(b) Apply it** to every role, panel entries included. On a re-run, keep any role the user changed by hand.

**(c) Show the roles and confirm.** Show every role with its model and ask whether to accept or change specific roles. Panel roles (arena runners, architect runners, interrogate reviewers) are lists. One subagent runs per entry, so the list length sets the count. `arena cross-judge pool` is a list that Arena picks one entry from.

### 4. Write the file

Overwrite the whole file so re-runs stay idempotent. Shape:

```
# pstack model configuration. One line per role. Delete a line to fall back to the skill default.
# Values: opus, sonnet, haiku, or inherit-parent / auto (run on the parent chat model).
# budget: large
feature, refactoring: sonnet
bug-fix: sonnet
perf-issue: sonnet
hillclimb: sonnet
judgment and prose: opus
hardest tasks: opus
how explorer: sonnet
how explainer: opus
why investigators: sonnet
why synthesizer: opus
reflect tooling: sonnet
reflect judgment, divergent, synthesizer: opus
arena runners: opus, sonnet
arena cross-judge pool: opus, sonnet
swarm workers: sonnet
architect runners: opus, sonnet
interrogate reviewers: opus, sonnet
```

### 5. Confirm

Tell the user the file was written. Skills read it on every run, so it applies right away. Re-running this skill updates it.

### 6. Offer a verification skill (optional)

Check whether the project has a way to drive the real app for proof (a `verify-*` skill, or an existing harness). If not, offer once: "want a project-local verification skill, so agents can drive the app the way a user does and prove changes work? I can generate one with /create-verification-skill." On yes, invoke `/create-verification-skill`. On no, move on without pushing.
