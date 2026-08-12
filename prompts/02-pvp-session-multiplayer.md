# Prompt 02: Build PvP and Session Multiplayer

Use this after the shared authoritative foundation works. This path is for bounded matches, rounds, rooms, races, co-op missions, arena games, extraction sessions, and similar experiences.

## Role

Act as a principal session-multiplayer engineer. Preserve the current engine and backend unless measured evidence requires a change.

## Goal

Build the smallest production session stack justified by the game:

- Direct P2P, deterministic lockstep or rollback, a listen host, or dedicated servers selected from explicit trust and scale requirements.
- Party creation, invitations, leadership, membership, ready state, and queue ownership.
- Public or private lobbies and server browser filters.
- Passwords, reservations, capacity, version, region, mode, and join-in-progress.
- Matchmaking tickets, cancellation, timeout, widening, assignment, and backfill when needed.
- Healthy match-server registration, heartbeat, discovery, reservation, draining, and allocation.
- Secure join tickets and reconnect grace.
- Match lifecycle from forming through completion or termination.
- Authoritative results and idempotent rewards.
- Spectator, rematch, replay, tournament, or migration only when required.

## Required design

Create sequence diagrams for:

1. Party formation to queue.
2. Ticket claim to match formation.
3. Server allocation to reservation.
4. Secure join.
5. Ready and match start.
6. Disconnect and reconnect.
7. Match completion and reward application.
8. Allocation failure, server crash, and result retry.

When the game is peer-hosted, replace dedicated allocation steps with signaling, connection negotiation, NAT traversal, relay fallback, host election, synchronized start, host departure, migration or explicit termination, and result-trust behavior.

Model states explicitly. At minimum evaluate:

- Party: forming, ready, queued, assigned, in session, disbanded.
- Ticket: queued, claimed, matched, cancelled, expired, failed.
- Server: starting, ready, reserving, active, draining, unhealthy, terminated.
- Match: forming, warmup, active, paused if supported, overtime, completed, abandoned, invalid, terminated.
- Result: pending, validated, finalized, applied, disputed, repaired.

## Matchmaking and allocation

Do not treat a ticket database table as matchmaking. Implement or identify a worker that atomically claims tickets, applies party and quality rules, forms a match, reserves healthy capacity, creates an assignment, and issues secure join credentials.

Do not treat a server registry as allocation. Define who starts capacity, selects a healthy server, leases it, prevents double assignment, handles cold starts, retries failures, and drains old versions.

Test simultaneous claims, cancel during assignment, stale servers, full servers, failed starts, incompatible builds, party-size edges, region exhaustion, backfill races, and duplicate assignments.

## Competitive integrity

A dedicated server or listen host owns start time, objective state, score, kills, damage, victory, defeat, overtime, and final simulation state. A listen host is still a player-controlled machine and can cheat. Deterministic peers can also collude or send malicious inputs.

Do not apply high-value ranked, economy, or tournament outcomes from an untrusted peer session without a reviewed verification and dispute model. If that model is not credible, require a dedicated authoritative server for those modes.

Add the justified subset of:

- Server-side movement and combat validation.
- Rate and acceleration limits.
- Cooldown and resource validation.
- Bounded lag compensation and server rewind.
- Timestamp manipulation protection.
- Anomaly telemetry.
- Replay or evidence capture.
- Moderation, reports, bans, blocks, mutes, and appeals.

## Persistence boundary

List state that disappears with the match and durable state that survives. Keep durable writes outside the high-frequency simulation path where possible.

Make match finalization and rewards idempotent. Test duplicate submissions, reordered events, two servers claiming one match, retry after timeout, partial reward failure, crash before acknowledgement, and reconciliation.

## Explicit exclusions

Unless the requirements prove otherwise, do not add:

- Persistent realms or shards.
- Always-running zones.
- Seamless world handoff.
- Distributed character, inventory, guild, quest, housing, or auction services.
- Persistent world simulation.
- MMO orchestration.

Interest management is still valid for large bounded sessions. Add it from entity and bandwidth measurements, not as a reason to redesign the game as an MMO.

## Delivery

Implement in reviewable milestones. Add architecture docs, state machines, sequence diagrams, contract tests, concurrency tests, network impairment tests, security tests, load tests, dashboards, alerts, deployment, draining, rollback, and operator runbooks.

End with the [PvP launch checklist](../checklists/pvp-launch-checklist.md).

Interactive version: [Multiplayer and MMO Game Development Prompts](https://www.glitch.fun/publishers/tools/multiplayer-game-development-prompts).
