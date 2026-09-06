# UZI-Skill (stock-deep-analyzer)

Vendored as a project-level Claude Code skill because this environment does
not support `/plugin marketplace add` / `/plugin install`.

- Source: https://github.com/wbh604/UZI-Skill
- Plugin: `stock-deep-analyzer` v3.9.4
- License: MIT (see `UZI-Skill-LICENSE` in this directory)
- Author: FloatFu-true

## What was copied

- `skills/deep-analysis`, `skills/investor-panel`, `skills/lhb-analyzer`,
  `skills/trap-detector` → `.claude/skills/`
- `commands/*.md` → `.claude/commands/`
- `agents/investor-panel.md` → `.claude/agents/uzi-investor-panel.md`

## What was intentionally left out

- `hooks/` (SessionStart hook) was not wired into `.claude/settings.json`.
  It runs a background GitHub update check and prints a skill summary on
  every session start — left disabled by default since that's an
  unrequested, standing behavior change. The original hook files are in
  the upstream repo if you want to add them yourself.

## Known differences from a real plugin install

- As project commands, these run as `/analyze-stock`, `/dcf`, etc.
  (no `stock-deep-analyzer:` namespace prefix like a marketplace plugin
  would have).
- Some command docs reference `<plugin_root>` assuming `commands/` and
  `skills/` are siblings at a repo root. Here they live under
  `.claude/commands/` and `.claude/skills/` respectively — resolve
  `<plugin_root>` as this repo's root and skill scripts as
  `.claude/skills/<skill-name>/scripts/`.

## Runtime dependencies

The analysis scripts need Python packages, not installed here:

```bash
pip install -r .claude/skills/deep-analysis/requirements.txt
playwright install chromium
```
