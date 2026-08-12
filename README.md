# MMO and Multiplayer Game AI Prompts

This repository is a provider-neutral guide for planning, building, auditing, and improving multiplayer games with an AI coding agent. It separates bounded PvP or co-op sessions from persistent MMO worlds so a team can build the smallest architecture its game actually needs.

Use the interactive prompt picker and comparison guide on Glitch:

- [Multiplayer and MMO Game Development Prompts](https://www.glitch.fun/publishers/tools/multiplayer-game-development-prompts)
- [General AI Game Development Prompts](https://www.glitch.fun/publishers/tools/ai-game-development-prompts)

The prompts do not require Glitch. They work with an existing engine, backend, cloud, database, transport, and identity provider. Glitch multiplayer and hosting options are documented as one possible integration path, with explicit boundaries for systems the game still needs to own.

## Start with the correct path

### Choose PvP or session multiplayer when

- Matches, races, rounds, rooms, or co-op missions have a beginning and end.
- Most authoritative world state can disappear when the session ends.
- Durable data is limited to accounts, progression, ranks, unlocks, cosmetics, or match history.
- A lobby, party, invite, server browser, queue, peer-hosted session, or dedicated match server covers the core experience.

This path still needs serious networking and security. It usually does not need realms, shards, persistent zones, distributed inventory services, guild services, housing, or a persistent world economy.

Start here:

1. [Choose the right architecture](prompts/00-choose-the-right-multiplayer-architecture.md)
2. [Build the shared authoritative foundation](prompts/01-shared-authoritative-foundation.md)
3. If no separate gameplay server is justified, [build peer-to-peer or listen-server multiplayer](prompts/02a-peer-to-peer-and-listen-server.md).
4. [Build PvP and session multiplayer](prompts/02-pvp-session-multiplayer.md)
5. [Use the PvP launch checklist](checklists/pvp-launch-checklist.md)

### PvP does not always require a dedicated server

A two-player or small-group game can connect players directly. Common models are:

- Direct peer-to-peer mesh, normally only for very small groups.
- A listen server, where one player is the authoritative host and also plays.
- Deterministic lockstep, where peers exchange ordered inputs and simulate the same state.
- Rollback networking, where peers predict remote inputs and re-simulate when the real input arrives.

Removing the dedicated gameplay server does not remove every online service. Internet P2P usually still needs an authenticated lobby or signaling service, NAT discovery, hole punching, relay fallback for difficult networks, session credentials, and optional matchmaking. The game must also define host advantage, malicious-host risk, hidden information, desync detection, host migration or session termination, and how final results are trusted.

Dedicated servers are usually safer when the game has high-value ranked outcomes, valuable rewards, hidden information a host must not see, many players, strict cheat resistance, or no acceptable host-migration behavior.

### Choose MMO or persistent-world architecture when

- Players return to durable characters, inventories, progression, social structures, or world state.
- The world must be partitioned into realms, shards, zones, layers, or instances.
- The game needs interest management, variable replication rates, durable ownership boundaries, economy safety, orchestration, and recovery.
- Failures must preserve valuable state across many game-server and service processes.

Start here:

1. [Choose the right architecture](prompts/00-choose-the-right-multiplayer-architecture.md)
2. [Build the shared authoritative foundation](prompts/01-shared-authoritative-foundation.md)
3. [Design the persistent world](prompts/03-mmo-persistent-world.md)
4. [Protect persistence and the economy](prompts/06-persistence-and-economy-safety.md)
5. [Use the MMO readiness checklist](checklists/mmo-readiness-checklist.md)

### Large-session games are not automatically MMOs

A battle royale, extraction game, social deduction game, large co-op operation, or 200-player battlefield may need aggressive interest management, variable update rates, stronger server allocation, and larger load tests. It can still remain session-based if the authoritative world ends with the session and durable data is limited.

Add the scaling parts that the measured game needs. Do not add persistent-world services only because the player count is high.

## Prompt library

| Guide | Use it for |
| --- | --- |
| [00 — Choose the architecture](prompts/00-choose-the-right-multiplayer-architecture.md) | Classify the game before designing infrastructure |
| [01 — Shared authoritative foundation](prompts/01-shared-authoritative-foundation.md) | Trust boundaries, messages, prediction, reconciliation, interpolation, identity, and reconnect |
| [02 — PvP and session multiplayer](prompts/02-pvp-session-multiplayer.md) | Parties, lobbies, server browser, queues, match servers, results, and anti-cheat |
| [02A — Peer-to-peer and listen server](prompts/02a-peer-to-peer-and-listen-server.md) | Direct connections, signaling, NAT traversal, relay fallback, host authority, lockstep, rollback, and migration |
| [03 — MMO persistent world](prompts/03-mmo-persistent-world.md) | Realms, zones, instances, AOI, world handoff, services, and orchestration |
| [04 — Network quality and lag](prompts/04-network-quality-and-lag.md) | Latency, jitter, packet loss, lag compensation, rewind, and network simulation |
| [05 — Matchmaking and allocation](prompts/05-matchmaking-and-server-allocation.md) | Ticket workers, match formation, party rules, region selection, and healthy capacity |
| [06 — Persistence and economy safety](prompts/06-persistence-and-economy-safety.md) | Characters, inventory, currency, trading, idempotency, duplication, backups, and recovery |
| [07 — Security, observability, and load](prompts/07-security-observability-and-load-testing.md) | Threat modeling, moderation, telemetry, SLOs, load tests, release safety, and incidents |
| [08 — Glitch integration options](prompts/08-glitch-integration-options.md) | Optional Glitch session, MMO control-plane, hosting, database, and adapter integration |

## How to use the prompts

1. Complete the [multiplayer architecture brief](templates/multiplayer-architecture-brief.md).
2. Give the AI the brief, repository, current documentation, and access to the real tests.
3. Run one prompt at a time.
4. Require an audit and plan before implementation.
5. Review assumptions, especially player count, persistence, transport, tick rate, region, and latency targets.
6. Commit a working milestone before moving to the next system.
7. Re-run network, concurrency, load, security, and recovery tests after every architectural change.

The AI should never be asked to “add multiplayer” as one undifferentiated task. Multiplayer is a chain of trust, simulation, transport, session, persistence, and operations decisions. Breaking that chain into explicit milestones produces safer code and much better evidence.

## Shared principles

- Choose the simulation authority explicitly. A dedicated server or listen host validates client intent; deterministic lockstep or rollback peers exchange inputs and detect desync.
- PvP can avoid a separate dedicated gameplay server, but Internet P2P still needs a connectivity, security, host-failure, and result-trust plan.
- Responsive presentation does not require client authority. Use prediction, reconciliation, interpolation, and carefully bounded lag compensation.
- A matchmaking ticket store is not a complete matcher. A server registry is not a fleet allocator.
- Realtime negotiation is not the same as an implemented realtime event pipeline.
- MMO topology records are not the same as authoritative world simulation.
- Durable rewards and economy changes need idempotency, concurrency control, audit history, reconciliation, backups, and restore tests.
- Provider-neutral boundaries reduce migration risk and make local testing possible.
- Every production claim needs measured evidence under latency, loss, load, rolling deployment, and failure.

## Suggested progression

For a new game, prove multiplayer in this order:

1. Two authenticated players can enter one session using the chosen direct-P2P, listen-host, lockstep, rollback, or dedicated-server model.
2. Inputs, state replication, prediction, reconciliation, interpolation, disconnect, and reconnect work.
3. One complete PvP or co-op match can form, run, finish, and apply trusted results exactly once.
4. Matchmaking and server allocation work under concurrency and regional capacity pressure.
5. Add durable character state only if the design needs it.
6. Add one persistent realm and zone vertical slice.
7. Add interest management, instances, service extraction, orchestration, and multi-region recovery from measured need.

This sequence lets an MMO grow from a correct multiplayer foundation without forcing a PvP game to carry MMO complexity.

## Contributing

Keep additions provider-neutral by default. A provider-specific prompt must:

- State the exact capability being integrated.
- Identify what remains game-owned or requires another provider.
- Avoid claiming that a database model, queue record, negotiation response, or control-plane API is a complete runtime.
- Include local-development, contract-test, migration, and failure behavior.
- Link back to the [Glitch multiplayer prompt guide](https://www.glitch.fun/publishers/tools/multiplayer-game-development-prompts).
