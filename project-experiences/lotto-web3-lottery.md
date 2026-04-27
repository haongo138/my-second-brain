---
type: Project Experience
role: Full-Stack Engineer
domain: Web3 / Gaming
scope: Small team (2–5)
start_date: TBD
end_date: TBD
status: Shipped
tech_stack: []
related_to: []
---

# Lotto — Web3 Lottery & Scratch-Card Game

## Summary

Built **Lotto**, a Web3 lottery and scratch-card game where users connect an EVM wallet, buy/play tickets, and scratch cards to reveal BNB and EDU token prizes. Shipped as a Turborepo monorepo (Next.js 15 + React 19) with a tRPC v11 API, Drizzle/PostgreSQL persistence, Goldsky GraphQL for indexed on-chain data, and a shared `@repo/ui` design system.

## Problem & Context

Casual Web3 games need a fast, wallet-native loop — connect, play, win, claim — without ceremony, while still backing prizes and referrals with auditable on-chain data. Lotto pairs a tactile scratch-to-reveal UX with wallet-keyed identity, indexed chain data via Goldsky, and a referral system that ties growth directly to wallet addresses. The monorepo is engineered so that UI, API, schema validation, and FP error handling stay consistent across the web app and a separate docs/playground app.

## My Contributions

- **Architected the Turborepo monorepo** — `web` and `docs` apps plus shared packages (`ui`, `api`, `db`, `auth`, `tailwind-config`, `schema-validation`, `fp`, `utils`, `hooks`, `constants`, `error-codes`) with a centralized dependency catalog in `pnpm-workspace.yaml`.
- **Built the scratch-to-reveal game UX** — canvas/touch-based scratch interaction with a configurable reveal threshold, multiple scratch icon assets, and prize display, modelled as a type-safe state machine (`idle → loading → active → unopened-cards`) using `assertUnreachable` from `@repo/utils`.
- **Designed the tRPC v11 API layer** with TanStack Query, Zod validation, and SuperJSON, gated by NextAuth v5 sessions for protected procedures.
- **Modeled the domain in PostgreSQL + Drizzle ORM** under the `lotto_*` schema — wallet-keyed users, referrals (with a unique-referee constraint), and game state — exposed via the shared `@repo/db` package.
- **Integrated Goldsky GraphQL for on-chain data** — derived win logs by joining `claimStarteds` and `claimSettleds` on `seqNo`, with optional address filtering for per-user stats and amount-based filtering for the global feed.
- **Implemented a wallet-based referral system** keyed by EVM address, with a unique-referee constraint, referrer/referee tracking, and BSC address validation in the shared schema package.
- **Built a shared `@repo/ui` design system** with `ui-`-prefixed Tailwind classes to avoid host-app conflicts, plus design tokens (`brand-*`, `text1`, `card` shadow) in `@repo/tailwind-config` reused across both apps.
- **Established an `fp-ts`-based error model** in a custom `@repo/fp` package — `action`, `Success`/`Failed`, `run`, `pipe`, typed error codes, and HTTP status codes — used by tRPC procedures for GraphQL and external API calls.
- **Wired wallet identity** with RainbowKit + Wagmi + Viem for connect/balance flows, and integrated CoinGecko for token pricing in prize and "fund raised" widgets.

## Key Achievements

- Delivered a **wallet-native game loop** (connect → play → scratch → claim) with on-chain-backed win logs, on Next.js 15 + React 19.
- Shipped a **type-safe scratch-card state machine** using `assertUnreachable` exhaustiveness checks, eliminating an entire class of UI state bugs at compile time.
- Stood up **Goldsky GraphQL as the source of truth for win history**, decoupling the product from RPC polling and unlocking efficient global and per-user feeds.
- Built a **monorepo design system** (`@repo/ui` + `@repo/tailwind-config`) with a `ui-` Tailwind prefix, enabling safe component reuse across the `web` and `docs` apps.
- Codified a **functional error-handling pattern** (`@repo/fp` with `fp-ts` `TaskEither`/`Either`) used uniformly across tRPC, GraphQL, and external API integrations.
- Enforced **wallet-keyed identity** end-to-end — referrals, game features, and BSC address validation — keeping the product crypto-native without traditional account ceremony.

## Tech & Tools

**Monorepo & build:** Turborepo, pnpm workspaces, dependency catalog in `pnpm-workspace.yaml`.

**Apps:** Next.js 15 (App Router), React 19; separate `web` and `docs` apps.

**Frontend:** Tailwind CSS (shared `@repo/tailwind-config`, `ui-` prefix), Motion / Framer Motion, Radix UI, RainbowKit, Wagmi, Viem.

**API:** tRPC v11, TanStack Query, Zod, SuperJSON.

**Database:** Drizzle ORM, PostgreSQL (scoped `lotto_*` schema).

**Chain data:** Goldsky GraphQL (`claimStarteds` / `claimSettleds`), CoinGecko API for prices.

**Auth:** NextAuth v5 (beta), `@auth/drizzle-adapter`, optional OAuth (Discord).

**Functional helpers:** `fp-ts` (`TaskEither`, `Either`), custom `@repo/fp` (`action`, `Success`/`Failed`, `run`, `pipe`), HTTP status codes.

**Validation & types:** Zod, drizzle-zod, shared `@repo/schema-validation` (EVM address, game/referral inputs).

**Testing:** Jest.

**Tooling:** TypeScript 5.7, ESLint, Prettier.

## Lessons Learned

- _(STAR-style story to add: e.g. why win logs were moved from RPC polling to Goldsky GraphQL, or how the `@repo/fp` error model evolved to keep tRPC + GraphQL + external API errors consistent.)_

## Notes

_Private context — strip before sharing externally._

- One-liner for resume:
  > **Built a Web3 lottery web app (Turborepo monorepo) with wallet-based scratch cards, referral tracking, tRPC API, Drizzle + PostgreSQL, Goldsky GraphQL for on-chain win logs, and a shared design system (Tailwind, React 19, Next.js 15).**
