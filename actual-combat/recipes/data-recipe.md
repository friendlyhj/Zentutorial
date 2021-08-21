# 数据驱动合成修改



## 数据驱动合成修改

本章介绍的是一种特殊的合成修改架构，可以尝试使用。

使用映射保存所有需要的合成信息，你需要添加的在映射内的合成材料输入与输出，不用再重复写`recipes.addShaped`和`recipes.remove`了。

```csharp
import crafttweaker.item.IItemStack;
import crafttweaker.item.IIngredient;

val shapedRecipes as IIngredient[][][IItemStack] = { // 保存要修改的有序配方信息
    <minecraft:iron_block> : [
        [<ore:ingotIron>, <ore:ingotIron>, <ore:ingotIron>],
        [<ore:ingotIron>, <ore:ingotGold>, <ore:ingotIron>],
        [<ore:ingotIron>, <ore:ingotIron>, <ore:ingotIron>]
    ],
    <minecraft:stick> * 4: [
        [<ore:plank>, null],
        [null, <ore:plank>]
    ]
};

val shapelessRecipes as IIngredient[][IItemStack] = { // 保存要修改的无序配方信息
    <minecraft:grass> : [
        <minecraft:dirt>, <minecraft:sapling:*>
    ]
};

val bannedItems as IItemStack[] = [ // 保存要ban掉的物品
    <extrautils2:angelring:*>,
    <mekanism:basicblock:6>
];

// =====================================================================

for item, ingredients in shapedRecipes { // 遍历映射，开始合成修改
    recipes.remove(item);
    recipes.addShaped(item, ingredients);
}

for item, ingredients in shapelessRecipes {
    recipes.remove(item);
    recipes.addShapeless(item, ingredients);
}

for item in bannedItems { // 遍历数组，删除数组内所有物品的合成
    recipes.remove(item);
}
```

