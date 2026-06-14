# Neynar

Neynar is the complete Farcaster developer platform providing infrastructure REST APIs for querying casts, channels, user profiles, feeds, reactions, and building applications on the Farcaster decentralized social protocol. As of January 2026, Neynar acquired Farcaster from Merkle Manufactures, taking operational responsibility for the protocol, client, and related infrastructure.

- **Website:** https://neynar.com
- **API Docs:** https://docs.neynar.com
- **Base URL:** https://api.neynar.com
- **OpenAPI Spec:** https://github.com/neynarxyz/OAS

## APIs

- **Neynar Farcaster API** — 148 endpoints across 22+ tag groups including Users, Casts, Channels, Feeds, Reactions, Notifications, Signers, Frames, Webhooks, Onchain, Agents, and more
- **Neynar Hub HTTP API** — Direct protocol-level access to Farcaster hub data

## Authentication

All API endpoints require an API key passed as the `x-api-key` header. API keys are obtained from the [Developer Portal](https://dev.neynar.com).

## Plans

| Plan | Rate Limit (per endpoint) | Global RPM |
|------|--------------------------|------------|
| Free | Limited | Limited |
| Starter | 300 RPM / 5 RPS | 500 RPM |
| Growth | 600 RPM / 10 RPS | 1,000 RPM |
| Scale | 1,200 RPM / 20 RPS | 2,000 RPM |
| Enterprise | Custom | Custom |

See [plans/plans.yml](plans/plans.yml) for full details.

## Pricing Model

Neynar uses a credit-based pricing model. Each API endpoint consumes a defined number of credits per call, with multipliers applied for bulk operations and paginated results. Active signers (for write access) cost 20,000 credits per monthly active signer.

See [finops/finops.yml](finops/finops.yml) for full details.
