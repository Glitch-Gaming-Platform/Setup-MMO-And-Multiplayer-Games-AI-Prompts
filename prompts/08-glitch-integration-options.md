# Prompt 08: Evaluate and Integrate Glitch Multiplayer and Hosting Options

This prompt is optional. Run the architecture classifier first. Compare providers before selecting Glitch or any alternative.

Glitch documentation and APIs can change. Verify current official contracts, limits, pricing, regions, transports, and product status before implementation.

## Part A: Provider-neutral comparison

Act as a principal game-platform architect. Convert the approved architecture brief into a requirements matrix, then compare self-hosting and relevant managed providers, including Glitch when it fits.

Score:

- Identity and authorization.
- P2P signaling, NAT traversal, relay services, host selection, and migration.
- Lobbies and parties.
- Server browser.
- Reservations and join tickets.
- Matchmaking ticket storage.
- Matcher worker.
- Server registration and health.
- Fleet startup and allocation.
- Authoritative compute and supported transports.
- Realtime event delivery.
- Voice media.
- Realms, zones, layers, instances, and presence.
- Spatial lookup and interest-management support.
- Character and world persistence.
- Managed SQL, NoSQL, and cache.
- Autoscaling, regions, deployment, draining, and rollback.
- Observability, moderation, backups, and disaster recovery.
- Pricing and cost predictability.
- Local development, portability, data export, and migration.

Distinguish a feature available as an end-to-end runtime from a primitive the game must complete.

Recommend provider-neutral interfaces around identity, session directory, reservation, join credentials, matchmaking, allocation, topology, presence, realtime events, voice, persistence, hosting, and telemetry.

## Part B: Glitch capabilities to evaluate

Based on the Glitch backend reviewed for this guide, evaluate the current documented availability of:

### Session multiplayer control plane

- Lobby creation and membership.
- Game-server registration and discovery.
- Capacity and heartbeat records.
- Reservations.
- Short-lived join tickets.
- Server favorites and recent-server history.
- Voice-room metadata and fallback packet APIs.

### MMO control plane

- Realm records.
- Zone records.
- Instance or layer records.
- Presence and spatial lookup.
- Matchmaking ticket enqueue, poll, and cancel.
- Ban records.
- Realtime negotiation contracts.

### Hosting

- Static web game hosting.
- Containerized service stacks.
- Deployment configuration and domains.
- Managed PostgreSQL.
- Managed MySQL.
- Managed Azure SQL.
- Managed Cosmos DB.
- Managed Redis.
- Billing and plan controls.

Use only capabilities confirmed by current documentation or source. Mark unknowns for verification.

## Part C: Responsibilities to keep explicit

Unless current Glitch documentation proves otherwise, assign these to the game, another provider, or an additional Glitch component that the team must build:

- Peer-to-peer signaling, NAT traversal, relay fallback, host selection, migration, and desync handling.
- Authoritative gameplay simulation.
- Combat, movement, physics, prediction, reconciliation, interpolation, and lag compensation.
- The matchmaking worker that claims tickets and forms matches.
- Process or fleet startup and healthy server allocation.
- Production realtime event publication and consumption.
- Production voice media transport and mixing.
- Managed UDP game-server fleets.
- Character, inventory, progression, economy, guild, quest, housing, and world persistence models.
- Economy transaction safety and reconciliation.
- Automatic instance placement and orchestration.
- Backups, restore tests, and game-specific disaster recovery.

Do not describe:

- Ticket storage as a complete matcher.
- A server registry as a fleet allocator.
- Realm, zone, or instance records as world simulation.
- Realtime negotiation as implemented event delivery.
- Voice-room records or packet fallback as a full production voice-media service.
- Managed databases as a finished game persistence model.

## PvP or session integration prompt

Map the approved session flow to Glitch:

1. Authenticate the player.
2. Create or join a party or lobby if required.
3. Choose either peer-hosted play or a dedicated authoritative server.
4. For P2P, use the lobby as control-plane context while a game-owned or third-party signaling and relay layer establishes the connection.
5. For dedicated play, discover or allocate a healthy authoritative server through the game-owned allocation boundary.
6. Create the justified reservation and short-lived session or join credential.
7. Validate the credential on the host, peers, or game server according to the trust model.
8. Run the match using listen-host, lockstep, rollback, or dedicated-server authority.
9. Submit and finalize only appropriately trusted results.
10. Persist progression through the game-owned durable data model.
11. Migrate or terminate a lost peer host, or drain and replace dedicated server versions safely.

Do not assume Glitch lobby, server-directory, reservation, ticket, or realtime-negotiation APIs automatically provide ICE signaling, STUN, TURN, platform relay, host migration, deterministic synchronization, or rollback networking. Verify current support and connect another provider or a game-owned service where needed.

Implement a Glitch adapter rather than spreading Glitch response models through game-domain code. Add contract tests, local fakes, secret handling, environment separation, timeout, retry, idempotency, metrics, and migration behavior.

## MMO integration prompt

Create a responsibility matrix with Glitch, game-owned services, authoritative game servers, databases, and any third-party providers.

Map:

1. Authentication.
2. Realm selection.
3. Zone or instance lookup.
4. Game-owned placement and allocation.
5. Secure join.
6. Authorized presence publication.
7. Authoritative simulation.
8. Game-owned character and economy persistence.
9. Zone transfer or instance exit.
10. Disconnect and reconnect.
11. Draining, restart, and recovery.

Use Glitch topology and presence as control-plane primitives unless current documentation proves an end-to-end runtime. Keep exclusive simulation ownership and durable data ownership explicit.

## Hosting integration prompt

For each deployable component decide whether it is:

- Static frontend.
- HTTP API.
- Long-lived realtime gateway.
- Authoritative game server.
- Matcher worker.
- Allocator or orchestration worker.
- Persistence service.
- Background job.
- Database.
- Cache.
- Queue or event system.
- Observability component.

Verify that the selected Glitch hosting product supports the process lifetime, transport, port, health, scaling, region, startup, storage, and network behavior each component requires. Do not assume container hosting is automatically a managed game-server fleet.

Document environment variables, secrets, service identity, domains, TLS, database connections, cache, migrations, health checks, readiness, draining, autoscaling, logs, metrics, backups, rollback, and cost.

## Required output

Return:

- Current capability verification with sources supplied to the AI.
- Requirement-to-provider matrix.
- Glitch responsibility matrix.
- Missing-component list with owner.
- Provider-neutral adapter design.
- PvP or MMO sequence diagrams.
- Implementation milestones.
- Contract, concurrency, network, load, security, and recovery tests.
- Deployment and rollback.
- Migration and data-export plan.
- Cost and operational risks.
- Definition of done.

Glitch guide: [Multiplayer and MMO Game Development Prompts](https://www.glitch.fun/publishers/tools/multiplayer-game-development-prompts).

General guide: [AI Game Development Prompts](https://www.glitch.fun/publishers/tools/ai-game-development-prompts).
