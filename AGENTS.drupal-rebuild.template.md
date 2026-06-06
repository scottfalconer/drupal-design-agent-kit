# Agent Guidance: Drupal CMS Rebuild

Copy this file to `AGENTS.md` in your Drupal implementation repository. It is opinionated on purpose — you should not have to fill in blanks. Read the site's intent from the design handoff, discover project specifics by inspecting the project, and follow the defaults below. Override a default only when the project clearly differs, and say so when you do.

This file is for the Drupal repo, not the AI design tool. For design-tool setup, see the README.

## What you're doing

Rebuild an approved, AI-generated design as a real Drupal CMS site. The design and its intent live in `docs/drupal-design-handoff/` — the handoff summary, design output, screenshots, and any prototype export. **Read those first.** Don't make the user restate the brief or fill out a worksheet; infer the goal from the handoff and inspect the project for the rest.

Treat exported prototype HTML/React/CSS as design evidence, not architecture. Rebuild through Drupal-owned routes, content, media, menus, Views, forms, page composition, components, and tokens.

Do not treat the project as a blank slate. Preserve the installed Drupal CMS shape unless the handoff clearly requires a change: existing routes, recipes, content types, fields, menus, components, Views, media types, and editorial workflow are hard inputs.

## Assumed setup (override only if the project differs)

- **Composer-managed Drupal CMS site**, local dev via **DDEV**.
- **Page composition** via Canvas; **components** as SDC (Single Directory Components); **theme** via design tokens in the active front-end theme — a sub-theme, never core themes.
- **Structural changes** via configuration management; **repeatable setup** via Drupal CMS **recipes** where it fits; **content** via content entities / default content.
- **Navigation** via menus, **forms** via Webform (or core Contact), **listings/search** via Views/Search, **assets** via Media.

If the project uses Lando, a native setup, or a hosting CLI instead of DDEV, detect it and use the equivalent commands — don't stop to ask.

## Discover, don't ask

Before changing anything, inspect the project and record what you find in `docs/ARCHITECTURE.md`:

```bash
ddev drush status                      # docroot, database, versions
ddev drush pm:list --status=enabled    # installed modules and recipes
ddev drush theme:list                  # active front-end and admin themes
ddev drush config:status               # configuration state
ddev drush role:list                   # roles and permissions model
```

That tells you the docroot, active theme, builder surface, enabled modules, and roles — the facts the rebuild depends on. Keep `docs/ARCHITECTURE.md` current as you work: routes, content types and fields, menus, components, Views, media, tokens, and known constraints.

## Working agreements

- Never claim tests or checks passed unless you ran them and recorded the exact command and result.
- Keep diffs scoped to the requested rebuild change.
- Stop and ask before destructive operations (database drops, deleting content or config, force operations).
- Never commit secrets, local settings, uploaded files, `vendor/`, or generated dependency directories.
- Never edit Drupal core or contributed projects in place — use sub-themes, configuration, recipes, or a custom module.
- Prefer configuration, content, theme tokens, SDC components, Views, forms, menus, media, and documented site-building over one-off code.

## Hard-won rules

These are the defaults from prior Drupal CMS and Canvas rebuilds:

- Confirm the exact mutable target before writing: local project, DDEV site, remote environment, tenant, route, and operation. Similar-looking Drupal projects are easy to confuse.
- Use the existing Drupal foundation first. If a design can be carried by current content types, Canvas/page composition, components, Views, menus, media, or theme tokens, use those before adding structure.
- Keep three truths separate: configuration/API state, editorial/admin state, and public browser rendering. A successful import, API write, cache rebuild, or component upload is not launch proof.
- Verify page-by-page and link-by-link when parity matters. Menus, PDFs, media paths, forms, filters, and mobile layouts often fail after the "main" page looks right.
- If the project uses Canvas or another page-composition system, remember pages may pin component versions or store component props. Updating a component may not update already-authored pages until they are republished, rebound, or re-exported.
- If an API, permission, moderation, or media-write path is blocked, document the blocker and the closest Drupal-native fallback. Do not fake parity with hardcoded markup.
- Keep known gaps explicit. A partially working site with named gaps is useful; an overclaimed site is not.

## Preferred change order

Solve design needs in this order; reach for the next level only when the one above genuinely can't carry the requirement:

1. Demo content, copy, media, and menu labels within the existing model.
2. Theme tokens: color, typography, spacing, radii, shadows, image treatment.
3. Existing component props and variants.
4. Existing Canvas page composition.
5. Existing View display styling.
6. Small new SDC / component variants.
7. New fields or content types — only after proving the existing model can't support the requirement.
8. New modules — only after a human accepts the maintenance cost.

## Architecture preservation

Don't change these without explicit human approval. When a design needs one, mark it optional, explain why the current model can't support it, and propose the smallest Drupal-native change:

- public route strategy,
- content types and field relationships,
- menu destinations,
- editorial workflow and roles,
- media ownership and licensing model,
- search / listing / form ownership,
- editorial update ownership,
- install profile / recipe assumptions,
- required accessibility behavior.

## Component and content rules

- Use content entities for repeatable, searchable, filterable, translated, workflow-managed, or reusable content.
- Use Canvas / page composition for one-off landing presentation.
- Keep navigation in menus and editorial copy in fields, menus, Webforms, Views, or Canvas content — never hardcoded in PHP or Twig.
- Use Media / file entities or packaged, licensed assets; no external hotlinks.
- Every major visual section maps to an existing component, View, block, menu, or content entity. If you add a component, document why no existing one works and what data source owns each prop or slot.
- Make explicit which changes an editor can make without code and which require a developer.

## Design quality bar

The site should feel specific, credible, and useful for its audience. Avoid generic pages, stock-looking imagery, one-note palettes, fake dashboards, AI faces, and lorem ipsum. Every pass preserves accessible contrast, visible focus states, semantic heading order, predictable navigation, mobile touch targets, keyboard-operable menus/filters/tabs/accordions/forms, readable text over images, and clear calls to action.

## Validation (run before claiming done)

```bash
ddev composer validate
ddev drush status
ddev drush cache:rebuild
```

Then verify and record results in `docs/VALIDATION.md`:

- all required public routes render,
- menus link to valid routes,
- forms render and submit (or have documented placeholders),
- listing/detail pages use Drupal-owned data,
- no missing images or broken media references,
- no unlicensed assets,
- accessibility, responsive, and performance checks have recorded outcomes.

For browser truth, capture at least the primary desktop and mobile routes or document why that was not possible. For editor truth, confirm normal content, menu, media, and form updates remain editor-owned rather than code-only.

## What to produce

- `docs/ARCHITECTURE.md` — the living map of routes, content types, menus, components, Views, media, and tokens.
- `docs/REBUILD_DELTA.md` — what changed from the source design and which differences are intentional.
- `docs/VALIDATION.md` — exact commands run and their outcomes.
- A short known-gaps section in the relevant doc when anything is blocked, deferred, mocked, or intentionally different from the design.

## References

- Drupal CMS: https://www.drupal.org/project/cms
- DDEV: https://docs.ddev.com/en/stable/
