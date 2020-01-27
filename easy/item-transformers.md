---
description: 想在配方当中使用工具又不想吞工具？想合成物品后，其中一个材料转换为另一个物品（像合成蛋糕那样牛奶桶变空桶）？你需要使用物品转换器！
---

# 物品转换器

### 例子

`recipes.addShapeless(<minecraft:stick> * 3, [<minecraft:stone_axe>.transformDamage(), <ore:plankWood>]);` 石斧和木板合成为3木棍，石斧掉1点耐久。

### 可用的物品转换器

| 基本格式 | 参数设置 | 作用 |
| :--- | :--- | :--- |
| `item.reuse()` | 无 | 返回这个物品本身，即该物品合成时不消耗 |
| `item.giveBack()` | 无 | 类似reuse，但合成后，物品将会进入物品栏，而不是在工作台上 |
| `item.transformReplace(itemToReplace)` | `itemToReplace`为一个物品 | 合成后，物品变成`itemToReplace`物品 |
| `item.transformDamage()` | 无 | 合成后，物品掉1点耐久 |
| `item.transformDamage(value)` | `value`为整数 | 合成后，物品掉`value`点耐久 |
| `item.noReturn()` | 无 | 强制使物品合成后消失 |
| `item.transformConsume(value)` | `value`为整数 | 物品将会消耗`value`个 |
| `item.transformNew(function)` | `function`为以这个物品为参数的匿名函数 | 自定义物品转换，具体用法将在高级运用讲解 |

此外，若你需要以一个装有流体的桶作为合成，合成后会自动返回桶，不需要用物品转换器。如果你不想返回桶，可用`.noReturn()`物品转换器。

