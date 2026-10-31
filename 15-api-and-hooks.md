# API And Hooks

**TechTree** includes API methods and hooks for other plugins.

These can be used to read player data, restore progression, clear unlocks, block an unlock, or react when a player unlocks a node.

---

## API Methods

```csharp
Dictionary<string, object> API_GetPlayerData(BasePlayer player)
```

Returns the player's TechTree data in an API-friendly format.

```csharp
bool API_SetPlayerData(BasePlayer player, Dictionary<string, object> apiData)
```

Imports player TechTree data from an API-friendly dictionary.

The plugin cleans invalid node IDs before saving.

```csharp
bool API_ClearPlayerWorkbenchData(BasePlayer player, Workbench workbench)
```

Clears the player's unlock data only for the provided workbench category.

```csharp
bool API_ClearPlayerData(BasePlayer player)
```

Clears all TechTree unlock data for the player.

---

## Player API Data Format

This is the format returned by `API_GetPlayerData`.

It is also the format expected by `API_SetPlayerData`.

```json
{
  "workbench": {
    "Workbench_1": [123, 456],
    "Workbench_2": [789],
    "Workbench_3": [],
    "Engineering": []
  }
}
```

Each workbench key contains a list of unlocked node IDs.

---

## API_GetPlayerData / API_SetPlayerData

These two calls let you read and write a player's unlocked nodes from another plugin.

### Read

```csharp
var data = TechTree?.Call<Dictionary<string, object>>("API_GetPlayerData", player);
if (data == null) return;

var workbenches = data["workbench"] as Dictionary<string, object>;

if (workbenches.TryGetValue("Workbench_1", out var raw))
{
    var unlocked = raw as List<int>;
    bool hasNode = unlocked?.Any(id => Convert.ToInt32(id) == 47) ?? false;
}
```

### Write

```csharp
var data = TechTree?.Call<Dictionary<string, object>>("API_GetPlayerData", player);
if (data == null) return;

var workbenches = data["workbench"] as Dictionary<string, object>;

if (!workbenches.ContainsKey("Workbench_1"))
    workbenches["Workbench_1"] = new List<int>();

var list = workbenches["Workbench_1"] as List<int>;
if (list != null && !list.Contains(47))
    list.Add(47);

bool success = TechTree.Call<bool>("API_SetPlayerData", player, data);
```

### Remove a node

```csharp
var data = TechTree?.Call<Dictionary<string, object>>("API_GetPlayerData", player);
if (data == null) return;

var workbenches = data["workbench"] as Dictionary<string, object>;

if (workbenches.TryGetValue("Workbench_1", out var raw))
{
    var list = raw as List<int>;
    list?.RemoveAll(id => Convert.ToInt32(id) == 47);
}

TechTree.Call<bool>("API_SetPlayerData", player, data);
```

> `API_SetPlayerData` also runs cleanup and saves to disk automatically.

---

## API_ClearPlayerWorkbenchData

```csharp
[PluginReference] Plugin TechTree;

private void ClearOpenedWorkbench(BasePlayer player, Workbench workbench)
{
    bool success = TechTree?.Call<bool>("API_ClearPlayerWorkbenchData", player, workbench);

    if (success)
    {
        player.ChatMessage("Your TechTree data for this workbench has been cleared.");
    }
}
```

`API_ClearPlayerWorkbenchData` expects the actual `Workbench` entity instance.

It does not take `Workbench_1` as a string.

---

## Node Dictionary Format

Hooks that expose a node use a dictionary similar to this:

```json
{
  "id": 123456,
  "vanillaId": 84,
  "price": 250,
  "parents": [111111],
  "isVanilla": true,
  "currency": {
    "itemId": -932201673,
    "skinId": 0
  }
}
```

Common values:

- `id`: TechTree node ID.
- `vanillaId`: Rust vanilla tech tree ID when the node is linked to vanilla.
- `price`: unlock cost.
- `parents`: parent node IDs.
- `isVanilla`: whether this node is linked to vanilla data.
- `currency.itemId`: item ID used as currency.
- `currency.skinId`: skin ID used by the currency item.

Always null-check values when reading hook dictionaries from another plugin.

---

## Tree Dictionary Format

The alternative unlock hook can also provide the full tree dictionary.

```csharp
{
  "workbench": Workbench,
  "nodes": [ nodeDictionary, nodeDictionary, ... ]
}
```

---

## Plugin Hooks

```csharp
OnNodeUnlock(Workbench workbench, Dictionary<string, object> node, BasePlayer player)
```

Called before a node is unlocked.

Return `false` to block the unlock.

Return `null` or `true` to allow it.

```csharp
OnNodeUnlock(BasePlayer player, Dictionary<string, object> node, Dictionary<string, object> tree)
```

Alternative hook format with the full tree dictionary.

Return `false` to block the unlock.

Return `null` or `true` to allow it.

```csharp
OnNodeUnlocked(Workbench workbench, Dictionary<string, object> node, BasePlayer player)
```

Called after a node has been unlocked.

```csharp
OnPathNodeUnlocked(Workbench workbench, List<object> nodes, BasePlayer player)
```

Called after multiple nodes were unlocked through a path unlock.

The `nodes` list contains node dictionaries.

---

## Example Blocking Hook

```csharp
private object OnNodeUnlock(Workbench workbench, Dictionary<string, object> node, BasePlayer player)
{
    int nodeId = (int)node["id"];

    if (nodeId == 123456 && !permission.UserHasPermission(player.UserIDString, "myplugin.allow"))
    {
        player.ChatMessage("You cannot unlock this node yet.");
        return false;
    }

    return null;
}
```

---

## Example After-Unlock Hook

```csharp
private void OnNodeUnlocked(Workbench workbench, Dictionary<string, object> node, BasePlayer player)
{
    int nodeId = (int)node["id"];

    Puts($"{player.displayName} unlocked TechTree node {nodeId}");
}
```

---

## Vanilla Compatible Hooks

TechTree also calls vanilla-compatible hooks for vanilla nodes where possible.

```csharp
OnTechTreeNodeUnlock(Workbench workbench, TechTreeData.NodeInstance node, BasePlayer player)
```

Called before a vanilla-derived node is unlocked.

Return `false` to block the unlock.

```csharp
OnTechTreeNodeUnlocked(Workbench workbench, TechTreeData.NodeInstance node, BasePlayer player, List<ItemDefinition> unlockedItems)
```

Called after a vanilla-derived node is unlocked.
