# Glossary

## Page

**Definition**: A routable unit of content with a slug, a template, and one or more content blocks.
**Type**: entity
**Relationships**: [ContentBlock] — a Page owns one or more ContentBlocks; [PageTemplate] — a Page selects one template for rendering
**Invariants**: A Page must have a unique slug. A Page must have at least one ContentBlock before it can be published.
**Synonyms (banned)**: screen, view (use Page)

---

## ContentBlock

**Definition**: A named slot of content (text or image) belonging to a Page, identified by a key.
**Type**: value
**Relationships**: [Page] — belongs to exactly one Page
**Invariants**: A ContentBlock key must be unique within its Page. A ContentBlock value must not be empty on a published Page.
**Synonyms (banned)**: field, section (use ContentBlock)

---

## Source of Truth

**Definition**: The system whose version of content is considered correct when a conflict exists.
**Type**: role
**Relationships**: Wagtail admin holds this role for all content in this project.
**Invariants**: There is exactly one source of truth per content type. Content edited outside the source of truth is discarded.

---

## Push

**Definition**: (Deprecated for this project) The act of sending a rendered Django screen to a Figma frame.
**Type**: process
**Note**: Removed per ADR 0001. Retained here to explain why it does not appear in the codebase.

---

## Pull

**Definition**: (Deprecated for this project) The act of exporting assets from Figma into `static/img/`.
**Type**: process
**Note**: Removed per ADR 0001. Retained here to explain why it does not appear in the codebase.
