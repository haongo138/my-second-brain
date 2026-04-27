---
type: Project Experience
role: Senior Full-Stack Engineer
domain: Creator Economy / Web3 / Livestreaming
scope: Small team (2–5)
start_date: TBD
end_date: TBD
status: Ongoing
tech_stack: []
related_to:
---

# Stream — Creator–Audience Livestream Engagement Platform

## Summary

Built a creator–audience livestream engagement platform with in-stream rewards, multi-platform livestream aggregation (YouTube / Twitch / Twitter Spaces), and a brand–creator campaign product (StreamFrens). Shipped as a Turborepo monorepo spanning a Next.js web app, 20+ Firebase Cloud Functions, a Chrome extension, Solidity smart contracts on Base, and a separate Postgres-backed campaign service.

## Problem & Context

Creators need lightweight tools to engage and reward live audiences across fragmented platforms (YouTube, Twitch, Twitter Spaces), and brands want a structured way to run creator campaigns. The platform unifies "who's live" discovery, in-stream gamified rewards (Stream Drops), gasless on-chain reward claims, and a brand campaign workflow — all from a single product surface, while balancing real-time Firestore-driven UX against relational campaign data and on-chain settlement.

## My Contributions

- **Scaled a Turborepo monorepo** with multiple apps (web, docs, Chrome extension) and 15+ shared packages (UI, hooks, schema-validation, firebase-utils, contracts), enabling consistent patterns across web and extension surfaces.
- **Designed and shipped the Stream Drops reward system**: in-stream games (trivia, whack-a-mole), score submission, automated/on-demand drops, and **ERC-1155 token claims on Base** with **gasless UX** via Alchemy Account Abstraction and Gas Manager policies.
- **Architected 20+ event-driven Firebase Cloud Functions** (Firestore triggers, scheduled jobs, callable/HTTP) with **isolated monorepo deploys** using `firebase-tools-with-isolate`, plus Cloud Tasks for async workflows.
- **Built creator discovery and livestream aggregation** across YouTube, Twitch, and Twitter Spaces — feed ingestion, live-state inference, platform-status sync, and a synced `discover-creators` index in Algolia powering search and filters.
- **Developed Solidity smart contracts** (Foundry, OpenZeppelin): Stream Points ERC-1155 with EIP-712 claim signing, TransparentUpgradeableProxy upgrade path, deploy/upgrade scripts, and ABI export to the frontend.
- **Built StreamFrens, the brand–creator campaign platform**, on **Drizzle ORM + PostgreSQL** (campaigns, invites, content approval, categories) running alongside Firestore-based product data.
- **Stood up a k6 load-testing pipeline** for Cloud Functions (e.g. `claimStreamDrop`) with seed pipelines and DB cleanup, surfacing scaling issues before launch.
- **Shipped a Chrome extension** for stream overlay and in-stream game integration (e.g. CIMU games), reusing hooks, UI components, and Zod schemas from the web app.

## Key Achievements

- Delivered **gasless ERC-1155 reward claims on Base** end-to-end — game → score → EIP-712 signing → Alchemy AA paymaster — removing crypto-onboarding friction for non-crypto fans.
- Unified live-state across **3 streaming platforms** (YouTube, Twitch, Twitter Spaces) into a single creator feed and Algolia-backed discovery index.
- Operated **20+ Firebase Cloud Functions** with isolated monorepo deploys, eliminating the "deploy the whole repo" tax and keeping function packages slim.
- Ran **two distinct datastores side-by-side** (Firestore for real-time product state, Postgres + Drizzle for relational campaign data) with clear ownership boundaries.
- Established **shared Zod schemas, feature flags, error codes, and Amplitude tracking** as cross-app contracts used by both the web app and Chrome extension.
- Smart contracts deployed to Base with **upgradeable proxy** pattern, supporting iterative reward-mechanic changes without redeploying token state.

## Tech & Tools

**Monorepo & build:** Turborepo, pnpm workspaces, Changesets, ESLint, Prettier, Husky, commitlint.

**Frontend:** Next.js 14, React 18, Tailwind CSS, shared `@repo/ui`, Storybook.

**Auth & identity:** Firebase Auth, Next-Auth 5, Dynamic Labs (wallet / smart accounts), linked Twitter / Twitch / YouTube via dedicated Cloud Functions.

**Backend:** Firebase (Firestore, Cloud Functions 2nd gen, Node 20), `firebase-tools-with-isolate` for monorepo deploy, Cloud Tasks for async jobs.

**Blockchain:** Solidity 0.8.26, Foundry, OpenZeppelin (ERC-1155, upgradeable proxy), Stream Points ERC-1155 on Base, Alchemy Account Abstraction + Gas Manager.

**Search:** Algolia (`discover-creators` index for creator search/filters).

**Databases:** Firestore (primary product data), Drizzle ORM + PostgreSQL (StreamFrens: brands, campaigns, creator_campaigns).

**Validation & types:** TypeScript, Zod (shared `@repo/schema-validation`).

**Analytics & ops:** Amplitude, Sentry, feature flags, structured error codes.

**Load testing:** k6, custom seed/cleanup pipelines.

**Extension:** Chrome extension (Vite, React), shared packages with the web app.

## Lessons Learned

- _(STAR-style story to add: e.g. trade-offs of running Firestore + Postgres in one product, or how the monorepo deploy strategy evolved.)_

## Notes

_Private context — strip before sharing externally._

- One-liner for resume:
  > **Stream (Creator–audience livestream platform)** — Turborepo monorepo (Next.js, 20+ Firebase Cloud Functions, Chrome extension); multi-platform livestream aggregation (YouTube/Twitch/Twitter Spaces); stream-drop rewards with ERC-1155 on Base and gasless claims (Alchemy AA); Algolia + Firestore creator discovery; StreamFrens campaigns on Drizzle/PostgreSQL; Solidity/Foundry smart contracts; k6 load testing.
