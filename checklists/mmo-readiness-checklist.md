# MMO and Persistent-World Readiness Checklist

Use this in addition to the shared and PvP/session checks. MMO systems add durable ownership, world partitioning, interest management, service coordination, economy safety, orchestration, and recovery.

## Persistent-world proof

- [ ] The design explains why session multiplayer is insufficient.
- [ ] One complete vertical slice proves login, character load, realm selection, zone entry, one authoritative action, one durable change, disconnect, and safe reconnect.
- [ ] Every durable aggregate has a single write authority.
- [ ] Disposable in-memory state and durable state are clearly separated.
- [ ] Valuable actions are idempotent and safe across retries and crashes.

## Realms, shards, zones, and instances

- [ ] Realm, shard, zone, layer, and instance have game-specific definitions.
- [ ] Every topology boundary has a stable ID, lifecycle, capacity, admission rule, owner, and failure policy.
- [ ] Party and guild co-location rules are explicit.
- [ ] Zone transfer and instance entry have normal and failure sequence diagrams.
- [ ] Seamless handoff is used only when the player experience justifies its complexity.
- [ ] Draining, restart, maintenance, version compatibility, and region evacuation are tested.

## Interest management

- [ ] The spatial index is justified by world shape and measured entity behavior.
- [ ] Subscriptions consider position, visibility, combat, party, ownership, quest, and privacy.
- [ ] Critical, nearby, distant, social, and dormant state use justified update tiers.
- [ ] Spawn and despawn hysteresis prevents boundary flapping.
- [ ] Crowded hubs, large fights, fast traversal, teleporting, reconnect, and zone boundaries are load tested.
- [ ] Bandwidth, fan-out, client entity count, stale-state risk, and worst-case processing are measured.

## Character, inventory, and economy safety

- [ ] Account, character, progression, inventory, equipment, currency, quests, guild, mail, crafting, trade, auction, housing, and world state are assigned to explicit owners.
- [ ] Transaction boundaries and consistency requirements are documented.
- [ ] Concurrent login and multiple active-session policy is enforced.
- [ ] Duplicate item and currency threat scenarios have automated tests.
- [ ] Trading, mail claims, auction settlement, crafting completion, and reward application are idempotent.
- [ ] Audit, reconciliation, compensation, and player-remediation tools exist.
- [ ] Schema migration, backup, point-in-time restore, and data-integrity checks are rehearsed.

## Service boundaries

- [ ] The system starts with the fewest deployable units that meet ownership and scale requirements.
- [ ] Every extracted service has a concrete scaling, security, ownership, availability, or deployment reason.
- [ ] Owned data, APIs, events, timeouts, retries, idempotency, and failure behavior are documented.
- [ ] Distributed transactions are identified and replaced with safe workflows, compensation, or reconciliation.
- [ ] Outbox and inbox patterns are used where event delivery must survive process or database failure.
- [ ] Local development and integration testing do not require a production-scale environment.

## Orchestration and capacity

- [ ] Zone and instance processes register health, version, region, capacity, ownership, and heartbeat.
- [ ] Placement and allocation are separate from topology records.
- [ ] Autoscaling signals reflect real simulation or queue pressure.
- [ ] Cold starts, warm pools, draining, failed placement, stale registration, and duplicate ownership are tested.
- [ ] A process crash cannot leave two authorities writing the same world partition.
- [ ] Regional degradation and disaster recovery have tested runbooks.

## Social, moderation, and privacy

- [ ] Friends, guilds, parties, chat, mail, trade, reports, blocks, mutes, bans, and appeals have explicit ownership.
- [ ] Presence reveals only authorized information.
- [ ] Chat and social systems have rate limits, retention rules, moderation evidence, and privacy controls.
- [ ] Operator tools use least privilege and audited actions.
- [ ] Data export, deletion, retention, and regional requirements are documented.

## Observability and recovery

- [ ] Correlation IDs follow a player from gateway through world, persistence, and economy workflows.
- [ ] Dashboards include login, realm admission, zone population, transfer success, tick time, AOI fan-out, durable-write latency, conflicts, duplication signals, and reconciliation backlog.
- [ ] SLOs and error budgets are defined for player-visible journeys.
- [ ] Failure tests cover database slowdown, cache loss, event delay, process crash, rolling release, network partition, region outage, and restore.
- [ ] Recovery objectives are measured rather than assumed.
- [ ] The team can explain how to detect and repair partially completed valuable actions.

Return to the [interactive Glitch multiplayer prompt guide](https://www.glitch.fun/publishers/tools/multiplayer-game-development-prompts).
