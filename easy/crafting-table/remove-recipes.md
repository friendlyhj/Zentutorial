# 移除配方

| 基本格式 | 用途 |
| :--- | :--- |
| `recipes.remove(item, NBTMatch);` | 删除物品的所有配方，NBTMatch（可省略）为布尔值（true/false），如果为true，删除配方的物品将匹配NBT。默认（即省略的话）为false，不匹配NBT。 |
| `recipes.removeShaped(item, inputBox);` | 删除物品的一个特定有序配方，inputBox可省略，这样指删除物品的所有有序配方。 |
| `recipes.removeShapeless(item,inputBox);` | 删除物品的一个特定无序配方，inputBox可省略，这样指删除物品的所有无序配方。 |
| `recipes.removeByRecipeName(recipeName);` | 以配方ID为依据删除配方。|
| `recipes.removeByRegex(regex);` | 删除所有 ID 符合给定正则表达式的配方。|
| `recipes.removeByMod(ModID);` | 删除一个mod的所有配方。 |
| `recipes.removeAll();` | 删除游戏内所有配方。 |

## 例子

```csharp
// 删除铁镐的配方
recipes.remove(<minecraft:iron_pickaxe>);
// 仅删除木板到木棍的有序配方
recipes.removeShaped(<minecraft:stick> * 4, [
    [<ore:plankWood>],
    [<ore:plankWood>]
]);
// 仅删除三纸一皮革合成书的无序配方
recipes.removeShapeless(<minecraft:book>, [
    <minecraft:paper>, <minecraft:paper>, <minecraft:paper>, <minecraft:leather>
])；
// 删除 ID 为 minecraft:golden_chestplate 的配方
// 请注意和 recipes.remove 区分，前者是删除一个物品的所有配方，后者是删除一个特定的配方
// 前者使用尖括号 <> 表示一个物品，后者使用引号 "" 表示一个字符串，一串文本
recipes.removeByRecipeName("minecraft:golden_chestplate");
// 删除植物魔法添加的所有工作台配方
recipes.removeByMod("botania");
```
