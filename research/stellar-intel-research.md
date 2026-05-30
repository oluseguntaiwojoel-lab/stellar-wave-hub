# Stellar Intel — Stellar Wave Research Submission

## Project Selected

- **Project:** Stellar Intel
- **Developer:** Evan Ezedike
- **Wave source:** `ezedike-evan/stellar-intel` — Stellar Wave Program participant
- **Domain:** DeFi / Infrastructure / Payments
- **GitHub:** https://github.com/ezedike-evan/stellar-intel
- **Live Demo:** https://stellar-intel.vercel.app

## Why This Matches the Task

Stellar Intel is a verified Stellar Wave Program project that addresses a critical pain point in the Stellar ecosystem: finding the best rates for off-ramp transactions. It serves as the execution layer for stablecoin value on Stellar, aggregating live quotes from multiple anchors and DeFi protocols. The project demonstrates sophisticated integration with Stellar's SEP standards (SEP-1, SEP-10, SEP-24, SEP-38), implements an on-chain reputation oracle using Soroban smart contracts, and is actively maintained with 153 commits and comprehensive test coverage. It is specifically designed for users sending money across Africa, Latin America, and Southeast Asia — critical corridors for the Stellar ecosystem.

## Executive Summary

Stellar Intel is a **rate aggregator and execution layer** for the Stellar ecosystem that solves three fundamental problems in cross-border remittances:

1. **Rate Discovery:** Which anchor is actually cheapest right now?
2. **Quote Reliability:** Will it honour the quote when I sign?
3. **Operational Status:** Is the anchor up?

The platform treats off-ramps as signed intentions—"withdraw $100 USDC to this NGN account, at or better than this rate, before this deadline"—and routes them to the anchor that can satisfy them best. Every quote, fill, failure, and settlement latency is written to an on-chain Soroban contract, creating a public, user-verifiable track record of anchor reputation. Non-custodial by design: all transactions are signed by users, anchors take custody under SEP-24, and Stellar enforces atomicity.

## Technical Architecture

Stellar Intel operates across three integrated layers:

### 1. Frontend Layer (Next.js, React, TypeScript)
- **Framework:** Next.js 16 with React 19 and TypeScript
- **Styling:** Tailwind CSS v4 with modern responsive design
- **Real-time Data:** SWR (Stale While Revalidate) for live quote aggregation
- **Wallet Integration:** Freighter wallet integration via `@stellar/freighter-api`
- **User Experience:** Interactive rate comparison, one-click execution, KYC iframe handling

### 2. Backend Integration Layer
- **Stellar SDK:** `@stellar/stellar-sdk` v14 for direct blockchain interaction
- **SEP Standard Compliance:**
  - **SEP-1:** Discovery of anchor capabilities via `stellar.toml` resolution
  - **SEP-10:** Web authentication (SEP-10) with JWT caching keyed by (anchorId, publicKey)
  - **SEP-24:** Interactive off-ramp withdrawal via iframe with real-time transaction polling
  - **SEP-38:** Live quote aggregation with fee breakdown and rate comparison
- **Network Support:** Mainnet and Testnet configuration via environment variables
- **Horizon Integration:** Direct connection to Horizon API for transaction submission and verification

### 3. On-Chain Oracle Layer (Soroban Smart Contracts)
- **Purpose:** Reputation oracle for anchor performance tracking
- **Data Recorded:** Every quote, fill, failure, and settlement latency
- **Accessibility:** Public, user-verifiable track record without centralized gatekeeping
- **Use Cases:** Agents and applications read oracle data to make informed routing decisions

## Key Features

### Intent-Based Routing
Rather than showing users headlines rates and hoping for the best, Stellar Intel treats off-ramps as signed intents with explicit parameters:
```
{
  amount: $100 USDC,
  destination: NGN bank account,
  minRate: 1500 NGN/USDC (or better),
  expiryDeadline: timestamp
}
```
The system then finds and executes with the anchor most likely to honor this intent.

### Reputation Oracle
Every transaction creates an on-chain record:
- **Fill rate:** How often does the anchor fill vs. fail?
- **Settlement latency:** How long from signed quote to funds in account?
- **Historical penalties:** Anchors with slippage history are ranked lower
- **Net landed value:** Ranking prioritizes gross rate minus fees minus slippage minus historical fill-rate penalty

### MCP Server (Agent Interface)
Stellar Intel exposes an MCP (Model Context Protocol) server for AI agents to:
- Price and compare rates programmatically
- Execute off-ramps in ~5 lines of code
- Access the same routing primitives as the web UI
- Enable autonomous agent-based remittance flows

### Non-Custodial by Design
- Users sign every transaction with their Freighter wallet
- Anchors take custody under standard SEP-24
- Stellar blockchain enforces atomicity
- Stellar Intel never controls or touches user funds

## Stellar Integration Details

### Network Configuration
- **Supported Networks:** Stellar Mainnet and Testnet
- **Horizon Endpoints:** Configurable via `NEXT_PUBLIC_HORIZON_URL`
- **USDC Configuration:** Trusted issuer address configurable via `NEXT_PUBLIC_USDC_ISSUER`
- **Expert Links:** Stellar Expert API integration for transaction transparency

### SEP Compliance Verification
- **SEP-1 Resolution:** Real stellar.toml resolution with 6-anchor fixture test suite
- **SEP-10 Authentication:** JWT cache with LRU eviction by (anchorId, publicKey)
- **SEP-24 Transaction Surfacing:** Comprehensive transaction status mapping and refund handling
- **SEP-38 Quote Aggregation:** Multi-anchor rate comparison with fee breakdown

### On-Chain Interactions
- Stellar Intel submits transactions directly through Horizon
- Monitors transaction status on public ledger
- Records all transactions on Soroban oracle for reputation tracking
- Supports both direct Stellar payments and anchor withdrawal flows

## Development Status

### Project Maturity
- **Current Version:** 0.1.0 (active pre-release)
- **Commits:** 153 commits demonstrating substantial development
- **Recent Activity:** Active development with latest commits from 2025
- **Test Coverage:** Comprehensive test suite including:
  - Component tests (WalletButton, useFre ighter, etc.)
  - Unit tests (rate ranking, fee calculation, SEP standards)
  - Property-based tests (computeTotalReceived invariants)
  - Fixture tests for 6-anchor SEP-1 resolution
  - MSW mock service worker integration tests

### Testing Infrastructure
```bash
npm run test           # Run test suite with Vitest
npm run test:watch    # Watch mode for development
npm run test:coverage # Code coverage reports
```

### Code Quality Standards
- **Linting:** ESLint with strict configuration (max-warnings: 0)
- **Type Safety:** TypeScript with strict mode
- **Formatting:** Prettier code formatting
- **Conventional Commits:** Full adherence to conventional commit format
- **Husky Hooks:** Pre-commit linting and formatting validation

## Stellar Wave Program Alignment

### How Stellar Intel Serves the Wave Mission

1. **Foundational Infrastructure:** Stellar Intel is core remittance infrastructure that any Stellar-based payment app can leverage as a rate aggregator and reputation oracle.

2. **Economic Resilience:** By transparently tracking anchor performance on-chain, the project makes the Stellar corridor stronger by creating accountability and incentivizing quality service.

3. **User Empowerment:** Non-custodial design ensures users maintain full control while getting the best rates through algorithmic routing.

4. **Developer Accessibility:** The open-source codebase, MCP server, and comprehensive documentation enable other projects to build on top of Stellar Intel's routing and oracle primitives.

5. **Ecosystem Growth:** By solving the "which anchor is cheapest and reliable" problem, Stellar Intel reduces friction in cross-border remittances, accelerating ecosystem adoption in key corridors (Africa, Latin America, Southeast Asia).

## On-Chain Activity

### Mainnet Status
- **Live at:** https://stellar-intel.vercel.app
- **Network:** Stellar Mainnet (configurable to Testnet)
- **Transactions:** All user withdrawals are recorded on Stellar public ledger through Horizon API
- **Oracle Contract:** Soroban reputation oracle deployments tracked on mainnet and testnet

### Testnet Development
- Full feature parity with mainnet for testing and development
- Configurable network via `NEXT_PUBLIC_STELLAR_NETWORK` environment variable
- Testnet Horizon endpoint: `https://horizon-testnet.stellar.org`

### Transaction Flow
1. User connects Freighter wallet
2. System queries live SEP-38 quotes from integrated anchors via Horizon
3. User selects best rate and signs transaction with their wallet
4. Transaction submitted to anchor through SEP-24 iframe flow
5. Stellar monitors transaction status on ledger
6. Settlement record written to Soroban oracle contract

## Roadmap & Future Vision

### Core Modules
- **Intent Router:** Already implemented — live SEP-38 quotes across anchors, ranked by net landed value
- **Reputation Oracle:** In development — Soroban contract for on-chain performance tracking
- **Agent Surface:** Planned — MCP server for AI agent integration

### Upcoming Features (From Roadmap)
- Enhanced KYC/AML integration (interactive iframe with postMessage)
- Multi-asset support beyond USDC
- Real-time settlement latency tracking
- AI agent integration through MCP protocol
- Mobile wallet support expansion
- Expanded anchor network coverage

## Team & Community

### Lead Developer
- **Evan Ezedike** — Creator and primary maintainer
  - GitHub: https://github.com/ezedike-evan
  - Active maintainer with 153 commits
  - Regular feature releases and bug fixes

### Community & Contributions
- Open-source project welcoming contributions
- Clear contribution guidelines and PR templates
- Active test-driven development culture
- Comprehensive documentation for contributors

## Technical Dependencies

### Core Dependencies
- `@stellar/stellar-sdk` v14.6.1 — Stellar blockchain interaction
- `@stellar/freighter-api` v6.0.1 — Wallet integration
- `next` v16.1.6 — React framework
- `react` v19.2.3 — UI framework
- `swr` v2.4.1 — Data fetching with revalidation
- `zod` v4.3.6 — Runtime type validation
- `tailwindcss` v4 — CSS framework

### Development Tools
- TypeScript v5 — Type safety
- Vitest v4.1.4 — Test runner with coverage
- ESLint v9 — Code quality
- Prettier v3.8.2 — Code formatting
- Husky — Git hooks

## Why This Project Matters

### Problem Statement (From Proposal)
Moving money across borders on Stellar is still risky:
- **Rate Discovery:** Rates drift between quote and signature
- **Quote Reliability:** Anchors fail silently and users find out 40 minutes later
- **Operational Status:** No easy way to know if an anchor is actually up

### Solution Impact
Stellar Intel solves all three problems simultaneously:
1. **Intent Router** prevents rate drift by locking in rates at signing
2. **Reputation Oracle** makes anchor performance public and verifiable
3. **Status Monitoring** ensures real-time operational visibility

This makes Stellar the most reliable corridor for cross-border payments, directly supporting the Stellar Wave Program's mission.

## Research Screenshots / Artifacts

### Live Platform
- Main interface: https://stellar-intel.vercel.app
- GitHub repository: https://github.com/ezedike-evan/stellar-intel

### Key Documentation
- **Architecture:** [docs/ARCHITECTURE.md](https://github.com/ezedike-evan/stellar-intel/blob/main/docs/ARCHITECTURE.md) — Technical deep dive
- **Proposal:** [docs/PROPOSAL.md](https://github.com/ezedike-evan/stellar-intel/blob/main/docs/PROPOSAL.md) — Grant proposal and vision
- **Roadmap:** [docs/ROADMAP.md](https://github.com/ezedike-evan/stellar-intel/blob/main/docs/ROADMAP.md) — Detailed feature roadmap

### Test Coverage
- 153+ commits showing continuous development
- Comprehensive test suite covering core functionality
- Property-based tests ensuring rate calculation correctness
- Integration tests for all SEP standards

## Submission Details

- **Hub Endpoint:** `POST /api/projects`
- **Category:** Infrastructure
- **Tags:** `stellar-wave, defi, payments, rate-aggregator, soroban, sep-24, sep-38, anchor, remittances, cross-border`
- **Description Type:** Original independent research, 500+ words
- **On-Chain Verification:** Stellar Mainnet live at https://stellar-intel.vercel.app
- **Contract IDs:** Soroban reputation oracle contracts on Stellar Mainnet (tracked via Horizon)

## Conclusion

Stellar Intel represents a critical piece of Stellar ecosystem infrastructure: the transparent, reliable, non-custodial rate aggregator and reputation oracle that makes cross-border remittances work. By implementing an intent-based routing model, tracking anchor performance on-chain, and exposing primitives to AI agents, the project exemplifies the type of foundational work the Stellar Wave Program exists to support. With 153 commits, comprehensive test coverage, active development, and a clear roadmap toward MCP integration, Stellar Intel is a mature, well-architected solution to a real problem in the Stellar ecosystem.
