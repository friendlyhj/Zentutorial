---
description: 配方函数可以决定配方输出结果，可以做到根据配方特定输入物品来决定输出物品将是怎样，还可以为配方是否能使用添加条件！
---

# 配方函数

## 声明

配方函数需要三个参数，一般叫`out` 、`ins` 和`info`，不过你也可以重命名，顺序为这样就行。

* `out` 是这个配方的输出（IItemStack\)
* `ins`：是一个映射，包含inputBox中所有标记过的材料（如何标记见[IIngredient接口章](https://youyi580.gitbook.io/zentutorial/advanced/iingredient)）
* `info`：一个ICraftingInfo对象，包含合成时的一些信息，基本上只需要用`player` ZenGetter获取进行合成的玩家对应的IPlayer对象 和`inventory`ZenGetter获取合成时的物品栏[ICraftingInventory](https://crafttweaker.readthedocs.io/zh_CN/latest/Vanilla/Recipes/Crafting/ICraftingInventory/)对象。

配方函数需要返回一个IItemStack作为配方实际的输出。若为`null`即为没有输出，不可合成。

## 例子

例子一：假合成（JEI能看到，其实上不能用）

```javascript
recipes.addShapeless("fake_recipe",<minecraft:diamond>,[<ore:dirt>,<ore:dirt>,<ore:dirt>],
    function (out,ins,info) {  // 声明配方函数
        return null;  // 直接返回null，不输出
    },
// 不需要配方事件，所以设置为null
null);
```

例子二：需要在下界才能使用的合成

```javascript
recipes.addShapeless("nether_recipe",<minecraft:netherrack>,
[<ore:cobblestone>,<ore:cobblestone>,<ore:cobblestone>],
    function (out,ins,info) { 
        return info.player.world.dimension == -1 ? out : null; 
    },
null);
```

例子三：继承原有NBT的升级配方（即可以做到升级镐后保留原来的附魔）

```javascript
import crafttweaker.data.IData;

recipes.addShaped("tag",<minecraft:diamond_pickaxe>,[
    [<ore:gemDiamond>,<ore:gemDiamond>,<ore:gemDiamond>],
    [null,<minecraft:golden_pickaxe:*>.marked("p"),null]],  // 注意金镐被标记了
    function(out,ins,info){
        var data as IData = ins.p.tag; // 获取标记为p的金镐的NBT
    return out.withTag(data); // 返回包含这个NBT的输出——钻石镐
    },
null);
```

例子四：修复镐（Meta值操控）

```javascript
val diaPick = ;

recipes.addShapeless("pickrepair",<minecraft:diamond_pickaxe>,
[<minecraft:diamond_pickaxe>.onlyDamaged().marked("p"),<minecraft:diamond>],
function(out, ins, cInfo){
    // 返回一个耐久为0或者现有耐久-500（取两个耐久值中的最大值）的镐子。这是用来防止负的耐久值。
    return ins.p.withDamage(max(0,ins.p.damage - 500));
},
// 我们不需要recipeAction，所以将它设置为null（空）
null);
```

例子五：NBT操控（这是我测试匠魂凿子转换为iChisel的脚本，不做注释了，你需要对原来的输入包含的NBT结构有足够了解，记住/ct hand）

```javascript
recipes.remove(<chisel:chisel_hitech>);

recipes.addShapeless("ichisel_tinker_go",<chisel:chisel_hitech>,
[<tcomplement:chisel>.marked("t"),<minecraft:redstone_block>,<minecraft:emerald>],
    function(out,input,info){
        var globaltdata as IData = input.t.tag;
        var stat as IData = globaltdata.Stats;
        var du as int = stat.Durability.asInt();
        var material as string = globaltdata.TinkerData.Materials.asString();
        var n as int = 3;
        for i in 3 .. material.length {
            if (material[i] == ",") {
                n = i - 1;
                break;
            }
        }
        var displaystring as string = "Material : " + material.substring(2,n);
        var meta as int = max(0,10049 - du);
        var display as IData = {display:{Lore:[displaystring]}};
        var Minmeta as IData = {Minmeta: meta as int};
        var materialInData as IData = {Material: material.substring(2,n)};
        return out.definition.makeStack(meta).withTag(display + Minmeta + materialInData);
    },
null);


recipes.addShapeless("ichisel_repair",<chisel:chisel_hitech>,
[<chisel:chisel_hitech>.anyDamage().marked("c"),<tconstruct:sharpening_kit>.marked("s")],
    function(out,input,info){
        var du as int = input.c.damage;
        var Minmeta as int = input.c.tag.Minmeta.asInt();
        if (input.s.tag.Material != input.c.tag.Material){
            return null;
        } else {
            var shouldRepair as int = du - Minmeta;
            if (!shouldRepair >= 1) {
                return null;
            } else {
                du -= max(1024,shouldRepair / 2);
                du = max(du,Minmeta);
                return out.definition.makeStack(du).withTag(input.c.tag);
            }
        }
    },
null);
```

