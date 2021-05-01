# 材料  

## 导入

通过 `import mods.contenttweaker.tconstruct.Material;` 导入Material类  
通过 `import mods.contenttweaker.tconstruct.MaterialBuilder;` 导入MaterialBuilder类

## 材料构建器

```javascript
val myMat as MaterialBuilder = mods.contenttweaker.tconstruct.MaterialBuilder.create(identifier as string);
```

## 指定参数

| 方法名 | 设定值类型 | 参数描述 |
| :--- | :--- | :--- |
| identifier | string | Material名称 |
| color | int | Material颜色 |
| hidden | bool | 隐藏材料 |
| liquid | ILiquidStack | 设置流体 |
| craftable | bool(默认false) | 部件加工台是否可合成 |
| castable | bool(默认false) | 冶炼炉是否可合成 |
| representativeItem | IItemStack | 在匠魂宝典里显示的物品 |
| representativeOre | IOreDictEntry | 同上, 只不过物品变成了矿物词典内的物品 |
| shard | IItemStack | 代替部件加工台的碎片 |
| localizedName | string | 本地化描述 |  

craftable 和 castable 可以同时为true  
castable 如果为 true 则还需要设置 liquid

## 设定物品来制作材料

@Optional 注解的括号内的数字为默认值

```javascript
myMat.addItem(item as IIngredient, @Optional(1) amountNeeded as int, @Optional(144) amountMatched as int));
```  

## 材料特性

可以向材料的部件添加特性(不然这材料一点特性都没有不好用啊:(
ContentTweaker 里的部件类型有:  

* null(不填会把这个特性附加到全部材料的部件上)
* "head"\-头部
* "handle"\-手柄
* "extra"\-大板,绑定节,坚韧手柄,坚韧绑定节,护手,宽护手,十字柄
* "bow"\-?
* "bowstring"\-弓弦
* "projectile"\-?
* "shaft"\-箭杆,弩箭核心
* "fletching"\-箭羽

注意 : 添加哪种特性至某种材料的部件都会多添加碎片的部件(除非已有)

添加 : 
```javascript
myMat.addMaterialTrait("fiery", "bowstring");
```
第一个参数可以填 Trait 对象, TraitBuilder 对象, String 类型的 identifier(特性名)  
第二个参数为部件类型

删除 : 
```javascript
myMat.removeMaterialTrait("fiery", "bowstring");
```
第一个参数只能为 String 类型的 identifier(特性名)  
第二个参数为部件类型

## 关于特性

1.翻看带有特性的工具的 nbt, 找到 trait, trait 后面的数组内的字符串即是特性名称  
2.安装 Infini-TiC Mod, 进入游戏后输入 /infinitic traits 获取所有已注册的特性

## MaterialStats

仅在向材料的某一部件添加特性的时候才需要设置对应的 MaterialStats 属性  
如果不使用 MaterialStats 添加材料某一部件的的属性, 那个部件将制作不出来  
例子:
```javascript
myMat.addMaterialTrait("fiery", "bowstring");
myMat.addBowStringMaterialStats(0.5f);
```

有以下方法设置 MaterialStats

```javascript
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

参数解析:

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

最后记得调用一下 `register` 零参方法, 否则游戏内会无反应  

## 本地化key

本地化key为 `material.材料名.name`

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
testMat.itemLocalizer = function(thisMaterial, itemName) {
    return "Cool " + itemName;
};
testMat.localizedName = "Wicked";
testMat.register();
```
