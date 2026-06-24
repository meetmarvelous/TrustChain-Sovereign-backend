# TrustChain Backend: Project State

**Date:** June 24, 2026
**Version:** v3.2.0 (Temporal Hardened)
**Status:** Production-Ready on Devnet. Mainnet deployment pending funding.

---

## Resume Point

The backend engine is stable and deployed on Vercel Serverless. The Temporal Sentiment Engine (standard deviation variance analysis), Burst Detection Logic, Gini/HHI Dual Gatekeeper, and Yellowstone gRPC integration are all operational. The `/api/verify` endpoint is live and returning scored responses to the frontend HUD.

The next development phase is blocked on mainnet funding (paid Yellowstone gRPC endpoint subscription). No additional backend features are required before grant submission.

---

## Current Architecture

- **Tech Stack:** Node.js (Express) + TypeScript (ESM)
- **Deployment:** Vercel Serverless (`api/index.js` bridge to compiled `dist/server.js`)
- **Key Constants:**
  - Gini Threshold: 0.70
  - HHI Dual Gatekeeper: Active
  - Temporal Sentinel Window: 3,000ms
  - Edge Cache TTL: 15 seconds
  - Latency Target: < 15ms
- **Vercel Config:**
  - Build: `npx tsc`
  - Rewrites: All traffic routed to `/api/index`

---

## Completed Work

- Temporal Sentiment Engine implemented in `integrityEngine.ts` (standard deviation of inter-arrival times)
- Burst detection logic for one-block LP pattern flagging
- Vercel 500 error resolved — guarded `SolanaGRPCService` for null pointer safety
- ESM build pipeline corrected for Vercel compatibility
- `temporalIndex` payload added to `/api/verify` response
- n/(n-1) corrected Gini math verified
- Pool ID bypass hardening completed
- Edge caching and request coalescing active

---

## Next Steps (Post-Funding)

- Transition from Devnet to Mainnet Solana network
- Subscribe to production-grade Yellowstone gRPC endpoint
- Set up persistent gRPC worker for continuous stream (replace polling fallback)
- Integrate Anchor Notary Bridge for on-chain PDA writes at mainnet scale
- Commission third-party audit of Gini, HHI, and Temporal logic
