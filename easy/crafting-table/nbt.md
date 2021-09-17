# NBT

NBT使得游戏更有趣！啥，你不知道NBT是啥？建议去看看wiki [传送门](https://minecraft-zh.gamepedia.com/NBT%E6%A0%BC%E5%BC%8F)

一个重命名为肥皂的铁锭是这么表示的。

`<minecraft:iron_ingot>.withTag({display: {Name: "肥皂"}})` `.withTag()`括号内的内容即为NBT。

你可以任意的把带有NBT的物品作为配方输入与输出。但其他模组的机器配方对NBT的支持与否是不好说的。

例子

```text
recipes.addShapeless("test001", <minecraft:iron_ingot>.withTag({display: {Name: "肥皂"}}),
[<ore:dirt>, <ore:dirt>, <minecraft:clay_ball>]);
```
