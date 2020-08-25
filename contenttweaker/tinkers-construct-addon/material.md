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
