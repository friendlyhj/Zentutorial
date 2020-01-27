# 一些忠告

### **isNull函数规避NPE异常**

一些Getter可能会返回null，而试图对null使用任何方法、Getter会抛出NPE异常。你需要事先用isNull函数判断其是否为null，不是则跳过操作。比如，你需要获取副手的物品的id，如果和指定的相同，则进行接下的操作

```javascript
var offItem as IItemStack = player.offHandHeldItem;
if (offItem.definition.id == "minecraft:sand") {
    ...
}
```

但是这样，若玩家副手没有物品，offItem就是null，对null使用方法会抛出异常。你需要用isNull函数

```javascript
var offItem as IItemStack = player.offHandHeldItem;
if (!isNull(offItem) && offItem.definition.id == "minecraft:sand") {
    ...
}
```

&&是短路逻辑和，若前面的运算结果为false，结果将直接为false，后面的运算不再运算。（前文的`||`同理）

在这个例子中，先判断isNull函数，如果offItem为null，isNull函数结果为true，取反后为false，（运算优先级：非大于和大于或）结果直接判断为false，后面的`offItem.definition.id == "minecraft:sand"`运算跳过。只有offItem不为null，才会检测其ID，从而规避NPE异常。

### **!world.remote保证事件只在服务端处理**

MC分为服务端和客户端，服务端用来处理事件、存储存档，而客户端用来渲染、向服务端发送数据包。大部分事件**只能**在服务端内执行，客户端不能执行。单人游戏同样存在内置服务端和客户端。

IWorld的remote ZenGetter用来判断是否在服务端还是客户端。服务端这个ZenGetter会返回false，客户端为true。一旦和存档有关系，比如召唤实体、修改方块，必须使用!world.remote来保证只有服务端能执行这个事件。

```javascript
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

