# 材料部件信息

你也许对于批量生成的 `MaterialPart` 还有更多的需求，还想要修改一些其他的数值。这就需要 `MaterialPartData` 类对其进行进一步的修改。你可以用这个类的 `addDataValue` 方法对材料部件进行更多修改。

## 导入

`import mods.contenttweaker.MaterialPartData;`

## 获取

可以用 `MaterialPart` 实例的 `getData()` 方法获得该类的一个实例。

## 可用方法

| 方法名 | 参数描述 | 描述 |
| :--- | :--- | :--- |
| addDataValue\(name, value\) | name为字段名，value为该字段的值（均为字符串） | 为材料部件添加/覆盖特定的字段 |

其他两个方法为高级运用，跳过。

## 可用字段名

不同的 `Part` 有不同可用字段，下列列出。

物品：

| 字段名 | 字段值 | 是否是必要的？ |
| :--- | :--- | :--- |
| burn（燃烧时间） | 一个"整数"（如"100"） | No |

盔甲：

| 字段名 | 字段值 | 是否是必要的？ |
| :--- | :--- | :--- |
| durability（耐久度） | 一个“整数”（如"500"） | No |
| enchantability（附魔能力） | 一个“整数”（如"10"） | No |
| reduction（防御点数） | 四个“整数”（如"2, 5, 6, 2"）分别代表靴子、护腿、胸甲、头盔 | No |
| toughness（盔甲韧性） | 一个“浮点数”（如"2.4"） | No |

流体：

| 字段名 | 字段值 | 是否是必要的？ |
| :--- | :--- | :--- |
| temperature（温度） | 一个“整数”（如"300"） | No |
| density（密度） | 一个“整数”（如"1000"） | No |
| luminosity（亮度） | 一个“整数”（如"0"） | No |
| viscosity（黏度） | 一个“整数”（如"1000"） | No |
| vaporize（在下界是否会蒸发） | 一个“布尔值”（如"false"） | No |

矿石：

| 字段名 | 字段值 | 是否是必要的？ |
| :--- | :--- | :--- |
| drops（掉落物品） | 一个“物品列表”（如"minecraft:redstone,minecraft:gold\_ingot"） | No |
| variants（矿物基底） | 一个“方块列表”（如"minecraft:stone,minecraft:end\_stone"） | No |
| hardness（硬度） | 一个“整数列表”（如"3, 3"） | No |
| resistance（抗爆等级） | 一个“整数列表”（如"20, 20"） | No |
| harvestLevel（挖掘等级） | 一个“整数列表”（如"2, 2"） | No |
| harvestTool（挖掘工具） | 一个“工具列表”（如"pickaxe,pickaxe"） | No |

## 例子

```csharp
import mods.contenttweaker.MaterialSystem;

val oreData = MaterialSystem.getMaterialBuilder().setName("Lawrencium").setColor(15426660).build().registerPart("ore").getData();
oreData.addDataValue("drops", "minecraft:redstone,minecraft:gold_ingot");
oreData.addDataValue("variants", "minecraft:stone,minecraft:end_stone");
oreData.addDataValue("hardness", "3,3");
oreData.addDataValue("resistance", "15,15");
oreData.addDataValue("harvestLevel", "1,1");
oreData.addDataValue("harvestTool", "pickaxe,shovel");
```

