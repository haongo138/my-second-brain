---
type: Project Experience
status: Shipped
related_to:
  - "[[surroundfi]]"
relationships:
  Type:
    - "[[project experience]]"
---

# Eva01 — Real-Time Surroundfi Liquidator on Solana

## Summary

Built **Eva01**, a Rust-based real-time liquidator for the **Surroundfi** lending protocol on Solana. Eva01 streams account and oracle updates via Yellowstone gRPC (Geyser), maintains an in-memory state cache, detects underwater lending accounts, and submits liquidation transactions through Jito bundles for fast inclusion. A built-in rebalancer keeps the liquidator's own account healthy by swapping non-preferred deposits, repaying liabilities, draining token-account dust, and redepositing preferred mints (e.g. USDC). Operational safety is enforced via margin checks, Slack alerts, and optional Prometheus metrics.

## Problem & Context

Liquidations on Solana lending protocols are latency- and precision-sensitive: under-collateralized positions must be detected the instant oracle prices or account state shift, and transactions must land in the right block to capture the liquidation discount before competing bots. Eva01 was designed to solve this end-to-end for **Surroundfi** — combining a real-time Geyser stream, fixed-point health math, multi-oracle support (Pyth Push, Switchboard Pull, Switchboard on-demand via Crossbar), Jito bundle submission, and an autonomous rebalancer that keeps the liquidator's own collateral and liabilities in a target shape so it can keep liquidating profitably without manual intervention.

## My Contributions

- **Architected the pipeline** — Geyser → `GeyserProcessor` (updates cache, sets run flags) → `Liquidator` / `Rebalancer` (consume cache) → `TransactionManager` (builds Jito bundles with compute budget + tip) → `TransactionChecker` (bundle status), coordinated via crossbeam channels and atomic flags.
- **Built the real-time data layer** — Yellowstone gRPC (Geyser plugin) ingestion of Surroundfi accounts, oracle accounts, and token accounts into an in-memory cache, with rayon-parallel RPC bootstrap (program accounts, banks, oracles, token accounts) and optional ATA creation.
- **Implemented liquidation logic** — Detect accounts below maintenance health (bankrupt threshold), compute max liquidatable amount and profit at the 2.5% liquidation discount, and submit liquidation transactions as **Jito bundles** with compute budget + tip for fast inclusion.
- **Built the rebalancer** — Sells non-preferred deposits, repays liabilities, drains token-account dust into the preferred mint (e.g. USDC), and redeposits preferred tokens; integrates the **Sega swap API** for quote + transaction, with Jupiter quote URL configurable, and uses direct RPC with retries and confirmation for swaps.
- **Used `I80F48` fixed-point math** (`fixed` crate) throughout health-factor, collateral, liquidation-amount, and profit-threshold calculations to eliminate float-rounding inconsistencies vs the on-chain program.
- **Multi-oracle support** — Pyth (StakedWithPythPush), Switchboard (Pull), and Switchboard on-demand via a `SwbCranker` that simulates/fetches Crossbar prices before liquidation and rebalance.
- **Codified operational safety** — Stop liquidations when the liquidator's own margin is too low (e.g. health ratio ≤ 50%), Slack webhook alerts for liquidations and rebalance failures, and optional Prometheus counters/histograms with an HTTP endpoint.
- **Group filtering** — Whitelist/blacklist of Surroundfi groups so only targeted groups' accounts are tracked and liquidated.
- **Configurable risk envelope** — Min profit (USD), optional max liquidation value, isolated-banks toggle, preferred mints, dust threshold, and swap slippage (bps), all driven by TOML configs (general, liquidator, rebalancer) plus a CLI setup wizard.
- **Concurrency model** — Tokio async runtime for I/O, crossbeam channels for cross-service handoff, rayon for parallel cache loading, and multi-threaded services for liquidation and rebalance loops.
- **Packaged for deployment** — Multi-stage Docker image (Debian bookworm-slim), GCP workflow, and shell scripts for ops.

## Key Achievements

- Delivered a **production liquidator** that detects, prices, and submits liquidations end-to-end in real time, capturing the 2.5% liquidation discount at competitive latency via Jito bundles.
- Built an **autonomous rebalancer** that keeps the liquidator's account in a target shape (preferred mint deposits, drained dust, repaid liabilities) so the bot can run unattended.
- Stood up a **multi-oracle pricing layer** (Pyth Push, Switchboard Pull, Switchboard on-demand via Crossbar) with a cranker that simulates prices before risky actions.
- Eliminated float-rounding drift vs the on-chain program by using **`I80F48` fixed-point math** for all health, collateral, and profit calculations.
- Designed a **clean pipeline** (Geyser → cache → liquidator/rebalancer → transaction manager → checker) using crossbeam channels and atomic run-flags, keeping I/O, decision, and submission concerns separated.
- Codified **operational safety** — margin-aware liquidation gating, Slack webhook alerts for liquidations and rebalance failures, and optional Prometheus metrics for observability.
- Containerized for **GCP deployment** with a multi-stage Docker build and shell-script ops glue.

## Tech & Tools

**Language:** Rust (edition 2021).

**Blockchain:** Solana SDK 1.18, Anchor (from `mrgnlabs`), Surroundfi mainnet client (`no-entrypoint`).

**Real-time data:** Yellowstone gRPC (Geyser plugin) for account and oracle streams.

**Transaction submission:** Jito block engine (bundles with compute budget + tip), Solana RPC for swap and confirmation paths.

**Swap / rebalancing:** Sega swap API (quote + transaction); Jupiter quote URL configurable.

**Oracles:** Pyth (StakedWithPythPush), Switchboard (Pull), Switchboard on-demand (Crossbar simulation via `SwbCranker`).

**Math:** `fixed` crate (`I80F48`) for health, collateral, liquidation amounts, and profit thresholds.

**Concurrency:** Tokio (async), crossbeam channels, rayon (parallel cache load), multi-threaded services.

**Config:** TOML (general, liquidator, rebalancer) + CLI setup wizard.

**Observability:** `env_logger`, Slack webhooks, Prometheus counters/histograms with optional HTTP endpoint.

**Deployment:** Docker (multi-stage, Debian bookworm-slim), GCP workflow, shell scripts.

## Lessons Learned

- _(STAR-style story to add: e.g. how `I80F48` fixed-point math closed a drift gap vs the on-chain program that float math couldn't, or how the Geyser → cache → liquidator/rebalancer → transaction-manager → checker pipeline evolved from a monolithic loop into channel-coordinated services to keep latency and safety guarantees clean.)_

## Notes

_Private context — strip before sharing externally._

- One-liner for resume:
  > **Eva01 (Solana liquidator)** — Built a Rust-based real-time liquidator for the Surroundfi lending protocol on Solana: Yellowstone gRPC for account/oracle streams, in-memory state cache, `I80F48` fixed-point liquidation math, Jito bundle submission, and an automated rebalancer using the Sega swap API with Slack alerts and optional Prometheus metrics.
