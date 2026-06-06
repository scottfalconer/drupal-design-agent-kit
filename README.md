# Drupal Design Agent Kit

Helps AI design tools — Lovable, Replit, Claude Design, v0, Claude, ChatGPT, and similar — produce website designs that rebuild cleanly in Drupal CMS.

The kit is not the designer. Your design tool stays the designer and runs the whole design conversation; the kit is the Drupal CMS compatibility layer that keeps the result — routes, menus, content, media, forms, listings, components, tokens, and editorial ownership — rebuildable in Drupal.

You add the Drupal CMS guidance, design the way you normally would, and the tool hands you a Drupal CMS rebuild summary at the end. Here's the whole flow.

## How It Works

### 1. Add the Drupal CMS guidance

Give your design tool the **drupal-ready-design** guidance so it designs with Drupal in mind. Use it as a skill if your tool supports skills; otherwise attach the guidance file. If you're unsure, attach the file — that always works. Both deliver the exact same guidance.

Not sure which?

- Claude Design, v0, ChatGPT, or another design chat → **attach the file**.
- Claude Code, Replit, or another agent with skill support → **install the skill**.
- Unsure → **attach the file**.

**Install it as a skill** — the tool then loads it on its own whenever you design:

| Tool | Install at |
| --- | --- |
| Claude Code | `.claude/skills/drupal-ready-design/` (or `~/.claude/skills/`) |
| Replit | `.agents/skills/drupal-ready-design/` |
| Lovable | import the skill (public GitHub repo or ZIP), or add it to project/workspace knowledge |

**Attach the file** — attach [`skills/drupal-ready-design/DRUPAL_CMS_DESIGN_GUIDANCE.md`](skills/drupal-ready-design/DRUPAL_CMS_DESIGN_GUIDANCE.md) as background context (an uploaded file, project/workspace knowledge, or pasted into the chat). It's the same file the skill points to, so you lose nothing by attaching it directly.

Either way it works in the background — you don't read it or act on it. If you have them, also give the tool the usual design inputs: source URLs, screenshots, brand assets, reference sites, or an existing prototype link.

*Lovable and Replit emit real app code — treat it as design evidence, not the architecture; Replit is also a coding surface, so keep design output separate from implementation.*

### 2. Prompt normally

Type the same design request you'd give the tool anyway — a plain description of the site, not a Drupal architecture spec:

> Build me a modern, trustworthy website for an independent auto shop — booking, repair specialties, testimonials, and contact.

> Create a website for a small architecture studio: calm, premium, editorial, with project case studies and a strong contact path.

> Redesign this nonprofit site so it's easier to donate, volunteer, and find impact stories.

### 3. Let the tool design

Let your tool run its normal design conversation, iteration, and prototype generation. As it designs, the guidance keeps the output mapped to Drupal — repeatable content stays structured instead of hardcoded, navigation stays menu-shaped, reusable sections stay component-shaped — without you having to think about any of it.

### 4. Ask for the handoff summary

When the design feels right, ask:

> Create a Drupal CMS rebuild handoff summary using the Drupal CMS guidance.

The tool generates this for you — you don't write it by hand. It captures the Drupal ownership of the design: routes, navigation, structured vs one-off content, forms/listings/search, components and tokens, media, accessibility and mobile notes, what editors can change without code, and any rebuild risks. The exact contents are listed in the [guidance](skills/drupal-ready-design/DRUPAL_CMS_DESIGN_GUIDANCE.md); if the tool wants a structure to fill, point it at [`docs/DRUPAL_REBUILD_HANDOFF.template.md`](docs/DRUPAL_REBUILD_HANDOFF.template.md).

### 5. Save the outputs

Keep them together — a coding agent reads them as a set:

- the design output or prototype link,
- desktop and mobile screenshots,
- any exported HTML or code,
- the generated handoff summary.

### 6. Hand off to a Drupal build

You need a Drupal CMS implementation repository or local Drupal CMS project for this step — the kit prepares the design evidence and agent guidance, but it doesn't create the Drupal site itself.

Put `AGENTS.drupal-rebuild.template.md` in the repo as `AGENTS.md` (it's opinionated and ready to use — but you can always add it to an existing AGENTS.md) and the saved outputs under `docs/drupal-design-handoff/`, then point a coding agent at it. The prompt is the same for any agent:

> Look at the design handoff in `docs/drupal-design-handoff/` — the handoff summary, screenshots, and any export — and build it out as a Drupal CMS site, following `AGENTS.md`. Inspect the project first; rebuild through Drupal-owned content, menus, Views, forms, Canvas/page composition, components, and tokens; verify each page against the prototype (screenshots, plus the live preview URL if provided) in a browser; and record what you ran in `docs/VALIDATION.md`.

**Claude Code** — easiest in the Claude Code app, which has browser use built in for the verify loop; the `claude` CLI works too (add a Playwright or Chrome MCP for the browser checks). Either way, keep it iterating with `/loop` until each page matches the prototype.

**Codex** — likewise easiest in the Codex app (browser use built in, same as the Claude Code app); the `codex` CLI works too. Using the /goal command usually works well here.

**Tips:**

- Give the agent the **live preview / prototype URL** if your design tool provides one — a running prototype it can open and compare against beats screenshots alone.
- Install **Drupal-specific agent skills** so it knows current Drupal CMS and Canvas patterns, not just generic code — e.g. [drupal-canvas/skills](https://github.com/drupal-canvas/skills) and [acquia/nebula](https://github.com/acquia/nebula).
- **Budget hours, not minutes.** A full multi-page rebuild can run for several hours depending on complexity — run it on a plan that won't cut you off mid-build (a Pro tier or higher).

**It isn't done until it's verified in a browser** — page by page: links, forms, media, filters, and mobile, not just the homepage, and not when an import or cache rebuild "succeeds." Have it diff the rendered pages against the prototype and record the results in `docs/VALIDATION.md`.

## Example

1. Add `DRUPAL_CMS_DESIGN_GUIDANCE.md` to your design tool (install the skill, or attach the file).
2. Type:

   > Build me a modern, trustworthy website for an independent auto shop. It should help people book service, understand repair specialties, see testimonials, and contact the shop. Make it feel local, credible, and not like a generic SaaS landing page.

3. Iterate with the design tool until the design feels right.
4. Ask:

   > Create a Drupal CMS rebuild handoff summary using the Drupal CMS guidance.

5. Save the prototype link, screenshots, exported code if available, and the handoff summary.
6. Hand those to a coding agent in the Drupal repo and let it build it out — Claude Code or Codex (see step 6 above for the prompt and commands).

## Kit Contents

- [`skills/drupal-ready-design/`](skills/drupal-ready-design/) — the skill to install in your design tool. `SKILL.md` is the entry; `DRUPAL_CMS_DESIGN_GUIDANCE.md` is the full guidance it follows (and the file to attach directly if your tool can't install skills).
- [`AGENTS.drupal-rebuild.template.md`](AGENTS.drupal-rebuild.template.md) — opinionated, ready-to-use guidance for the Drupal coding agent at rebuild time (copy to `AGENTS.md`).
- [`docs/DRUPAL_REBUILD_HANDOFF.template.md`](docs/DRUPAL_REBUILD_HANDOFF.template.md) — the expected shape of the generated handoff summary.

## Scope

Design preparation and rebuild handoff only, targeting Drupal CMS (Canvas/page composition with Drupal-owned content, media, menus, forms, listings, components, and tokens). Drupal packaging, deployment, and long-term implementation happen after this kit's handoff.

## TODO

Future versions should let teams adjust the default assumptions for other Drupal starting points — an existing Drupal site, an agency starter, a custom distribution, a contributed theme, a vertical template, or a non-Canvas build path. For this release, the default target is the Drupal CMS + Canvas/page composition model described in Scope above.
