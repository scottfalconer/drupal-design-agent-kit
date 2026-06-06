# Drupal Rebuild Handoff

Most users should not fill this out manually. When the design is approved, ask the design tool:

```text
Create a Drupal CMS rebuild handoff summary using the attached guidance.
```

For structured teams, use this file as the expected shape for that generated summary. Copy it to:

```text
docs/drupal-design-handoff/DRUPAL_REBUILD_HANDOFF.md
```

Use it as the handoff artifact for the Drupal implementation repository. Start the coding agent with `AGENTS.md` and this handoff summary.

## Project Summary

Project name:

Site purpose:

Primary audience:

Primary editor/site owner:

Approved design direction:

## Source Evidence

| Evidence | Location | Notes |
| --- | --- | --- |
| Approved design output or prototype | | |
| Source URLs, screenshots, or examples used by the design tool | | |
| Brand assets or design references | | |
| Desktop screenshots | | |
| Mobile screenshots | | |
| Exported HTML/code, if available | | |

## Route Inventory

| Route | Page purpose | Source evidence | Drupal owner | Notes |
| --- | --- | --- | --- | --- |
| Home | | | | |
| About | | | | |
| Contact | | | | |

## Content Ownership Map

| Content | Repeatable? | Drupal owner | Key fields | Editor updates where? | Notes |
| --- | --- | --- | --- | --- | --- |
| | | | | | |

## Editorial Experience Map

| Site area | What editors can update | Drupal owner | Editing surface | Should not require code? | Notes |
| --- | --- | --- | --- | --- | --- |
| Homepage hero | Headline, body, CTA, image | Canvas/page composition + Hero component | Page editor / Canvas | Yes | |
| Resource cards | Title, summary, image, tags | Content type + View | Content editor | Yes | |
| Primary navigation | Labels, destinations, order | Drupal menu | Menu UI | Yes | |
| Contact form | Fields, labels, success state | Webform or Drupal form | Form builder/config | Yes | |

A design is not Drupal-ready until it is clear what an editor can update in Drupal and which changes would require developer work.

## Component Usage Map

| Route | Section | Component/block/View/form/menu | Data source | Reusable? | Notes |
| --- | --- | --- | --- | --- | --- |
| | | | | | |

## Token Map

| Token area | Design decision | Drupal/theme token target | Notes |
| --- | --- | --- | --- |
| Color | | | |
| Typography | | | |
| Spacing | | | |
| Radii | | | |
| Shadow | | | |
| Motion | | | |

## Form/List/Search Ownership

| Feature | Expected behavior | Drupal owner | Optional/required | Notes |
| --- | --- | --- | --- | --- |
| Contact form | | | | |
| Resource listing | | | | |
| Search | | | | |

## Accessibility And Responsive Notes

Contrast:

Focus states:

Keyboard behavior:

Heading order:

Form labels:

Mobile behavior:

Text over images:

## Asset And Media Notes

| Asset/media | Source | License/rights | Drupal owner | Notes |
| --- | --- | --- | --- | --- |
| | | | | |

## Parity Expectations

| Route | Source screenshot | Expected Drupal result | Intentional differences |
| --- | --- | --- | --- |
| | | | |

## Open Questions

- 

## Rebuild Risks

- 

## Optional Architecture Changes

| Change | Why it may be needed | First-pass alternative | Approval status |
| --- | --- | --- | --- |
| | | | |

## Implementation Start

In the Drupal implementation repository:

1. Copy `AGENTS.drupal-rebuild.template.md` to `AGENTS.md` and fill in project-specific values.
2. Copy the approved design output, screenshots, export, and this handoff summary to `docs/drupal-design-handoff/`.
3. Start the coding agent with `AGENTS.md` and this handoff summary.
4. Require exact validation commands and outcomes in `docs/VALIDATION.md`.
