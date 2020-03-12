# IIngredient接口



让我们重新看到最基本的合成添加语句：

`recipes.addShaped(recipeName, output, inputBox);`

实际上，output是IItemStack，而inputBox则是IIngredient的二维数组。

IIngredient——材料，它用来匹配一个合成的材料，输入或输出。IIngredient是IItemStack（物品堆）、IOreDictEntry（矿物辞典）、ILiquidStack（流体堆）的接口。这意味着IIngredient可用的方法，IItemStack、IOreDictEntry、ILiquidStack一样可用。对于一个需要IIngredient为参数的函数/方法或者定义IIngredient数组，也可以用IItemStack、IOreDictEntry、ILiquidStack输入。（你加合成的时候，用的不就是IItemStack或者IOreDictEntry嘛）实际上前文的物品条件和物品转换器就是针对IIngredient的。（对于流体不可用，不过我想没人对流体加条件）

需要`import crafttweaker.item.IIngredient;`导入有关包。

**标记**

使用marked方法用一个字符串标记一个材料，在下文的配方函数和配方事件中将会用到。

```text
recipes.addShapeless("test002", <minecraft:stone:2>, 
[<minecraft:iron_ingot>.marked("iron"),<minecraft:dirt>]);
```

**数量**

你们早就知道用`* 数量`来表示数量吧。你可以使用amount ZenGetter获取一个材料对象的数量。

**或**

用`|`将两个材料连接起来，使得一个配方的某个槽可以使用材料A或材料B，而不用写多个配方。在某些时候，比OD更好用！

```text
recipes.addShaped("te_frame_machine", <thermalexpansion:frame>,
[[<ore:ingotIron>|<ore:ingotAluminum>,<enderio:item_basic_capacitor>,<ore:ingotIron>|<ore:ingotAluminum>],
[<ore:blockGlass>,<ore:gearTin>,<ore:blockGlass>],
[<ore:ingotIron>|<ore:ingotAluminum>,<ore:blockGlass>,<ore:ingotIron>|<ore:ingotAluminum>]]);
```

**获得匹配的物品和流体**

用items或itemArray ZenGetter获取匹配的物品，返回IItemStack列表或数组。

用liquids ZenGetter获取匹配的流体，返回ILiquidStack列表。

```javascript
//Returns an IItemStack List
//possible items: All iron ingots and the gold ingot from MC
val itemsIngredient = <ore:ingotIron> | <minecraft:gold_ingot>;


//Returns an ILiquidStack List
//possible liquids: Lava and Water
val liquidsIngredient = <liquid:lava> | <liquid:water>;


for item in itemsIngredient.items{
    //Prints each possible item's Display name
    print(item.displayName);
}

for item in itemsIngredient.itemArray{
    //Prints each possible item's Display name
    print(item.displayName);
}

for liquid in liquidsIngredient.liquids{
    //Prints each possible liquid's Display name
    print(liquid.displayName);
}
```

