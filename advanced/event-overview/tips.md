# 一些忠告

## **!world.remote保证事件只在服务端处理**

MC分为服务端和客户端，服务端用来处理事件、存储存档，而客户端用来渲染、向服务端发送数据包。大部分事件**只能**在服务端内执行，客户端不能执行。单人游戏同样存在内置服务端和客户端。

IWorld的remote ZenGetter用来判断是否在服务端还是客户端。服务端这个ZenGetter会返回false，客户端为true。一旦和存档有关系，比如召唤实体、修改方块，必须使用!world.remote来保证只有服务端能执行这个事件。

```csharp
val bat = VanillaFactory.createItem("forestbat");
bat.onItemUse = function(player, world, pos, hand, facing, blockHit) {
    if (!world.remote) {
        player.getHeldItem(hand).shrink(1);
        <entity:minecraft:bat>.spawnEntity(world, pos.getOffset("up", 1));
        player.sendMessage("新人请说出常用模组。");
        return ActionResult.success();
    }
    return ActionResult.pass();
};
```

这个是ConttentTweaker的脚本，创建一个物品，手持该物品对一个方块右键，召唤一只蝙蝠。你现在只需要注意函数内内容，这里需要使用`!world.remote`，否则右键执行事件后，会出现两只蝙蝠，一个正常，一个在原地不动，无法交互。

你应该用合适的Getter获取到IWorld对象。比如`player.world`

## 将数据持久化保存

> 读懂此条目需要有较高的水平，请确保对以下关键词已有相当了解：事件，IPlayer，IData，DataMap，NBT格式。

你可能会对数据有着更多的需求，例如长久保存一些数据来使用。但即使是全局、静态变量，它们也不是长久保存的，在游戏关闭后这些变量都会被释放。

我们可以将数据保存到玩家数据中，在退出、保存游戏时，我们的数据也随着保存到硬盘上了，即使游戏关闭了也依然存在。

### 写入数据

```csharp
import crafttweaker.events.IEventManager;
import crafttweaker.event.PlayerCraftedEvent;

events.onPlayerCrafted(function(event as PlayerCraftedEvent) {
    if(event.player.world.remote) return;// 保证仅在服务端执行
    event.player.update({custom: 1 as byte});// 向玩家数据中写入自定义数据
    print(event.player.data);// 打印出玩家数据的字符串形式
});
```

当玩家触发`PlayerCraftedEvent`事件时，就会写入该自定义标签到玩家数据中，同时输出调试信息。

```log
[SERVER_STARTED][SERVER][INFO] {custom: 1 as byte}
```

这个标签的位置具体在哪里呢？借用`FTB Utilities`模组提供的游戏内 NBT 编辑工具，在游戏内输入命令`/nbtedit player`打开可视化工具，在`ForgeData`标签下即可以看到我们的自定义标签`custom`了，它的值为`1`。

- 需要注意的是，**直接保存在**`ForgeData`**下的数据会在玩家死亡时被清空**，如果你希望玩家死亡后清空或重置该数据，那么你可以将数据保存在此处。

那么要玩家死亡了也不会清空呢？你可以在`ForgeData`下建立`PlayerPersisted`这个标签，将数据保存在里面即可。

```csharp
import crafttweaker.events.IEventManager;
import crafttweaker.event.PlayerCraftedEvent;

events.onPlayerCrafted(function(event as PlayerCraftedEvent) {
    if(event.player.world.remote) return;// 保证仅在服务端执行
    event.player.update({PlayerPersisted: {custom: 1}});// 向PlayerPersisted中写入子标签{custom: 1}
    print(event.player.data);// 打印出玩家数据的字符串形式
});
```

输出的调试信息为

```log
[SERVER_STARTED][SERVER][INFO] {PlayerPersisted: {custom: 1}}
```

- 在`PlayerPersisted`内部的数据即可做到真正的持久化保存，即使玩家死亡了也不会清空。

### 读取、修改数据

这里就要简单许多了，但是还有几点需要注意，先看代码。

```csharp
import crafttweaker.events.IEventManager;
import crafttweaker.event.PlayerCraftedEvent;

events.onPlayerCrafted(function(event as PlayerCraftedEvent) {
    if(event.player.world.remote) return;// 保证仅在服务端执行
    event.player.update({PlayerPersisted: {custom: 1}});// 向PlayerPersisted中写入子标签{custom: 1}
    print(event.player.data.PlayerPersisted.custom);// 获取并输出custom标签保存的值
});
```

- 尽管你可以通过`event.player.data.PlayerPersisted.custom`来获取`custom`标签保存的值，但是你不可以给它赋值，也就是说类似于`event.player.data.PlayerPersisted.custom = 10;`的这种写法是错误的。

想修改玩家数据，只能去覆盖它（详见DataMap）。

```csharp
import crafttweaker.events.IEventManager;
import crafttweaker.event.BlockPlaceEvent;
import crafttweaker.player.IPlayer;
import crafttweaker.data.IData;

events.onPlayerCrafted(function(event as PlayerCraftedEvent) {
    if(event.player.world.remote) return;// 保证仅在服务端执行
    var data as IData = event.player.data;// 获取玩家数据
    if(isNull(data.PlayerPersisted.custom)) return;// 防止该标签为空时出现空指针异常
    event.player.update({PlayerPersisted: {custom: 10}});// 该操作为覆盖，最终相当于修改custom标签的值
    print(event.player.data.PlayerPersisted.custom);// 获取并输出custom标签保存的值
});
```

当玩家触发`BlockPlaceEvent`事件时，就会修改他保存着的`custom`标签的数据，同时输出调试信息。

```log
[SERVER_STARTED][SERVER][INFO] 10
```
