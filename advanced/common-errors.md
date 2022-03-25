# 编写脚本时的常见错误

### 前言

在编写魔改脚本时，可能会出现一些常见的，有通用解的错误，在此列出名称、起因。

人工整理，可能有加较多纰漏，欢迎纠错。


### 语法错误

缺分号，括号不对称等。

示例：
```csharp
// 缺少分号
// 讲真，这连插件语法检查都过不去...
recipes.remove(<minecraft:apple>)
```

报错：
```log
[INITIALIZATION][CLIENT][ERROR] blah_blah_blah.zs:2 > unexpected end of file - ; expected
[INITIALIZATION][CLIENT][ERROR] [crafttweaker | SIDE_CLIENT]: Error parsing blah_blah_blah.zs:2 -- ; expected
```


### 导包错误

导入的包不存在。

示例：
```csharp
// 少打了个 .
import crafttweaker.itemIItemStack;
```

报错：
```log
[INITIALIZATION][CLIENT][ERROR] no_easter_egg_for_you.zs:1 > No such member: itemIItemStack
[INITIALIZATION][CLIENT][ERROR] no_easter_egg_for_you.zs:1 > Not a valid type
```


### 缺少导包

除了基本数据类型，其他所有出现 `as Type` 的语句，比如声明变量，函数的参数与返回值，强制转型等，都需要导入对应的类。

示例：
```csharp
// 需要导入 IItemStack 包
val apple as IItemStack = <item:minecraft:apple>;

function foo(item as IItemStack) {
    print(item.commandString);
}
```

报错：
```log
[INITIALIZATION][CLIENT][ERROR] did_you_miss_me.zs:1 > could not find type IItemStack
[INITIALIZATION][CLIENT][ERROR] did_you_miss_me.zs:3 > could not find type IItemStack
[INITIALIZATION][CLIENT][ERROR] did_you_miss_me.zs:4 > any values not yet supported
```


### 导入语句未写在脚本头部

所有 import 必须写在一起，且在脚本的头部。

示例：
```csharp
val foo as string = "bar";

import crafttweaker.item.IItemStack;
val apple as IItemStack = <item:minecraft:apple>;
```

报错：
```log
[INITIALIZATION][CLIENT][ERROR] [crafttweaker | SIDE_CLIENT]: Error parsing hello_mister_freeman.zs:3 -- Invalid expression, last token: import
```


### 方法传入参数错误

示例：
```csharp
// 输入为 recipes.addShaped(string, IOreDictEntry, IIngredient[][]);
// 其中 IOreDictEntry 类型错误，输出类型只能为 IItemStack。
recipes.addShaped("recipe_name_here", <ore:ingotCopper>, [
    [<ore:nuggetCopper>, <ore:nuggetCopper>, <ore:nuggetCopper>],
    [<ore:nuggetCopper>, null, <ore:nuggetCopper>],
    [<ore:nuggetCopper>, <ore:nuggetCopper>, <ore:nuggetCopper>]
]);
```

报错：
```log
// 有 2 个可用方法，但你的脚本并不匹配其中任何一个
[INITIALIZATION][CLIENT][ERROR] wake_up_and_smell_the_ashes.zs:1 > 2 methods available but none matches the parameters (string, ZenTypeNative: crafttweaker.oredict.IOreDictEntry, any[])

// 这一般是您脚本中有问题，而不是模组的问题
This is usually an error in your script, not in the mod

// 可用方法对应参数一览
addShaped(string, ZenTypeNative: crafttweaker.item.IItemStack, ZenTypeNative: crafttweaker.item.IIngredient[][], Optional ZenTypeNative: crafttweaker.recipes.IRecipeFunction, Optional ZenTypeNative: crafttweaker.recipes.IRecipeAction)
addShaped(ZenTypeNative: crafttweaker.item.IItemStack, ZenTypeNative: crafttweaker.item.IIngredient[][], Optional ZenTypeNative: crafttweaker.recipes.IRecipeFunction, Optional ZenTypeNative: crafttweaker.recipes.IRecipeAction)
```


### 使用加号连接字符串与数字

示例：
```csharp
print(3 + "and");
```

报错：
```log
[INITIALIZATION][CLIENT][ERROR] [crafttweaker]: Error executing {[0:crafttweaker]: i_just_wanna_dance.zs}: For input string: "and"
java.lang.NumberFormatException: For input string: "and"
	at java.lang.NumberFormatException.forInputString(NumberFormatException.java:65)
	at java.lang.Integer.parseInt(Integer.java:580)
	at java.lang.Integer.parseInt(Integer.java:615)
	at I_just_wanna_dance.__script__(i_just_wanna_dance.zs:1)
	at __ZenMain__.run(I_just_wanna_dance)
    ......
```

请使用飘号 (`~`) 连接字符串。


### 数组越界

数组越界错误有若干成因，在此使用最常见的索引超出数组长度问题举例。

示例：
```csharp
import crafttweaker.item.IItemStack;

// 数组长度为 2，最大索引为1
val toRemove as IItemStack[] = [
    <minecraft:apple>,
    <minecraft:stick>
];


// 鉴于 ZenScript 支持遍历非整数类型数组
// 更好的写法其实是 for remove in toRemove {}
for i in 0 .. 3 {
    // 0 .. 3 实际返回为 [0, 1, 2]
    recipes.remove(toRemove[i]);
}
```

报错：
```log
[INITIALIZATION][CLIENT][ERROR] [crafttweaker]: Error executing {[0:crafttweaker]: ladies_and_gentlemen_we_got_him.zs}: 2
java.lang.ArrayIndexOutOfBoundsException: 2
	at Ladies_and_gentlemen_we_got_him.__script__(ladies_and_gentlemen_we_got_him.zs:15)
	at __ZenMain__.run(Ladies_and_gentlemen_we_got_him)
	at crafttweaker.runtime.CrTTweaker.loadScript(CrTTweaker.java:240)
	at crafttweaker.runtime.CrTTweaker.loadScript(CrTTweaker.java:105)
	at crafttweaker.mc1120.events.CommonEventHandler.registerRecipes(CommonEventHandler.java:71)
    ......
```

### 空指针

// ...

### 字符串落双引号

缺少双引号的 string 会被识别为变量关键字，但在声明 map 的 key 中例外，变量会被当成字符串处理。

示例：
```csharp
// 缺少双引号，按变量关键字处理
print(itshouldbeastringbutitsnot);
```

报错：
```log
[INITIALIZATION][CLIENT][ERROR] hey_my_name_is_gary.zs:1 > could not find itshouldbeastringbutitsnot
```

### 没有对应方法

示例：
```csharp
<minecraft:apple>.retard();
```

报错：
```log
// 在 IItemStack 类中（因为 <minecraft:apple> 是 IItemStack）找不到名为 retard 的方法
[INITIALIZATION][CLIENT][ERROR] whos_next_im_tired.zs:1 > No such member in crafttweaker.item.IItemStack: retard
```

IItemStack 类没有名字为 `method` 的方法。

### 尖括号引用错误

一般是拼错单词导致的，为啥不用 `/ct hand` 呢？

示例：
```csharp
// 我很确定原版没有菠萝
print(<minecraft:pineapple>.commandString);
```

报错：
```log
// 无法解析 <minecraft:pineapple>
[INITIALIZATION][CLIENT][ERROR] what_the_hell_is_a_pineapple.zs:1: Could not resolve <minecraft : pineapple>
```

### CoT 脚本内声明物品需 item: 开头

这个 `/ct syntax` 查不出来的（


### 找不到变量

打错这算是低级错误。可以提下变量作用域？


### 对 val 变量重新赋值

报错 `value cannot be changed`


### 对函数参数重新赋值

报错 `not a valid lvalue`

真的有人在 zs 干这事？但 java 允许，我也经常这么写。


### 匿名函数内对外部变量进行赋值

报错 `not a valid lvalue`

事件什么的都是匿名函数的说。不过更新数组、Map 的元素是可以的。


### 声明重名变量与函数

~~哈哈，所以我用 zenclass 有重载~~
