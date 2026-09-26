# Standard Skills

Portable engineering guidelines as agent skills — **judgment and contracts**, not stack scaffolds.

**Frontend (React-core)** is included first: URL lists, `FormSheetShell`, controlled+Zod forms, `ServerFormError`, UX hierarchy. No Next.js/Vite lock-in. RHF is an alternate form stack.

Contrast with [graphland-dev/skills](https://github.com/graphland-dev/skills): that pack scaffolds a specific GraphLand stack. This pack ([graphland-dev/standard-skills](https://github.com/graphland-dev/standard-skills)) teaches portable patterns.

## Install

```bash
npx skills add graphland-dev/standard-skills --all -y
npx skills add graphland-dev/standard-skills --all -a cursor -y   # Cursor only
npx skills add graphland-dev/standard-skills --all -g -y          # global
npx skills add graphland-dev/standard-skills --list
npx skills update -g                                             # update a global install later
```

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
