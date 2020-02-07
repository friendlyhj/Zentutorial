# 物品条件

有时候普通的物品还不足以使用，可能需要一些特殊的合成，只有在完全满足对应条件下才会工作。可以在物品后面添加一些物品条件小尾巴，给物品添加条件。你甚至可以同时使用两个物品条件，例如：

`<minecraft:iron_pickaxe>.onlyDamaged().withTag({display: {Lore: "我是消耗了耐久的铁镐"}});`

可用的物品条件

| 基本格式 | 参数描述 | 作用 |
| :--- | :--- | :--- |
| `item.anyDamage()` | 无 | 输入物品的耐久值不影响合成（也可用Meta值通配符） |
| `item.onlyDamaged()` | 无 | 只有有损耗的物品才能参与合成 |
| `item.onlyDamageAtLeast(value)` | `vaule`为整数 | 只有耐久不小于`value`值才能参与合成 |
| `item.onlyDamageAtMost(value)` | `vaule`为整数 | 只有耐久不大于`value`值才能参与合成 |
| `item.onlyDamageBetween(valueA, valueB)` | `valueA`和`valueB`均为整数 | 只有耐久在两者之间才能参与合成 |
| `item.withTag(NBT)` | `NBT`为物品所带NBT | 需要带有设定NBT标签的物品才能参与合成，JEI内显示带设定NBT的物品（用于输入）或将带设定NBT的物品作为合成成品（用于输出） |
| `item.onlyWithTag(NBT)` | `NBT`为物品所带NBT | 需要**只**带有设定NBT的物品才能参与合成 |
| `item.withDamage(value)` | `value`为整数 | 输出带有`value`点耐久损耗的物品 |
| `item.only(function)` | `function`为以这个物品为参数的匿名函数 | 自定义物品条件，具体用法将在高级运用讲解 |

