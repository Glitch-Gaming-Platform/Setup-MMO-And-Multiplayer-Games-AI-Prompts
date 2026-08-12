# Prompt 02A: Build Peer-to-Peer or Listen-Server Multiplayer

Use this when a bounded PvP or co-op game does not justify a separate dedicated gameplay server.

Peer-to-peer does not mean that every online service disappears. Most Internet games still need some combination of identity, invitations, lobbies, signaling, matchmaking, NAT discovery, relay fallback, telemetry, moderation, and durable progression.

## Role

Act as a senior peer-to-peer networking, gameplay-simulation, security, and platform-integration engineer. Inspect the engine, current networking code, target stores and consoles, backend, game rules, player count, hidden information, competitive stakes, and reward model before changing code.

## Choose and justify the topology

Evaluate:

### Direct peer-to-peer mesh

Every peer connects to every other required peer.

Use when:

- The group is very small.
- Bandwidth grows acceptably with peer count.
- The game can manage multiple connections.
- Trust and hidden-information risks are accepted.

Avoid when:

- Player count makes connection and bandwidth growth too large.
- Peers must not see one another's network information.
- One stable authority is required.

### Listen server or host-authoritative peer

One player's game process acts as the authoritative server while that player also plays.

Use when:

- The group is small.
- Host advantage and host power are acceptable.
- A host can be selected with acceptable latency and reachability.
- Host departure can migrate safely or terminate the session.

Risks:

- The host can inspect or modify authoritative state.
- The host has lower latency.
- The session depends on the host's hardware, bandwidth, and uptime.
- Migration can be complex or exploitable.

### Deterministic lockstep

Peers exchange ordered inputs and simulate the same deterministic state.

Use when:

- The simulation can be deterministic.
- Input delay is acceptable.
- Bandwidth should scale with input rather than world state.
- The genre fits, such as many strategy games.

Risks:

- The slowest peer can delay progress.
- Nondeterminism causes desync.
- Hidden information and peer cheating still need design.

### Rollback networking

Peers predict missing remote inputs, restore an earlier snapshot, and re-simulate when the real input arrives.

Use when:

- Immediate input response is critical.
- The game has a small deterministic simulation.
- Snapshot and re-simulation cost is bounded.
- The genre fits, such as many fighting games.

Risks:

- Rollback artifacts grow with latency.
- Simulation state must be reproducible.
- Audio, particles, animation, and other side effects need rollback-safe presentation.

## Dedicated-server escalation criteria

Recommend a dedicated authoritative server when one or more of these cannot be accepted:

- A player host can cheat or inspect hidden information.
- High-value ranked, tournament, progression, currency, or item outcomes depend on the session.
- Host advantage materially changes competitive fairness.
- Player count or bandwidth exceeds peer-hosted limits.
- Host migration is required but cannot be made safe.
- The game needs stable public servers or long-running sessions.
- Platform policy or cross-play rules require controlled server infrastructure.
- Denial-of-service and peer IP exposure risks are unacceptable.

## Signaling and connection establishment

Design an authenticated signaling flow. Signaling can be a small service even when gameplay is P2P.

It should exchange:

- Session and peer IDs.
- Short-lived connection credentials.
- Protocol and build version.
- Supported transport.
- ICE or equivalent connection candidates.
- Relay assignment when needed.
- Host choice.
- Ready and synchronized-start state.
- Reconnect or migration metadata.

Do not use signaling messages as proof that a gameplay connection succeeded. Add explicit connection, authentication, and ready acknowledgement.

## NAT traversal and relay

For Internet play, evaluate and implement the target-platform equivalent of:

- ICE-style candidate gathering.
- STUN for public endpoint discovery.
- UDP hole punching.
- IPv4 and IPv6.
- Full-cone, restricted, port-restricted, and symmetric NAT.
- Carrier-grade NAT.
- Corporate, school, hotel, and mobile networks.
- TURN or a platform relay when direct connection fails.

Do not depend only on manual port forwarding or UPnP. They can be optional optimizations, not the only path.

Prefer a relay or platform privacy layer when exposing player IP addresses creates unacceptable privacy, harassment, or denial-of-service risk.

Measure direct-connection success rate, relay rate, time to connect, connection failure, regional relay latency, bandwidth, and relay cost.

## Security

- Authenticate the session and every peer.
- Bind short-lived credentials to player, session, peer role, purpose, and expiry.
- Encrypt gameplay traffic.
- Prevent replay and reject stale sequence numbers.
- Validate message type, size, frequency, order, timing, and semantics.
- Rate-limit signaling and gameplay paths.
- Do not send long-lived account credentials to peers.
- Do not let a player host directly grant durable currency, items, entitlements, or ranked rewards.
- Protect peer network information and logs.
- Threat-model malicious hosts, colluding peers, packet forgery, desync attacks, disconnect abuse, and host-migration abuse.

## Simulation and synchronization

For a listen host:

- Define host-authoritative state.
- Sequence and validate client input.
- Predict locally where needed.
- Reconcile clients to host state.
- Interpolate remote state.
- Bound lag compensation.
- Make host advantage visible in testing.

For lockstep:

- Use a fixed simulation step.
- Define input delay and ordering.
- Isolate nondeterministic time, random, physics, iteration, and floating-point behavior.
- Hash state regularly.
- Detect and diagnose desync.
- Define pause, drop, resync, or terminate behavior.

For rollback:

- Define input prediction.
- Store bounded snapshots.
- Restore and re-simulate deterministically.
- Separate simulation from presentation side effects.
- Define maximum rollback window.
- Handle inputs older than the window.
- Add frame-by-frame replay and desync debugging.

## Host selection and migration

Score host candidates by:

- Measured latency to all peers.
- Direct and relay reachability.
- Upload bandwidth.
- Hardware and frame stability.
- Platform support.
- Party ownership.
- Trust or moderation constraints.
- Battery and network type for mobile devices.

Define what happens when:

- The host leaves intentionally.
- The host crashes.
- The host loses network.
- Two peers believe they are the new host.
- The old host returns.
- Migration occurs during a valuable action.
- No eligible host remains.

If safe migration is not justified, terminate the session clearly and preserve only independently trusted durable state.

## Results and progression

Separate match simulation from durable rewards.

For casual or private sessions, peer or host results may be accepted with clearly documented risk. For ranked, tournament, economy-bearing, or valuable outcomes, require a credible verification design such as a trusted dedicated server, authoritative replay verification where technically sound, cross-peer evidence with dispute handling, or a limited reward model that contains abuse.

Do not describe peer consensus as trustworthy when peers can collude.

## Test matrix

Test:

- Same LAN.
- Two different home NATs.
- Symmetric NAT.
- Carrier-grade NAT.
- IPv6-only and mixed IPv4/IPv6 where supported.
- Direct connection.
- Relay-only connection.
- High latency, jitter, loss, duplication, and reordering.
- Host advantage.
- Host CPU and network degradation.
- Host departure before start, during play, and during finalization.
- Migration success and split-host prevention.
- Mobile network changes.
- Suspend and resume.
- Malformed and malicious peer messages.
- Credential replay.
- Lockstep or rollback desync.
- Relay capacity exhaustion.
- Platform cross-play.

## Delivery

Return:

- Topology decision and dedicated-server escalation criteria.
- Signaling and connection sequence diagrams.
- NAT traversal and relay design.
- Host selection and migration or termination policy.
- Trust and result-integrity model.
- Protocol contracts.
- Implementation milestones.
- Automated, network, security, desync, and failure tests.
- Direct and relay measurements.
- Player-facing connection and recovery messages.
- Changed files and commands.
- Known risks.
- Definition of done.

Interactive version: [Multiplayer and MMO Game Development Prompts](https://www.glitch.fun/publishers/tools/multiplayer-game-development-prompts).
