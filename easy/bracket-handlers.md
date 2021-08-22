# 尖括号调用

Zenscript用`<`和`>`来表示游戏的一个对象。比如物品、矿辞。

通过在尖括号内的字符串，你可以获取游戏内的特定物品、矿辞

例子

```csharp
<item:minecraft:apple>  // 获取苹果物品(IItemStack) 这里的 item: 可省略

<ore:ingotIron> //获取铁锭矿辞(IOreDictEntry)

<entity:minecraft:creeper> //获取原版苦力怕实体定义(IEntityDefinition)

<blockstate:minecraft:stone> //获取原版石头方块状态(IBlockState)

<potion:minecraft:speed> //获取原版速度效果(IPotion)
```

