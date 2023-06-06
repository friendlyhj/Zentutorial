---
description: Yep，你真的以为魔改仅仅只是个改合成的东西吗？它也可以参与mod制作！上文的一堆Getter，可能你会觉得一点用都没有，但在这里将会大量用到。
---

# 事件概论

什么是事件？某个时间点上发生一件值得关注的事。你可以使用 CrT 在一件事发生时，额外执行别的行为。

```csharp
// onPlayerCrafted 当玩家合成时
events.onPlayerCrafted(function(event){
    // ...
});
```

在匿名函数内部可以编写你想要的行为，这个函数内部的代码将在玩家合成时才会执行，而不像一般配方修改的脚本那样在游戏加载时执行。

```csharp
// onPlayerCrafted 当玩家合成时
events.onPlayerCrafted(function(event){
    print("A player crafted something.");
});
```

比如这样，在玩家合成时，在日志打印信息。

## 具体游戏逻辑

不对啊，只是在日志打印个消息有啥用。我们需要在游戏有一个具体行为才行啊。我们便需要利用这个匿名函数的 event 参数，当这个事件发生时，这个函数执行时会传入这个参数，这个参数包含了这个事件发生的背景。简单来说，可以利用 event 参数的 ZenGetter 获取各种游戏对象，比如玩家、坐标、世界、方块等等，通过操作这些游戏对象，你就可以在合理的时机做你想要的新的游戏逻辑，限制你的只有想象力而已。

例如下面的例子，每次玩家合成时受到 1 点伤害。

```csharp
import crafttweaker.event.PlayerCraftedEvent; //导入玩家合成事件的类

// onPlayerCrafted 当玩家合成时
// 由于 ZenScript 的限制，在这里你需要给 event 指定对应的事件类，否则你无法获取事件包含的信息
// 这里就是 PlayerCraftedEvent 玩家合成事件，记得在脚本最前面导入该类
events.onPlayerCrafted(function(event as PlayerCraftedEvent) {
    // 获取是哪个玩家合成了物品
    var player = event.player;
    // 让玩家受到 1 点魔法伤害
    player.attackEntityFrom(<damageSource:MAGIC>, 1.0f);
});
```

## 取消事件

有的时候你希望一些原版行为不会发生，你可以使用 `cancel` 方法取消事件来阻止原版行为。

下面的例子为阻止苦力怕的生成。

```csharp
import crafttweaker.event.EntityJoinWorldEvent; //导入实体进入世界事件

// onPlayerCrafted 当玩家合成时
// 由于 ZenScript 的限制，在这里你必须要给 event 参数指定对应的事件类，否则你无法获取事件包含的信息
// 这里就是 PlayerCraftedEvent 玩家合成事件，记得在脚本最前面导入该类
events.onEntityJoinWorld(function(event as EntityJoinWorldEvent) {
    // 获取将被加入的实体的定义
    val definition = event.entity.definition;
    // 如果该实体为玩家，definition 会返回 null，需要先进行判空
    // 然后再判断这个实体的 ID 是否是苦力怕
    if (!isNull(definition) && definition.id == "minecraft:creeper") {
        // 取消该事件
        // 取消实体加入世界的结果自然是阻止实体加入世界
        event.cancel();
    }
});
```

## 后记

本教程不可能列出所有可用的事件，以及所有游戏对象和可供使用的操作。你依旧需要官方 wiki 作为「工具书」来查找。

[可用事件列表](https://docs.blamejared.com/1.12/en/Vanilla/Events/IEventManager/)

常用游戏对象：

* [IPlayer](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Players/IPlayer/) ：指定玩家，包含玩家的各种信息。IPlayer继承 [IEntityLivingBase](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Entities/IEntityLivingBase/#ientitylivingbase) 类
* [IEntityLivingBase](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Entities/IEntityLivingBase/#ientitylivingbase)：指定一个Mob 继承 [IEntity](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Entities/IEntity/) 类
* [IEntity](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Entities/IEntity/) ：指定一个实体
* [IWorld](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/World/IWorld/#iworld)：包含世界中的一个维度的信息，包含天气效果、方块信息、服务端客户端等信息。可以用来在世界中召唤一个实体
* [IBlockPos](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/World/IBlockPos/) ：指定世界中一个坐标，常用这个获取或更改一个IWorld的指定坐标的IBlockState
* [ICommandSender](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Commands/ICommandSender/) ：指令发送者，如果想用 zs 发送指令需要用这个，但也要注意权限，推荐用直接用 `server` 关键词，表示服务器发送指令
* [IBlock](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Blocks/IBlock/) ：方块
* [IBlockState](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Blocks/IBlockState/) ：方块状态，真正在世界里的方块，包含方块定义和当前的状态，比如草方块是否被雪覆盖，炼药锅装了多少水。
