---
description: 部件是这个物品是什么，比如齿轮、板、外壳、箔...
---

# 部件

## 导入

`import mods.contenttweaker.Part;`

`import mods.contenttweaker.PartBuilder;`

`import mods.contenttweaker.PartType;`

## 预设部件

以下是CoT已经预设好的部件。你也可以用`/ct parts` 命令将所有已经注册的部件打印至CrT日志中。

### Items:

* Beam![icon](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Materials/Parts/Assets/beam.png)
* Bolt![icon](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Materials/Parts/Assets/bolt.png)
* Casing![icon](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Materials/Parts/Assets/casing.png)
* Clump![icon](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Materials/Parts/Assets/clump.png)
* Crystal Crystal![icon](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Materials/Parts/Assets/crystal.png)
* Crushed Ore \(crushed\_ore\)![icon](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Materials/Parts/Assets/crushed_ore.png)
* Dense Plate \(dense\_plate\)![icon](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Materials/Parts/Assets/dense_plate.png)
* Dirty Dust \(dirty\_dust\)![icon](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Materials/Parts/Assets/dirty_dust.png)
* Dust![icon](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Materials/Parts/Assets/dust.png)
* Gear![icon](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Materials/Parts/Assets/gear.png)
* Ingot![icon](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Materials/Parts/Assets/ingot.png)
* Nugget![icon](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Materials/Parts/Assets/nugget.png)
* Plate![icon](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Materials/Parts/Assets/plate.png)
* Rod![icon](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Materials/Parts/Assets/rod.png)
* Shard![icon](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Materials/Parts/Assets/shard.png)

### Blocks:

* Block![icon](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Materials/Parts/Assets/block.png)

### Ores:

* Ore
* Dense Ore \(dense\_ore\)
* Poor Ore\(poor\_ore\)

### Fluids:

* Molten

### Armor:

* Armor ![head icon](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Materials/Parts/Assets/armor_head.png)![chest icon](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Materials/Parts/Assets/armor_chest.png)![legs icon](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Materials/Parts/Assets/armor_legs.png)![feet icon](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Materials/Parts/Assets/armor_feet.png)

### Minecart

* Minecart

## 部件构建器

如果预设的不满足你的需要，你可以创建新的部件。

与材料构建器类似，用MaterialSystem包的getPartBuilder方法获取材料构建器。

```text
var pBuilder as PartBuilder = MaterialSystem.getPartBuilder();
```

### 部件类型

你需要为你将要创建的部件指定类型，通过MaterialSystem包的getPartType方法获取 你可以使用：

* item （物品）
* block （方块）
* ore（矿石）
* fluid（流体）
* armor（护甲）
* minecart （矿车）

### 设定参数

你可以用以下方法指定所构建的部件的参数

| 方法名 | 参数描述 | 功能 |
| :--- | :--- | :--- |
| setHasOverlay\(hasOverlay\) | hasOverlay为布尔值 | 部件是否有overlay（该部分不会被染色） |
| setName\(name\) | name为字符串 | 设置部件ID |
| setPartType\(partType\) | partType为部件类型 | 设置部件类型 |
| setOreDictName\(prefix\) | prefix为字符串 | 设置将来构建的材料部件的矿辞的部件名（如`gearCopper`中的gear\) |
| setAdditionalOreDictNames\(prefixes\) | ？ | ？ |

### 构建

最后你需要对PartBuilder使用`build`方法来构建材料，这个方法将会返回一个Part对象。记得用变量储存，以便接下来构建材料部件！

### 实例脚本

```javascript
var pBuilder = mods.contenttweaker.MaterialSystem.getPartBuilder();
pBuilder.setName("dense_gear");
pBuilder.setPartType(MaterialSystem.getPartType("item"));
var denseGearPart = pBuilder.build();

var denseIngotPart = mods.contenttweaker.MaterialSystem.getPartBuilder().setName("dense_ingot").setPartType(mods.contenttweaker.MaterialSystem.getPartType("item")).setOreDictName("superIngot").build();
```

## 本地化

本地化key为`contenttweaker.part.PartID`

其的值需要有个%s，这个将会在其构建的材料部件中被材料名替代

例子：

```text
contenttweaker.part.dense_gear=致密%s齿轮
contenttweaker.part.dense_ingot=致密%s锭
```

## 材质

需要在所需的文件夹放置于文件名与部件名相同的png文件。

例如上文的例子需要在/resources/contenttweaker/textures/items放置dense_gear.png和dense_ingot.png
