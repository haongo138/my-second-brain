---
type: Project Experience
role: Backend / Bot Engineer
domain: Web3 / Payments / Discord Tooling
scope: Small team (2–5)
start_date: TBD
end_date: TBD
status: Shipped
tech_stack: [TypeScript, discord.js, Node.js, Kafka, Redis, Canvas, Ethers.js, Solana, TON]
related_to: [mochi-web]
---
# Mochi Discord — Multi-Chain Crypto Bot for Discord Communities

## Summary

Built and maintained **Mochi Discord**, a TypeScript Discord bot serving Web3 communities with crypto tipping, wallet management, airdrop campaigns, NFT tracking, DeFi tooling, price alerts, and social features (kudos, feed, inbox) — all backed by the Mochi Pay and Mochi API services, a Kafka event queue, Redis caching, and server-side Canvas image generation for rich embed responses.

## Problem & Context

Web3 communities live in Discord, but existing bots force users to leave for a browser or CEX just to tip a friend, check a portfolio, or claim an airdrop. Mochi's goal was to bring the entire payments and DeFi surface into Discord — tip with any token, manage wallets across EVM/Solana/TON, run airdrops, get price alerts, and track NFT portfolios — without ever leaving the server.

The codebase had to support 30+ command categories across slash and text command surfaces, stay type-safe against multiple evolving backend services, handle high interaction throughput via Kafka, and generate server-side images (charts, QR codes, canvases) for embed-rich responses — all in a single Node.js process deployed to GKE.

## My Contributions

- **Designed and implemented the command architecture** — each command category structured into `slash.ts` (Discord interaction definition), `processor.ts` (reusable business logic), and optional `text.ts` (text-prefix variant), allowing the same logic to serve both interaction and message-based invocations.
- **Built the adapter layer** — typed HTTP clients for Mochi API, Mochi Pay, Profile Indexer, DeFi, and Pod Town services using a custom `fetcher` abstraction with retry logic, giving the rest of the codebase a stable interface against backend drift.
- **Implemented multi-chain wallet features** — balance display, deposit, withdrawal, and transfer commands wired to Ethereum (ethers.js), Solana (`@solana/web3.js`, SPL tokens), and TON (`@ton/core`) with address validation and on-chain confirmation flows.
- **Shipped airdrop and reward campaigns** — time-bound airdrop creation and claim flows, wired to Mochi Pay, with countdown embeds and post-claim UX.
- **Built price alert and market data commands** — configurable price alerts (above/below threshold), token heatmaps, and gainers/losers views backed by the DeFi adapter.
- **Developed server-side image generation** — Canvas + Chart.js pipeline (`chartjs-node-canvas`) for portfolio charts, sparklines, and QR code embeds, keeping visual responses self-contained without external image hosts.
- **Integrated Kafka for async event processing** — producer/consumer queue (`kafkajs`) for tip notifications, airdrop events, and cross-platform activity feed updates, decoupling Discord interactions from slow downstream side-effects.
- **Wired Unleash feature flags** — conditional feature rollout for commands and UI variants, with automatic slash command re-sync when flags change in production.
- **Set up structured logging and error tracking** — Pino for structured logs piped to Discord alert/log channels, Sentry for production error aggregation, and custom error hierarchy for domain-specific handling.
- **Maintained deployment pipelines** — multi-stage Docker builds (Node 18 Alpine + native canvas deps), GitHub Actions for test/lint/CodeQL, and GKE deploy workflows for dev, preview, and production environments, with semantic-release for automated versioning.
- **Implemented social commands** — kudos giving, inbox notifications, community feed management, and cross-platform profile resolution (Discord, Telegram) via `@consolelabs/mochi-formatter` and `@consolelabs/mochi-rest`.

## Key Achievements

- Unified **three chain ecosystems (EVM, Solana, TON)** in a single bot surface, so users never need to specify chain context for wallet and payment commands.
- Kept **30+ command categories** maintainable through a consistent `slash / text / processor` separation, making business logic reusable and independently testable.
- Shipped **server-side Canvas image generation** for charts and portfolio views, making Discord embeds visually distinctive without relying on external render services.
- Established **Kafka-backed async processing** for tip and airdrop events, preventing Discord interaction timeouts on slow downstream operations.
- Built a **typed adapter layer** across five backend services (Mochi API, Mochi Pay, Profile, DeFi, Pod Town) that gave the bot compile-time safety against API contract changes.
- Delivered **GKE multi-environment pipelines** (dev / preview / prod) with semantic-release, enabling rapid iteration and safe production deployments.

## Tech & Tools

**Runtime:** Node.js 18, TypeScript 4.4, Vite 4 (build + dev execution via `vite-node`).

**Discord:** discord.js 13, `@discordjs/builders`, `@discordjs/rest` — slash commands, buttons, select menus, message embeds.

**Chains & wallets:** ethers.js 5 (EVM), `@solana/web3.js` + `@solana/spl-token` (Solana), `@ton/core` (TON), `@noble/ed25519` / `@noble/hashes` (cryptography), tweetnacl.

**API layer:** `@consolelabs/mochi-rest` (primary API wrapper), `wretch` / custom fetcher, typed adapters for Mochi Pay, Profile Indexer, DeFi, ecocal, Chotot.

**Async & cache:** kafkajs (Kafka producer/consumer), ioredis (Redis), node-cache (in-memory).

**UI / graphics:** Canvas 2, Chart.js 3 + `chartjs-node-canvas`, QR-code, `@consolelabs/mochi-formatter`, `@consolelabs/mochi-ui`.

**Observability:** Pino + pino-pretty (structured logs → Discord channels), Sentry 7.

**Feature flags:** Unleash 5.

**Testing:** Jest 27, ts-jest.

**Deploy:** Docker (multi-stage, Alpine), GitHub Actions (test / commitlint / CodeQL / GKE deploy), semantic-release, Lefthook (pre-commit).

## Lessons Learned

- *(STAR-style story to add: e.g. how the Kafka queue was introduced to fix Discord interaction timeout issues under airdrop load, or the tradeoffs of server-side Canvas rendering vs. external image services for bot embeds.)*

## Notes

*Private context — strip before sharing externally.*

- One-liner for resume:

> **Mochi Discord** — Built and maintained a multi-chain crypto Discord bot (TypeScript, discord.js v13) with 30+ command categories covering tipping, wallet management (EVM/Solana/TON), airdrops, price alerts, and NFT tracking; Kafka-backed async processing, Redis caching, server-side Canvas image generation, typed adapters against Mochi Pay/Profile APIs, and GKE deployment pipelines.
