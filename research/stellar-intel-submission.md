# Stellar Intel — Stellar Wave Research Submission

## Project Selected

- **Project Name:** Stellar Intel
- **Developer:** Evan Ezedike
- **Wave Source:** `ezedike-evan/stellar-intel` — Stellar Wave Program participant
- **Domain:** Infrastructure / DeFi / Payments
- **Website:** https://stellar-intel.vercel.app
- **Repository:** https://github.com/ezedike-evan/stellar-intel
- **Documentation:** https://github.com/ezedike-evan/stellar-intel/tree/main/docs

## Why This Matches the Task

Stellar Intel is an active Stellar Wave Program project that solves a critical problem in the Stellar ecosystem: finding the best rates for off-ramp transactions reliably. It serves as the execution layer for stablecoin value on Stellar by aggregating live quotes from multiple anchors, tracking anchor reputation on-chain via Soroban smart contracts, and enabling non-custodial transaction execution. With 153 commits, comprehensive test coverage, and active development, the project demonstrates mature infrastructure thinking — exactly what the Stellar Wave Program exists to support. The project was not previously submitted to the Hub at the time of this submission.

## Project Overview

Stellar Intel is a **rate aggregator and execution layer** for the Stellar ecosystem that directly addresses three fundamental problems in cross-border remittances:

1. **Rate Discovery:** Which anchor offers the best rate right now?
2. **Quote Reliability:** Will the anchor honor the rate when the transaction is signed?
3. **Operational Status:** Is the anchor actually up and functioning?

The platform treats off-ramps as signed intentions: _"withdraw $100 USDC to this NGN account, at or better than this rate, before this deadline"_ — and intelligently routes them to the anchor most likely to satisfy the terms. By recording every quote, fill, failure, and settlement latency to an on-chain Soroban contract, Stellar Intel creates a public, verifiable reputation oracle that incentivizes quality service and makes the ecosystem more resilient.

## Stellar Integration Details

### Live Deployment
- **Mainnet:** https://stellar-intel.vercel.app (production-live)
- **Network:** Stellar Mainnet (Testnet also supported)
- **Horizon Integration:** Direct connection to Stellar Horizon API for transaction submission and verification
- **Wallet Support:** Freighter wallet integration for user transaction signing

### SEP Standard Compliance
- **SEP-1:** Real stellar.toml resolution for anchor discovery (6-anchor test suite)
- **SEP-10:** Web authentication with JWT caching by (anchorId, publicKey)
- **SEP-24:** Interactive off-ramp withdrawal via iframe with transaction polling
- **SEP-38:** Live quote aggregation with fee breakdown and multi-anchor comparison

### On-Chain Components
- **Soroban Reputation Oracle:** Records every transaction (quote, fill, settlement latency) for anchor performance tracking
- **Intent Router:** Analyzes quotes from multiple anchors and routes to best match
- **MCP Server:** Model Context Protocol interface for AI agents to access routing and oracle primitives

## Technical Stack

- **Framework:** Next.js 16 with React 19 and TypeScript
- **Blockchain:** `@stellar/stellar-sdk` v14.6.1, `@stellar/freighter-api` v6.0.1
- **Styling:** Tailwind CSS v4
- **Data Fetching:** SWR (Stale While Revalidate)
- **Testing:** Vitest with comprehensive coverage
- **Code Quality:** ESLint, Prettier, TypeScript strict mode

## Development Status

### Maturity Metrics
- **Total Commits:** 153+ commits showing substantial development
- **Current Version:** 0.1.0 (active pre-release)
- **Recent Activity:** Active development with commits through 2025
- **Repository Health:** Excellent (comprehensive tests, CI/CD, conventional commits)

### Test Coverage
- Unit tests for rate ranking, fee calculation, and SEP standards
- Component tests for wallet integration and UI
- Property-based tests for rate computation invariants
- Integration tests for 6-anchor SEP-1 resolution
- MSW mock service worker integration testing

### Code Quality Standards
- ESLint with strict configuration (max-warnings: 0)
- TypeScript strict mode for type safety
- Prettier automated formatting
- Conventional commit format
- Husky pre-commit hooks

## Why This Project Matters

### Problem Context
Moving money across borders on Stellar is still risky for users:
- Rates drift between when they're quoted and when transactions are signed
- Anchors fail silently — users don't find out for 40 minutes
- No visibility into which anchors are actually reliable

### Solution Impact
Stellar Intel solves all three problems simultaneously through:
1. **Intent-Based Routing:** Locks in rates at signing, preventing slippage
2. **Reputation Oracle:** Makes anchor performance public and on-chain verifiable
3. **Real-Time Monitoring:** Provides operational status visibility across the ecosystem

This directly advances the Stellar Wave Program's mission by making Stellar the most reliable and transparent corridor for cross-border remittances globally.

## Stellar Wave Program Alignment

**Foundational Infrastructure:** Stellar Intel is core ecosystem plumbing that any Stellar-based payment application can leverage as a rate aggregator and reputation oracle.

**Economic Resilience:** By transparently tracking anchor performance on-chain, the project strengthens the entire Stellar corridor through accountability and quality incentives.

**User Empowerment:** Non-custodial design ensures users maintain full control while benefiting from algorithmic rate optimization.

**Developer Accessibility:** Open-source codebase, comprehensive documentation, SDK, and MCP server enable other projects to build on Stellar Intel's routing primitives.

**Ecosystem Growth:** By solving the "cheapest and most reliable anchor" problem, Stellar Intel reduces friction in cross-border remittances and accelerates adoption in key corridors (Africa, Latin America, Southeast Asia).

## Key Documentation

All documentation is available in the repository:
- **Architecture:** [docs/ARCHITECTURE.md](https://github.com/ezedike-evan/stellar-intel/blob/main/docs/ARCHITECTURE.md) — Technical deep dive into intent routing, oracle, and agent interfaces
- **Proposal:** [docs/PROPOSAL.md](https://github.com/ezedike-evan/stellar-intel/blob/main/docs/PROPOSAL.md) — Stellar Wave grant proposal and vision statement
- **Roadmap:** [docs/ROADMAP.md](https://github.com/ezedike-evan/stellar-intel/blob/main/docs/ROADMAP.md) — Detailed feature roadmap and milestones

## Submission Data

- **Hub Submission Category:** Infrastructure
- **Primary Tags:** `stellar-wave`, `defi`, `payments`, `rate-aggregator`, `soroban`, `sep-24`, `sep-38`, `anchor`, `remittances`, `cross-border`
- **Description:** Stellar Intel is the execution layer for stablecoin value on Stellar — an intent-based rate aggregator that compares off-ramp fees across anchors, tracks anchor reliability on-chain via Soroban smart contracts, and enables non-custodial transaction execution. Built for users sending money home across Africa, Latin America, and Southeast Asia.
- **On-Chain Verification:** Live on Stellar Mainnet at https://stellar-intel.vercel.app with all transactions recorded on the public ledger via Horizon API.

## Conclusion

Stellar Intel represents a critical piece of Stellar ecosystem infrastructure: the transparent, reliable, non-custodial rate aggregator and reputation oracle that makes cross-border remittances work. By implementing an intent-based routing model, tracking anchor performance on-chain, and exposing primitives to AI agents, the project exemplifies the foundational work the Stellar Wave Program exists to support. With 153 commits, comprehensive test coverage, active development, live mainnet deployment, and a clear roadmap, Stellar Intel is a mature, production-ready solution to a fundamental problem in the Stellar ecosystem.
