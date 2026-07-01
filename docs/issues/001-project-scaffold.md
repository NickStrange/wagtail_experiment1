# Issue 001 — Project scaffold: Wagtail + PostgreSQL + python-decouple

**Status**: Open
**Blocked by**: None — can start immediately
**User stories**: 1

## What to build

Bootstrap Wagtail project with PostgreSQL database and python-decouple for secrets. Set up dev tooling and pre-commit hooks. This is the foundation every other slice depends on.

End-to-end: running `python manage.py runserver` connects to PostgreSQL, reads config from `.env`, and serves the default Wagtail home page.

## Acceptance criteria

- [ ] Wagtail project created via `wagtail start`
- [ ] PostgreSQL configured via python-decouple + `.env` (no hardcoded credentials)
- [ ] `SECRET_KEY` and `DEBUG` from environment only, no fallback defaults
- [ ] `ALLOWED_HOSTS` explicit in settings
- [ ] CSRF protection enabled
- [ ] `.env` in `.gitignore`, `.env.example` committed with placeholder values
- [ ] `requirements.txt` with runtime deps (wagtail, psycopg2, python-decouple)
- [ ] `requirements-dev.txt` with dev deps (black, flake8, isort, coverage, pre-commit)
- [ ] Pre-commit hooks enforce black, flake8 (max line length 88), isort
- [ ] `python manage.py migrate` runs clean against PostgreSQL
- [ ] `python manage.py runserver` starts without errors
