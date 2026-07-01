# Wagtail CMS Experiment

Feasibility experiment: build a multi-page site with Wagtail, validate that content
editing, page preview, and image management in the Wagtail admin is sufficient for a
solo developer to ship 20–30 pages without a separate design tool workflow.

Figma integration is out of scope — see ADR 0001.

## Tech Stack

- Python 3.12, Wagtail (latest), PostgreSQL
- Secrets via `python-decouple` + `.env`

## Security

- No hardcoded credentials, keys, or secrets anywhere
- `.env` never committed — always in `.gitignore`
- `SECRET_KEY` and `DEBUG` from environment only, no fallback defaults
- `ALLOWED_HOSTS` must be explicit
- CSRF protection always enabled
- No sensitive data in logs, error pages, or HTTP headers

## Pages

Two initial pages with shared header, footer, and logo:

- **Home** (`/`) — hero section with headline and body text
- **About** (`/about/`) — about section with headline and body text

All content (text + images) managed via Wagtail admin. No hardcoded copy in templates.

## Project Artefacts

All specs, issues, ADRs, glossary, and decisions live as files in this repo. External
systems (GitHub issues, project boards) are mirrors — not the source of truth.

- `docs/adr/` — Architecture Decision Records
- `docs/issues/` — build slices (one file per issue)
- `docs/glossary.md` — canonical term definitions
- `docs/prd.md` — Product Requirements Document

## Development Rules

- **TDD** — write the test before the implementation, every time
- **PEP 8** — enforced via `flake8`, max line length 88
- **Type hints** on every function, method, and class attribute
- `black` for formatting, `isort` for imports
- Pre-commit hooks enforce all of the above
- Dev dependencies (`black`, `flake8`, `isort`, `coverage`, `pre-commit`) in `requirements-dev.txt`
