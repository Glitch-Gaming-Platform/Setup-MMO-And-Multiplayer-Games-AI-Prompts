# Prompt 03: Design and Build an MMO Persistent World

Use this only after the shared authoritative multiplayer foundation works and the game has demonstrated persistent-world requirements.

## Role

Act as a principal MMO, distributed-systems, gameplay-server, and site-reliability architect.

## First rule

Do not begin by creating dozens of services. Build one complete vertical slice:

1. Authenticate.
2. Select one realm.
3. Load one character.
4. Enter one zone or instance.
5. Publish authorized presence.
6. Perform one authoritative gameplay action.
7. Persist one valuable result.
8. Disconnect.
9. Reconnect and prove the state is neither lost nor duplicated.

## World topology

Define the game-specific meaning of:

- Realm.
- Shard.
- Zone.
- Layer.
- Instance.
- Social group.
- Gameplay group.
- Region.

For each boundary specify stable ID, lifecycle, capacity, admission, authoritative owner, in-memory state, durable state, party and guild co-location, transfer, reconnect, failure, version, maintenance, draining, metrics, alerts, and operator controls.

Create normal and failure sequence diagrams for login-to-world, zone transfer, instance entry, reconnect, process crash, stale ownership, rolling deployment, and regional outage.

Challenge the need for seamless handoff. If a loading transition safely meets the player experience for the first milestone, implement it before a distributed seamless transfer protocol.

## Interest management

Measure entity counts, visibility, combat ranges, movement speeds, update size, bandwidth, server fan-out, and client processing.

Choose and justify a grid, quadtree, octree, bounding-volume hierarchy, scene hierarchy, or hybrid. Define subscriptions by position, visibility, party, combat, ownership, quest, and privacy.

Use update tiers for:

- Critical nearby combat.
- Nearby visible movement.
- Distant visible entities.
- Social presence.
- Dormant or unchanged state.

Add hysteresis at subscription boundaries. Test crowded hubs, large fights, fast travel, teleporting, zone edges, reconnect resynchronization, and many static or low-priority entities.

## Durable ownership

Inventory account, character, progression, inventory, equipment, currency, quests, guilds, friends, mail, crafting, trade, auction, housing, world state, and moderation records.

Assign one write authority to every durable aggregate. Define transaction boundaries, consistency, idempotency, concurrency control, audit, reconciliation, compensation, cache policy, schema migration, backup, restore, and player remediation.

Do not permit game clients or arbitrary zone processes to update durable economy state without the owning authority.

## Service boundaries

Evaluate identity, gateway, realm directory, world or zone simulation, instance management, character, inventory, economy, guild, friends, chat, matchmaking, moderation, telemetry, and administration.

Keep a system in the current deployable unit unless extraction has a concrete ownership, scaling, availability, security, or release reason. For every extracted service define:

- Owned data.
- Synchronous APIs.
- Asynchronous events.
- Timeout budget.
- Retry and idempotency.
- Outbox or inbox needs.
- Failure behavior.
- Reconciliation.
- Observability.
- Local-development and integration-test strategy.

Identify dangerous distributed transactions and unsupported exactly-once assumptions.

## Orchestration

Separate topology, placement, allocation, and simulation.

Define how zone and instance processes:

- Start.
- Register.
- Prove health.
- Claim exclusive ownership.
- Receive players.
- Report capacity.
- Scale.
- Drain.
- Transfer or persist state.
- Recover from crash.
- Avoid split authority.
- Terminate.

Test cold starts, stale registrations, duplicate ownership, failed placement, capacity exhaustion, deployment, process crash, cache loss, database slowdown, event delay, network partition, and region loss.

## Delivery

Produce a staged architecture:

1. One realm, one zone, one durable character change.
2. Multiple zones with explicit transfer.
3. Instances and placement.
4. Interest management at measured scale.
5. Extracted services only where justified.
6. Multi-region and disaster recovery only after the ownership model is proven.

Include changed files, tests, load profiles, dashboards, alerts, runbooks, backup and restore evidence, known risks, and a definition of done.

End with the [MMO readiness checklist](../checklists/mmo-readiness-checklist.md).

Interactive version: [Multiplayer and MMO Game Development Prompts](https://www.glitch.fun/publishers/tools/multiplayer-game-development-prompts).
