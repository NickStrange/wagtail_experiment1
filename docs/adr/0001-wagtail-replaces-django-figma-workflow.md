# 0001 — Wagtail replaces Django + Figma integration

**Status**: Accepted
**Date**: 2026-06-30

## Context

The original experiment aimed to push Django screens to Figma for visual preview,
tweak text and images there, and pull changes back into Django. A domain modeling
session surfaced that this workflow creates an unsolvable mapping problem: text
edited in Figma has no reliable path back to the correct line in a Django template
or database record.

Further grilling revealed that the stated goals — see final screens without running
the app, edit text and images as a solo developer — are already solved by Wagtail:

- **Page preview**: built in, no separate tool needed
- **Content editing**: Wagtail admin, all text and images in the database
- **Image management**: Wagtail image library, no `static/img/` pipeline
- **Routing at scale**: slug + template_name per page, no per-page models or URLs

The Figma integration added complexity (MCP sync, push/pull scripts, image mapping)
without adding capability for a solo developer with no designer in the loop.

## Decision

Use Wagtail as the CMS. Drop the Figma MCP integration entirely.

## Consequences

**Easier**: shipping pages, editing content, previewing screens, managing images.
**Lost**: the learning goal of the original experiment (Django–Figma MCP integration).
**Risk**: if a designer joins later, Figma integration may need to be revisited —
at that point a Wagtail + Figma push/pull workflow is still viable but not pre-built.
