# ADR-NNN: <Short decision title>

> **COMP-4960 Software Engineering — Fall 2026 · Wentworth Institute of Technology · Dr. Memo Ergezer**
>
> This template lives in `docs/adr/`. Copy it to `docs/adr/NNN-title.md` for every consequential decision —
> naming convention `docs/adr/NNN-title.md` (e.g., `docs/adr/001-use-sqlite-for-mvp.md`), numbered in the
> order decisions were made. Your Design Document's Section 5 ("Architecture Decision Records") should
> **summarize** these files, not replace them — the files in the repo are the source of truth, and graders
> will check them against the repo at the Sprint 1 Check-in (Nov 19) and again at the Final Presentation.
>
> Minimum 3 ADRs per team. Keep each one to about a page. Update the `Status` field as a decision evolves
> (`Proposed` → `Accepted`, or `Superseded by ADR-XXX`) instead of deleting old ADRs — an ADR is a record of
> what you decided *and why*, even after you change your mind.

## Status

`Proposed` | `Accepted` | `Rejected` | `Deprecated` | `Superseded by ADR-XXX`

## Date

YYYY-MM-DD

## Owners

<name(s) of whoever made and is accountable for this decision>

## Context

<What forces, constraints, or requirements made this decision necessary? What were you trying to solve?
Keep this factual — this is the "why now," not the "what we picked." 2–5 sentences is usually enough.>

## Decision

<What did you decide, stated as a single clear sentence? Avoid hedging — say what you're doing, not what
you're "leaning towards.">

## Consequences

**Positive:**

- <What this decision gets you>

**Negative / tradeoffs:**

- <What this decision costs you, or what you now have to live with. Every real decision has at least one
  of these — if you can't name one, you probably haven't picked a real alternative below either.>

**Follow-ups:**

- <Anything this decision obligates you to do later — a migration, a revisit date, a monitoring task>

## Alternatives considered

<What else did you seriously evaluate, and why did it lose? This is the section teams skip and the section
graders check first. "We didn't consider anything else" is not an acceptable answer at the design defense
during the Final Presentation — pick at least one real alternative that a reasonable team could have chosen,
and say why you didn't.>

---

## Worked example — do not copy into your repo, read it for the pattern

# ADR-004: Use SQLite Instead of PostgreSQL for the MVP Datastore

## Status

Accepted

## Date

2026-10-14

## Owners

Priya N. (Module C — Data & Persistence)

## Context

Our MVP needs a relational datastore for referrals, users, and audit-log rows behind a Python web
backend (FastAPI). The team has three weeks until the Sprint 1 Check-in (Nov 19) and no production
deployment target yet — we are running locally and on a single free-tier hosting instance for demos.
We need something the whole team can set up in minutes without a shared server, that supports the
joins and constraints our data model needs, and that won't consume time we don't have on
infrastructure instead of features.

## Decision

We will use SQLite (via SQLAlchemy, so the ORM layer is swappable) as the datastore for the MVP,
with the database file ignored by Git and a `seed.py` script that recreates it from synthetic fixtures.

## Consequences

**Positive:**

- Zero setup: every teammate runs the app with no separate database server to install, configure,
  or keep in sync — this matters with a walking skeleton due in Week 5.
- Fast tests: our test suite runs against a fresh in-memory SQLite database per test run, so CI stays
  fast with no external service dependency or test-data leakage between runs.
- The whole team already has to learn SQLAlchemy for the ORM; using SQLite vs. Postgres underneath
  it is a one-line connection-string change, not a rewrite.

**Negative / tradeoffs:**

- SQLite has weaker concurrent-write support than Postgres — fine for a single-user demo, but this
  will not hold up under real multi-user concurrent load.
- We lose Postgres-only features we might eventually want (e.g., native JSONB querying, row-level
  security) if the project continues past this course.
- SQLite's type system is looser (type affinity, not strict types), which has already hidden one bug
  where a string was silently accepted into an integer column during synthetic-data seeding.

**Follow-ups:**

- Because we used SQLAlchemy rather than raw SQLite calls, migrating to Postgres later is a
  configuration change plus a data-migration script, not a rewrite. If this project moves toward a
  real multi-user deployment, revisit this ADR before that deployment, not after.
- Add an integration test that specifically exercises concurrent writes, so we notice if SQLite's
  concurrency limits start to matter before a real user does.

## Alternatives considered

- **PostgreSQL:** the "default" choice for a production Python web app, and what we'd reach for if
  this were shipping to real users this semester. Rejected for the MVP because it requires either a
  shared hosted instance (a new dependency and a new single point of failure for four teammates to
  coordinate around) or a local Docker setup (extra onboarding cost we don't have time for before the
  Week 5 walking skeleton). We would revisit this immediately if the project's pathway required
  real concurrent multi-user access before the semester ends.
- **A flat JSON file / no real database:** rejected because our data model has real relationships
  (referrals → documents → audit events) that we'd end up re-implementing as manual joins and losing
  the data-integrity constraints (foreign keys, uniqueness) that even SQLite gives us for free.
