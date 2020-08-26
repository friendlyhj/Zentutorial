# 材料  

## 导入
通过`import mods.contenttweaker.tconstruct.Material;`导入Material类  
通过`import mods.contenttweaker.tconstruct.MaterialBuilder;`导入MaterialBuilder类

## 材料构建器

```javascript
val myMat = mods.contenttweaker.tconstruct.MaterialBuilder.create(identifier);
```

## 指定参数
| 方法名 | 设定值类型 | 参数描述 |
| :--- | :--- | :--- |
| identifier | string | Material名称 |
| color | int | Material颜色 |
| hidden | bool | 隐藏材料 |
| liquid | ILiquidStack | 设置流体 |
| craftable | bool | 部件加工台是否可合成 |
| castable | bool | 冶炼炉是否可合成 |
| representativeItem | IItemStack | 在匠魂宝典里显示的物品 |
| representativeOre | IOreDictEntry | 同上,只不过是变成了矿物词典 |
| shard | IItemStack | 代替部件加工台的碎片(仅此材料) |
| localizedName | string | 本地化描述 |  

**craftable和castable可以同时为true,默认值是false**  
**castable如果为true则还需要设置liquid**  

## 设定物品来制作材料
`//myMaterial.addItem(IIngredient item, @Optional(1) int amountNeeded, @Optional(144) int amountMatched));`  
item为该物品,amountNeeded:?,amountMatched:?

## ItemLocalizer函数
该函数用于计算材料名称  
例子:`myMAt.itemLocalizer = function(thisMaterial, itemName){return "Cool " + itemName;};`  
结果:在名字前面加上Cool  

## 材料特性
可以向材料添加特性  
部件类型有:  
 * null(默认,要是不填会把这个特性附加到全部材料上)
 * "head"-头部 
 * "handle"-手柄
 * "extra"-大板,绑定节,坚韧手柄,坚韧绑定节,护手,宽护手,十字柄
 * "bow"-?
 * "bowstring"-弓弦
 * "projectile"-?
 * "shaft"-箭杆,弩箭核心
 * "fletching"-箭羽

**无论添加哪种部件都会多添加且只添加一次碎片的材料**  
添加例子:`myMaterial.addMaterialTrait("fiery", "bowstring");`  
删除例子:`myMaterial.remove("cactus", "bowstring");`

## 关于特性
获取特性目前的方法只有翻看带有特性的工具的nbt,找到trait,trait后面的数组即是特性名称

## Material Stats
仅在向材料添加特性的时候才需要调用对应的Material Stats  
**如果不使用Material Stats添加材料的属性,材料的部件将制作不出来**  
例子:在写`myMaterial.addMaterialTrait("fiery", "bowstring");`的时候也要写`myMat.addBowStringMaterialStats(0.5f);`  

有以下方法设置(删除)Material Stats
```
myMat.addHeadMaterialStats(int durability, float miningSpeed, float attackDamage, int harvestLevel);
myMat.removeHeadMaterialStats();

myMat.addHandleMaterialStats(float modifier, int durability);
myMat.removeHandleMaterialStats();

myMat.addExtraMaterialStats(int extraDurability);
myMat.removeExtraMaterialStats();

myMat.addBowMaterialStats(float drawSpeed, float range, float bonusDamage);
myMat.removeBowMaterialStats();

myMat.addBowStringMaterialStats(float modifier);
myMat.removeBowStringMaterialStats();

myMat.addArrowShaftMaterialStats(float modifier, int bonusAmmo);
myMat.removeArrowShaftMaterialStats();

myMat.addFletchingMaterialStats(float accuracy, float modifier);
myMat.removeFletchingMaterialStats();

myMat.addProjectileMaterialStats();
myMat.removeProjectileMaterialStats();
```
**参数解析:**  
 * durability\-耐久度
 * miningSpeed\-挖掘速度
 * attackDamage\-伤害
 * harvestLevel\-挖掘等级
 * modifier\-系数
 * extraDurability\-耐久度
 * drawSpeed\-?
 * range\-范围
 * bonusDamage\-?
 * bonusAmmo\-额外弹药
 * accuracy\-精准度

## 注册材料
最后不要忘了`.register();`一下,否则游戏内会无反应

## 本地化key
本地化key为`material.材料名.name`

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
testMat.addMaterialTrait("dense", null);
testMat.addMaterialTrait("dance", null);
testMat.itemLocalizer = function(thisMaterial, itemName){return "Cool " + itemName;};
testMat.localizedName = "Wicked";
testMat.register();
```
