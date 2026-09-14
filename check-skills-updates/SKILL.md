---
name: check-skills-updates
description: >-
  Checks whether globally installed agent skills (via npx skills) have upstream
  updates, reports what changed, and optionally applies updates. Use when the
  user asks to check skill updates, update skills, skillsの更新, スキル更新確認,
  or whether frontend-design / baseline-ui / other npx skills are outdated.
---

# Check Skills Updates

## When to use

User wants to know if personal/global skills installed with `npx skills` have newer upstream versions, or wants them updated. Agent-agnostic (Cursor, Claude Code, Copilot, etc.).

## Steps

1. Run (network required):

```bash
npx skills check
```

2. Show the result briefly in Japanese:
   - up to date → 「全部最新」と伝える
   - updates available → どの skill が古いか列挙する

3. If the user wants to apply updates (or clearly asked to update, not only check), run:

```bash
npx skills update -g -y
```

Then re-run `npx skills list -g` and confirm `frontend-design` / `baseline-ui` (and any others) are still present.

4. Do **not** update project-local skills under a repository (e.g. `.agents/skills/`, `.cursor/skills/`, `.claude/skills/`) unless the user explicitly asks. Those are often hand-written and are not managed by `npx skills`.

## Notes

- Lock file: `~/.agents/.skill-lock.json`
- Canonical installs: `~/.agents/skills/`
- Per-agent dirs (`~/.cursor/skills/`, `~/.claude/skills/`, …) are usually symlinks or copies of the above
- Custom skills in `agent-personal-skills` are git-managed separately from `npx skills`
- `check` is read-only; `update -g -y` writes
