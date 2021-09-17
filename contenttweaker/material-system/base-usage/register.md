---
description: 当你有了材料和部件，你就可以把这两个合起来注册材料部件了
---

# 注册材料部件

## 由材料类注册

Material类有以下方法构建材料部件

```text
registerParts(String[] partNames); 
//参数为字符串数组，为所需要注册的部件ID（可以使用预设部件的ID)
registerParts(IPart[] parts);
//参数也可以为部件对象数组

registerPart(String partName);
//参数为字符串，为所需要注册的部件ID（可以使用预设部件的ID)
registerPart(IPart part);
//参数为部件对象
```

registerParts方法会返回材料部件对象列表

registerPart方法会返回一个材料部件对象

一般做到这就完事了，所需要的物品已经注册进游戏内。

伪代码表示

铜材料.registerPart\(齿轮部件\) ---&gt; 返回铜齿轮材料部件对象并注册铜齿轮这个物品（因为齿轮部件的部件类型是物品）

## 由部件类注册

Part类有以下方法构建材料部件

```text
registerToMaterial(Material material);
//参数为材料对象
registerToMaterials(Material[] materials);
//参数为材料对象数组
```

与上文的基本同理，不阐述

## 完全例子

```csharp
val copper as Material = MaterialSystem.getMaterialBuilder().setName("Copper").setColor(0xFF9933).build();
copper.registerParts(["gear", "casing", "rod"]); //同时注册铜齿轮、铜质外壳、铜杆三个 MaterialPart

val denseIngotPart = MaterialSystem.getPartBuilder().setName("dense_ingot").setPartType(MaterialSystem.getPartType("item")).setOreDictName("denseIngot").build(); //构建致密锭 Part
copper.registerPart(denseIngotPart); //注册致密铜锭 MaterialPart
```
