# Prompt 05: Build Matchmaking and Server Allocation

Use this for PvP queues, co-op activities, ranked modes, MMO instances, dungeon finders, and any system that must convert waiting players into an assigned session. Dedicated-server sessions need capacity allocation; P2P sessions need host selection and connection negotiation instead.

## Role

Act as a principal matchmaking, distributed-systems, and game-server capacity engineer.

## Audit first

Determine which parts currently exist:

- Ticket creation, polling, cancellation, and expiry.
- Party ownership and membership snapshot.
- Matcher worker.
- Skill or quality model.
- Region and latency data.
- Server registry and health.
- Process or fleet startup.
- Capacity reservation.
- Match and assignment record.
- Secure join credential.
- P2P host selection, signaling, NAT traversal, and relay assignment when peer-hosted play is supported.
- Backfill.
- Observability and operator tools.

Do not call the system complete matchmaking if it only stores tickets. Do not call it server allocation if it only lists registered servers.

## Queue model

Define the smallest justified set of queue dimensions:

- Game mode.
- Ruleset.
- Client and server build compatibility.
- Platform and cross-play policy.
- Input method.
- Region and measured latency.
- Skill rating and uncertainty.
- Party size and party integrity.
- Team size and composition.
- Player role.
- Language.
- Trust, moderation, or restricted-pool status.
- Tournament or event identifier.

For each dimension state whether it is hard, soft, or widened over time. Define acceptable quality, maximum wait, widening steps, and player-facing queue estimates.

## Ticket lifecycle

Model queued, claimed, proposed if used, matched, assigning, assigned, joining, cancelled, expired, failed, and completed states.

Specify:

- Idempotent enqueue.
- Party owner and immutable membership snapshot.
- Atomic claim and lease.
- Lease expiry and recovery.
- Cancellation during every state.
- Timeout and retry.
- Duplicate request behavior.
- Client polling or push.
- Version and region change behavior.
- Audit history.

Use database or queue primitives that prevent two matcher workers from owning the same ticket. Test the actual concurrency behavior.

## Match formation

Document:

- Candidate selection.
- Party-preserving rules.
- Team construction.
- Skill and uncertainty calculation.
- Region and latency choice.
- Role or composition constraints.
- Rematch avoidance.
- Widening.
- Proposal acceptance if required.
- Backfill.
- Deterministic tie-breaking.
- Quality score.

Create deterministic unit tests with fixed inputs and expected matches. Add property tests or large simulation tests for fairness, starvation, and queue growth.

## Server allocation

Separate match formation from capacity allocation.

For P2P or listen-host sessions, server allocation may be omitted. Instead define host selection, signaling, reachability checks, relay fallback, synchronized peer assignment, and host-failure behavior. A signaling record is not a successful peer connection.

Define:

- Who starts server processes.
- Registration, heartbeat, version, region, mode, endpoint, and capacity.
- Ready, reserving, active, draining, unhealthy, and terminated states.
- Atomic reservation or lease.
- Prevention of double assignment.
- Warm pools and cold starts.
- Autoscaling signal.
- Failed startup and failed reservation.
- Retry and alternate region policy.
- Session configuration delivery.
- Secure join credential issuance.
- Release and cleanup.

For MMO instances, include topology ownership and instance lifecycle. For session games, avoid MMO topology when a match assignment is sufficient.

## Join security

Join credentials should be short-lived and bound to player, party or assignment, server, session, purpose, and expiry. Include nonce or token ID, replay protection, revocation, clock skew, and one-time behavior where appropriate.

The game server must validate the credential with trusted configuration or a trusted backend. A client-visible assignment is not proof of authorization.

## Failure and concurrency tests

Test:

- Two workers claim the same tickets.
- Ticket cancel during claim, formation, allocation, and assignment.
- Party membership changes while queued.
- Stale or unhealthy server record.
- Server becomes full after discovery.
- Server process fails to start.
- Reservation timeout.
- Assignment written twice.
- Join credential replay.
- Region capacity exhausted.
- Build version mismatch.
- Matcher restart.
- Database or queue slowdown.
- Backfill race.
- Reconnect while a replacement is being considered.

## Metrics

Measure queue time, queue abandonment, match quality, widened constraints, party integrity, region choice, estimated versus actual latency, allocation latency, cold-start rate, allocation failure, join success, backfill success, empty-server waste, and cost per active player-hour.

Deliver architecture, state machines, sequence diagrams, changed files, tests, simulations, dashboards, alerts, runbooks, and rollback.

Interactive version: [Multiplayer and MMO Game Development Prompts](https://www.glitch.fun/publishers/tools/multiplayer-game-development-prompts).
