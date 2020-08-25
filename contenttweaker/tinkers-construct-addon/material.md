# 材料  

## 导入
通过`import mods.contenttweaker.tconstruct.Material;`导入Material对象  
通过`import mods.contenttweaker.tconstruct.MaterialBuilder;`导入MaterialBuilder对象

## 材料构建器

```javascript
val myMat = mods.contenttweaker.tconstruct.MaterialBuilder.create(identifier);
```

## 指定参数
| 方法名 | 设定值类型 | 参数描述 |
| :--- | :--- | :--- |
| identifier | string | Material名称 |
| color | int | Material颜色 |
| hidden | bool | ? |
| liquid | ILiquidStack | 设置流体 |
| craftable | bool | 部件加工台是否可合成 |
| castable | bool | 冶炼炉是否可合成 |
| representativeItem | IItemStack | 在匠魂宝典里显示的物品 |
| representativeOre | IOreDictEntry | 同上,只不过是变成了矿物词典 |
| shard | 	IItemStack | ? |
| localizedName | string | 本地化描述 |

## 设定物品来制作材料
`//myMaterial.addItem(IIngredient item, @Optional(1) int amountNeeded, @Optional(144) int amountMatched));`  
item为该物品,amountNeeded为多少个物品增加1点,amountMatched:?

## ItemLocalizer函数
该函数用于计算材料名称  
例子:`myMAt.itemLocalizer = function(thisMaterial, itemName){return "Cool " + itemName;};`  
结果:在名字前面加上Cool  

## 材料特征
可以向材料添加特征  
部件类型有:  
 * null  
 * "head"  
 * "handle"  
 * "extra"  
 * "bow"  
 * "bowstring"  
 * "projectile"  
 * "shaft"  
 * "fletching"
 
添加例子:`myMaterial.addMaterialTrait("fiery", "bowstring");`  
删除例子:`myMaterial.remove("cactus", "bowstring");`

## Material Stats
仅在向材料添加特征的时候才需要调用对应的Material Stats  
例子:在创建`myMaterial.addMaterialTrait("fiery", "bowstring");`的时候也要创建`myMat.addBowStringMaterialStats(float modifier);`  

## 注册材料
最后不要忘了`myMaterial.register();`一下,否则会报错的。

## 官方例子
```javascript
#loader contenttweaker
#modloaded tconstruct

val testMat = mods.contenttweaker.tconstruct.MaterialBuilder.create("kindlich_mat");
testMat.color = 0x8e661b;
testMat.craftable = true;
testMat.liquid = <liquid:lava>;
testMat.castable = true;
testMat.addItem(<item:minecraft:comparator>);
testMat.addItem(<item:minecraft:repeater>, 1, 2);
testMat.addItem(<item:minecraft:red_flower:4>);
testMat.representativeItem = <item:minecraft:red_flower:4>;
testMat.addHeadMaterialStats(100, 1.5f, 5.5f, 5);
testMat.addHandleMaterialStats(0.3, 500);
testMat.addBowStringMaterialStats(0.5f);
testMat.addMaterialTrait(<ticontrait:kindlich_test>, "bowstring");
testMat.addMaterialTrait(<ticontrait:kindlich_test>, "head");
testMat.addMaterialTrait("blasting", "bowstring");
testMat.addMaterialTrait("blasting", "head");

//null (or not specifying that parameter at all) means that this is a default trait.
//Default traits are only queried when no other traits are added to that material type.
//In this case, the dense trait will only be on toolrods, because bowstrings and heads already have other traits.
testMat.addMaterialTrait("dense", null);

//Faulty, should error, though only during init, as then the strings will be checked.
testMat.addMaterialTrait("dance", null);

testMat.itemLocalizer = function(thisMaterial, itemName){return "Cool " + itemName;};
testMat.localizedName = "Wicked";
testMat.register();
```
