---
type: Note
status: Active
---

# SurroundFi

The **SurroundFi** ecosystem — a Solana-based decentralized lending and borrowing platform (Marginfi v2-style) — spans three distinct deliverables I contributed to. This hub note groups them so the wider context is one click away from any single entry.

## Components

- [[SurroundFi Protocol — On-Chain Lending Protocol on Solana]] — The on-chain protocol itself: multi-program Anchor/Rust workspace (`marginfi`, `liquidity-incentive-program`, mocks, brick, test transfer hooks), deterministic risk engine, flash loans, fixed-point (`I80F48`) math, fuzz-tested accounting, Rust CLI, and verifiable builds.
- [[SurroundFi — Solana DeFi Lending & Borrowing Protocol]] — The full-stack dApp that consumes the protocol: Next.js 15 + React 19 frontend, tRPC API, Drizzle + PostgreSQL, NextAuth, Pyth Hermes oracle pricing, Zustand stores, and the Turborepo monorepo.
- [[Eva01 — Real-Time Surroundfi Liquidator on Solana]] — The off-chain Rust liquidator: Yellowstone gRPC streaming, in-memory state cache, Jito bundle submission, Sega-swap-powered rebalancer, and Slack/Prometheus observability.

## How they fit together

```
                      ┌──────────────────────────────┐
                      │   SurroundFi Protocol        │
                      │   (Anchor programs on-chain) │
                      └──────────────┬───────────────┘
                                     │
                ┌────────────────────┼────────────────────┐
                ▼                                         ▼
   ┌──────────────────────────┐              ┌──────────────────────────┐
   │   SurroundFi dApp        │              │   Eva01 Liquidator       │
   │   (user-facing UI)       │              │   (real-time keeper bot) │
   └──────────────────────────┘              └──────────────────────────┘
```

The **protocol** defines the rules (banks, margin accounts, risk weights, liquidation paths). The **dApp** is how end users lend, borrow, and manage positions against it. **Eva01** is an autonomous keeper that watches the same chain state and liquidates underwater positions to protect pool solvency.

## CV framing

These are kept as separate Project Experience notes because they showcase distinct skill sets:

- **Protocol** — Rust/Anchor smart-contract engineering, fuzz-tested protocol accounting
- **dApp** — Full-stack TypeScript / Web3 frontend, monorepo + CI/CD
- **Eva01** — Rust real-time systems, MEV/keeper bot architecture

See the `surroundfi` saved view for the grouped list.
