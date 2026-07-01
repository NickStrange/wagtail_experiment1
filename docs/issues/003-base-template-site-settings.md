# Issue 003 — Base template + SiteSettings: header, footer, logo

**Status**: Open
**Blocked by**: 002
**User stories**: 2, 3, 4, 5, 6

## What to build

Shared base HTML template with header, content area, and footer. SiteSettings model (BaseSiteSetting) for site-wide logo and footer text. Header nav populated from the three published pages — no manual link management.

End-to-end: any page that extends the base template renders with logo, nav, and footer pulled from SiteSettings.

## Acceptance criteria

- [ ] `SiteSettings` model using `wagtail.contrib.settings` (`BaseSiteSetting`)
- [ ] Logo field: image uploaded via Wagtail image library
- [ ] Footer field: rich text (dummy placeholder content initially)
- [ ] `wagtail.contrib.settings` added to `INSTALLED_APPS`
- [ ] Base template renders header (logo + nav), `{% block content %}`, footer
- [ ] Header nav links to Home, About, Contact pages
- [ ] All colours, fonts, border-radius reference tokens from `tokens.css`
- [ ] Test: logo and footer text appear in rendered base template via page render
