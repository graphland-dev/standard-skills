# Standard Skills

Portable engineering guidelines as agent skills — **judgment and contracts**, not stack scaffolds.

**Frontend (React-core)** and **backend (framework-agnostic API)** packs. Patterns are portable: Nest/GraphQL/Mongoose/etc. appear only as optional adapters. RHF is an alternate form stack on the FE side.

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
3. In chat, name the skill: `Use react-forms for this sheet`, `/api-review`, etc.

#### `AGENTS.md` snippet

Add (or merge) something like this at the repo root:

````markdown
## Agent skills

Install once per clone:

    npx skills add graphland-dev/standard-skills --all -y

### Frontend (React)

| Skill | When |
| --- | --- |
| `react-patterns` | Default guideline — lists, sheets, forms, data ops, UX, shadcn |
| `react-lists` | URL-driven tables / search / filters |
| `react-forms` | Create/edit forms, validation, server errors |
| `react-overlays` | Sheets vs routes, confirms |
| `react-shadcn` | Adding or wrapping shadcn/ui components |
| `react-ux` | Visual hierarchy, spacing, empty states |
| `react-review` | PR / diff checklist |

### Backend (API)

| Skill | When |
| --- | --- |
| `api-patterns` | Default guideline — tenancy, validation, pagination, errors, auth |
| `api-modules` | Scaffolding a new feature module |
| `api-review` | PR / module audit (TENANT / AUTH / ERR / …) |

Prefer naming the skill in the prompt (`Use react-lists…`, `Use api-patterns…`). Match the host stack; don’t migrate frameworks unprompted.
````

If the app already has project-specific skills (e.g. under `.agents/skills/`), list those first and say: when a pattern isn’t covered there, follow **standard-skills** (`react-patterns`, `api-patterns`, …).

### Invoking a skill

Standard [Agent Skills](https://agentskills.io) — name the skill in plain language:

```
Use react-patterns for this list page.
Fix the form with react-forms.
Review this PR with react-review.
Use api-patterns + tenancy for this mutation.
Scaffold the invoice feature with api-modules.
Audit this module with api-review.
```

`react-patterns` / `api-patterns` are the auto-load guidelines; siblings go deep when named.

## What's inside

### `frontend/` — core React UI

| Skill            | What it does                                                                                         |
| ---------------- | ---------------------------------------------------------------------------------------------------- |
| `react-patterns` | Guideline — lists, sheets, forms, data ops, share-vs-local, open/closed, UX, hygiene. Auto-load when relevant. |
| `react-forms`    | Schema-first forms, create/edit one component, field UX, submit errors.                              |
| `react-lists`    | Server-paginated lists, URL-synced page/sort/search/filters, debounce.                               |
| `react-overlays` | Sheet / modal / route decision tree, reset-on-open, focus.                                           |
| `react-ux`       | Visual hierarchy, spacing, type, color, empty states (Refactoring UI–inspired).                      |
| `react-shadcn`   | shadcn/ui — ui/form/reui layers, CLI add, FormField wraps, cn(), when not to add.                    |
| `react-review`   | PR/diff checklist against these guidelines.                                                          |

### `backend/` — framework-agnostic API

| Skill          | What it does                                                                              |
| -------------- | ----------------------------------------------------------------------------------------- |
| `api-patterns` | Guideline — layout, tenancy, validation, pagination, auth, errors, side effects. Auto-load when relevant. |
| `api-modules`  | Feature scaffold checklist (DTO → service → transport → catalog).                         |
| `api-review`   | TENANT / AUTH / ERR / LAY / PAGE / SIDE review flags.                                     |

Nest/GraphQL/Mongo mappings live only under `api-patterns/references/adapters.md`.

## Sample prompts

```
The product table refetches on every keystroke. Fix search using react-lists / react-patterns.

Add create/edit for Invoice as a sheet (one form component). Follow react-overlays + react-forms.

Use react-shadcn — add a FormField wrapper, don’t edit ui/input.tsx.

Use react-review on this branch — focus on URL state and mutation invalidation.

Add invoice list+create with api-modules; scope every query with api-patterns tenancy.

Use api-review on this module — check TENANT and ERR.
```

## Principles (one-liner)

**Frontend**

1. **URL owns list state** — page, sort, search, filters are shareable and reload-safe.
2. **Sheets over routes for simple CRUD** — keep list context; reserve full pages for complex entities.
3. **Schema-first forms** — one schema drives validation + types; create and edit share one form.
4. **Co-locate data ops** — queries/mutations/schema live next to the feature, not in a global grab-bag.
5. **Adapt, don't dictate** — prefer the project's existing libs; these skills describe contracts, not a mandated stack.
6. **Share only when shared** — feature-local UI first; no single-use “shared” components.
7. **Open/closed for shared UI** — extend by wrap/compose; don’t edit shared primitives for one screen.
8. **shadcn: wrap, don’t fork** — CLI into `ui/`; product fields via `FormField*`.

**Backend**

1. **Co-locate features** — transport + service + inputs in one folder.
2. **Tenancy from auth context** — never trust body-only org ids; scope every query.
3. **Validate at the boundary** — inputs ≠ entities; whitelist unknowns.
4. **One list contract** — `{ nodes, meta }` (or host equivalent).
5. **Thin transport** — rules in services; structured `code` + `message` errors.
6. **Policy-driven AuthZ** — catalog every operation; UI hide ≠ security.
7. **Side effects after write** — mail/queues/events after durable success.
