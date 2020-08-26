# 特性

## 导入
通过`import mods.contenttweaker.tconstruct.Trait;`导入Trait对象  
通过`import mods.contenttweaker.tconstruct.TraitBuilder;`导入TraitBuilder对象  
通过`import mods.contenttweaker.tconstruct.TraitDataRepresentation;`导入TraitDataRepresentation对象  

## 特性构建器
`val myTrait = mods.contenttweaker.tconstruct.TraitBuilder.create(String identifier, int color, @Optional int maxLevel, @Optional int countPerLevel);`  
**其实你填完第一个参数就可以不填,剩下的由Setter方法填也是可以的。**

## 设定参数
**你可以通过一下方法设定特性的参数**
| 参数 | 设定值类型 | 参数描述 |
| :---- | :---- | :---- |
| identifier | string | 设定名称(一般在写构建器的时候就写了,不会用到) |
| color | int | 设定颜色 |
| maxLevel | int | 最高等级 |
| countPerLevel | int | 设定升级到第二级(前提是有,无就不需要写)需要多少个countPerLevel |
| hidden | bool | ? | 
| localizedDescription | string | 本地化描述 |
| localizedName | sting | 本地化名称 |

## CanApplyTogether函数
**可以使特性(附魔)不能同存**  
例子1:`myTrait.canApplyTogetherTrait = function(TraitRepresentation thisTrait, String otherTrait){return otherTrait != 特性名称(identifier)};`  
例子2:`myTrait.canApplyTogetherEnchantment = function(TraitRepresentation thisTrait, IEnchantmentDefinition enchant){return enchant != 附魔名称};`

## Extra info函数
**可以在工具装配台看到额外信息**  
例子:
```javascript
myTrait.extraInfo = function(TraitRepresentation thisTrait, IItemStack item, IData tag){
    val infos as string[] = ["1","2"];
    for i, info in infos {
        return "Cool" ~ info;
    }
};
```
结果,额外信息显示Cool1,Cool2  

## 访问特性数据
例子:`(val myTraitData = )myTrait.getData(itemWithTrait);`  
**myTrait指特性,itemWithTrait指工具**  

## TraitDataRepresentation
### 设定参数
**ZenGetter与ZenSetter**  
| 参数 | 是否有ZenGetter | 是否有ZenSetter | 返回(设定)值类型 | 参数描述 |
| :---- | :---- | :---- | :---- | :---- |
| identifier | √ | √ | string | 名称 |
| extraInfo | √ | √ | string | 额外信息 |
| info | √ | × | string | ? |
| colorString | √ | × | string | ? |
| level | √ | √ | int | 等级 | 
| color | √ | √ | int | 颜色 |
| current | √ | √ | int | ? |
| max | √  | √ | int | ? |

## 函数
onUpdate函数  
每Tick都会加载  
**参数类型:Trait Representation类的`trait`,IItemStack类的`tool`,IWorld类的`world`,IEntity类的`owner`,int类型的`itemSlot`,boolean类型的`isSelected`**  
不需要返回值  
函数写法:`myTrait.getMiningSpeed = function(trait, tool, world, owner, itemSlot, isSelected) {//内容自写};`

getMiningSpeed函数  
在破坏方块时调用  
**请注意,这会被我的世界的破坏方块事件监听到**  
**参数类型:Trait Representation类的`trait`,IItemStack类的`tool`,一个PlayerBreakSpeedEvent事件**  
不需要返回值  
函数写法:`myTrait.getMiningSpeed = function(trait, tool, event) {//内容自写};`

beforeBlockBreak函数  
在方块被破坏之前调用  
**请注意,这会被我的世界的破坏方块事件监听到**  
**参数类型:Trait Representation类的`trait`,IItemStack类的`tool`,一个BlockBreakEvent事件**  
不需要返回值  
函数写法:`myTrait.beforeBlockBreak = function(trait, tool, event) {//内容自写};`

afterBlockBreak函数
在方块被破坏之后调用
**参数类型:Trait Representation类的`trait`,IItemStack类的`tool`,IWorld类的`world`,IBlockState类的`block`,IEntityLivingBase类的`miner`,boolean类型的`wasEffective`**  
不需要返回值  
函数写法:`myTrait.afterBlockBreak = function(trait, tool, world, blockstate, miner, wasEffective) {//内容自写};`  

onBlockHarvestDrops函数  
每当方块被破坏时调用  
**请注意,这会被我的世界BlockHarvestBreak事件监听到**  
**参数类型:Trait Representation类的`trait`,IItemStack类的`tool`,一个BlockHarvestDropsEvent事件**  
不需要返回值  
函数写法:`myTrait.onBlockHarvestDrops = function(trait, tool, event) {//内容自写};`  

calcCrit函数
对实体造成伤害之前调用~~以确定它是否暴击(?)(看机翻的狼灭),返回`false`并不会阻止已经是爆击的命中~~  
**参数类型:Trait Representation类的`trait`,IItemStack类的`tool`,IEntityLivingBase类的`attacker`,IEntityLivingBase类的`target`**  
需要返回值,返回true或者false  
函数写法:`myTrait.calcCrit = function(trait, tool, attacker, target) {//内容自写 return true; //or false};`  

calcDamage函数
对实体造成伤害,在实体和暴击伤害加成之前调用  
**参数类型:Trait Representation类的`trait`,IItemStack类的`tool`,IEntityLivingBase类的`attacker`,IEntityLivingBase类的`target`,float类型的`originalDamage`,float类型的`newDamage`,boolean类型的`isCritical`**   
需要返回值,返回float类型的新伤害或者返回newDamage  
函数写法:`myTrait.calcDamage = function(trait, tool, attacker, target, originalDamage, newDamage, isCritical) {//内容自写 return newDamage; //或修改后的值};`  
