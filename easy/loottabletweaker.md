---
description: 需要附属mod LootTableTweaker
---

在阅读此页面前, 强烈建议先阅读 [LootTable : 导论](/easy/loottable-introduction.md) 页面, 了解 LootTable 的相关原版概念.

其次, LootTweaker 和 LootTableTweaker **并不冲突, 且互相都有对方没有的功能**, 实操时推荐两者都安装, 再根据自己的实际需求选用.

# 导包
```csharp
import mods.ltt.LootTable;
```

# 方法一览
```csharp
LootTable.removeTable("table"); // 移除指定的 LootTable
LootTable.removePool("table", "pool"); // 移除指定的随机池
LootTable.removeEntry("table", "pool", "entry"); // 移除指定的被抽出项
LootTable.removeItem("table", "pool", "itemid"); // 移除指定的物品
LootTable.removeModEntry("modid"); // 移除所有指定模组添加的被抽出项
LootTable.removeModItem("modid"); // 移除所有指定模组添加的物品
LootTable.removeModTable("modtable"); // 移除所有指定模组添加的 LootTable
LootTable.removeGlobalItem("itemid"); // 从所有 LootTable 中移除指定物品
```

# 原版箱子 LootTable 一览
```csharp
"minecraft:chests/abandoned_mineshaft"
"minecraft:chests/desert_pyramid"
"minecraft:chests/end_city_treasure"
"minecraft:chests/igloo_chest"
"minecraft:chests/jungle_temple"
"minecraft:chests/jungle_temple_dispenser"
"minecraft:chests/nether_bridge"
"minecraft:chests/simple_dungeon"
"minecraft:chests/spawn_bonus_chest"
"minecraft:chests/stronghold_corridor"
"minecraft:chests/stronghold_crossing"
"minecraft:chests/stronghold_library"
"minecraft:chests/village_blacksmith"
"minecraft:chests/woodland_mansion"
```

# 实例

```csharp
import crafttweaker.item.IItemStack;
import mods.ltt.LootTable;

// 移除沙漠神殿箱子的 LootTable
LootTable.removeTable("desert_pyramid");

// 移除末地城宝藏箱子的 LootTable 的 main 池.
LootTable.removePool("end_city_treasure", "main");

// 移除村庄铁匠铺箱子的 LootTable 的 main 池中的 minecraft:iron_ore 这一被抽出项
LootTable.removeEntry("minecraft:chests/village_blacksmith", "main", <minecraft:iron_ore>.id;

/*指定 LootTable "minecraft:chests/simple_dungeon" (小刷怪房箱子)
  选中此 LootTable 中的 "main" 池
  从此池中移除物品 "minecraft:iron" (为 IItemStack 调用 .id, 返回带 namespace 的物品名称)
*/
LootTable.removeItem("minecraft:chests/simple_dungeon", "main", <minecraft:iron>.id);

// 在所有 pool 中移除所有 ActuallyAdditons 添加的被抽出项
LootTable.removeModEntry("actuallyadditions");

// 在所有 pool 中移除所有 EnderIO 添加的物品
LootTable.removeModItem("enderio");

// 移除所有 GrowthCraft 添加的 LootTable
LootTable.removeModTable("growthcraft");

// 从所有 LootTable 中移除 minecraft:iron_sword 这一物品
LootTable.removeGlobalItem(<minecraft:iron_sword>.id);

```

是的, LootTableTweaker 无法添加 LootTable 或向任何 LootTable 中添加任何物品.

想要创建 LootTable 或向 LootTable 中添加物品, 请移步 [LootTweaker](/easy/loottweaker-easy.md)
