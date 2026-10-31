# API And Hooks

**TechTree** includes API methods and hooks for other plugins.

They can read player data, restore progression, clear unlocks and check tree completion.

Hooks can change prices, block an unlock, or react when a player unlocks a node.

---

## API Methods

```csharp
Dictionary<string, object> API_GetPlayerData(BasePlayer player)
```

Returns the player's TechTree data in an API-friendly format.

```csharp
bool API_SetPlayerData(BasePlayer player, Dictionary<string, object> apiData)
```

Replaces the player's TechTree data with an API-friendly dictionary.

Returns `false` and keeps the existing data if the format is invalid.

Unknown workbenches and node IDs are removed before saving.

```csharp
bool API_ClearPlayerWorkbenchData(BasePlayer player, Workbench workbench)
```

Clears the player's unlock data for the provided workbench, subcategories included.

```csharp
bool API_ClearPlayerData(BasePlayer player)
```

Clears all TechTree unlock data for the player.

```csharp
bool API_IsTreeComplete(BasePlayer player, Workbench workbench, string subcategoryId)
```

Returns `true` when the player has unlocked every node of a tree.

Use `null` or an empty string for the main tree, or the subcategory ID (its file name).

These methods do not grant or remove blueprints, and do not run rewards or hooks.

The open TechTree UI is refreshed after a change.

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

Subcategory nodes are in the same list as the main tree of their workbench.

---

## API_GetPlayerData / API_SetPlayerData

These two calls let you read and write a player's unlocked nodes from another plugin.

### Read

```csharp
var data = TechTree?.Call<Dictionary<string, object>>("API_GetPlayerData", player);
if (data == null) return; // TechTree not loaded

var workbenches = data["workbench"] as Dictionary<string, object>;

if (workbenches.TryGetValue("Workbench_1", out var raw))
{
    var unlocked = raw as List<int>;
    bool hasNode = unlocked?.Contains(47) ?? false;
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
    list?.Remove(47);
}

TechTree.Call<bool>("API_SetPlayerData", player, data);
```

`API_SetPlayerData` also runs cleanup and saves to disk automatically.

---

## API_ClearPlayerWorkbenchData

```csharp
[PluginReference] Plugin TechTree;

private void ClearOpenedWorkbench(BasePlayer player, Workbench workbench)
{
    bool success = TechTree?.Call<bool>("API_ClearPlayerWorkbenchData", player, workbench) ?? false;

    if (success)
    {
        player.ChatMessage("Your TechTree data for this workbench has been cleared.");
    }
}
```

`API_ClearPlayerWorkbenchData` expects the actual `Workbench` entity instance.

It does not take the name `Workbench_1` as a string.

---

## API_IsTreeComplete

```csharp
bool mainDone = TechTree?.Call<bool>("API_IsTreeComplete", player, workbench, null) ?? false;
bool vipDone = TechTree?.Call<bool>("API_IsTreeComplete", player, workbench, "vip_tree") ?? false;
```

An unknown subcategory ID is treated as the main tree.

An empty tree is never complete.

---

## Node Dictionary Format

Hooks that expose a node use a dictionary similar to this:

```json
{
  "id": 123456,
  "vanillaId": 84,
  "price": 1,
  "parents": [111111],
  "isVanilla": true,
  "currency": {
    "itemId": -143481979,
    "skinId": 0
  }
}
```

Common values:

- `id`: TechTree node ID.
- `vanillaId`: Rust vanilla tech tree ID, or `null` for custom nodes.
- `price`: node price, after the economy model.
- `parents`: parent node IDs.
- `isVanilla`: whether this node is linked to vanilla data.
- `currency.itemId`: item ID used as currency, after the economy model.
- `currency.skinId`: skin ID used by the currency item.

`price` is the node's own price.

It does not include workbench upgrades, `OnNodeUnlockCost`, free unlocks or Salvage.

Always null-check values when reading hook dictionaries from another plugin.

---

## Tree Dictionary Format

The alternative unlock hook also provides the tree dictionary.

```csharp
{
  "workbench": Workbench,
  "nodes": [ nodeDictionary, nodeDictionary, ... ]
}
```

`nodes` contains the nodes of the tree currently shown, main tree or subcategory.

---

## Plugin Hooks

```csharp
object OnNodeUnlockCost(BasePlayer player, int price)
```

Called when TechTree computes a cost for the player.

Return an `int` to replace the cost. Negative values become 0.

Return `null` to keep the cost.

It receives the total of one currency, after workbench upgrades.

`techtree.unlock.free` is applied after this hook.

It is called when the player selects a node, not at payment time.

```csharp
object OnNodeUnlock(Workbench workbench, Dictionary<string, object> node, BasePlayer player)
```

Called before a node is unlocked, normally or with a prototype.

Return `false` to block the unlock.

Return `true` to allow it and skip the alternative hook below.

Return `null` to let the alternative hook decide.

```csharp
object OnNodeUnlock(BasePlayer player, Dictionary<string, object> node, Dictionary<string, object> tree)
```

Alternative hook format with the tree dictionary.

Return `false` to block the unlock.

Both hooks receive only the node the player clicked, not every node of the path.

```csharp
void OnNodeUnlocked(Workbench workbench, Dictionary<string, object> node, BasePlayer player)
```

Called after each unlocked node, once rewards and blueprints have been given.

For a normal unlock, the node dictionary is a snapshot taken when the player clicked.

```csharp
void OnPathNodeUnlocked(Workbench workbench, List<object> nodes, BasePlayer player)
```

Called after several nodes were unlocked through a path unlock.

The `nodes` list contains node dictionaries.

Do not keep a reference to the list: it is released after the call.

It is not called for prototype unlocks.

---

## Example Price Hook

```csharp
private object OnNodeUnlockCost(BasePlayer player, int price)
{
    if (permission.UserHasPermission(player.UserIDString, "myplugin.discount"))
        return price / 2;

    return null;
}
```

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

## Vanilla Hooks

TechTree no longer calls the vanilla hooks `OnTechTreeNodeUnlock` and `OnTechTreeNodeUnlocked`.

Use the TechTree hooks above instead.

---

## Good To Know

- After the player switches workbench tabs, the `workbench` argument can be a template workbench.
- In that case it is not the workbench the player is using.
- Branch and subcategory permissions are not registered by TechTree.
