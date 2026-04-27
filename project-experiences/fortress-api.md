---
type: Project Experience
role: Backend Engineer
domain: Internal Operations / People Ops
scope: Small team (2–5)
start_date: TBD
end_date: TBD
status: Shipped
tech_stack: []
related_to: []
---

# Fortress API — Internal Operations & People Platform Backend

## Summary

Built and maintained **Fortress API**, the Go/Gin backend powering Dwarves Foundation's internal operations platform — a single surface for HR, projects, clients, payroll, surveys, delivery metrics, accounting, and deep integrations with Notion, Discord, Basecamp, and Google. The service exposes REST endpoints, scheduled cronjobs, and stateless webhooks behind RBAC-scoped middleware, backed by PostgreSQL via GORM.

## Problem & Context

A consultancy running dozens of concurrent projects, contractors, and client engagements needs one source of truth for *people* and *delivery* — not a sprawl of spreadsheets, Notion pages, and Discord channels. Fortress consolidates HR records, project staffing, payroll, survey/feedback loops, and finance workflows into one backend, then meets the team where it already works (Discord for notifications, Notion for content, Basecamp for accounting). The challenge was keeping a wide surface area maintainable: many domains, many integrations, many scheduled jobs, all sharing one auth and permission model.

## My Contributions

- **Designed the layered backend architecture** — handler → store (repository) → model split, with `IHandler`/`IStore` interfaces per domain, request/view DTOs, and middleware for auth and permissions, keeping each domain independently testable and extensible.
- **Built fine-grained RBAC** — defined permission constants (e.g. `employees.read`, `projects.edit`, `cronjobs.execute`) in `pkg/model/permissions.go` and enforced them via `PermissionMiddleware`, giving every endpoint an explicit access contract.
- **Implemented the HR & people domain** — employee CRUD, profiles, line managers, roles, base salary, skills, seniorities, chapters, positions, onboarding/invitations, payroll commit (incl. BHXH), salary advance, and office check-in.
- **Implemented the projects domain** — lifecycle, members/slots, work units, commission models, status/survey state, ICY weekly distribution, and dashboards (sizes, work surveys, action items, engineering health, audits).
- **Built the surveys & feedback subsystem** — survey create/send/list, topics, reviewers, performance/engagement reviews, feedback submission, and unread counters used across the team.
- **Shipped accounting & finance flows** — invoices (list/status/template/send), bank accounts, valuation, payroll, vault transactions, conversion rates, and Basecamp expense/accounting webhook handlers.
- **Integrated Notion as a content backend** — earns, tech radar, audiences, events, digests, updates, memos, issues, staffing demands, hiring positions, project milestones, DF updates, changelogs, and newsletter sending via `go-notion`.
- **Built the Discord integration layer** — birthday/on-leave messages, scheduled events, brainery and delivery-metric reports, memo sync/sweep, weekly memo notifications, OGIF events, MMA scores, salary advance, earn transactions, office check-in, research topics.
- **Architected the cronjob runtime** — separate `cmd/cronjob` entrypoint alongside `cmd/server`, scheduling audits sync, accounting todo sync, project member status sync, vault transaction store, engagement message indexing, brainery/delivery reports, conversion-rate sync, memo sync/sweep, and YouTube broadcast transcription.
- **Implemented stateless webhooks** for n8n and Basecamp (expense validate/create/uncheck, accounting transaction, invoice mark paid, on-leave validate/approve), driving workflows without polling.
- **Set up the test infrastructure** — `testify` + `go-testfixtures` against a Dockerized Postgres via `make migrate-test`, enabling integration tests against real SQL behavior rather than mocks.
- **Generated Swagger docs** from handler annotations using Swaggo (`make gen-swagger`), keeping the public contract discoverable for frontend and external consumers.

## Key Achievements

- Delivered a **single backend covering 10+ domains** (HR, projects, clients, surveys, accounting, Notion, Discord, dashboards, cronjobs, webhooks) without devolving into a monolith — each domain isolated behind its own handler/store interface pair.
- Established **permission-scoped middleware as the access primitive** for every endpoint, making "who can do what" auditable from a single file rather than scattered through handlers.
- Stood up a **multi-entrypoint Go service** (`cmd/server` + `cmd/cronjob`) sharing one codebase, one DB, and one auth model — avoiding a separate worker service while keeping HTTP and scheduled work cleanly separated.
- Wired **deep integrations with Notion, Discord, Basecamp, Google, SendGrid, and crypto/earn (Mochi, Ethereum)** into a coherent operations surface — the team interacts with Fortress through the tools they already use.
- Built a **Dockerized Postgres test pipeline** with seed fixtures, enabling integration tests that exercise real GORM/SQL behavior — catching schema and query bugs that mocked tests miss.
- Shipped **PDF generation for invoices** (`go-wkhtmltopdf` + MJML email templates via SendGrid) end-to-end, from accounting state to client inbox.

## Tech & Tools

**Language & runtime:** Go 1.21.

**Web framework:** Gin.

**Database:** PostgreSQL via GORM (`lib/pq`, `pgx`); SQL migrations and seeds under `migrations/` driven by `make migrate-up` / `make seed` / `make migrate-test`.

**Auth:** JWT (`golang-jwt/jwt` v4), API keys, permission-based middleware.

**Config & logging:** Viper, godotenv, Logrus.

**API docs:** Swaggo (Swagger generated from handler annotations).

**Integrations:** Google (GCS, OAuth), Notion (`go-notion`), Discord (`discordgo`), Basecamp webhooks, SendGrid, GitHub, Wise, HashiCorp Vault, Mochi (`consolelabs/mochi-go-sdk`), ImprovMX, Reddit, YouTube, Dify, Ethereum (`go-ethereum`).

**Storage & email:** Google Cloud Storage; SendGrid + MJML (`Boostport/mjml-go`); PDFs via `go-wkhtmltopdf`.

**Testing:** `testify`, `go-testfixtures`, Dockerized Postgres for integration tests.

**DevOps:** Docker, Docker Compose, Make (`init`, `migrate`, `seed`, `dev`, `test`), devbox, Colima.

**Misc:** CORS, `pprof`, `go-money`, `shopspring/decimal`, `go-nanoid`, `go-cache`.

## Lessons Learned

- _(STAR-style story to add: e.g. how the permission system evolved from ad-hoc role checks to constant-defined `PermissionMiddleware`, or why cronjobs were split into a separate `cmd/cronjob` entrypoint instead of running inside the API server.)_

## Notes

_Private context — strip before sharing externally._

- One-liner for resume:
  > **Backend Engineer — Fortress API (Go/Gin):** Designed and maintained the core backend for an internal operations platform (HR, projects, clients, payroll, surveys, delivery metrics) with RBAC, PostgreSQL, and integrations to Notion, Discord, Basecamp, and Google; exposed REST APIs, cronjobs, and webhooks with Swagger docs and permission-scoped middleware.
