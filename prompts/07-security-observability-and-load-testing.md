# Prompt 07: Security, Observability, Load Testing, and Release Safety

## Role

Act as a game security engineer, site-reliability engineer, performance engineer, and incident commander. Read the actual code, infrastructure, test setup, dashboards, and runbooks before proposing changes.

## Threat model

Map:

- Valuable assets.
- Trust boundaries.
- Player, game-server, backend, database, cache, queue, provider, and operator identities.
- Privileged actions.
- External attack surface.
- Insider and operator risk.
- Privacy and retention obligations.

Evaluate:

- Modified clients and bots.
- Malicious listen hosts, colluding peers, peer IP exposure, signaling abuse, relay exhaustion, desync attacks, and host-migration abuse.
- Movement, speed, teleport, aim, cooldown, damage, score, objective, and result manipulation.
- Inventory, currency, trade, mail, auction, reward, and purchase duplication.
- Join credential theft and replay.
- Queue manipulation, smurfing, collusion, and denial of service.
- Chat spam, harassment, hate, evasion, impersonation, and malicious user content.
- API abuse and scraping.
- Secret exposure.
- Dependency and supply-chain risk.
- Malicious or compromised game-server process.
- Excessive operator privilege.

Prioritize authoritative validation, rate limits, anomaly signals, audit evidence, moderation, and remediation. Do not make invasive client anti-cheat the default. Justify it against threat, platform, privacy, support, and accessibility cost.

## Abuse and moderation

Define reports, evidence, mutes, blocks, chat restrictions, matchmaking restrictions, temporary bans, permanent bans, appeals, escalation, retention, privacy, and operator audit.

Player-facing messages should be safe and understandable. Detailed detection logic and sensitive evidence belong in trusted tools and logs.

## Observability

Create stable correlation identifiers for player journey, account, party, lobby, ticket, assignment, server, match, realm, zone, instance, character, transaction, and deployment.

Add metrics, structured logs, traces, dashboards, and alerts for:

- Authentication and authorization.
- Ticket enqueue, queue time, match quality, cancellation, and abandonment.
- Server startup, heartbeat, capacity, reservation, allocation, draining, and termination.
- P2P signaling, direct-connect success, NAT type, relay use, connection time, host selection, migration, desync, and relay cost where peer-hosted play is supported.
- Join success, connection count, disconnect, reconnect, and session duration.
- Tick time, snapshot rate, bandwidth, packet loss, jitter, prediction corrections, and AOI fan-out.
- Zone population, transfer, instance lifecycle, and ownership conflicts.
- Database latency, lock conflicts, cache behavior, queue backlog, event age, and worker retries.
- Durable writes, idempotency hits, duplication signals, reconciliation backlog, and restore health.
- Match finalization, reward application, disputes, and repairs.
- Moderation volume and abuse signals.
- Cost by region, server type, session, and active player-hour.

Every alert needs an owner, threshold, severity, player impact, dashboard, runbook, and safe action.

## Workload model

Build the load model from:

- Concurrent players.
- Login and reconnect bursts.
- Parties and queue submissions per second.
- Matches, rooms, zones, and instances.
- Players and entities per simulation process.
- Input and snapshot frequency.
- Message size and fan-out.
- Persistence reads and writes.
- Economy and social transactions.
- Chat traffic.
- Operator and deployment actions.
- Regional distribution.

State assumptions and compare them with production telemetry when available.

## Load and failure tests

Test:

- Launch burst.
- Queue burst.
- Many simultaneous match starts.
- Crowded hub or large battle.
- Fast movement across interest-management boundaries.
- Packet latency, jitter, loss, duplication, and reordering.
- Reconnect storm.
- Game-server crash.
- Matcher restart.
- Stale server registration.
- Database slowdown and failover.
- Cache loss.
- Queue or event delay.
- Duplicate event delivery.
- Rolling deployment.
- Draining.
- Version incompatibility.
- Network partition.
- Regional degradation.
- Backup restore and disaster recovery.

Measure p50, p95, p99, saturation, error rate, queue growth, recovery time, and player-visible impact.

## Service-level objectives

Define realistic targets for login success, queue time, allocation, join success, disconnect rate, reconnect success, tick time, durable-write latency, transfer success, result finalization, and recovery.

Tie autoscaling to meaningful pressure such as ready capacity, allocation latency, queue depth, simulation tick saturation, active connections, or worker backlog. Avoid scaling from CPU alone when it does not represent player pressure.

## Release safety

Create environment separation, reproducible builds, infrastructure versioning, schema migration, canary, compatibility window, feature flags where appropriate, server draining, maintenance messaging, smoke tests, rollback, incident response, and post-incident review.

Prove that an old and new client or server combination behaves safely during the supported rolling window.

## Delivery

Implement the highest-risk missing controls first. Return:

- Threat model and prioritized risks.
- Dashboards and alert catalog.
- Workload model.
- Load and failure test harness.
- Results and bottlenecks.
- SLOs and capacity thresholds.
- Release and recovery runbooks.
- Changed files and commands.
- Known gaps and owners.
- Definition of done.

Interactive version: [Multiplayer and MMO Game Development Prompts](https://www.glitch.fun/publishers/tools/multiplayer-game-development-prompts).
