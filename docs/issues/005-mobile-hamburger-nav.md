# Issue 005 — Mobile hamburger nav: vanilla JS toggle below 768px

**Status**: Open
**Blocked by**: 003
**User stories**: 7

## What to build

Collapse header nav to a hamburger icon below 768px. Tapping the icon toggles a dropdown showing all three page links. No JS library dependency.

End-to-end: on a viewport narrower than 768px, nav links are hidden behind a hamburger icon; tapping it reveals and hides the dropdown.

## Acceptance criteria

- [ ] Hamburger icon visible in header below 768px
- [ ] Desktop nav links hidden below 768px
- [ ] Tapping hamburger toggles dropdown with Home, About, Contact links
- [ ] Tapping again (or a nav link) closes the dropdown
- [ ] Implemented in vanilla JS — no library or framework
- [ ] Icon and dropdown colours reference tokens from `tokens.css`
