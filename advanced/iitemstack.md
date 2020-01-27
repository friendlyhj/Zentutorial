---
description: IItemStack——一个物品。正经叫法叫做物品堆。这是你魔改最常用到的类。作为一个物品，它可以做什么，不仅仅只是作为合成的输入和输出。
---

# IItemStack类型的重新认识

需要`import crafttweaker.item.IItemStack;`导入有关包。

IItemStack有如下的ZenGetter和ZenSetter。

| ZenGetter | ZenSetter | 类型 | 作用 |
| :--- | :--- | :--- | :--- |
| definition |  | IItemDefinition | 获取物品的物品定义 |
| name |  | string | 获取物品名称 |
| displayName | displayName | string | 获取或修改物品显示名称 |
| maxStackSize | maxStackSize | int | 获取或修改物品堆叠数量 |
| damage |  | int | 获取物品耐久损耗值 |
| maxDamage | maxDamage | int | 获取或修改物品耐久 |
| hasTag |  | bool | 物品是否带NBT |
| tag | 使用withTag物品条件 | IData | NBT（如果物品不带NBT，将会返回`{}`，绝不会是null） |
| ores |  | IOreDictEntry数组 | 获取物品所带的矿辞（由于物品所带矿辞可为多个，所以返回为数组） |
| toolClasses |  | 字符串List（可按照数组处理） | 获取物品属于哪些工具（由于存在万能工具，所以返回为List） |
| itemEnchantability |  | int | 获取物品附魔能力 |
| containerItem |  | IItemStack | ? |
| hasContainerItem |  | bool | ? |
| repairCost | repairCost | int | ？ |
| canEditBlocks |  | bool | ？ |
| isOnItemFrame |  | bool | 是否在物品展示框上？ |
| isEnchantable |  | bool | 是否可附魔 |
| isEnchanted |  | bool | 是否已附魔 |
| isDamaged |  | bool | 是否有耐久损耗 |
| isDamageable |  | bool | 是否可耐久损耗 |
| isStackable |  | bool | 是否可堆叠？ |
| isBeaconPayment |  | bool | 是否可作为信标消耗品 |
| hasEffect |  | bool | ？ |
| hasDisplayName |  | bool | 是否有显示名称 |
| metadata |  | int | 返回Meta值 |
| hasSubtypes |  | bool | ？ |
| isEmpty |  | bool | ？ |
| burnTime |  | int | 返回熔炉燃烧时间 |
| showsDurabilityBar |  | bool | ？ |
| hasCustomEntity |  | bool | ？ |
| enchantments |  | IEnchantment List（可按照数组处理） | 返回物品所带附魔 |

更多内容详见wiki对此的条目[点我](https://crafttweaker.readthedocs.io/zh_CN/latest/Vanilla/Items/IItemStack/)

