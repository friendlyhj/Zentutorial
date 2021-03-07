# 特性

## 导入

通过`import mods.contenttweaker.tconstruct.Trait;`导入Trait类

通过`import mods.contenttweaker.tconstruct.TraitBuilder;`导入TraitBuilder类

## 特性构建器

`val myTrait = mods.contenttweaker.tconstruct.TraitBuilder.create(String identifier, int color, @Optional int maxLevel, @Optional int countPerLevel);`  

其实你填完第一个参数就可以不填,剩下的由Setter方法填也是可以的。

## 设定参数

| 参数 | 设定值类型 | 参数描述 |
| :---- | :---- | :---- |
| identifier | string | 设定名称(一般在写构建器的时候就写了,不会用到) |
| color | int | 设定颜色 |
| maxLevel | int | 最高等级(默认为1) |
| countPerLevel | int | 设定升级到第二级(前提是有,无就不需要写)需要多少个countPerLevel |
| hidden | bool | 隐藏特性 |
| localizedDescription | string | 本地化描述 |
| localizedName | sting | 本地化名称 |

## 访问特性数据

例子:`val myTraitData = myTrait.getData(itemWithTrait);`  

myTrait指特性,itemWithTrait指带有特性的工具

## 函数

### CanApplyTogether函数

可以使特性或附魔不能同存
例子1:`myTrait.canApplyTogetherTrait = function(thisTrait, otherTrait){return otherTrait != 特性名称(identifier)};`  
例子2:`myTrait.canApplyTogetherEnchantment = function(thisTrait, enchant){return enchant != 附魔名称};`

### Extra info函数

可以在工具装配台看到额外信息

例子:

```javascript
myTrait.extraInfo = function(thisTrait, item, tag){
    val infos as string[] = ["1","2"];
    for i, info in infos {
        return "Cool" ~ info;
    }
};
```

结果:额外信息显示Cool1,Cool2

### onUpdate函数  

每Tick都会调用

* Trait Representation类的`trait`
* IItemStack类的`tool`
* IWorld类的`world`
* IEntity类的`owner`
* int类型的`itemSlot`
* boolean类型的`isSelected`  

不需要返回值

函数写法:`myTrait.onUpdate = function(trait, tool, world, owner, itemSlot, isSelected) {//内容自写};`

### getMiningSpeed函数

在破坏方块时调用

请注意,这也会被 MC 的破坏方块事件监听到

* Trait Representation类的`trait`
* IItemStack类的`tool`
* 一个`PlayerBreakSpeedEvent`事件

不需要返回值

函数写法:`myTrait.getMiningSpeed = function(trait, tool, event) {//内容自写};`

### beforeBlockBreak函数

在方块被破坏之前调用。

请注意,这会被 MC 的破坏方块事件监听到。

* Trait Representation类的`trait`
* IItemStack类的`tool`
* 一个`BlockBreakEvent`事件

不需要返回值  
函数写法:`myTrait.beforeBlockBreak = function(trait, tool, event) {//内容自写};`

### afterBlockBreak函数

在方块被破坏之后调用。

* Trait Representation类的`trait`
* IItemStack类的`tool`
* IWorld类的`world`
* IBlockState类的`block`
* IEntityLivingBase类的`miner`
* boolean类型的`wasEffective`

不需要返回值。

函数写法:`myTrait.afterBlockBreak = function(trait, tool, world, blockstate, miner, wasEffective) {//内容自写};`  

### onBlockHarvestDrops函数

每当方块被破坏时调用

请注意,这会被 MC 的 BlockHarvestBreak事件监听到

* Trait Representation类的`trait`
* IItemStack类的`tool`
* 一个`BlockHarvestDropsEvent`事件

不需要返回值  
函数写法:`myTrait.onBlockHarvestDrops = function(trait, tool, event) {//内容自写};`  

### calcCrit函数

对实体造成伤害之前调用以确定它是否暴击，返回`false`并不会阻止已经确定是爆击的命中。

* Trait Representation类的`trait`
* IItemStack类的`tool`
* IEntityLivingBase类的`attacker`
* IEntityLivingBase类的`target`

需要返回值,返回`true`或者`false`

函数写法:`myTrait.calcCrit = function(trait, tool, attacker, target) {//内容自写 return true; //or false};`  

### calcDamage函数

对实体造成伤害,在实体和暴击伤害加成之前调用  

* Trait Representation类的`trait`
* IItemStack类的`tool`
* IEntityLivingBase类的`attacker`
* IEntityLivingBase类的`target`
* float类型的`originalDamage`
* float类型的`newDamage`
* boolean类型的`isCritical`

需要返回值,返回float类型的新伤害或者返回`newDamage`

函数写法:`myTrait.calcDamage = function(trait, tool, attacker, target, originalDamage, newDamage, isCritical) {//内容自写 return newDamage; //或者一个新耐久度};`  

### onHit函数

在对实体即将造成伤害之前调用,在此之前所有的伤害都计算完毕(最后一步)

* Trait Representation类的`trait`
* IItemStack类的`tool`
* IEntityLivingBase类的`attacker`
* IEntityLivingBase类的`target`
* float类型的`newDamage`
* boolean类型的`isCritical`

不需要返回值

函数写法:`myTrait.onHit = function(trait, tool, attacker, target, damage, isCritical) {//内容自写};`  

### calcKnockBack函数

怪物被命中后调用,以修改击退

* Trait Representation类的`trait`
* IItemStack类的`tool`
* IEntityLivingBase类的`attacker`
* IEntityLivingBase类的`target`
* float类型的`danage`
* float类型的`originalKnockback`
* float类型的`newKnockback`
* boolean类型的`isCritical`

需要返回一个float类型的数据,或者返回`newKnockback`

函数写法:`myTrait.calcDamage = function(trait, tool, attacker, target, damage, originalKnockBack, newKnockBack, isCritical) {//内容自写  return newDamage; //或者一个新耐久};`  

### afterHit函数

在实体受到伤害后调用  

* Trait Representation类的`trait`
* IItemStack类的`tool`
* IEntityLivingBase类的`attacker`
* IEntityLivingBase类的`target`
* float类型的`dealtDamage`
* boolean类型的`wasCritical`
* boolean类型的`wasHit`

不需要返回值  
函数写法:`mytrait.afterHit = function(trait, tool, attacker, target, damageDealt, wasCritical, wasHit) {//内容自写};`  

### onBlock函数  

当持有工具的玩家阻挡攻击时调用

* Trait Representation类的`trait`
* IItemStack类的`tool`
* IPlayer类的`player`
* 一个`EntityLivingHurtEvent`事件

不需要返回值

函数写法:`myTrait.onBlock = function(trait, tool, player, event) {//内容自写};`  

### onPlayerHurt函数

当持有工具的玩家未阻挡攻击时调用

* Trait Representation类的`trait`
* IItemStack类的`tool`
* IPlayer类的`player`
* IEntityLivingBase类的`attacker`
* 一个`EntityLivingHurtEvent`事件

不需要返回值

函数写法:`myTrait.onPlayerHurt = function(trait, tool, player, event) {//内容自写};`  

### onToolDamage函数

在工具降低耐久度之前调用  

* Trait Representation类的`trait`
* IItemStack类的`tool`
* int类型的`unmodifiedAmount`
* int类型的`newAmount`
* 代表当前工具的`holder`(IEntityLivingBase类型)

返回一个新的int类型的新耐久度或者返回newAmount

函数写法:`myTrait.onToolDamage = function(trait, tool, unmodifiedAmount, newAmount, holder) {//内容自写  return newAmount; //或者一个新耐久};`  

### calcToolHeal函数

在工具提高耐久度之前调用

* Trait Representation类的`trait`
* IItemStack类的`tool`
* int类型的`unmodifiedAmount`
* int类型的`newAmount`
* 代表当前工具的`holder`(IEntityLivingBase类型)

返回一个新的int类型的新耐久度或者返回newAmount

函数写法:`myTrait.onToolDamage = function(trait, tool, unmodifiedAmount, newAmount, holder) {//内容自写  return newAmount; //或者一个新耐久};`  

### onToolRepair函数

在使用材料修复工具前调用，请勿于`onToolHeal`混淆，如果不止一次使用这个物品，将被调用多次。  

* Trait Representation类的`trait`
* IItemStack类的`tool`
* int类型的`amount`

不需要返回值

函数写法:`myTrait.onToolRepair = function(trait, tool, amount) {//内容自写};`

## 注册特性

最后记得调用一下`register`零参方法,否则游戏会无反应  

## 本地化

本地化为上文的`localizedDescription`和`localizedName`  

## 官方例子

```javascript
#loader contenttweaker
#modloaded tconstruct

val testTrait = mods.contenttweaker.tconstruct.TraitBuilder.create("kindlich_test");
testTrait.color = 0xffaadd;
testTrait.maxLevel = 100;
testTrait.countPerLevel = 20;
testTrait.addItem(<item:minecraft:iron_pickaxe>);
testTrait.addItem(<item:minecraft:iron_block>, 4, 2);
testTrait.localizedName = "Whooooooooo";
testTrait.localizedDescription = "This is fun! Sadly, it doesn't do anything... \u2639";
testTrait.afterHit = function(thisTrait, tool, attacker, target, damageDealt, wasCrit, wasHit) {
    attacker.heal(damageDealt);
};
testTrait.register();
```
