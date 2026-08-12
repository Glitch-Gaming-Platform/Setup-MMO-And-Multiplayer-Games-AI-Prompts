# Prompt 04: Improve Network Quality, Prediction, and Lag Compensation

## Role

Act as a multiplayer network and gameplay-feel specialist. Do not tune by intuition alone. Capture a reproducible baseline before changing the implementation.

## Measure first

Record:

- Input-to-local-feedback latency.
- Input-to-authoritative-confirmation latency.
- Server tick rate and p50, p95, and p99 tick time.
- Snapshot or replication rate.
- Packet size, message rate, and bandwidth per player.
- Round-trip latency distribution.
- Jitter and packet loss.
- Input acknowledgement age.
- Prediction error.
- Correction count and magnitude.
- Interpolation buffer depth.
- Extrapolation time.
- Visible remote-player jitter.
- Hit disagreement or collision disagreement.

Add developer overlays and server metrics when the measurements do not exist.

## Prediction and reconciliation

Inspect whether the client:

- Sequences input.
- Predicts only safe local presentation and movement.
- Stores unacknowledged inputs.
- Receives authoritative state with the last processed input.
- Rewinds to the server result.
- Replays later inputs.
- Smooths small visual corrections without hiding material state changes.
- Hard-snaps teleports and large corrections.

Inspect whether the server:

- Validates input rate, order, timing, acceleration, speed, collision, cooldown, and resources.
- Simulates accepted input.
- Rejects or clamps impossible input.
- Reports enough state for reconciliation.
- Prevents stale or replayed input from changing trusted state.

## Remote interpolation

Implement a bounded snapshot buffer. Choose the interpolation delay from measured snapshot interval and jitter. Define behavior for late, missing, duplicated, and reordered snapshots.

Use bounded extrapolation only when gameplay tolerates it. Stop or transition safely when the extrapolation limit is reached. Add teleport and discontinuity handling.

## Server rewind and lag compensation

Use rewind only for actions that require historical validation.

Define:

- Historical state retained by the server.
- Snapshot precision and memory budget.
- Validated action timestamp.
- Clock synchronization.
- Maximum rewind window.
- Which entities and hitboxes rewind.
- Which obstructions and world state are historical.
- Fairness policy for low- and high-latency players.
- Timestamp manipulation and future-time protection.
- Debug visualization of current and rewound state.

Test rapid cover changes, moving platforms, teleporting, projectiles, melee, vehicles, extreme latency, forged timestamps, packet bursts, high server load, and players with very different latency.

## Network simulation matrix

At minimum test representative combinations of:

- 20, 50, 100, 180, and 300 ms RTT.
- Stable and bursty jitter.
- 0, 1, 3, 5, and 10 percent packet loss where the target platform requires it.
- Packet duplication.
- Packet reordering.
- Client frame stalls.
- Server tick stalls.
- Bandwidth restriction.
- Disconnect and reconnect.

Do not optimize only for average latency. Report behavior and player impact at p95 and the supported worst case.

## Delivery

Provide:

- Baseline and after measurements.
- Chosen tick, snapshot, and buffer values with reasoning.
- Network simulation commands or test harness.
- Automated tests.
- Gameplay tradeoffs.
- Bandwidth and memory cost.
- Remaining failure cases.
- Safe rollback.
- Definition of done.

Keep trusted outcomes authoritative even when local presentation is predicted.

Interactive version: [Multiplayer and MMO Game Development Prompts](https://www.glitch.fun/publishers/tools/multiplayer-game-development-prompts).
