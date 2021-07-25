# IItemDefinition & IBlockDefinition

物品定义和方块定义包括了一个物品或方块的定义信息，可以获取和修改更多底层信息。分别用IItemStack和IBlock类的definition ZenGetter获取。定义针对该ID下的所有物品，不包含Meta值和NBT！

相关wiki界面 [物品定义](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemDefinition/) [方块定义](https://docs.blamejared.com/1.12/en/Vanilla/Blocks/IBlockDefinition/)

以下为使用物品定义的makeStack方法遍历Meta值的例子。

```javascript
import crafttweaker.item.IItemDefinition;

val itemDef as IItemDefinition = <minecraft:wool>.definition;

//移除自 <minecraft:wool:3> 羊毛到 <minecraft:wool:12> 的羊毛
for i in 3 to 13{
    recipes.remove(itemDef.makeStack(i));
}

val numArray as int[] = [3,4,5,6,7,8,9,10,11,12];

//<minecraft:wool:3> 羊毛到 <minecraft:wool:12> 的羊毛
for i in numArray{
    itemDef.makeStack(i).addTooltip("无法合成");
}

//<minecraft:wool:3> 羊毛到 <minecraft:wool:12> 的羊毛，不过不包括 5 和 9
for i in 3 .. 13{
    if(i != 5 && i != 9){
        itemDef.makeStack(i).addShiftTooltip("帮帮我！");
    }
}
```

修改方块硬度和采掘等级

```javascript
<item:tinker_io:ore_crusher>.asBlock().definition.hardness = 3.0f;
<item:minecraft:quartz_ore>.asBlock().definition.setHarvestLevel("pickaxe", 1);
```
