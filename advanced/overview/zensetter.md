# ZenSetter

ZenSetter与ZenGetter差不多，但他是设置数据，而不是获取数据。还以IItemStack有一个ZenSetter，也叫"displayName"，我们知道这个信息应该是字符串。

```csharp
//对象.ZenGetter = 新的值
<minecraft:iron_ingot>.displayName = "我是铁锭";
//将<minecraft:iron_ingot>这个IItemStack类的一个实例的displayName ZenSetter设置为"我是铁锭"。
//ZenSetter不返回任何值。
```

如果一个类有同名的ZenSetter和ZenGetter，你可以使用赋值运算符。

```csharp
//因为同时拥有同名 ZenGetter 和 ZenSetter 方法，下列所有两个语句都是等价的：
//对象.zenSetter += 数据;
//对象.zenSetter = object.zenGetter + 数据;

<minecraft:iron_ingot>.displayName += "最棒啦";
<minecraft:iron_ingot>.displayName = <minecraft:iron_ingot>.displayName + "最棒啦";
```
