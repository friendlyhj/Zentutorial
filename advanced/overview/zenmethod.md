# ZenMethod\(方法\)

ZenMethod就是实打实的方法，需要参数，会执行一些特殊的东西。可能不返回值，也可能会返回。具体看各个ZenMethod的描述。例如IItemDefintion类有一个makeStack方法，会返回IItemStack。

```csharp
//用IItemStack类的definition ZenGetter获取一个IItemDefinition
var wool as IItemDefiniton = <minecraft:wool>.defintion;
//IItemDefintion类的makeStack方法，需要一个整型参数
wool.makeStack(13);
//将会返回<minecraft:wool:13>
```
