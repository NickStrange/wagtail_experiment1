# Issue 007 — Page preview verification: StandardPage and FormPage

**Status**: Open
**Blocked by**: 004, 006
**User stories**: 19

## What to build

Verify Wagtail's built-in page preview works end-to-end for both StandardPage and FormPage. No new code expected — this slice confirms the integration is wired correctly and documents any gaps found.

## Acceptance criteria

- [ ] Wagtail admin preview renders StandardPage (Home) with correct two-column layout
- [ ] Wagtail admin preview renders StandardPage (About) with correct two-column layout
- [ ] Wagtail admin preview renders FormPage (Contact) with form visible
- [ ] Preview matches the live page appearance (tokens, layout, nav, footer)
- [ ] Any gaps found are documented as follow-up issues
