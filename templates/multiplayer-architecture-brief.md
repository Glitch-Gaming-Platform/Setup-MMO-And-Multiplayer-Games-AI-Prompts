# Multiplayer Architecture Brief

Complete this before asking an AI to design or implement multiplayer. Unknown answers should be marked Unknown and turned into a research or prototype task.

## Game and repository

- Game:
- Genre and core loop:
- Engine and version:
- Client platforms:
- Current repository structure:
- Current backend:
- Current hosting:
- Current identity provider:
- Current transport:
- Proposed topology: direct P2P, mesh, listen server, deterministic lockstep, rollback, or dedicated:
- Current databases and cache:
- Existing multiplayer code:
- Existing tests and test commands:

## Session model

- Competitive, cooperative, social, or mixed:
- Players per party:
- Players per match or room:
- Players visible in the busiest location:
- Players per zone:
- Sessions have a clear end:
- State discarded when a session ends:
- State that survives a session:
- Join-in-progress:
- Backfill:
- Spectators:
- Replays:
- Host migration:
- Dedicated, listen-server, direct-P2P, lockstep, or rollback model:
- Separate gameplay server required:
- Host selection:
- Host advantage accepted:
- Malicious-host risk accepted:
- Hidden information visible to host:
- Signaling service:
- STUN or NAT discovery:
- Hole punching:
- TURN or platform relay fallback:
- IPv4, IPv6, carrier-grade NAT, and mobile-network support:
- Host migration or explicit session termination:
- Desync detection and recovery:

## Gameplay and networking

- Target server tick rate:
- Target snapshot or replication rate:
- Target client frame rate:
- Fastest player movement:
- Fastest projectile or vehicle:
- Physics requirements:
- Maximum acceptable input latency:
- Expected regional RTT:
- Packet loss and jitter target:
- Prediction required:
- Reconciliation required:
- Interpolation buffer:
- Lag compensation or rewind:
- Interest-management rules:
- Maximum entities relevant to one player:
- Estimated bytes per player per second:

## Parties, lobbies, and matchmaking

- Party rules:
- Lobby rules:
- Public server browser:
- Private sessions and passwords:
- Queue dimensions:
- Skill model:
- Region and latency policy:
- Cross-platform and input policy:
- Role or team composition:
- Queue widening:
- Match acceptance:
- Backfill:
- Server allocation:
- Cold-start tolerance:
- Reconnect grace:

## Persistence

- Account state:
- Character state:
- Progression:
- Inventory and equipment:
- Currency:
- Crafting:
- Trading:
- Mail:
- Auction:
- Guilds:
- Friends:
- Quests:
- Housing:
- World state:
- Match history:
- Rankings:
- Required consistency for each:
- Backup and restore targets:

## MMO topology, if required

- Realm meaning:
- Shard meaning:
- Zone meaning:
- Layer meaning:
- Instance meaning:
- Capacity per boundary:
- Party and guild co-location:
- Zone transfer:
- Seamless or loading transition:
- Server ownership:
- State handoff:
- Crash recovery:
- Draining and maintenance:

## Security and safety

- Trusted server decisions:
- Client data that is never trusted:
- Join credential design:
- Replay protection:
- Rate limits:
- Cheat threats:
- Economy threats:
- Chat and social abuse:
- Moderation tools:
- Ban and appeal policy:
- Operator access:
- Secrets management:
- Audit retention:

## Scale and operations

- Expected concurrent players now:
- Expected concurrent players at launch:
- Growth milestone:
- Regions:
- Availability target:
- Queue-time target:
- Join-success target:
- Tick-time target:
- Persistence-latency target:
- Deployment frequency:
- Rolling deployment strategy:
- Draining:
- Rollback:
- Autoscaling:
- Load-test plan:
- Incident ownership:
- Disaster-recovery target:

## Provider decisions

- Systems to build:
- Systems to buy:
- Providers being evaluated:
- Glitch capabilities being considered:
- Provider-neutral adapter boundaries:
- Export and migration plan:
- Cost assumptions:
- Capabilities requiring current documentation verification:

## Definition of done

- First vertical slice:
- Required automated tests:
- Required network impairment tests:
- Required concurrency tests:
- Required load tests:
- Required security tests:
- Required recovery tests:
- Required dashboards and alerts:
- Required documentation:
- Known risks accepted for this milestone:
