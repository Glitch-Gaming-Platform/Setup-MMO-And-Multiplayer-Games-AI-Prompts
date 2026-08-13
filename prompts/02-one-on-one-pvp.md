# Prompt: Add One-on-One PvP

Use this when exactly two players compete in one match.

Examples:

- Chess or card games
- Fighting games
- One-on-one racing
- Tennis or other sports duels
- Turn-based battles
- Simple arena duels

This should be the smallest online setup in the guide.

Copy everything below into your AI coding tool.

---

# Add the smallest practical one-on-one online mode

This game has exactly two players in one match. Treat this as a small feature, not a general multiplayer platform or MMO.

Read the repository, game loop, tests, engine, target platforms, and existing online code before making changes.

## Choose the lightest option

Choose one and explain why:

1. Direct connection: the two players connect to each other.
2. Player host: one player runs the match and the other joins.
3. Lockstep or rollback: the players share button presses or moves and both run the same game.
4. Small dedicated server: use only when ranked play, valuable rewards, hidden information, cheating, platform rules, or host advantage require it.

## Build only this basic flow

- One player creates a private match or invite code.
- The second player joins.
- Both players say they are ready.
- The match starts.
- The players send only the moves or game information this game needs.
- The game handles normal delay and one short disconnect.
- A player can surrender or leave.
- The match ends with one valid result.
- Save only the result or progress the game actually needs.

## Do not build these unless the game clearly needs them

- General matchmaking or skill queues
- Parties or party leaders
- Public lobby lists
- Server browsers
- Players joining a match that already started
- Replacing players who leave
- Spectators
- Several hosting regions
- Automatic fleets of game servers
- Host migration; ending or pausing a short match may be safer
- MMO worlds, realms, shards, zones, or instances
- Guilds, auctions, mail, trading, housing, or a world economy
- A database when the game does not save accounts, rankings, history, or rewards
- Voice chat when it is not part of the game

## Keep the match fair

For a casual private match, explain the risk of trusting a player host.

For ranked play, tournaments, valuable rewards, gambling-like stakes, or secret information, do not trust a player-controlled computer without a reviewed safety plan. Recommend a small dedicated server only if it is truly needed.

## Connect the players

Use the engine or platform's built-in networking service when possible.

For Internet play, add only the small service needed to introduce the two players and a backup connection when direct connection fails. Do not build a global server system for a two-player game.

## Test

Test:

- Two players on the same network
- Two players on different home networks
- A connection that needs the backup connection service
- Normal delay and lost messages
- One player disconnecting
- Reconnect or surrender
- Duplicate or invalid moves
- Both players claiming different final results

## Done means

Two players can create or join one private match, play the full game, handle a disconnect safely, finish with one valid result, and start another match without old data leaking into it.

Return:

- Files changed
- Tests run
- Risks that remain
- The next smallest improvement

---

[Return to the simple Glitch prompt picker](https://www.glitch.fun/publishers/tools/multiplayer-game-development-prompts).
