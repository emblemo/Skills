# Skills

A collection of skills for coding agents (Claude Code, Cursor, Codex, OpenCode, and others supporting [Agent Skills](https://agentskills.io)).

## Install

Install all skills from this repo:

```
npx skills add emblemo/Skills
```

Install just one specific skill:

```
npx skills add emblemo/Skills --skill design-polish
```

For a specific agent:

```
npx skills add emblemo/Skills --skill design-polish -a claude-code
```

Globally (available across all projects, not just the current one):

```
npx skills add emblemo/Skills --skill design-polish -g
```

## Reference

- **[design-polish](skills/design-polish/SKILL.md)** — automates a "design pass" after the first UI iteration. Audits the existing interface against a `DESIGN.MD` file (treated as the project's source of truth), asks about anything `DESIGN.MD` doesn't cover, applies styling without changing the layout, and updates `DESIGN.MD` at the end so it stays a complete standard.
  - Includes `templates/DESIGN.baseline.md` — a baseline, monochrome `DESIGN.MD` (dark-only) used when the project doesn't have its own standard yet.

More skills will be added here as additional folders under `skills/`.

## How it works

Trigger it with something like "polish the UI", "do a design pass", "make the styling consistent" — or the agent will propose it on its own when you mention wrapping up the first iteration of a project that already has a UI.

The skill always checks first whether the project has a `DESIGN.MD`:
- if it does — it treats it as the standard and audits the UI against it,
- if not — it asks whether you want the baseline template (`templates/DESIGN.baseline.md`) or a `DESIGN.MD` generated from analyzing your existing code.

No styling change goes into effect without first asking you about cases `DESIGN.MD` doesn't cover.

## Update

```
npx skills update design-polish
```

## License

MIT
