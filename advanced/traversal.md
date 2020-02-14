# 穷举与遍历



是的，你正在用循环做批量魔改。可为什么你可以对一些物品做批量魔改？那是因为这些物品都有相同点。而你需要找到所有你要改的物品，保存在一个数组中，这是穷举。但为什么不换个思路，直接遍历游戏内所有物品，找到符合你需要的条件的物品后，进行合成修改呢？

首先你需要知道的是：

* 矿辞的结构是"类型+金属名"
* 可以用contains方法检查一个字符串是否包含某些字
* 可以用`oreDict.get()`用字符串呼出一个OD
* 可以用`itemUtils.getItem()`用字符串和Meta值（可选，若是32767即为Meta通配符）呼出一个IItemStack
* [ICraftingRecipe](https://crafttweaker.readthedocs.io/zh_CN/latest/Vanilla/Recipes/Crafting/ICraftingRecipe/)类包含了一个配方的信息，可以用`recipes.all()`调出游戏内所有ICraftingRecipe的列表
* 可以用`oreDict.entries`调出游戏内所有OD的列表

例子一：删除一个物品所参与的所有合成配方

```javascript
//checkIngredient自定义函数，用于判断一个材料对象是否在材料对象数组中
//具体讲解将下章阐述
function checkIngredient (o as IIngredient, a as IIngredient[]) as bool {
    for i in a {
        if (!isNull(i) && (i in o)) {
            return true;
        }
    }
    return false;
}

for recipe in recipes.all() { // 遍历游戏内所有注册物品
    //用ICraftingRecipe的ingredients1D ZenGetter获取配方的材料，返回IIngredient[]
    if (checkIngredient(<minecraft:iron_ingot>, recipe.ingredients1D)) {
        recipes.removeByRecipeName(recipe.name);
    }
}
```

例子二：根据OD对齿轮进行合成修改

```javascript
import crafttweaker.item.IItemStack;
import crafttweaker.item.IIngredient;
import crafttweaker.oredict.IOreDictEntry;
import crafttweaker.oredict.IOreDict;

for ench in oreDict.entries /* oreDict.entries 在所有注册OD中循环 */ {
    var oreName as string = ench.name;
    var enchGear as IItemStack = ench.firstItem; // 获得OD的第一个物品
    // 进行条件判断，第二个条件是当时魔改时，排除EIO充能合金齿轮等的干扰
    if (oreName.startsWith("gear") && enchGear.definition.owner != "enderio") {
        var key as string = oreName.substring(4, oreName.length); // 获取金属名
        // 获取魔改需要的该金属的其他部件，杆和板
        var stick as IOreDictEntry = oreDict.get("stick" ~ key);
        var plate as IOreDictEntry = oreDict.get("plate" ~ key);
        var ingot as IItemStack = oreDict.get("ingot" ~ key).firstItem;
        // 排除空矿辞，排除木齿轮和石齿轮等的干扰
        if (!stick.empty && !plate.empty) {
            // 经典合成修改
            recipes.remove(enchGear); 
            mods.forestry.Carpenter.addRecipe(enchGear,
            [[stick,plate,stick],
            [plate,<contenttweaker:bushing>,plate],
            [stick,plate,stick]], 6, <liquid:soldering> * 72); 
            mods.immersiveengineering.MetalPress.removeRecipe(enchGear);
            mods.thermalexpansion.Compactor.removeGearRecipe(ingot); 
            mods.tconstruct.Casting.removeTableRecipe(enchGear); 
        }
    }
}
```

例子三：遍历游戏内所有物品
```javascript
for mod in loadedMods { //遍历游戏内所有的模组，loadedMods一个全局关键词，包括游戏内所有模组(IMod[string])
    for item in mod.item { //再遍历一个模组的所有物品
        recipes.remove(item); 
        //这只是个例子！要删除游戏内所有物品的配方，用recipes.removeAll();就好了
    }
}
