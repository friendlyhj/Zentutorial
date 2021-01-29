# 全局和静态变量

你肯定受够了局部变量只能在当前脚本使用，有什么方法可以调用其他脚本的变量呢？使用全局变量或静态变量，允许跨脚本调用！

声明全局变量或静态变量非常简单。注意`as 类型名` 不能省略，且已定义的全局、静态变量之后**不能再次定义，修改其类型或值**。全局变量可以直接在其他脚本中使用，静态变量还需要跨脚本调用。

```javascript
import crafttweaker.item.IItemStack;

// 定义一个全局变量
global stone as IItemStack = <minecraft:stone>;

// 定义一个静态变量
static dirt as IItemStack = <minecraft:dirt>;
```

* 含有全局变量的脚本需要用优先级预加载器保证其优先加载。
* 局部变量可以覆盖全局变量。
* 全局变量可以在任何地方直接调用，但坏处就是你（或别人）可能不记得（或不知道）该变量的定义处在哪里。
* 静态变量的使用需跨脚本引用，但好处就是很容易知道该变量是在哪个脚本里定义的，容易维护。

# 可修改的全局和静态变量

如果要跨脚本、事件和函数这三个作用域之间操作变量，你会发现它们之间的变量是无法直接操作的。

比方来说，如果你正想暂时保存一个值，并且在脚本中任何地方都可以再次修改或调用它，那么这就是上面所说的情况。

这里有一个方法可以绕过全局、静态变量定义后不能再次修改的窘境。

```javascript
// 在脚本中定义一个静态数组
static array as int[] = [1];

// 修改数组内第一个元素的值
array[0] = 10;

// 输出数组第一个元素的值
print(array[0]);
```

尽管`array as int[]`这个数组不能再次定义和修改其类型，但数组内部的元素还是可以修改的。

不只是数组，你也可以定义一个静态的map，尽管该map不能再次定义和修改类型，但是同样可以多次修改其内部的数据。

# 将数据持久化保存

> 读懂此条目需要有较高的水平，请确保对以下关键词已有相当了解：事件，IPlayer，IData，DataMap，NBT格式。

你可能会对数据有着更多的需求，例如长久保存一些数据来使用。但即使是全局、静态变量，它们也不是长久保存的，在游戏关闭后这些变量都会被释放。

我们可以将数据保存到玩家数据中，在退出、保存游戏时，我们的数据也随着保存到硬盘上了，即使游戏关闭了也依然存在。

## 写入数据

```javascript
import crafttweaker.events.IEventManager;
import crafttweaker.event.PlayerCraftedEvent;

events.onPlayerCrafted(function(event as PlayerCraftedEvent) {
    if(event.player.world.remote) { return; }// 保证仅在服务端执行
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

```javascript
import crafttweaker.events.IEventManager;
import crafttweaker.event.PlayerCraftedEvent;

events.onPlayerCrafted(function(event as PlayerCraftedEvent) {
    if(event.player.world.remote) { return; }// 保证仅在服务端执行
    event.player.update({PlayerPersisted: {custom: 1}});// 向PlayerPersisted中写入子标签{custom: 1}
    print(event.player.data);// 打印出玩家数据的字符串形式
});
```

输出的调试信息为

```log
[SERVER_STARTED][SERVER][INFO] {PlayerPersisted: {custom: 1}}
```

- 在`PlayerPersisted`内部的数据即可做到真正的持久化保存，即使玩家死亡了也不会清空。

## 读取、修改数据

这里就要简单许多了，但是还有几点需要注意，先看代码。

```javascript
import crafttweaker.events.IEventManager;
import crafttweaker.event.PlayerCraftedEvent;

events.onPlayerCrafted(function(event as PlayerCraftedEvent) {
    if(event.player.world.remote) { return; }// 保证仅在服务端执行
    event.player.update({PlayerPersisted: {custom: 1}});// 向PlayerPersisted中写入子标签{custom: 1}
    print(event.player.data.PlayerPersisted.custom);// 获取并输出custom标签保存的值
});
```

- 尽管你可以通过`event.player.data.PlayerPersisted.custom`来获取`custom`标签保存的值，但是你不可以给它赋值，也就是说类似于`event.player.data.PlayerPersisted.custom = 10;`的这种写法是错误的。

想修改玩家数据，只能去覆盖它（详见DataMap）。

```javascript
import crafttweaker.events.IEventManager;
import crafttweaker.event.BlockPlaceEvent;
import crafttweaker.player.IPlayer;
import crafttweaker.data.IData;

events.onPlayerCrafted(function(event as PlayerCraftedEvent) {
    if(event.player.world.remote) { return; }// 保证仅在服务端执行
    var data as IData = event.player.data;// 获取玩家数据
    if(isNull(data.PlayerPersisted.custom)) { return; }
    event.player.update(data + {PlayerPersisted: {custom: 10}});// 该操作为覆盖，最终相当于修改custom标签的值
    print(event.player.data.PlayerPersisted.custom);// 获取并输出custom标签保存的值
});
```

当玩家触发`BlockPlaceEvent`事件时，就会修改他保存着的`custom`标签的数据，同时输出调试信息。

```log
[SERVER_STARTED][SERVER][INFO] 10
```