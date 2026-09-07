# COMP-4960 Team Project — Starter Template

> COMP-4960 Software Engineering — Fall 2026 · Wentworth Institute of Technology · Dr. Memo Ergezer

This is the starter template every team repository is created from. It gives you the governance files, a CI stub, and a home for your architecture decisions — **not** a prescribed application structure. Build your project (FastAPI, Streamlit, or your approved stack) on top of it.

## What's here

- **`CONTRACT.md`** — your team working agreement. Fill it in together during Lab 1 and merge it via a reviewed pull request.
- **`AI_LOG.md`** — your Category 1 AI-use log. Add a row as you go, per the Co-Pilot policy in the syllabus.
- **`docs/adr/ADR_Template.md`** — copy to `docs/adr/NNN-title.md` for each consequential decision (minimum 3). Your Design Document summarizes these; the files in the repo are the source of truth.
- **`.github/workflows/ci.yml`** — a GitHub Actions CI stub (lint + tests) that runs on every pull request. It comes fully alive in Lab 8; it already runs the smoke test below.
- **`tests/test_smoke.py`** — one trivial passing test so CI is green from day one. Replace and extend it with real tests.
- **`requirements.txt`** — Python dependencies (starts with `pytest` + `ruff`; add your stack, e.g. `fastapi`/`uvicorn` or `streamlit`).

## Where your code goes

Put application code in a top-level package (e.g. `src/` or `app/`) and tests in `tests/`. Keep `main` protected — no direct pushes; every change lands through a reviewed pull request. Use `feat:` / `fix:` / `refactor:` commit prefixes.

## Run it locally

```bash
python -m venv .venv && source .venv/bin/activate    # Windows: .venv\Scripts\activate
pip install -r requirements.txt
pytest -q
```

## Note: `.gitignore` is intentionally NOT included

You'll create and justify your `.gitignore` in **Lab 1, Part 5** (Path A: an AI assistant; Path B: the official GitHub Python template / gitignore.io). Don't add one before then. Until you do, avoid committing `__pycache__/`, `.venv/`, and `.pytest_cache/`.

## Before your final handoff

Work through the repository handoff checklist posted with the course materials: README current, runs cold from a fresh clone, no secrets in the repo, tests green in CI, ADRs up to date, and known limitations listed. A `LICENSE` is optional for coursework — add one if your team wants.
