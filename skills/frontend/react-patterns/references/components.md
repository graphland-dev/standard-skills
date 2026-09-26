# Components — share only when shared

Don’t create “shared” UI for a single call site. Prefer feature-local components; promote only when reuse is real.

## Default placement

| Put it… | When |
| --- | --- |
| Next to the feature (`pages/<feature>/components/`, route `_components/`, etc.) | Entity forms, one-off cards, feature sheets/dialogs, feature-only helpers |
| App shared kit (`components/form`, `components/table`, `components/ui`, …) | Cross-app primitives: field wrappers, sheet shell, data table, buttons |
| Domain shared (`components/merchant/…`, similar) | List chrome used on many routes, or thin sheet adapters imported by multiple pages |

**Start local.** Extract upward only after a second (real) consumer appears — or when it’s clearly a primitive (input, shell, table).

## Good splits

- **Form body** (fields, schema, mutations) → feature-local `*-form.tsx`
- **Sheet chrome** (`FormSheetShell`, titles, `formId`) → thin `*-form-sheet.tsx` (shared only if multiple routes open the same sheet)
- **List chrome** (search bar, toolbar, data table) → shared once many lists use it
- **One-feature card** (`ThemeCard`, `PluginCard`) → stay local even if “card-shaped”

## Promote to shared when

- Two or more unrelated features import it, **or**
- It’s a design-system primitive (no domain words in the API), **or**
- Create + edit + admin (or equivalent) already share one heavy form and forking would drift

## Do not promote when

- “We might reuse this later”
- Only the sheet wrapper needs to be reachable from one list page
- It’s a settings one-liner alias around another form
- You’re abstracting props for a single screen (“flexible SharedCard with 12 optional slots”)

## Anti-patterns

- `components/SharedX.tsx` with a **single** importer
- Moving `customer-form.tsx` into global `components/` just because a sheet exists
- Fusing sheet + form into one mega shared component
- Premature `components/common/` grab-bags
- Duplicating a second “shared” form beside a feature-local one (pick one home)

## Checklist

- [ ] New UI started feature-local
- [ ] Shared kit only for primitives or proven multi-route reuse
- [ ] Form body local; sheet adapter thin
- [ ] No single-use “shared” cards/sections
