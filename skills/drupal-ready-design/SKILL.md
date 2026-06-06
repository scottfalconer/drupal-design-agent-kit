---
name: drupal-ready-design
description: Use when designing or prototyping a website in any AI design tool (Lovable, Replit, v0, Claude Design, ChatGPT, Claude) that may later be rebuilt in Drupal CMS. Keeps the design mapped to Drupal-owned routes, structured content, menus, media, forms, Views, components, and tokens, and produces a Drupal rebuild handoff summary on approval.
---

# Drupal-Ready Design

When designing or prototyping a website that may be rebuilt in Drupal CMS, design freely but keep the result rebuildable. Follow the full guidance in [DRUPAL_CMS_DESIGN_GUIDANCE.md](DRUPAL_CMS_DESIGN_GUIDANCE.md) — it covers the Drupal CMS ownership model, the design decisions to make as you go, what to avoid, and the handoff summary to produce once the design is approved.

Core principle: generated HTML, React code, client-side state, and hardcoded repeated content are design evidence, not the final architecture. Every major part of the design should map to something Drupal owns — a route, content type, menu, media item, View, form, component, or token — or be flagged as a gap.
