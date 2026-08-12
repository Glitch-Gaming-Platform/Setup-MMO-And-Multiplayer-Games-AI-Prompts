# Prompt 01: Build the Shared Authoritative Foundation

PvP and MMO games share this foundation. The MMO path adds persistence, topology, distributed ownership, orchestration, and recovery later.

## Role

Act as a senior multiplayer gameplay, backend, and network engineer. Inspect the existing repository and architecture before changing code.

## Goal

Build or repair the smallest end-to-end vertical slice in which two authenticated players:

1. Obtain secure permission to enter one session.
2. Connect through the chosen direct-P2P, listen-host, lockstep, rollback, or dedicated-server topology.
3. Send sequenced input intent.
4. Receive replicated authoritative state.
5. See responsive local prediction and smooth remote interpolation where the gameplay needs it.
6. Recover from corrections.
7. Disconnect and reconnect without duplicating state.
8. Leave with a clear authoritative outcome.

## Trust boundary

Create a matrix for movement, physics, combat, abilities, cooldowns, items, objectives, score, results, progression, currency, purchases, chat, and social actions.

For every action define:

- Client intent schema and protocol version.
- Authentication, authorization, and session checks.
- Size, frequency, semantic, and rate-limit validation.
- Authoritative state transition.
- Idempotency and duplicate behavior.
- Replication audience and privacy.
- Rejection behavior for the player.
- Detailed diagnostics for trusted logs.
- Automated tests and abuse tests.

For a listen server or dedicated server, never trust client positions, hit results, damage, cooldown completion, ownership, currency, score, victory, rewards, or progression without host or server validation.

For deterministic lockstep or rollback, define which peer inputs are accepted, how state hashes detect desync, how malicious or impossible inputs are rejected, and which outcomes cannot be trusted for high-value ranked or economy changes.

## Protocol

Design connect, authenticate, reserve, join, ready, input, snapshot, delta, event, correction, spawn, despawn, chat, heartbeat, disconnect, reconnect, resynchronize, leave, and server-shutdown messages.

For each message record:

- Direction.
- Reliable or unreliable delivery.
- Ordering requirements.
- Maximum size.
- Expected frequency.
- Validation.
- Authorization.
- Privacy.
- Version compatibility.
- Behavior under duplication, delay, loss, and reordering.

Use sequence numbers, acknowledgements, timestamps, clock synchronization, heartbeat, timeout, and resynchronization appropriate to the transport. For Internet P2P, include signaling, NAT discovery, hole punching, relay fallback, peer authentication, and host migration or termination behavior.

## Responsiveness

Measure before changing:

- Input-to-feedback latency.
- Server tick time and rate.
- Snapshot or replication rate.
- Packet size and bandwidth.
- Correction frequency and magnitude.
- Interpolation buffer.
- Visible jitter.

Implement the justified subset of:

- Local input prediction.
- Server replay of validated inputs.
- Reconciliation from the last acknowledged input.
- Buffered interpolation for remote entities.
- Bounded extrapolation.
- Teleport and hard-snap thresholds.
- Clock and timestamp handling.
- Debug overlays for ping, jitter, packet loss, buffer depth, acknowledgements, and corrections.

## Identity and reconnect

Use short-lived, audience-bound, single-purpose join credentials. Define expiry, replay protection, nonce or token ID, clock skew, reservation ownership, reconnect grace, duplicate connection, takeover, kick, ban, server restart, and revocation behavior.

Test expired, replayed, forged, wrong-player, wrong-server, already-consumed, and revoked credentials. Prove reconnect cannot duplicate participation, character state, inventory, match results, or rewards.

## Required evidence

Test at representative latency levels with jitter, packet loss, duplication, reordering, malformed messages, client frame stalls, server stalls, disconnects, and reconnects. Include protocol compatibility and rolling-deployment tests.

Deliver:

- Architecture and sequence diagrams.
- Message catalog.
- Trust-boundary matrix.
- Changed files.
- Tests and commands run.
- Before and after measurements.
- Known limitations.
- Next milestone.
- Definition of done.

Do not add matchmaking, dedicated server allocation, MMO topology, or distributed persistence until this vertical slice works and the game has proved it needs them.

Interactive version: [Multiplayer and MMO Game Development Prompts](https://www.glitch.fun/publishers/tools/multiplayer-game-development-prompts).
