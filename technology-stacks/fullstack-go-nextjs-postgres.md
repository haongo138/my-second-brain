---
type: Technology Stack
relatedTo:
  - "[[technology-stack]]"
relationships:
  related_to:
    - "[[technology-stack]]"
  primary_language:
    - "[[go]]"
    - "[[typescript]]"
  Type:
    - "[[technology stack]]"
---

# Fullstack — Go + Next.js + Postgres

A pragmatic fullstack setup: Go on the backend for fast, boring services; Next.js + Refine on the frontend for a data-driven React app that talks to the Go API; Postgres as the system of record. Optimized for small teams that want type safety end-to-end without the weight of a monorepo framework.

## Architecture

- **Backend**: Go HTTP/JSON API (Gin + GORM).
- **Frontend**: Next.js (App Router, React Server Components) — talks to the Go API via fetch on the server, hydrates on the client.
- **Database**: PostgreSQL 16+, single primary, logical backups via `pg_dump`/managed snapshots.
- **Frontend data layer**: **Refine (refinedev)** with a REST data provider pointed at the Go API. Next.js has *no* direct database access — every read and write goes through the Go API. This keeps business logic, validation, and authorization in one place.
- **Auth**: Sessions issued by the Go API as signed, HttpOnly cookies. Refine's `authProvider` calls `/auth/login`, `/auth/logout`, `/auth/me`; Next.js middleware validates the cookie and forwards.
- **Deploy**: Go service in a distroless container; Next.js on Vercel or a Node container; Postgres managed (Neon, Supabase, RDS).

## Languages

- **Go** — Backend services, workers, CLIs.
- **TypeScript** — Frontend, shared types, scripts.
- **SQL** — PostgreSQL dialect; source of truth for schema lives in `.sql` migrations.
- **Bash** — CI glue, container entrypoints.
- **Dockerfile** — Multi-stage builds for the Go service.

## Backend (Go)

See [[Go Stack]] for the full opinionated breakdown. Highlights for this stack:

- **Gin** — HTTP router and middleware framework.
- **GORM** (`gorm.io/gorm` + `gorm.io/driver/postgres`) — ORM and query builder. Models are struct-tagged; associations, hooks, and transactions go through GORM. Schema changes still ship via `go-migrate` SQL files (GORM's `AutoMigrate` is **not** used in this stack — migrations are explicit and reviewable).
- **`gorm.io/gorm/logger`** — SQL query logger. Configured with a slog-backed writer so query logs land in the same structured pipeline as app logs (single sink, single format). Threshold typically `Warn` in prod, `Info` in dev to surface slow queries.
- **go-migrate** (`golang-migrate/migrate`) — Database migrations as raw SQL. Owns schema; GORM consumes it.
- **golangci-lint** — Aggregated Go linter; runs locally and in CI.
- **slog** — App-level structured logging (request IDs, business events, errors). GORM's logger bridges into slog so there's one log stream end-to-end.
- **otel-go** — Tracing exported to the same collector as the frontend. GORM has an OpenTelemetry plugin (`gorm.io/plugin/opentelemetry`) for span-per-query tracing.
- **testcontainers-go** — Real Postgres in integration tests; GORM points at the container DSN.

## Frontend (Next.js)

### Framework
- **Next.js (App Router)** — React Server Components by default; client components only where interactivity demands it.
- **React 19** — Hooks, Suspense, and `use()` for data fetching.
- **TypeScript** — Strict mode (`"strict": true`, `"noUncheckedIndexedAccess": true`).

### Data
- **Refine (refinedev)** — React framework for data-intensive UIs. Provides hooks (`useList`, `useOne`, `useCreate`, `useUpdate`, `useDelete`, `useTable`, `useForm`) and the data-provider abstraction that all CRUD routes through.
- **`@refinedev/simple-rest`** — REST data provider configured against the Go API base URL. Wrapped with a `fetch` interceptor that forwards the auth cookie and normalizes Go error envelopes.
- **`@refinedev/nextjs-router`** — Router bindings for Next.js App Router so resource URLs stay idiomatic.
- **TanStack Query** — Underlies Refine's cache and mutation lifecycle; surfaced here because optimistic updates and manual cache invalidation use it directly.
- **Generated TS types** — Server response types come from the Go OpenAPI spec via `openapi-typescript`, then plug into Refine's generic resource types for end-to-end safety.

### UI
- **Tailwind CSS** — Utility-first styling.
- **shadcn/ui** — Copy-in component primitives built on Radix.
- **Radix UI** — Headless, accessible primitives.
- **lucide-react** — Icon set.
- **sonner** — Toast notifications; mounted once in the root layout, triggered from Refine mutation hooks (`onSuccess`/`onError`) and form submit handlers.
- **next/font** — Self-hosted fonts, no layout shift.
- **next/image** — Image optimization.

### Forms & Validation
- **Zod** — Runtime schema validation; shared between client and server.
- **react-hook-form** — Form state with Zod resolvers.

### Auth
- **Refine `authProvider`** — Custom provider whose `login` / `logout` / `check` / `getIdentity` / `onError` methods call the Go API. No client-side session storage; the HttpOnly cookie is the source of truth.
- **OAuth handled server-side** — OAuth callback URLs land on the Go API, which exchanges the code, persists the user, and issues the session cookie. Next.js never sees the OAuth secret.
- **Middleware** — `middleware.ts` calls `/auth/me` (or verifies a signed JWT cookie locally if you prefer stateless sessions) and gates protected routes.

### Tooling
- **pnpm** — Package manager.
- **Turbopack** — Dev server and builds (built into Next.js).
- **ESLint** + **eslint-config-next** — Linting.
- **Prettier** — Formatting.
- **Vitest** — Unit tests.
- **Playwright** — E2E tests.
- **MSW** — Mock the Go API in component tests.

## Database (Postgres)

- **PostgreSQL 16+** — Primary datastore.
- **Migrations**: Owned exclusively by the Go service via **go-migrate** (`migrations/*.up.sql` / `*.down.sql`). No second migration tool — Next.js has no DB connection.
- **Connection pooling**:
  - Go service: `database/sql` pool tuned via GORM (`db.SetMaxOpenConns`, `SetMaxIdleConns`, `SetConnMaxLifetime`). In-process, no external pooler.
  - No Next.js pooler needed — the frontend never opens DB connections.
- **Extensions**: `uuid-ossp` or `pgcrypto` for IDs, `pg_stat_statements` for query insight, `pg_trgm` for fuzzy search.
- **Backups**: Daily logical backup + PITR on the managed provider.
- **Local dev**: Postgres via `docker compose` or `testcontainers-go` for tests.

## Shared Tooling

- **devbox** — Reproducible local dev shells (Nix-backed). Pins Go, Node, pnpm, Postgres client, `golang-migrate`, and `golangci-lint` versions per repo so contributors get an identical toolchain on first `devbox shell`.
- **Taskfile.dev** (`task`) — Cross-cutting commands (`task dev`, `task migrate`, `task test`) that wrap both Go and pnpm scripts.
- **just** — Acceptable alternative to `task`.
- **direnv** — Per-directory env vars for local dev (composes well with `devbox`).
- **mkcert** — Local HTTPS so cookies behave like prod.

## Observability

- **OpenTelemetry** — Both Go and Next.js export traces/metrics to the same collector.
- **Sentry** — Error tracking with shared release tags across BE/FE.
- **Vercel Analytics** or **Plausible** — Web analytics for the frontend.
- **Grafana + Prometheus** (or managed equivalent) — Metrics and dashboards for the Go service.

## CI/CD

- **GitHub Actions** — Single workflow with parallel jobs:
  - `go test ./...` + `golangci-lint`
  - `pnpm typecheck` + `pnpm lint` + `pnpm test`
  - `pnpm playwright test` against a preview deploy.
- **goreleaser** — Tagged releases of the Go binary + container image.
- **Vercel** — Preview deploys per PR for the Next.js app.
- **Migration gate**: PRs that change `migrations/*.up.sql` block merge until applied to the staging DB and the OpenAPI spec / generated TS types are up to date.

## Notes

- **Single data path.** All reads and writes from Next.js flow through the Go API via Refine's data provider. No dual ORM, no DB credentials in the frontend, no schema duplication. Authorization, validation, and business logic live in exactly one place.
- **Schema ownership belongs to the backend.** Migrations live with the Go service; the frontend consumes the API contract, not the schema directly.
- **GORM, but no `AutoMigrate`.** Schema changes are SQL files reviewed in PRs and applied by `go-migrate` — not derived from struct tags at boot. GORM owns *queries and models*, not *schema evolution*. This keeps prod migrations explicit, reversible, and gated in CI.
- **One log stream.** GORM's query logger is wired to slog so SQL traces, app events, and request logs share format, fields, and sink. Avoid running GORM's default stdout logger in prod — it bypasses your structured pipeline.
- **Refine fits CRUD-shaped UIs especially well.** Admin panels, dashboards, and list/detail/edit flows benefit most from its hooks and resource conventions. For highly custom UIs, you can still drop down to TanStack Query directly — Refine doesn't get in the way.
- **Shared types via OpenAPI.** Generate TS types from the Go API spec (`oapi-codegen` for the server, `openapi-typescript` for the client). Refine's generics consume those types so resource hooks are end-to-end typed.
- **Cookies, not bearer tokens.** Same-origin or subdomain cookies keep auth simple between Next.js and the Go API. Use `HttpOnly` + `Secure` + `SameSite=Lax` and rotate signing secrets via env.
- **No Next.js → Postgres connections.** Removes a whole category of serverless-pooling pain. Connection budget belongs to the Go service.
- **One repo or two?** Start as a monorepo (`/api`, `/web`, `/migrations`) with Taskfile orchestration. Split only when team boundaries demand it.
- **Distroless for Go, Node slim for Next.js.** Smallest viable images, no shell, fewer CVEs.
