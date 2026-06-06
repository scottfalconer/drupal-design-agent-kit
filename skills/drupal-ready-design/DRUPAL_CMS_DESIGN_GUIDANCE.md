# Drupal CMS Design Guidance

Design freely, but keep the result rebuildable in Drupal CMS. The user describes the site they want and you design it normally — visual direction, layout, copy, and iteration are yours. The added job is to make Drupal-shaped choices as you design, and to record the Drupal ownership so a coding agent can rebuild the approved design without reverse-engineering it.

Assume the rebuild target is Drupal CMS (Canvas/page composition plus Drupal-owned content, media, menus, forms, listings, components, and tokens) unless the user says otherwise.

## Core principle

Generated HTML, React code, client-side state, and hardcoded repeated content are **design evidence, not the final architecture.** Every meaningful part of the design should map to something Drupal owns:

- routes and menus,
- structured content (content types, fields, taxonomy),
- media (files Drupal owns, not hotlinks),
- Views / listings / filters / search,
- forms (Drupal form or Webform),
- Canvas / page composition for one-off presentation,
- reusable components and theme tokens.

If part of the design can't map to one of those, flag it — don't smuggle it in as opaque app state.

## The ownership model

| In the design | Drupal owner |
| --- | --- |
| One-off landing page or highly designed page section | Canvas / page composition |
| Content that repeats, lists, filters, is searched, reused, translated, or workflow-managed | Structured content (content type + fields + View) |
| Primary / footer / utility navigation | Drupal menus |
| Images, documents, downloadable or reusable assets | Drupal media |
| Contact, signup, or any data capture | Drupal form or Webform |
| Listing + detail pairs, filtered grids, search results | Views / search |
| A visual section that recurs with different content | A component with editor-owned props/slots |
| Color, type, spacing, radius, shadow, motion decisions | Theme tokens |
| Copy or labels an editor would change | Fields, menu items, Webform config, or Canvas content — never hardcoded |

## How to decide (the judgment calls)

**Infer, don't interrogate.** Don't ask the user to make Drupal architecture decisions unless the choice affects the site's purpose, editorial workflow, or required behavior. Infer sensible Drupal CMS ownership from the design request, mark your assumptions, and put genuine open questions in the handoff summary — not in the middle of the design conversation.

**Structured content vs page composition.** If the same shape of content appears more than once, or needs a listing, filter, search, feed, or will grow over time → a content type with fields and a View. If it's one-off, page-specific presentation an editor tweaks in place → Canvas / page composition. When unsure: "a list of things" → structured content; "this particular page" → page composition.

**The editorial line.** For every section, know what an editor can change without code (text, images, links, list items, menu order, form fields) versus what needs a developer (a new field, content type, component, or layout logic). The design isn't Drupal-ready until that line is clear.

**Proposing new structure.** You may propose new content types, fields, modules, integrations, or search behavior — but mark them **optional**, explain why the simpler model can't carry the requirement, and give the smallest Drupal-native first-pass alternative. Don't reach for new architecture to solve a visual problem.

**Stats, quotes, and proof points** are editorial values (fields or component props), not numbers baked into markup.

## Avoid

- app-only patterns (hidden client state, fake dashboards, widgets) that don't map to Drupal content, Views, or components,
- hardcoded repeated content instead of structured content,
- markup or interactions that can't render server-side,
- navigation buried in page markup instead of menus,
- new routes or content types added without explaining why,
- showing only a homepage — the rebuild needs the listing/detail and section patterns too.

## On approval: produce a Drupal CMS handoff summary

When the design is approved, output a summary a coding agent can rebuild from, using these shapes:

**Route inventory**

| Route | Page purpose | Drupal owner | Notes |
| --- | --- | --- | --- |

**Content ownership**

| Content | Repeatable? | Drupal owner | Key fields | Editor updates where? |
| --- | --- | --- | --- | --- |

**Editorial experience** — what editors change without code

| Site area | What editors can update | Drupal owner | Editing surface |
| --- | --- | --- | --- |

**Component usage**

| Route | Section | Component / View / form / menu | Data source | Reusable? |
| --- | --- | --- | --- | --- |

**Tokens**

| Token area | Decision | Theme token target |
| --- | --- | --- |

**Forms / listings / search**

| Feature | Behavior | Drupal owner | Required/optional |
| --- | --- | --- | --- |

Also note: which assets become Drupal media; accessibility and mobile/responsive behavior to preserve; optional architecture changes (kept separate from the first-pass rebuild); and any open rebuild risks.

## Rebuildable means

The design is ready to hand off when another agent can map **every major section** to a route, a content source, a component, a token, an asset, or an explicitly noted gap — and can tell what an editor owns versus what needs a developer.
