# Metadata



什么是Meta值？Meta值即为/give命令所需的数据值。比如不同颜色的羊毛以Meta值0~15区分（虽然1.13的扁平化干掉了这个）一个物品尖括号引用一般为这样。`<item:modid:itemid:meta>`。item表示这是个物品，不过一般item是省略的。一个红色羊毛即为`<minecraft:wool:14>`。Meta值允许通配符。工具的耐久度也是用Meta值表示的，你可以用通配符表示任意耐久度的工具。

```csharp
//表示所有羊毛
var wood = <minecraft:wool:*>;
//表示所有木板
var plank = <minecraft:planks:*>;
//任意木板都可合成木棍
recipes.addShaped("stick_across", <minecraft:stick> * 4,
[[null,plank],
[plank,null]]);
```

