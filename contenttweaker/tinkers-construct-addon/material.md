---
description: 实际上是部件(?)
---

# 材料  

## 导入
通过`import mods.contenttweaker.tconstruct.Material;`导入Material对象  
通过`import mods.contenttweaker.tconstruct.MaterialBuilder;`导入MaterialBuilder对象

## 材料构建器

```javascript
val myMat = mods.contenttweaker.tconstruct.MaterialBuilder.create(identifier);
```

## 指定参数
| 方法名 | 设定值类型 | 参数描述 |
| :--- | :--- | :--- |
| identifier | string | Material名称 |
| color | int | Material颜色 |
| hidden | bool | ? |
| liquid | ILiquidStack | 设置流体 |
| craftable | bool | 部件加工台是否可合成 |
| castable | bool | 冶炼炉是否可合成 |
| representativeItem | IItemStack | 在匠魂宝典里显示的物品 |
| representativeOre | IOreDictEntry | 同上,只不过是变成了矿物词典 |
| shard | 	IItemStack | ? |
| localizedName | string | 本地化描述 |

## 设定物品来制作材料
//`myMaterial.addItem(IIngredient item, @Optional(1) int amountNeeded, @Optional(144) int amountMatched));`
//item为该物品,amountNeeded为多少个物品增加1点,amountMatched:?

## ItemLocalizer方法
该函数用于计算材料名称  
例子:`myMAt.itemLocalizer = function(thisMaterial, itemName){return "Cool " + itemName;};`  
结果:在名字前面加上Cool  
