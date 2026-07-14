---
name: design-polish
description: Automates a stylistic "design pass" after the first iteration of a UI — polishes an existing product to match the consistent standard described in DESIGN.MD, without touching the layout. Use this skill when: (1) the user has finished a first iteration/prototype of a UI and says things like "polish the UI", "do a design pass", "make the styling consistent", "apply the design system"; (2) the user mentions wrapping up/finishing an iteration of a project in a frontend/UI context, even without explicitly asking for styling, if the project has a freshly built interface; (3) DESIGN.MD already exists in the project or should be created as the source of truth for its look. The skill checks whether DESIGN.MD already exists, audits the UI against it (covered / missing / conflicting), ALWAYS asks the user before introducing anything ambiguous, applies styling without changing structure/layout, and finally updates DESIGN.MD so it stays a complete and current standard.
---

# design-polish

## When this triggers

- Explicit: "polish the UI", "design pass", "make the styling consistent", "apply the design system".
- Implicit: the user says they're wrapping up a first iteration, prototype, or draft version of a project, and there's UI in it (components, pages, panels) — even if they didn't use the word "style". In that case, briefly propose a design pass instead of assuming it's not wanted.

## Step 0 — check whether `DESIGN.MD` exists in the project

Look for a `DESIGN.MD` file in the project root (and, as a fallback, in typical locations: `/docs`, `/design`, `.claude/`).

**If `DESIGN.MD` exists** → go to Step 1, treating it as the standard/source of truth.

**If `DESIGN.MD` does NOT exist** → always stop and ask the user before generating or changing anything:

> "This project doesn't have a `DESIGN.MD` yet. Would you like:
> (a) the baseline `DESIGN.MD` from this skill's template (a monochrome, dark-only system — see `templates/DESIGN.baseline.md`), or
> (b) a `DESIGN.MD` generated from your existing UI (I'll pull the real colors, fonts, radii, and shadows out of your current code and turn them into tokens)?"

Don't guess which option to pick, and don't mix the two without confirmation. After the answer:
- (a) → copy `templates/DESIGN.baseline.md` into the project root as `DESIGN.MD`.
- (b) → analyze the existing styles (CSS / Tailwind config / styled-components / tokens in code), extract the values actually in use for colors, typography, radii, shadows, spacing, and build a `DESIGN.MD` with the same structure as the template (frontmatter with tokens + Colors/Typography/Shapes/Components sections), and show it to the user for approval BEFORE using it to style anything.

Only proceed once you have an approved `DESIGN.MD`.

## Step 1 — audit the UI against `DESIGN.MD` (mandatory, before any change)

Review the whole UI of the project and compare it with `DESIGN.MD`. Split the result into three categories and present them to the user:

1. **Directly covered** — components with a clear counterpart in `DESIGN.MD` (button, select, toggle, slider, etc.). Short list.
2. **Missing from the spec** — UI elements that `DESIGN.MD` doesn't describe (modal, tooltip, table, notifications, badge, card, chart, empty state, loader, breadcrumb, etc.). For each: how it looks today + your proposed style derived from the file's general principles (palette, alpha ramp, typography, radii, single depth) — without implementing it yet.
3. **Ambiguous / conflicting** — places that conflict with the rules (local shadows, an extra accent color, a different way of signaling active state, a fourth font size) without an obvious resolution.

## Step 2 — ask before touching any code

For items in categories 2 and 3 from Step 1: **stop and ask specific questions**, one at a time, each with a proposed solution to choose from (e.g. "modal: `.surface` + the single ambient shadow, or a different depth treatment?"). Don't start implementation until the user has answered.

## Step 3 — implementation (only after Steps 0–2)

Hard rules, always apply:

1. **Don't change the layout.** DOM structure, sidebar/panel placement, section order, `position`, `top/right/left/bottom`, layout container widths/heights, page-layout breakpoints — leave untouched. Only change the visual layer (color, typography, borders, shadow, radius, transitions, states).
2. **Only use tokens from `DESIGN.MD`.** No new colors, font sizes, radii, or shadows outside the file. Missing case → nearest existing token, not a new value.
3. **Monochrome / dark-only** (if that's what `DESIGN.MD` specifies) — remove brand colors/accents/gradients not in the file.
4. **Active state = inversion** (white fill + black content), per the "Active = inversion" section of the file — don't introduce a different state signal.
5. **Only as many typography sizes as `DESIGN.MD` has** — map existing text onto those levels.
6. **A single depth across the whole app** (`ambient` shadow on the surface) — remove all other per-element `box-shadow`.
7. **`DESIGN.MD` must get updated.** Any new rule/exception agreed on in Step 2 goes back into the file (new entry in `components:` + matching CSS section) before you consider the task done.

Go component by component: find the counterpart in `DESIGN.MD` → apply that exact spec (color, border, radius, height, transitions, hover/focus/active/disabled states). Import the font and `:root` variables from the "Foundations" section if the project doesn't already have them; if it has similar ones under different names — unify the values rather than mass-renaming variables across the codebase (regression risk).

## Not allowed

- Changing page/view layout, navigation, or DOM component hierarchy.
- New colors/font sizes/shadows outside `DESIGN.MD`.
- Changing component logic/behavior — style only.
- Implementing category 2/3 items (Step 1) without the user's answer from Step 2.

## At the end

Short summary: which files/components were changed, which cases had no clear counterpart in `DESIGN.MD` and how they were resolved, and confirmation that all of these decisions were written back into `DESIGN.MD`.

## Supporting files for this skill

- `templates/DESIGN.baseline.md` — a baseline, monochrome `DESIGN.MD` used for option (a) in Step 0.
