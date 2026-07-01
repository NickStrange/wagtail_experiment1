# Issue 002 — Design token system: tokens.css with autumnal palette

**Status**: Open
**Blocked by**: 001
**User stories**: 16, 17, 18

## What to build

Single `tokens.css` file defining all visual constants as CSS custom properties on `:root`. No component CSS yet — tokens only. Every component built after this slice references tokens, never raw values.

## Acceptance criteria

- [ ] `tokens.css` created and loaded in base template
- [ ] Autumnal colour palette defined as tokens: burnt orange, warm brown, deep red, gold, forest green
- [ ] Button tokens defined: `--btn-bg`, `--btn-color`, `--btn-border-radius`
- [ ] Typography tokens defined: `--font-family`, `--font-size-base`, heading sizes
- [ ] No raw colour values, font names, or sizes appear outside `tokens.css`
- [ ] Changing a token value updates every component that references it (verified manually)
