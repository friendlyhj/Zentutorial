---
description: 需要mod Chickens, ContentTweaker
---

# 更多鸡联动

ContentTweaker 与 Chickens 模组的联动, 可以创建自定义款式的鸡, 生产各种物品.

### 导包
```csharp
import mods.contenttweaker.ChickenFactory;
```

### 创建 ChickenRepresentation

想要注册自定义鸡, 要先创建一个本质上是一只鸡的模板的 ``ChickenRepresentation``.

调用以下方法, 返回一个 ``ChickenRepresentation`` 对象 :

```csharp
ChickenFactory.createChicken(String name, CTColor color, IItemStack item);
```
* name - 鸡的名字
* color - 鸡的颜色
* item - 鸡的产物


### 实例
```csharp
#loader contenttweaker
#modloaded chickens

import mods.contenttweaker.ChickenFactory;
import mods.contenttweaker.Color;

val chickenRepresentation = ChickenFactory.createChicken("bedrocked_chicken", Color.fromInt(0xffffff), <item:minecraft:bedrock>);
chickenRepresentation.setForegroundColor(Color.fromInt(0xabcdef));
chickenRepresentation.register();
```
