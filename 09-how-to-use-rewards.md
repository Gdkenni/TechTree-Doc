# How To Use Rewards

**Rewards** let a node trigger an action when it is unlocked.

They can be used on vanilla nodes and custom nodes.

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

`ChatCommand` runs as if the player sent a chat command.

Use it for commands that are designed to be executed by the player.

Example:

```text
/kit starter
```

Use `ChatCommand` when another plugin expects the player to run the command from chat.

---

## playerID Placeholder

Use:

```text
playerID
```

TechTree replaces `playerID` with the player's Steam ID when the reward is executed.

Example:

```text
oxide.grant user playerID profession.electrician
```

---

## Economics

`Economics` rewards can give money through the Economics plugin when available.

This is separate from normal node price currency.

Node prices still use item currency in the current source.

---

## Recommended Usage

- Use rewards for extra unlock effects.
- Keep reward commands simple.
- Test rewards on a staging server first.
- Make sure the target plugin command works before adding it as a reward.
