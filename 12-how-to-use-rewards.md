# How To Use Rewards

**Rewards** let a node trigger an action when it is unlocked.

They can be used on vanilla nodes and custom nodes.

Add them in the `Economy` tab of the node modal, under `Reward`.

---

## Reward Types

TechTree supports these reward types:

- `ChatCommand`.
- `ConsoleCommand`.
- `Economics`.

---

## ConsoleCommand

`ConsoleCommand` runs from the server console.

Use it for commands that must be executed by the server or by another plugin from the server side.

Examples:

```text
inventory.giveto playerID stones 1000
oxide.grant user playerID some.permission
```

Use `ConsoleCommand` when the command normally belongs in the server console.

---

## ChatCommand

`ChatCommand` sends the command to the player's own console, as if the player typed it there.

Use it for commands that are designed to be executed by the player.

To run a chat command, send it through `chat.say`:

```text
chat.say "/kit starter"
```

Use `ChatCommand` when another plugin expects the player to run the command.

---

## playerID Placeholder

Use:

```text
playerID
```

TechTree replaces `playerID` with the player's Steam ID when the reward is executed.

The placeholder is case-sensitive.

Example:

```text
oxide.grant user playerID profession.electrician
```

---

## Economics

`Economics` rewards give money through the Economics plugin when it is loaded.

The value is the amount, for example `250`.

Use a whole number: the decimal separator depends on the server language settings.

This is separate from the node price currency.

Node prices always use item currency.

---

## When Rewards Run

- When the node is unlocked, alone or as part of a path.
- When the node is unlocked with a prototype.
- When a player studies a blueprint and the matching vanilla node unlocks automatically.

---

## Tree Completion Rewards

Each tree can also give rewards when a player unlocks **every node** of that tree.

They are set in the data file of the tree, under `Extra`. See **Data Files**.

They are not available in the editor.

They are not triggered by prototypes or blueprint study.

---

## Recommended Usage

- Use rewards for extra unlock effects.
- Keep reward commands simple.
- Test rewards on a staging server first.
- Make sure the target plugin command works before adding it as a reward.
