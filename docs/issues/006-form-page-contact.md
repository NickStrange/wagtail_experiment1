# Issue 006 — FormPage (Contact): AbstractEmailForm with DB submissions

**Status**: Open
**Blocked by**: 003
**User stories**: 12, 13, 14, 15, 22

## What to build

Contact page using Wagtail's `AbstractEmailForm`. Default fields: Name, Email, Message. Submissions stored in the Wagtail admin database. Fields editable in admin without code changes.

End-to-end: visiting `/contact/`, filling in the form, and submitting creates a submission record visible in Wagtail admin.

## Acceptance criteria

- [ ] `FormPage` model extends `AbstractEmailForm` (`wagtail.contrib.forms`)
- [ ] Default fields: Name (single line), Email (email), Message (multiline)
- [ ] `wagtail.contrib.forms` added to `INSTALLED_APPS`
- [ ] Submissions stored in DB, viewable in Wagtail admin
- [ ] Form fields reorderable and editable in Wagtail admin without code changes
- [ ] Wagtail admin page preview works for FormPage
- [ ] Button styles reference tokens from `tokens.css`
- [ ] Test: POST valid data to `/contact/` creates one submission record
- [ ] Test: POST invalid data (missing required field) re-renders form with errors, no submission created
