---
description: 配方事件也是有三个参数的函数，用来指定合成完成后会发生什么事。
---

# 配方事件

## 声明

配方事件需要的三个参数为：

* `out`：配方输出
* `info` ： 一个ICraftingInfo对象，在这里可以用inventory ZenGetter
* `player` ： 进行合成的玩家对应的IPlayer对象

例子：合成后玩家生命值减少5点

```csharp
  recipes.addShapeless("recipe_action_test", <minecraft:sapling>,
  [<minecraft:stick>,<minecraft:leaves>],
    function (out,ins,info) {
          //生命值只有大于 5 才能合成，防止掉 5 点血后直接死亡
          return info.player.health > 5 ? out : null;
    },
    function (out,info,player) { // 声明配方事件
          //合成后玩家受到 5 点魔法伤害
          player.attackEntityFrom(<damageSource:MAGIC>, 5.0f);
  });
```

这里是事件部分对于配方的一个延伸。注意事件已经开始像写mod了，你的编写要十分小心，不是仅仅语法没问题就行，如果执行事件时产生一些异常（空指针异常、数组越界等等），将不会是简简单单的报错，而是游戏崩溃了。具体更多内容，将在事件概论里阐述。
