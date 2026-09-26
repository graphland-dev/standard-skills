# Standard Skills

Portable engineering guidelines as agent skills — **judgment and contracts**, not stack scaffolds.

**Frontend (React-core)** is included first: URL lists, `FormSheetShell`, controlled+Zod forms, `ServerFormError`, UX hierarchy. No Next.js/Vite lock-in. RHF is an alternate form stack.

Contrast with [graphland-dev/skills](https://github.com/graphland-dev/skills): that pack scaffolds a specific GraphLand stack. This pack ([graphland-dev/standard-skills](https://github.com/graphland-dev/standard-skills)) teaches portable patterns.

## Install

From your **project root** (recommended — skills are committed and shared with the team):

```bash
npx skills add graphland-dev/standard-skills --all -y
npx skills add graphland-dev/standard-skills --all -a cursor -y   # Cursor only
npx skills add graphland-dev/standard-skills --list
```

Global (every project on your machine):

```bash
npx skills add graphland-dev/standard-skills --all -g -y
npx skills update -g
```

Project installs land under agent skill dirs the CLI detects (commonly `.agents/skills/`, and/or `.cursor/skills/`, `.claude/skills/`, …). Commit those paths (or the symlinks the CLI creates) so teammates get the same skills.

### Use in a project

1. Install as above from the repo root.
2. Point agents at the pack from root **`AGENTS.md`** (always-on context). Skills stay **on-demand** — don’t paste full `SKILL.md` bodies into `AGENTS.md`.
3. In chat, name the skill: `Use react-forms for this sheet`, `/react-review`, etc.

#### `AGENTS.md` snippet

Add (or merge) something like this at the repo root:

````markdown
## Agent skills

Install once per clone:

    npx skills add graphland-dev/standard-skills --all -y

For React UI work, load these skills instead of inventing patterns:

| Skill | When |
| --- | --- |
| `react-patterns` | Default guideline — lists, sheets, forms, data ops, UX, shadcn |
| `react-lists` | URL-driven tables / search / filters |
| `react-forms` | Create/edit forms, validation, server errors |
| `react-overlays` | Sheets vs routes, confirms |
| `react-shadcn` | Adding or wrapping shadcn/ui components |
| `react-ux` | Visual hierarchy, spacing, empty states |
| `react-review` | PR / diff checklist |

Prefer naming the skill in the prompt (`Use react-lists…`). Match the host stack; don’t migrate form libraries unprompted.
````

If the app already has project-specific skills (e.g. under `.agents/skills/`), list those first and say: when a pattern isn’t covered there, follow **standard-skills** (`react-patterns`, …).

### Invoking a skill

Standard [Agent Skills](https://agentskills.io) — name the skill in plain language:

```
Use react-patterns for this list page.
Fix the form with react-forms.
Review this PR with react-review.
```

`react-patterns` is the auto-load guideline; siblings go deep when named.

## What's inside

### `frontend/` — core React UI

| Skill            | What it does                                                                                         |
| ---------------- | ---------------------------------------------------------------------------------------------------- |
| `react-patterns` | Guideline — URL list state, sheets, forms, data ops, UX hierarchy, hygiene. Auto-load when relevant. |
| `react-forms`    | Schema-first forms, create/edit one component, field UX, submit errors.                              |
| `react-lists`    | Server-paginated lists, URL-synced page/sort/search/filters, debounce.                               |
| `react-overlays` | Sheet / modal / route decision tree, reset-on-open, focus.                                           |
| `react-ux`       | Visual hierarchy, spacing, type, color, empty states (Refactoring UI–inspired).                      |
| `react-shadcn`   | shadcn/ui — ui/form/reui layers, CLI add, FormField wraps, cn(), when not to add.                    |
| `react-review`   | PR/diff checklist against these guidelines.                                                          |

## Sample prompts

```
The product table refetches on every keystroke. Fix search using react-lists / react-patterns.

Add create/edit for Invoice as a sheet (one form component). Follow react-overlays + react-forms.

Use react-review on this branch — focus on URL state and mutation invalidation.
```

## Principles (one-liner)

1. **URL owns list state** — page, sort, search, filters are shareable and reload-safe.
2. **Sheets over routes for simple CRUD** — keep list context; reserve full pages for complex entities.
3. **Schema-first forms** — one schema drives validation + types; create and edit share one form.
4. **Co-locate data ops** — queries/mutations/schema live next to the feature, not in a global grab-bag.
5. **Adapt, don't dictate** — prefer the project's existing libs; these skills describe contracts, not a mandated stack.
6. **Share only when shared** — feature-local UI first; no single-use “shared” components.
