# 移除配方



| 基本格式 | 用途 |
| :--- | :--- |
| `recipes.remove(item, NBTMatch);` | 删除物品的所有配方，NBTMatch（可省略）为布尔值（true/false），如果为true，删除配方的物品将匹配NBT。默认（即省略的话）为false，不匹配NBT。 |
| `recipes.removeShaped(item, inputBox);` | 删除物品的一个特定有序配方，inputBox可省略，这样指删除物品的所有有序配方。 |
| `recipes.removeShapeless(item,inputBox);` | 删除物品的一个特定无序配方，inputBox可省略，这样指删除物品的所有无序配方。 |
| `recipes.removeByRecipeName(recipeName);` | 以配方ID为依据删除配方。可以使用正则表达式。 |
| `recipes.removeByMod(ModID);` | 删除一个mod的所有配方。 |
| `recipes.removeAll();` | 删除游戏内所有配方。 |

