# Prompt 06: Protect Multiplayer Persistence and Economy State

Use this for accounts, characters, progression, inventory, equipment, currency, rewards, crafting, trade, mail, auctions, guild banks, housing, and persistent world changes.

## Role

Act as a principal game backend, database, security, and economy-integrity engineer.

## Inventory durable state

Read the repository, schema, migrations, caches, queues, game-server code, APIs, jobs, tests, backup configuration, and operator tools.

List every durable aggregate and assign:

- Stable identifier.
- Single write authority.
- Readers.
- Transaction boundary.
- Consistency requirement.
- Concurrency strategy.
- Idempotency key.
- Audit history.
- Cache policy.
- Event publication.
- Reconciliation.
- Backup and restore requirement.
- Player-remediation procedure.

Evaluate account, character, progression, inventory, equipment, currency, quests, guild membership, guild bank, friends, mail, crafting, trade, auction, housing, world state, match history, rankings, purchases, and entitlements as applicable.

## Authority rules

- Clients never set balances, ownership, rewards, item creation, item destruction, trade completion, crafting completion, or progression.
- Game servers submit trusted domain commands or results; they do not bypass the owner of durable data.
- Every valuable mutation is authorized, validated, auditable, idempotent, and safe to retry.
- One aggregate should not have multiple independent writers.
- Cache is not the only source of truth for valuable state.

## Duplication and loss threat model

Create explicit scenarios for:

- Double click or repeated request.
- Network retry after the server committed but the response was lost.
- Client disconnect during trade, craft, purchase, mail claim, reward, or zone transfer.
- Two active sessions for one character.
- Two game servers believing they own one character.
- Match result submitted more than once.
- Job or event redelivery.
- Service timeout after a downstream commit.
- Database deadlock or failover.
- Cache loss or stale cache.
- Rollback to an older world process.
- Partial trade or transfer.
- Auction expiry racing with purchase.
- Mail attachment claimed twice.
- Crafting completion worker running twice.
- Backup restore followed by replay.

For each scenario document prevention, detection, audit evidence, reconciliation, and player remediation.

## Transaction and workflow design

Use a single database transaction when all required state shares one owner and database. When a valuable workflow crosses owners:

- Define the state machine.
- Persist intent before side effects.
- Use idempotency at every boundary.
- Use outbox and inbox patterns where event delivery must survive process failure.
- Define timeouts and retries.
- Avoid holding distributed locks across services.
- Use compensation or reconciliation for partial completion.
- Expose pending states safely to players.

Do not claim exactly-once delivery. Prove exactly-once business effect through ownership, idempotency, and reconciliation.

## Concurrency

Choose optimistic concurrency, pessimistic locking, serializable transactions, atomic database operations, or queues per aggregate. Explain the tradeoff.

Test simultaneous:

- Item moves.
- Currency spends.
- Reward claims.
- Trade acceptance and cancellation.
- Auction purchase and expiry.
- Mail claim and deletion.
- Craft completion and cancellation.
- Character login.
- Guild bank withdrawal.
- Zone transfer and logout.

## Database, cache, and schema

Document:

- Primary keys and uniqueness constraints.
- Foreign-key or invariant enforcement.
- Indexes and hot-key risks.
- Schema versioning.
- Online migration and rollback.
- Cache invalidation and stampede behavior.
- Read replicas and stale-read risk.
- Data partitioning.
- Retention.
- Backup schedule.
- Point-in-time recovery.
- Restore validation.

Create integrity queries and reconciliation jobs that detect impossible balances, duplicate ownership, negative inventory, missing references, stuck workflows, and divergent summaries.

## First vertical slice

Prove:

1. Authenticate.
2. Load a durable character.
3. Enter one authoritative session or zone.
4. Perform one valuable action.
5. Commit exactly one business effect.
6. Lose the response and retry.
7. Disconnect and reconnect.
8. Verify audit, state, and player-visible result.
9. Restore a test backup and verify integrity.

## Delivery

Include data ownership diagrams, workflow state machines, migrations, tests, concurrency harnesses, failure injection, dashboards, alerts, reconciliation tools, backup and restore evidence, rollout, rollback, and accepted risks.

Interactive version: [Multiplayer and MMO Game Development Prompts](https://www.glitch.fun/publishers/tools/multiplayer-game-development-prompts).
