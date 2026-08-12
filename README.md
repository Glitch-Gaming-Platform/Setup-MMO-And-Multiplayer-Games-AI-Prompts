# Make Your Game Work Online

New to multiplayer? This guide is for you.

You do not need to understand servers or networking before you start. Pick the option that sounds like your game, copy one prompt, and give it to your AI coding tool.

[Open the simple prompt picker on Glitch](https://www.glitch.fun/publishers/tools/multiplayer-game-development-prompts)

## Start with three questions

1. Does the game end after each match?
2. Should the player's character, items, or money still exist tomorrow?
3. How many players are together at one time?

## Pick your game type

### Small online game

Choose this for:

- One-versus-one games
- Small co-op games
- Racing, fighting, sports, or arena matches
- Private games with friends

Start with [Choose the simplest online setup](prompts/00-choose-the-right-multiplayer-architecture.md).

If you want players to connect without renting a separate computer to run the match, use [Connect players directly](prompts/02a-peer-to-peer-and-listen-server.md).

### Large online match

Choose this when many players are in one match, but the match still ends.

Examples include a battle royale, large battlefield, or large survival round.

Start with [Set up a normal online match](prompts/02-pvp-session-multiplayer.md).

### Online world or MMO

Choose this only when players return later and expect their character, items, money, friends, or world changes to still be there.

Start with [Build one small part of an MMO world](prompts/03-mmo-persistent-world.md).

MMOs are much harder. Begin with one player, one character, one area, and one saved change.

## Can players connect without renting a game server?

Yes, sometimes.

For a small game:

- Two players can connect directly.
- One player can host the match.
- Fighting and strategy games can sometimes share button presses instead of sending the whole game world.

You may still need a small online helper to introduce the players. Some home and mobile internet connections also need a backup connection service.

Use a separate computer to run the match when:

- Winning or rewards are valuable.
- A player host could cheat.
- The host must not see secret information.
- Many players are in one game.
- The match must keep running when one player leaves.

## How to use a prompt

1. Open the prompt that matches your problem.
2. Copy the whole prompt.
3. Paste it into your AI coding tool.
4. Let the AI inspect your project before it changes anything.

The prompt may contain technical words. That is okay. The prompt is written for the AI, not for you.

Use one prompt at a time. Test the game before moving to the next prompt.

## Prompt list

| I need help with... | Use this |
| --- | --- |
| Choosing the right setup | [Choose the simplest online setup](prompts/00-choose-the-right-multiplayer-architecture.md) |
| Making the game rules trustworthy | [Choose who controls the match](prompts/01-shared-authoritative-foundation.md) |
| Connecting players without renting a game server | [Connect players directly](prompts/02a-peer-to-peer-and-listen-server.md) |
| Making a normal match or co-op game | [Set up an online match](prompts/02-pvp-session-multiplayer.md) |
| Building an MMO world | [Build a persistent online world](prompts/03-mmo-persistent-world.md) |
| Fixing lag or shaky movement | [Improve online movement and lag](prompts/04-network-quality-and-lag.md) |
| Putting waiting players into games | [Set up matchmaking](prompts/05-matchmaking-and-server-allocation.md) |
| Saving characters, items, and money | [Protect saved progress](prompts/06-persistence-and-economy-safety.md) |
| Testing cheating, crashes, and many players | [Prepare for real players](prompts/07-security-observability-and-load-testing.md) |
| Using Glitch | [Connect the game to Glitch](prompts/08-glitch-integration-options.md) |

## Simple planning sheets

- [Plan a small match](checklists/pvp-launch-checklist.md)
- [Plan an MMO](checklists/mmo-readiness-checklist.md)
- [Answer a few questions about your game](templates/multiplayer-architecture-brief.md)

## Where Glitch can help

Glitch can help with:

- Helping players find and join games
- Listing available matches or game servers
- Giving players short-lived join passes
- Organizing MMO worlds into areas
- Hosting a web game or supporting service
- Providing places to save accounts, progress, items, and other data

Your game still needs:

- Its own movement, combat, scores, and win rules
- Code that decides which players should play together
- Direct-connection or backup-connection code when a player runs the match
- Rules for saving characters, items, money, and world changes

You do not have to use Glitch. The prompts can be used with other providers or your own setup.
