# PvP and Session Multiplayer Launch Checklist

Use this for matches, rooms, races, rounds, co-op missions, arena games, and other bounded sessions.

## Architecture

- [ ] The game is explicitly classified as session-based, with durable and disposable state listed.
- [ ] Direct P2P, listen host, deterministic lockstep or rollback, or dedicated server is chosen from explicit trust, fairness, scale, cost, and failure requirements.
- [ ] The dedicated server or listen host owns validated simulation outcomes, or deterministic peers exchange validated inputs with desync detection.
- [ ] Untrusted peers never directly set durable currency, items, progression, or ranked rewards.
- [ ] MMO-only systems have been excluded unless a documented requirement justifies them.

## Peer-to-peer and listen-host sessions

- [ ] The game documents host advantage, malicious-host power, hidden-information exposure, peer cheating, and acceptable result trust.
- [ ] Signaling is authenticated and separate from gameplay transport.
- [ ] Internet connectivity covers NAT discovery, hole punching, IPv4 and IPv6 as required, carrier-grade NAT, and relay fallback.
- [ ] Relay capacity, region, latency, privacy, and cost are measured.
- [ ] Session credentials authenticate peers and gameplay traffic is encrypted and replay-protected.
- [ ] Host selection considers latency, reachability, hardware, party ownership, and trust.
- [ ] Host departure has tested migration or an explicit player-safe termination policy.
- [ ] Lockstep or rollback games test determinism, state hashing, desync, rollback windows, resynchronization, and replay debugging.
- [ ] Same-LAN, different-NAT, symmetric-NAT, relay-only, mobile network change, suspend/resume, and host-drop scenarios are tested.
- [ ] High-value ranked or economy outcomes do not trust a player host without a reviewed verification design.

## Connection and session lifecycle

- [ ] Connect, authenticate, authorize, reserve, join, ready, play, disconnect, reconnect, leave, and expire are explicit states.
- [ ] Join credentials are short-lived, audience-bound, replay-protected, and safe to revoke.
- [ ] Reconnect has a defined grace period and cannot duplicate participation, state, results, or rewards.
- [ ] Full, stale, draining, restarting, version-incompatible, private, kicked, and banned server responses are player-readable.
- [ ] Server heartbeats, health, capacity, and stale-record cleanup are implemented.

## Parties, lobbies, and matchmaking

- [ ] Party leadership, invitations, ready state, queue ownership, cancellation, and disconnect behavior are defined.
- [ ] Lobby privacy, passwords, capacity, reservations, and join-in-progress rules are enforced on the server.
- [ ] Matchmaking has an actual worker or service that claims tickets and forms matches.
- [ ] Party integrity, region, latency, skill, platform, input, mode, role, and build-version policies are tested.
- [ ] Server allocation reserves healthy capacity atomically and recovers from failed allocation.
- [ ] Queue timeout, widening, cancel, retry, backfill, and player messaging are defined.

## Networking and fairness

- [ ] Tick rate and snapshot rate are measured under representative load.
- [ ] Prediction, reconciliation, interpolation, extrapolation limits, and hard-correction thresholds are documented.
- [ ] Sequence numbers, timestamps, ordering, duplication, loss, jitter, and reconnect resynchronization are tested.
- [ ] Lag compensation or rewind has a bounded policy and timestamp-abuse protection where needed.
- [ ] Bandwidth per player and per server is measured.
- [ ] Debug tools expose ping, jitter, loss, input acknowledgement, correction count, and interpolation buffer.

## Match integrity

- [ ] Match lifecycle is an explicit state machine.
- [ ] A trusted server finalizes valuable results, or the accepted peer-result verification and dispute model is documented and tested.
- [ ] Result submission and rewards are idempotent.
- [ ] Duplicate, late, reordered, conflicting, and retried result submissions are tested.
- [ ] Crash, abandonment, invalid match, maintenance, and disputed-result policies are documented.
- [ ] Ranked and reward changes have audit records and operator remediation.

## Security and player safety

- [ ] Every client message has authentication, authorization, schema, size, frequency, and semantic validation.
- [ ] Rate limits and abuse tests cover gameplay, queue, lobby, chat, and account paths.
- [ ] Cheat threats and telemetry are documented.
- [ ] Chat, voice, reports, blocks, mutes, bans, appeals, and evidence retention are implemented as required.
- [ ] Secrets, operator access, service identity, and dependency security have been reviewed.

## Production operations

- [ ] Dashboards cover login, queue time, match quality, allocation, join success, active sessions, tick time, bandwidth, disconnects, reconnects, and result finalization.
- [ ] Alerts have an owner, threshold, runbook, and player impact description.
- [ ] Load tests include launch bursts, queue bursts, full regions, stale servers, reconnect storms, and rolling deployments.
- [ ] Servers can drain without accepting new matches.
- [ ] Deployment, migration, canary, rollback, maintenance, and incident procedures are rehearsed.
- [ ] Durable progression has backups, restore tests, and a reconciliation process.

Return to the [interactive Glitch multiplayer prompt guide](https://www.glitch.fun/publishers/tools/multiplayer-game-development-prompts).
