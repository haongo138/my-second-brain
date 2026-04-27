---
type: Project Experience
role: Protocol Engineer
domain: Web3 / DeFi
scope: Small team (2–5)
start_date: TBD
end_date: TBD
status: Shipped
tech_stack: []
related_to:
  - "[[surroundfi]]"
---
# SurroundFi Protocol — On-Chain Lending Protocol on Solana

## Summary

Contributed to the **on-chain SurroundFi protocol** (Marginfi v2-style) — a Solana-based decentralized lending and borrowing platform written in Rust/Anchor. Users open margin accounts under a marginfi group, deposit collateral, and borrow across up to 16 supported assets (SOL, USDC, USDT, wBTC, ETH (Portal), BONK) with deterministic, oracle-driven risk and health-factor liquidations. The workspace ships multiple programs (marginfi core, liquidity-incentive-program, mocks, brick, test transfer hooks), a Rust CLI, an indexer, and Dataflow ETLs into BigQuery — plus verifiable builds, fuzz-tested accounting, and mainnet + staging deployments.

## Problem & Context

DeFi lending protocols live or die on the correctness of their risk math and the reliability of their liquidations. SurroundFi's design draws the lines explicitly: a **marginfi group** owns a lending pool of **banks** (each bank = mint + oracle + risk parameters), users hold **margin accounts** that aggregate balances across banks, and a **deterministic risk engine** evaluates health using oracle-driven asset/liability weights. Real-time liquidations use the maintenance margin against a real-time oracle price; isolated risk tiers limit contagion from long-tail assets; flash loans (start/end instructions) enable in-protocol arbitrage; and a Liquidity Incentive Program (LIP) escrows rewards for time-locked deposits. The protocol must also support staked collateral via SPL Single Pool, Token-2022 with transfer hooks, and emissions/fees at both bank and program level — all while remaining auditable, verifiable, and fuzz-tested against actual token balances.

## My Contributions

- **Worked in the multi-program Anchor workspace** — `marginfi` core, `liquidity-incentive-program`, plus `mocks`, `brick`, and `test_transfer_hook` programs sharing Anchor/Solana workspace dependencies.
- **Implemented lending primitives** — deposit, borrow, repay, withdraw, and health-check accounts, with asset/liability weights and group/bank-level LTV.
- **Built deterministic risk and liquidation logic** — health-factor evaluation using real-time oracle prices for maintenance margin, with on-chain liquidation paths that protect pool solvency.
- **Used** `I80F48` **fixed-point math** (`fixed` crate) for rates, weights, and risk calculations to eliminate float-rounding drift across deposits, withdraws, interest accrual, and liquidations.
- **Integrated Pyth as the primary oracle** with Switchboard support, plus oracle setup variants (legacy, push, staked-with-push) per bank.
- **Supported Token-2022 and transfer hooks** alongside SPL Token, including a `test_transfer_hook` program for end-to-end hook testing.
- **Implemented flash loans** as paired start/end instructions for in-protocol arbitrage and leveraged strategies.
- **Built the Liquidity Incentive Program (LIP)** — permissionless campaigns with fixed/minimum yield, lock-up periods, and rewards escrowed at creation, integrated with marginfi deposits.
- **Added staked-collateral support** via SPL Single Pool (Solana Foundation), enabling staked SOL and similar assets as collateral.
- **Modeled emissions and fees** — configurable per-bank emissions, bank fee collection, insurance and fee withdrawal, and global program fee state.
- **Wrote fuzz tests** that validate protocol accounting (deposit, withdraw, liquidate, accrue interest, oracle update, bankruptcy) against actual token balances to catch invariant violations.
- **Built the Rust CLI** (`marginfi-cli`) for managing groups, banks, accounts, and Pyth oracle lookups.
- **Stood up the observability stack** — Rust indexer for chain data, Google Dataflow (Python) ETLs into BigQuery, and PagerDuty alerting.
- **Shipped verifiable builds** via Ellipsis Labs `solana-verify` for both mainnet and staging deployments, with overflow checks and LTO in the release profile.

## Key Achievements

- Delivered an **on-chain lending protocol** with margin accounts, multi-asset borrowing across up to 16 assets, and deterministic oracle-driven liquidations.
- Built **fuzz-tested accounting** that validates deposit, withdraw, liquidate, interest accrual, oracle update, and bankruptcy flows against real token balances — closing whole classes of invariant bugs before audit.
- Shipped **flash loans** as paired start/end instructions, enabling in-protocol arbitrage and leveraged strategies without trusting external relayers.
- Built the **Liquidity Incentive Program (LIP)** with permissionless campaigns, fixed/minimum yield, lock-ups, and pre-escrowed rewards integrated with marginfi deposits.
- Added **staked collateral** via SPL Single Pool so staked SOL and similar assets can serve as collateral without unstaking.
- Stood up an **observability pipeline** — Rust indexer + Google Dataflow ETLs into BigQuery + PagerDuty — for protocol-level monitoring and alerting.
- Shipped **verifiable builds** with Ellipsis Labs `solana-verify` for mainnet and staging, supporting independent build reproduction.
- Codified **risk tiers** — collateral vs isolated — so long-tail assets can be onboarded without polluting the collateral set.

## Tech & Tools

**Chain / runtime:** Solana (SVM), Anchor 0.30.1, Solana 2.1.x, x86_64 builds for ABI stability.

**Programs (Rust):** `marginfi`, `liquidity-incentive-program`, `mocks`, `brick`, `test_transfer_hook`.

**Oracles:** Pyth (primary), Switchboard (present/planned), with oracle setup variants per bank.

**Tokens:** SPL Token, Token-2022, transfer hooks, SPL Single Pool (staking).

**Math / precision:** `I80F48` fixed-point math (`fixed` crate) for rates and risk.

**Testing:** Rust `cargo test-bpf`, inline unit tests; Anchor TypeScript/Mocha (`ts-mocha`), `anchor test`, bankrun; fuzz tests for accounting invariants.

**Clients & tooling:** TypeScript client SDK (`@mrgnlabs/marginfi-client-v2`), Rust CLI (`marginfi-cli`).

**Observability:** Rust indexer, Google Dataflow (Python) ETLs into BigQuery, PagerDuty alerting.

**Verification & build:** Ellipsis Labs verifiable builds (`solana-verify`), overflow checks and LTO in release profile.

**Deployments:** Mainnet and staging; distinct LIP and marginfi program IDs; optional staked-collateral and SPL Single Pool deployment.

## Lessons Learned

- *(STAR-style story to add: e.g. how fuzz-testing protocol accounting against actual token balances surfaced an invariant violation that unit tests missed, or how the marginfi-group → lending-pool → bank hierarchy with collateral vs isolated risk tiers evolved to safely onboard long-tail assets without contaminating the core collateral set.)*

## Notes

*Private context — strip before sharing externally.*

- Companion note: [[SurroundFi — Solana DeFi Lending & Borrowing Protocol]] covers the full-stack dApp (Next.js + tRPC + Drizzle) that consumes this protocol.
- One-liner for resume:

> **SurroundFi Protocol (Solana, Marginfi v2-style)** — Contributed to a Solana-based decentralized lending protocol (Anchor/Rust): margin accounts, multi-asset borrowing, deterministic risk engine and liquidations, flash loans, Pyth/Switchboard oracles, fixed-point (I80F48) math, and fuzz-tested accounting; tooling included Rust CLI, indexer, Dataflow ETLs into BigQuery, and verifiable builds.
