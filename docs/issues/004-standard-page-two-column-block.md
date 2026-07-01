# Issue 004 — StandardPage + TwoColumnBlock: Home and About pages

**Status**: Open
**Blocked by**: 003
**User stories**: 8, 9, 10, 11, 20, 21

## What to build

`StandardPage` model (extends Wagtail `Page`) with a StreamField containing `TwoColumnBlock`. Create both Home and About page instances in Wagtail admin. Two-column CSS Grid layout with 768px responsive breakpoint.

End-to-end: visiting `/` and `/about/` renders content from the Wagtail admin in a two-column layout that reflows to single column on mobile.

## Acceptance criteria

- [ ] `StandardPage` model with StreamField accepting `TwoColumnBlock`
- [ ] `TwoColumnBlock`: StructBlock with `left` and `right` columns, each accepting RichTextBlock and ImageChooserBlock
- [ ] Blocks defined as standalone classes (importable and testable in isolation)
- [ ] Home page instance at `/` with headline and body content
- [ ] About page instance at `/about/` with headline and body content
- [ ] CSS Grid two-column layout: single column below 768px, two columns at 768px+
- [ ] Images uploadable via Wagtail image library into either column
- [ ] Wagtail admin page preview works for StandardPage
- [ ] Test: published StandardPage renders StreamField content at its URL
- [ ] Test: TwoColumnBlock validates with text in both columns
- [ ] Test: TwoColumnBlock validates with image in one column and text in the other
