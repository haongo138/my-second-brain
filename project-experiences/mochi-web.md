---
type: Project Experience
role: Frontend Engineer
domain: Web3 / Payments
scope: Small team (2–5)
start_date: TBD
end_date: TBD
status: Shipped
tech_stack: []
related_to: []
---

# Mochi Web — Multi-Chain Crypto Tipping & Payments Frontend

## Summary

Built and maintained **Mochi Web** (mochi.gg), the Next.js front end for **Mochi**, a multi-chain crypto tipping and payments product spanning **EVM, Solana, Sui, and Ronin**. Shipped a unified wallet-connect flow, shareable pay links, time-bound airdrops, an interactive tip-network force graph, a profile dashboard, and edge-rendered OG images for transfers and pay links — all backed by typed API clients generated from the Mochi Pay and Mochi Profile Swagger schemas.

## Problem & Context

Crypto tipping and payments only feel native when the user doesn't have to think about which chain they're on. Mochi spans EVM, Solana, Sui, and Ronin, with identities that resolve from Discord, Telegram, email, and on-chain addresses — so the front end has to abstract over wallet ecosystems, render cross-platform profiles consistently, and keep share surfaces (pay links, transfers, airdrops) fast and visually distinctive. The codebase had to stay safe across multiple Mochi backend services while serving both a marketing site and a product surface from a single Next.js app.

## My Contributions

- **Built a unified multi-chain wallet abstraction** — a single `WalletProvider` composing Sui → EVM → Solana providers, with one connect modal that handles wallet listing, QR pairing, and platform-specific connectors (MetaMask, wallet-adapter, @suiet/wallet-kit).
- **Shipped pay links and transaction surfaces** — `/pay/[pay_code]` and `/tx/[id]` flows, plus "Pay Me" and gift flows, wired to typed Mochi Pay and Mochi APIs through `wretch`.
- **Implemented airdrop campaigns** — time-bound joins keyed by join ID, countdown UX, and post-expiry redirect to pay links.
- **Built the tip-network visualization** — an interactive 2D force graph (`react-force-graph-2d`) of transaction flows between profiles, rendered with `@consolelabs/mochi-ui` for cross-platform profile display (`UI.render(Platform.Web, node.profile)`).
- **Designed edge-rendered OG image APIs** — `/api/transfer-og` and `/api/pay-og` on Vercel Edge with custom fonts and gradient themes, generating share cards for transfers and pay links.
- **Generated and integrated typed API clients** from the Mochi Pay and Mochi Profile Swagger schemas (`mochi-schema`, `mochi-profile-schema`), used end-to-end across stores and the API layer for compile-time safety against backend drift.
- **Modeled global state with Zustand** — separate stores for auth, profile, pay-request, and dashboard — paired with SWR for server state and `react-hook-form` for form handling.
- **Built the profile dashboard** with a reusable component library (documented at `mochi.gg/dashboard/_components`), plus Discord guild/server management and activity views.
- **Shipped the marketing surface** — homepage with a typed hero (Typed.js), feature sections, API integration showcase, chain/partner sections, developer docs, changelog, ToS, and privacy.
- **Set up an HTTPS-on-localhost dev workflow** (`pnpm dev:https` running `local-ssl-proxy` + Next dev) so wallet connectors that require a secure origin (e.g. mobile QR pairing) work end-to-end in development.
- **Established import aliases** (`~app`, `~components`, `~store`, `~utils`, `~envs`, `~cpn`) for consistent module resolution across the codebase.
- **Integrated Discord and Telegram** as first-class identity sources — guild/icon resolution, Telegram connect and deep links — surfaced through profile and tip UX.

## Key Achievements

- Unified **four chain ecosystems (EVM, Solana, Sui, Ronin)** behind a single connect flow, keeping the product chain-agnostic from the user's perspective.
- Established **Swagger-driven type safety** between the front end and Mochi Pay / Mochi Profile backends, eliminating a class of integration bugs as backend contracts evolved.
- Shipped **edge-rendered share cards** for transfers and pay links (Vercel Edge + custom fonts), making every Mochi transaction a self-promoting share surface.
- Built the **tip-network force graph** as a visual identity for the product, rendering cross-platform profiles consistently via `@consolelabs/mochi-ui`.
- Stood up a **secure-origin dev environment** that supported real wallet pairing (including mobile) on localhost, removing friction for cross-chain wallet debugging.
- Delivered both the **marketing site and product surface** from one Next.js app while keeping concerns cleanly separated through alias-based imports and Zustand store boundaries.

## Tech & Tools

**Framework:** Next.js 13 (Pages Router), React 18.

**Language:** TypeScript 4.9.

**Styling:** Tailwind CSS, `class-variance-authority`, `clsx`.

**State & data:** Zustand (auth, profile, pay-request, dashboard), SWR for server state, `react-hook-form` for forms.

**Chains & wallets:** wagmi (EVM), `@solana/wallet-adapter-*` (Solana), `@suiet/wallet-kit` (Sui), ethers, `@solana/web3.js`.

**API client:** `wretch` against typed Mochi Pay, Mochi Profile, and Mochi APIs; types generated via `swagger-typescript-api` (`mochi-schema`, `mochi-profile-schema`).

**UI components:** `@consolelabs/mochi-ui`, `@consolelabs/ui-components`, Headless UI, `@dwarvesf/react-hooks`, `@dwarvesf/react-utils`.

**Visualization:** `react-force-graph-2d` (tip network), sparklines, `dom-to-image`.

**OG / images:** `@vercel/og` (edge runtime), `sharp`, `next/image` with remote Discord CDN.

**Dev & docs:** Storybook 7, ESLint, Prettier, conventional commits.

**Deploy:** Vercel (preview on PR, production on merge to master).

## Lessons Learned

- _(STAR-style story to add: e.g. how the unified `WalletProvider` evolved to compose Sui, EVM, and Solana ecosystems behind one connect modal, or why OG image generation was moved to Vercel Edge with custom fonts.)_

## Notes

_Private context — strip before sharing externally._

- One-liner for resume:
  > **Mochi Web (mochi.gg)** — Built and maintained the Next.js front end for a multi-chain crypto tipping and payments product (EVM, Solana, Sui), including wallet connect (wagmi/Solana/Sui), pay links, airdrops, tip network force-graph visualization, profile dashboard, and OG image generation (Vercel Edge); TypeScript, Tailwind, Zustand, SWR, and typed APIs from Swagger.
