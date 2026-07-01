# PRD — Wagtail Multi-Page Site

## Problem Statement

A solo developer needs to ship a 20–30 page content site without a separate design
tool or designer in the loop. Content (text, images) must be editable without
touching code. Pages must look consistent and professional on both desktop and
mobile. Visual style (colours, button shapes) must be changeable from a single
definition so that a rebrand does not require hunting through templates.

## Solution

A Wagtail CMS project with two content page types (standard and form), a shared
responsive layout, a site-wide settings model for header and footer, and a CSS
design token system. All content is managed in the Wagtail admin. No Figma
integration (see ADR 0001).

## User Stories

1. As a developer, I want a Wagtail project bootstrapped with PostgreSQL and
   python-decouple, so that I can start building without manual configuration.
2. As a developer, I want a base template with a header, footer, and content area,
   so that every page shares the same chrome without duplicating markup.
3. As a content editor, I want to edit the site logo in one place, so that it
   updates across all pages immediately.
4. As a content editor, I want to edit navigation links in one place, so that
   adding a new page to the header does not require a code change.
5. As a content editor, I want to edit footer content (address, contact info, legal)
   in one place, so that it stays consistent across all pages.
6. As a site visitor, I want to navigate between Home, About, and Contact from the
   header on every page, so that I can reach any page from anywhere.
7. As a site visitor, I want the header navigation to work on mobile, so that I can
   switch pages on a phone without pinching or scrolling horizontally.
8. As a content editor, I want to create a Home page with a two-column layout, so
   that I can place headline and body content side by side on desktop.
9. As a content editor, I want the two-column layout to reflow to a single column
   on mobile, so that the page is readable on a phone without horizontal scrolling.
10. As a content editor, I want to add images to either column of a page, so that
    I can mix text and visuals in the layout.
11. As a content editor, I want to create an About page with the same two-column
    layout as Home, so that the site looks consistent.
12. As a content editor, I want to create a Contact page with a form, so that
    visitors can submit enquiries without me sharing an email address publicly.
13. As a site visitor, I want to fill in and submit the contact form, so that I can
    send an enquiry without leaving the site.
14. As a content editor, I want form submissions stored in the Wagtail admin, so
    that I can review them without a third-party email service.
15. As a content editor, I want to add and reorder form fields in the Wagtail admin,
    so that I can change the contact form without a code change.
16. As a developer, I want button colours, border-radius, and typography defined as
    CSS custom properties, so that changing the design token changes every button
    and heading on the site simultaneously.
17. As a developer, I want a single tokens file that documents every design token,
    so that future developers know where to look when changing the visual style.
18. As a site visitor, I want buttons to look the same everywhere on the site, so
    that the UI feels consistent and professional.
19. As a content editor, I want to preview a page in the Wagtail admin before
    publishing, so that I can check the layout without making it live.
20. As a developer, I want all page models covered by tests, so that a Wagtail
    upgrade does not silently break page rendering.
21. As a developer, I want all StreamField blocks covered by tests, so that
    invalid block configurations are caught before deployment.
22. As a developer, I want the form page submission logic covered by tests, so that
    I can refactor form handling without breaking the submission flow.

## Implementation Decisions

### Page types

- **StandardPage** — used for Home and About. Extends Wagtail `Page`. Content
  defined as a StreamField with a `TwoColumnBlock`. Both pages are instances of
  this model; no separate `HomePage` / `AboutPage` models.
- **FormPage** — used for Contact. Extends Wagtail `AbstractEmailForm`
  (`wagtail.contrib.forms`). Default fields: Name, Email, Message. Fields are
  editable in the Wagtail admin. Submissions stored in the database.

### StreamField blocks

- **TwoColumnBlock** — a `StructBlock` with a `left` column and a `right` column,
  each accepting `RichTextBlock` and `ImageChooserBlock`. This is the primary layout
  unit for `StandardPage`.
- Blocks are defined as standalone classes so they can be imported and tested in
  isolation from the page model.

### Site settings

- A single `SiteSettings` model using `wagtail.contrib.settings` (`BaseSiteSetting`).
- Fields: logo (`ImageChooserBlock` — uploaded via Wagtail media library), footer
  text (rich text, dummy placeholder content initially).
- The header navigation is populated from the three published pages (Home, About,
  Contact) — no manual link management needed at this scale.

### Responsive layout

- Two-column layout implemented with CSS Grid.
- Breakpoint: single column below 768px, two columns at 768px and above.
- No CSS framework dependency — custom CSS only, scoped to the base template.

### Design token system

- All visual constants defined as CSS custom properties on `:root` in a single
  `tokens.css` file.
- Tokens cover: primary colour, secondary colour, button background, button text
  colour, button border-radius, font family, base font size, heading sizes.
- Colour palette: autumnal — burnt orange, warm brown, deep red, gold, forest green.
- All component styles reference tokens, never raw values.
- Changing a token in `tokens.css` updates every component that uses it.

### Mobile navigation

- At widths below 768px the header nav collapses to a hamburger icon.
- Tapping the hamburger toggles a dropdown showing all three page links.
- Implemented in vanilla JS — no library dependency.

### Wagtail configuration

- `wagtail.contrib.forms` enabled for FormPage.
- `wagtail.contrib.settings` enabled for SiteSettings.
- PostgreSQL via `python-decouple` `.env` file.
- Security settings per CLAUDE.md: no hardcoded secrets, explicit `ALLOWED_HOSTS`,
  CSRF always on.

## Testing Decisions

Good tests verify external behaviour through public interfaces. They survive
internal refactors. They do not test implementation details (e.g. which template
variable is set internally).

**Modules to test:**

- **StandardPage** — test that a published page renders with the correct content
  from its StreamField. Test via the Wagtail test client hitting the page URL.
- **TwoColumnBlock** — test that the block validates correctly (both columns
  present, accepts image and rich text). Test the block in isolation using
  Wagtail's `StreamFieldPanel` test utilities.
- **FormPage** — test that a POST to the form URL with valid data creates a
  submission record. Test that a POST with invalid data re-renders the form with
  errors. Test via the Wagtail test client.
- **SiteSettings** — test that the logo and footer text appear in the rendered
  base template. Test via a page render that includes the base template.

**Not tested at unit level:** CSS tokens (visual correctness), template markup
structure (too brittle), Wagtail admin UI interactions (covered by Wagtail's own
test suite).

## Out of Scope

- Figma integration (ADR 0001)
- User authentication or member-only pages
- Search functionality
- Blog or news feed
- Email delivery of form submissions (submissions stored in DB only for now)
- Deployment configuration (hosting, CI/CD)
- Internationalisation

## Further Notes

- Start with Home and About pages before building FormPage — validate the
  `StandardPage` + `TwoColumnBlock` pattern first.
- The design token system should be set up before any component CSS is written —
  retrofitting tokens is painful.
- See `docs/glossary.md` for canonical term definitions (Page, ContentBlock,
  Source of Truth).
- See `docs/adr/0001-wagtail-replaces-django-figma-workflow.md` for the decision
  that removed Figma from scope.
