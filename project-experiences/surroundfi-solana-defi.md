---
type: Project Experience
role: Full-Stack Engineer
domain: Web3 / DeFi
scope: Small team (2–5)
start_date: TBD
end_date: TBD
status: Shipped
tech_stack: []
related_to:
  - "[[surroundfi]]"
---

# SurroundFi — Solana DeFi Lending & Borrowing Protocol

## Summary

Built **SurroundFi**, a Solana-based DeFi lending and borrowing protocol where users connect a wallet, supply or borrow assets across pools (banks), and track portfolio positions and health factor. Shipped as a Turborepo monorepo (Next.js 15 + React 19) integrated with a custom Anchor program, Pyth Hermes oracles for pricing and confidence intervals, a tRPC v11 API, Drizzle/PostgreSQL persistence, NextAuth v5 with Discord, and a shared `@repo/ui` design system.

## Problem & Context

DeFi lending UX is unforgiving — users need to reason about supply, borrow, collateralization, oracle prices, and liquidation risk in real time, all while signing on-chain transactions. SurroundFi pairs a wallet-native interaction model (Backpack and other Solana wallet adapters) with a custom Anchor lending program, Pyth oracle pricing for weighted and realtime feeds, and a portfolio surface that exposes health factor and margin requirements clearly. The monorepo is engineered so on-chain integration, the web app, the docs site, the tRPC API, and shared schema/UI packages stay version-aligned and type-safe end to end.

## My Contributions

- **Architected the Turborepo monorepo** — `web` and `docs` apps plus shared packages (`ui`, `api`, `db`, `auth`, `utils`, `schema-validation`, `fp`, `constants`, `error-codes`, `tailwind-config`, `typescript-config`, `eslint-config`) with a centralized dependency catalog in `pnpm-workspace.yaml`.
- **Integrated the custom Anchor program** (`Surroundfi` IDL) for lending account init, deposit, borrow, repay, withdraw, health-check accounts, and oracle setup (Pyth legacy, Switchboard, Pyth Push, staked-with-Pyth-Push).
- **Wired Solana wallet adapters** (Backpack and others) for connect, lending account initialization on first use, and SOL wrap/unwrap and Token-2022 support.
- **Built the lend / borrow product surface** — mode toggle, pool list, transaction steps and preview, action widgets/dialogs, position-level actions (withdraw, repay), and health progress with tooltips.
- **Implemented Pyth Hermes price integration** (`@pythnetwork/hermes-client`) for weighted and realtime prices with confidence intervals, feeding health-factor and margin-requirement (Initial, Maintenance, Equity) calculations.
- **Modeled global state with Zustand** — separate stores for account, banks, oracle prices, config, simulation, token mints, and Address Lookup Table (LUT) data.
- **Designed the tRPC v11 API layer** with type-safe public/protected procedures, Zod validation, and SuperJSON, gated by NextAuth v5 sessions.
- **Modeled app-side data in PostgreSQL + Drizzle ORM** for sessions, posts, and ancillary product data, with `drizzle-kit` push/migrate/studio/seed workflows.
- **Set up NextAuth v5 (beta)** with the Drizzle adapter, Discord provider, and session token invalidation for protected procedures.
- **Built a shared `@repo/ui` design system** with Radix primitives, CVA variants, and `ui-`-prefixed Tailwind classes to prevent host-app class clashes; reused across `web` and `docs`.
- **Codified shared schema, error, and FP utilities** — `@repo/schema-validation` (Zod), `@repo/error-codes`, and `@repo/fp` (`fp-ts`) for consistent error handling across tRPC and on-chain integrations.
- **Set up CI/CD** — GitHub Actions for format, lint, typecheck, and test; Vercel deploys for preview, UAT, and production with manual workflow dispatch.

## Key Achievements

- Delivered a **wallet-native lending and borrowing dApp** on Solana with portfolio, health factor, and position-level actions, all backed by a custom Anchor program.
- Stood up **Pyth Hermes as the pricing source** for weighted and realtime feeds with confidence intervals, feeding margin-requirement and health-factor calculations.
- Shipped a **multi-oracle-setup-aware integration** (Pyth legacy, Switchboard, Pyth Push, staked-with-Pyth-Push) so banks can be onboarded with the right oracle topology.
- Built a **Turborepo monorepo design system** (`@repo/ui` + `@repo/tailwind-config`) with a `ui-` Tailwind prefix, enabling safe reuse across `web` and `docs`.
- Established **end-to-end type safety** from Anchor IDL through tRPC, Zod schemas, and Drizzle, eliminating a class of contract-drift bugs across the stack.
- Codified **store boundaries with Zustand** — account, banks, oracle prices, config, simulation, token mints, LUT — keeping on-chain state and UI concerns cleanly separated.
- Stood up a **CI/CD pipeline** (GitHub Actions + Vercel preview/UAT/prod) with format, lint, typecheck, and test gates on every change.

## Tech & Tools

**Monorepo & build:** Turborepo, pnpm workspaces, dependency catalog in `pnpm-workspace.yaml`.

**Apps:** Next.js 15 (App Router), React 19; separate `web` and `docs` apps.

**Frontend:** Tailwind CSS (shared `@repo/tailwind-config`, `ui-` prefix), Motion, Zustand, Radix UI, CVA.

**Web3 / chain:** Solana (`@solana/web3.js`, SPL Token, Token-2022), Anchor (`@coral-xyz/anchor`), Wallet Adapter (Backpack and others).

**Oracles:** Pyth Hermes (`@pythnetwork/hermes-client`) for weighted and realtime prices with confidence intervals.

**API:** tRPC v11, TanStack Query, Zod, SuperJSON.

**Database:** Drizzle ORM, Drizzle Kit (push, migrate, studio, seed), PostgreSQL.

**Auth:** NextAuth v5 (beta), `@auth/drizzle-adapter`, Discord provider, session token invalidation.

**Shared packages:** `@repo/ui`, `@repo/db`, `@repo/api`, `@repo/auth`, `@repo/utils`, `@repo/schema-validation` (Zod), `@repo/fp` (`fp-ts`), `@repo/constants`, `@repo/error-codes`, `@repo/tailwind-config`, `@repo/typescript-config`, `@repo/eslint-config`.

**Testing:** Jest (presets in repo).

**Tooling:** TypeScript 5.7, ESLint, Prettier.

**CI/CD:** GitHub Actions (format, lint, typecheck, test); Vercel deploy (preview, UAT, production) with manual workflow dispatch.

## Lessons Learned

- _(STAR-style story to add: e.g. how the multi-oracle setup enum (Pyth legacy / Switchboard / Pyth Push / staked-with-Pyth-Push) was abstracted behind a single pricing pipeline, or how Zustand store boundaries evolved to keep on-chain state, oracle prices, simulation, and LUT data cleanly separated.)_

## Notes

_Private context — strip before sharing externally._

- One-liner for resume:
  > **SurroundFi (Solana DeFi)** — Built a full-stack lending/borrowing dApp in a Turborepo monorepo: Next.js 15 + React 19 front end, Solana/Anchor program integration, Pyth Hermes oracles, tRPC API, Drizzle + PostgreSQL, NextAuth, shared UI and schema packages, and GitHub Actions CI/CD with Vercel preview/UAT/prod deployments.
