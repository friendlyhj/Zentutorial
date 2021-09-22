# 构建材料

## 导包

```csharp
import mods.contenttweaker.tconstruct.MaterialBuilder;
```

## 构建器

**记得导包!**

```csharp
var myMat as MaterialBuilder = MaterialBuilder.create(identifier as string);
```

## 可设置参数

| 字段 | 设定值类型 | 描述 |
| :--- | :--- | :--- |
| identifier | string | 材料名称 |
| color | int | 材料颜色 |
| hidden | bool | 是否隐藏材料 |
| liquid | [ILiquidStack](https://docs.blamejared.com/1.12/en/Vanilla/Liquids/ILiquidStack/) | 设置流体 |
| craftable | bool (默认false) | 部件加工台是否可制作此材料 |
| castable | bool (默认false) | 冶炼炉是否可制作此材料 |
| representativeItem | [IItemStack](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemStack/) | 在匠魂宝典里显示的物品 |
| representativeOre | [IOreDictEntry](https://docs.blamejared.com/1.12/en/Vanilla/OreDict/IOreDictEntry/) | 同上, 但为矿物辞典内物品循环显示 |
| shard | [IItemStack](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemStack/) | 代替部件加工台的碎片 |
| localizedName | string | 本地化描述 |

## 方法

| 方法 | 描述 |
| :---- | :---- |
| addItem(ingredient as [IIngredient](https://docs.blamejared.com/1.12/en/Vanilla/Variable_Types/IIngredient/), amountNeeded as int, amountMatched as int) | 使 `ingredient` 可以在部件加工台制作此材料对应的模板的部件, `amountNeeded` 为需求数量, `amountMatched` 为匹配数量, 后两个参数选填, 默认为 1 |
| removeItem(itemStack as [IItemStack](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemStack/)) | 使 itemStack 不能制作此材料 |

## 材料特性

可以向材料对应的部件添加一些特性

### 增删特性至部件的方法

```csharp
//第一个参数可以填 Trait 对象, TraitBuilder 对象, String 类型的 identifier(特性名)
//这里比较建议填 String 类型的 identifier
//第二个参数都为部件类型
myMat.addMaterialTrait("fiery", "bowstring");
//第一个参数只能为 String 类型的 identifier(特性名) 
myMat.removeMaterialTrait("fiery", "bowstring");
```

### CoT 自带的部件类型

ContentTweaker 自带的部件类型有以下几种

(不填部件类型会把这个特性添加到材料的所有的部件上)

* "head"\-头部
* "handle"\-手柄
* "extra"\-大板, 绑定节, 坚韧手柄, 坚韧绑定节, 护手, 宽护手, 十字柄
* "bow"\-弓箭
* "bowstring"\-弓弦
* "projectile"\-?
* "shaft"\-箭杆, 弩箭核心
* "fletching"\-箭羽

#### 为什么没有碎片部件

答 : 你只要使用一次 `addMaterialTrait` 方法就会自动添加碎片部件

### 怎么知道我想要的特性的 identifier ?

1.翻看带有此特性的工具的 `nbt`, 找到 `"trait"`, `trait` 后面的数组内的字符串即是特性名称

2.安装 Infini-TiC Mod, 进入游戏后输入 `/infinitic traits` 获取所有已注册的特性

3.使用 [Tinkers Exporter](https://www.mcmod.cn/class/2740.html) Mod 导出匠魂各类数据

## MaterialStats

如果未给材料可制作的部件设置各项属性, 那此部件无法制作出来

有以下方法增删 MaterialStats

```csharp
myMat.addHeadMaterialStats(durability as int, miningSpeed as float, attackDamage as float, harvestLevel as int);
myMat.removeHeadMaterialStats();

myMat.addHandleMaterialStats(modifier as float, durability as int);
myMat.removeHandleMaterialStats();

myMat.addExtraMaterialStats(extraDurability as int);
myMat.removeExtraMaterialStats();

myMat.addBowMaterialStats(drawSpeed as float, range as float, bonusDamage as float);
myMat.removeBowMaterialStats();

myMat.addBowStringMaterialStats(modifier as float);
myMat.removeBowStringMaterialStats();

myMat.addArrowShaftMaterialStats(modifier as float, int bonusAmmo as int);
myMat.removeArrowShaftMaterialStats();

myMat.addFletchingMaterialStats(accuracy as float, modifier as float);
myMat.removeFletchingMaterialStats();

myMat.addProjectileMaterialStats();
myMat.removeProjectileMaterialStats();
```

### 参数解析

* durability\-耐久度
* miningSpeed\-挖掘速度
* attackDamage\-伤害
* harvestLevel\-挖掘等级
* modifier\-系数
* extraDurability\-耐久度
* drawSpeed\-蓄力时间
* range\-范围
* bonusDamage\-箭矢的附加伤害
* bonusAmmo\-额外弹药
* accuracy\-精准度

## 注册材料

最后记得调用一下 `register` 零参方法, 否则游戏内会无反应  

## 本地化key

本地化key为 `material.材料名.name`

## 实例

```csharp
#loader contenttweaker
import mods.contenttweaker.tconstruct.MaterialBuilder;

var testMat = MaterialBuilder.create("kindlich_mat");
testMat.color = 0x8e661b;
testMat.craftable = true;
testMat.castable = true;
testMat.liquid = <liquid:lava>;
testMat.localizedName = "Wicked";
testMat.representativeItem = <item:minecraft:red_flower:4>;
testMat.addItem(<item:minecraft:red_flower:4>);
testMat.addHeadMaterialStats(100, 1.5f, 5.5f, 5);
testMat.addHandleMaterialStats(0.3, 500);
testMat.addBowStringMaterialStats(0.5f);
testMat.addMaterialTrait("blasting", "bowstring");
testMat.addMaterialTrait("blasting", "head");
testMat.addMaterialTrait("dense", null);
//此函数将在高级运用讲解
testMat.itemLocalizer = function(thisMaterial, itemName) {
    return "Cool " + itemName;
};
testMat.register();
```
