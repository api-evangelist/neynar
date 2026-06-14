# Neynar GraphQL Schema

## Overview

Neynar is the leading Farcaster API provider and, as of January 2026, the operational owner of the Farcaster protocol. Neynar exposes its developer platform as a REST API (OpenAPI spec v3.176.0). As of June 2026, Neynar does not operate a public GraphQL endpoint — a probe of `https://hub.neynar.com/graphql` and `https://api.neynar.com/graphql` returned no GraphQL response.

The schema in `neynar-schema.graphql` is a **conceptual GraphQL SDL** derived directly from the published OpenAPI specification at:

```
https://raw.githubusercontent.com/neynarxyz/OAS/main/src/api/spec.yaml
```

It faithfully represents the same data model the REST API exposes, expressed in GraphQL SDL notation for tooling, federation planning, and documentation purposes.

## Data Model

The schema is organized around the core Farcaster protocol entities:

### Identity
- **User** — full Farcaster user profile including FID, username, custody address, verified Ethereum/Solana addresses, social counts, viewer context, and optional experimental/pro fields
- **UserDehydrated** — lightweight user reference used in nested contexts (author fields, follow lists, etc.)
- **Signer / DeveloperManagedSigner** — Ed25519 key pairs that authorize apps to act on behalf of users

### Content
- **Cast** — a Farcaster post with full author, embedded media, reactions, replies, thread linkage, and channel context
- **CastDehydrated** — minimal cast reference (hash + author) used in embeds and notifications
- **Embed / EmbedUrl / EmbedCast** — URL and cast embeds attached to casts, with rich crawled metadata
- **Conversation** — a cast together with its threaded replies and optional AI-generated summary

### Social Graph
- **Follower / FollowerDehydrated** — follow relationships between users
- **ReciprocalFollower** — mutually-following pairs
- **MuteRecord / BlockRecord / BanRecord** — moderation relationships

### Reactions
- **ReactionLike / ReactionRecast** — FID/fname pairs reacting to casts
- **ReactionWithUserInfo / ReactionWithCastInfo** — enriched reaction records including full user or cast objects
- **ReactionType** enum: `like`, `recast`

### Channels
- **Channel** — topic-based community feeds with host/moderator/member hierarchy, follower counts, and lead user
- **ChannelDehydrated** — minimal channel reference
- **ChannelMember / ChannelMemberInvite** — membership records with roles (`member`, `moderator`, `host`)

### Notifications
- **Notification** — aggregated notification event (follows, likes, recasts, mentions, replies, quotes)
- **NotificationCampaign / NotificationCampaignStats** — broadcast notification campaigns sent to frame token holders

### Frames (Mini Apps)
- **Frame / FrameV1 / FrameV2 / FrameV2WithFullAuthor** — interactive mini-app manifests embedded in casts
- **FrameActionButton** — interactive buttons with action types: `post`, `post_redirect`, `tx`, `link`, `mint`
- **FarcasterManifest** — app manifest associated with a Frame v2 domain

### Onchain / Fungibles
- **Fungible** — ERC-20 and other onchain tokens (name, symbol, address, network, decimals, supply)
- **FarcasterFungible** — fungible token enriched with Farcaster cast engagement count
- **FungibleBalance / AddressBalance / TokenBalance** — wallet balance records

### Storage
- **StorageAllocation** — hub storage units purchased for a FID with expiry
- **StorageObject** — used vs. capacity summary

### Subscriptions (Hypersub / Protocol)
- **Subscription** — onchain subscription contract (chain, address, protocol version, tiers, pricing)
- **SubscriptionTier / Subscriber / SubscribedTo** — tier definitions and subscriber records

### Webhooks
- **Webhook** — real-time event delivery endpoint with rate-limit and subscription filter configuration
- **WebhookSubscription / WebhookSubscriptionFilters** — filter rules covering cast, reaction, follow, and user events
- **WebhookSecret** — signing secrets for webhook payload verification

### Trending / Discovery
- **TrendingTopic** — trending conversation topic with summary and top-level category
- **TrendingChannel** — channel trending by cast activity

### Moderation
- **MuteRecord / BlockRecord / BanRecord** — user-level and app-level moderation records

## Enumerations

| Enum | Values |
|------|--------|
| `ReactionType` | `like`, `recast` |
| `NotificationType` | `follows`, `recasts`, `likes`, `mentions`, `replies`, `quotes` |
| `CastNotificationType` | `cast`, `reply`, `quote` |
| `ChannelMemberRole` | `member`, `moderator`, `host` |
| `FrameButtonActionType` | `post`, `post_redirect`, `tx`, `link`, `mint` |
| `Network` | `ETHEREUM`, `OPTIMISM`, `BASE`, `ZORA`, `SOLANA` |
| `TopLevelTopic` | `crypto`, `technology`, `culture`, `politics`, `sports`, `science`, `entertainment`, `other` |
| `SharedSignerPermission` | `message`, `cast`, `reaction`, `follow`, `profile`, `username` |
| `NotificationCampaignStatus` | `pending`, `sent`, `failed` |
| `TransactionFrameStatus` | `pending`, `approved`, `rejected` |
| `TransactionFrameType` | `send_fungibles`, `pay` |

## Schema Source

- **Source type**: Conceptual SDL derived from REST/OpenAPI
- **OpenAPI spec**: `https://raw.githubusercontent.com/neynarxyz/OAS/main/src/api/spec.yaml`
- **OpenAPI version**: 3.176.0
- **GraphQL endpoint probe**: No public GraphQL endpoint found (June 2026)
- **Schema file**: `neynar-schema.graphql`

## Type Count

The schema defines **70+ named types** across the following categories:

- Object types: 57
- Enum types: 11
- Input types: 5
- Union types: 1
- Root types: `Query`, `Mutation`

## References

- Neynar Docs: https://docs.neynar.com
- API Reference: https://docs.neynar.com/reference
- OpenAPI Repository: https://github.com/neynarxyz/OAS
- Node.js SDK: https://github.com/neynarxyz/nodejs-sdk
- React SDK: https://github.com/neynarxyz/react
- Go SDK: https://github.com/neynarxyz/go-sdk
- Rust SDK: https://github.com/neynarxyz/rust-sdk
- Farcaster Protocol: https://docs.farcaster.xyz
