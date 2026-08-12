# Prompt 00: Choose the Right Multiplayer Architecture

Copy this prompt into an AI coding agent before asking it to implement multiplayer.

## Role

Act as a principal multiplayer game architect. Read the repository, game design, architecture notes, tests, deployment files, current backend, transport, identity, databases, and hosting configuration. Do not implement code yet.

## Goal

Classify the game as:

1. Session or PvP multiplayer: bounded matches or rooms that end.
2. Large-session multiplayer: bounded sessions with high player or entity counts.
3. MMO or persistent world: durable character, social, economy, or world state across realms, shards, zones, layers, or instances.
4. A justified hybrid, with each subsystem assigned to one of the models above.

Do not infer MMO from marketing language or player count alone. Persistence, world continuity, topology, durable ownership, and operational requirements are the deciding factors.

## Inspect and establish

- Engine, platforms, current networking code, backend, transport, databases, cache, cloud, and identity.
- Whether direct P2P, deterministic lockstep or rollback, a listen host, or dedicated servers fit the player count, trust, hidden-information, cheat-resistance, and cost requirements.
- Competitive, cooperative, social, or mixed gameplay.
- Players per party, match, room, visible area, zone, and region.
- Session start, end, join-in-progress, backfill, spectator, replay, reconnect, and host model.
- State discarded at session end and state that must survive.
- Tick rate, snapshot rate, movement speed, projectile speed, physics, latency tolerance, and bandwidth.
- Lobby, party, server browser, queue, skill, region, input, platform, role, and version requirements.
- Character, inventory, currency, trading, crafting, mail, auction, guild, quest, housing, and world persistence.
- Expected concurrency now, at launch, and at one realistic growth milestone.
- Availability, recovery, moderation, privacy, observability, and operational constraints.

## Required output

Create:

1. A one-paragraph classification with evidence.
2. A requirements matrix with Required now, Later after evidence, and Not justified columns.
3. A trust-boundary table for client, authoritative game server, backend services, database, and external providers.
4. A recommended architecture for the first production milestone.
5. A progression plan from two players to the required launch scale.
6. A list of systems deliberately excluded.
7. The largest unknowns and the cheapest prototypes or measurements that resolve them.
8. A definition of done with tests, metrics, documentation, and recovery evidence.

Cover authority, P2P feasibility, signaling, NAT traversal, hole punching, relay fallback, host selection and migration, direct transport, lockstep or rollback, prediction, reconciliation, interpolation, lag compensation, identity, join tickets, reconnect, party, lobby, matchmaking, allocation, match lifecycle, results, persistence, topology, interest management, economy safety, service boundaries, orchestration, security, moderation, load testing, observability, deployment, backups, and disaster recovery.

## Constraints

- Recommend the smallest complete architecture that satisfies the evidence.
- Do not require a separate dedicated gameplay server for a small PvP game when direct P2P, a listen host, lockstep, or rollback meets the stated trust, fairness, connectivity, and failure requirements.
- Do not call P2P serverless without listing signaling, NAT traversal, relay, identity, matchmaking, telemetry, and result-verification services that may still exist.
- Do not replace existing technology without proving a blocking limitation.
- Keep provider-specific integrations behind interfaces.
- Distinguish a stored ticket from a running matcher, a server registry from an allocator, a topology API from world simulation, and negotiation from realtime event delivery.
- Explicitly list MMO systems that a PvP-only game must not build.
- Do not claim readiness without measured network, concurrency, load, security, and failure tests.

Use the result to complete the [multiplayer architecture brief](../templates/multiplayer-architecture-brief.md), then continue with the correct implementation path.

Interactive version: [Multiplayer and MMO Game Development Prompts](https://www.glitch.fun/publishers/tools/multiplayer-game-development-prompts).
