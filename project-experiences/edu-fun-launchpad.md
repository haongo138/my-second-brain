---
type: Project Experience
role: Full-Stack Engineer
domain: Web3 / EdTech
scope: Small team (2–5)
start_date: TBD
end_date: TBD
status: Shipped
tech_stack: []
related_to: []
---

# edu.fun — University Community Token Launchpad

## Summary

Built **edu.fun**, a university community token launchpad and Web3 education platform that lets students and alumni tokenize school spirit, participate in decentralized seed funding, and access scholarships. Shipped as a Next.js 15 + tRPC app with PostgreSQL/Drizzle, multi-chain wallet integration, a LayerZero cross-chain bridge, staking, and Pump.fun-powered token discovery.

## Problem & Context

Universities lack a Web3-native way to channel school spirit into community funding, scholarships, and student engagement. edu.fun unifies school-verified identity, referral-driven growth, multi-stage fundraising, EVM wallet linking, and cross-chain token movement into one product, while keeping a verified-student moat (email-domain + manual admin verification) so that leaderboards and rewards stay tied to real campus communities.

## My Contributions

- **Designed and shipped the university verification system** — multi-method membership (`auto-by-school-domain`, `manual-approved-by-admin`, `auto-by-partner-domain`, `not-verified`) backed by a large static university domain list, full-text search via `websearch_to_tsquery`, and admin tooling for manual approval.
- **Built the multi-stage fundraising flow** end-to-end: Subscription → Private Round → Community Round → Snapshot → Distribution → Liquidity, with countdowns, tokenomics surfaces, and per-user "My Subscription" state.
- **Implemented EVM wallet linking and deposit handling** with RainbowKit/wagmi/viem — whitelisted-wallet checks, BNB/USDT/EDU deposits across BSC and Educhain, and CoinGecko-driven token pricing.
- **Integrated a LayerZero OFT cross-chain bridge** for the EDU token between BSC, Educhain, and Arbitrum, exposing it as a first-class bridge widget in-app.
- **Modeled the domain in PostgreSQL + Drizzle ORM** under the `edu.fun_*` schema namespace — users, school memberships, universities, referrals, EVM/whitelisted wallets, roles — plus DB views for total/today school member counts, total/verified referral counts, and school-member search.
- **Shipped a username-based referral system** with referral stats (total + verified), share links, and dynamic OG / Twitter images per referral code at `/ref/[code]`.
- **Built the auth + profile stack** on NextAuth v5 (beta) with Google + Resend magic link, Drizzle adapter, disposable-email blocking, and profile fields for LinkedIn / X / school selection (including "other school" support).
- **Integrated public Web3 data sources** — Pump.fun for "For You" coins, candlestick data, holder distribution, and replies; Helius RPC; CoinGecko prices — all behind a typed API client.
- **Established codebase conventions**: lowercase-with-dashes file/folder names, named-exports-only, and `fp-ts`-style result helpers (`run`, `getValue`, `getError`, `isFailed`, `FailedWrappedError`) for consistent error handling in auth and API code.

## Key Achievements

- Delivered a **full-stack Web3 product on Next.js 15 + tRPC v11** spanning verified identity, fundraising, staking, deposits, bridging, and token discovery — all behind a single typed API contract.
- Stood up **school-verified leaderboards and "UniBoard"** using PostgreSQL views and full-text search, enabling fast school-mate discovery by domain, major, and graduation year.
- Operated a **multi-chain footprint** (BSC, Educhain, Arbitrum) with whitelisted-wallet deposit checks and a LayerZero OFT bridge, removing custodial friction for users.
- Shipped **dynamic per-referral OG / Twitter images** that turned every share link into a personalized growth surface.
- Enforced **strict typing and validation across the stack** — TypeScript strict, Zod, `@t3-oss/env-nextjs`, and tRPC + React Query — catching contract drift at compile time.
- Implemented a **role-based admin area** with manual verification workflows, supporting the partner-school onboarding model.

## Tech & Tools

**Framework & language:** Next.js 15 (App Router, Turbopack dev), TypeScript (strict), React 18.

**API:** tRPC v11 with React Query integration.

**Database:** PostgreSQL + Drizzle ORM — `edu.fun_*` schema, migrations, DB views (school member counts, referral counts, member search), full-text search with `websearch_to_tsquery`.

**Auth:** NextAuth v5 (beta) with Drizzle adapter, Google OAuth + Resend magic link, disposable-email blocking.

**Web3:** wagmi, viem, RainbowKit, ethers; LayerZero OFT for the EDU cross-chain bridge (BSC ↔ Educhain ↔ Arbitrum).

**UI:** Tailwind CSS, Radix UI, CVA, react-hook-form + Zod, Embla Carousel, lightweight-charts, @number-flow/react.

**Functional helpers:** `fp-ts`-style result handling (`run`, `getValue`, `getError`, `isFailed`, `FailedWrappedError`).

**Email:** Resend, React Email.

**Storage:** Vercel Blob.

**Validation & types:** Zod, `@t3-oss/env-nextjs`.

**Testing:** Jest, Testing Library.

**Tooling:** pnpm, Prettier, ESLint, TypeScript strict.

**External integrations:** CoinGecko (prices), Pump.fun (tokens, candlesticks, holders, replies), Helius RPC.

## Lessons Learned

- _(STAR-style story to add: e.g. how the school-verification model evolved from email-domain-only to a multi-method system, or trade-offs of adopting tRPC + Drizzle for a Web3 product where chain state lives outside the typed contract.)_

## Notes

_Private context — strip before sharing externally._

- One-liner for resume:
  > **Built edu.fun** — a full-stack university community token launchpad (Next.js 15, tRPC, Drizzle, NextAuth) with university verification, referral system, multi-stage fundraising, EVM wallet linking, cross-chain EDU bridge (LayerZero), staking UI, and Pump.fun token discovery.
