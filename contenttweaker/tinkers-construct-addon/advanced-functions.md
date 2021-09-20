# 高级运用

## 更多实例

请看 [CrT 高级运用](https://ikexing.gitbook.io/crt/) ~~虽然咕咕咕了~~

## 运用于 MaterialBuilder 对象的函数

### ItemLocalizer 函数

导包

```csharp
import mods.tconstruct.materials.ItemLocalizer;
```

该函数用于计算材料名称  

此函数需要返回 string

* [Material](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Tinkers_Construct/Material/) 类的 `thisMaterial`
* String 类型的 `itemName`

例子

```csharp
myMat.itemLocalizer = function(thisMaterial, itemName) {
    return "Cool " + itemName;
};
```

游戏中 : ![iron](https://github.com/XHL315/ZentutorialPhotos/blob/master/Photos/Cool.png)

## 运用于 TraitBuilder 对象的函数

### CanApplyTogether 函数

导包

```csharp
import mods.tconstruct.traits.CanApplyTogetherTrait;
import mods.tconstruct.traits.CanApplyTogetherEnchantment;
```

此函数可以使特性或附魔不能同存  

此函数需要返回 bool

* [Trait](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Tinkers_Construct/Trait/) 类的 `thisTrait`
* String 类型的 `otherTrait`

例子1

```csharp
myTrait.canApplyTogetherTrait = function(thisTrait, otherTrait) {
    return otherTrait != 特性名称(也就是 identifier)
};
```

* [IEnchantmentDefinition](https://docs.blamejared.com/1.12/en/Vanilla/Enchantments/IEnchantmentDefinition/) 类的 `thisTrait`
* String 类型的 `enchantmentDefinition`

例子2

```csharp
myTrait.canApplyTogetherEnchantment = function(thisTrait, enchantmentDefinition) {
    return enchant != 附魔名称(不要傻傻的填个 "附魔名称")
};
```

### ExtraInfo 函数

导包

```csharp
import mods.tconstruct.traits.ExtraInfo;
```

可以在工具装配台看到额外信息

此函数需要返回 string[]

* [Trait](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Tinkers_Construct/Trait/) 类的 `thisTrait`
* [IItemStack](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemStack/) 类的 `item`
* [IData](https://docs.blamejared.com/1.12/en/Vanilla/Data/IData/) 类的 `tag`

例子 :

```csharp
myTrait.extraInfo = function(thisTrait, item, tag){
    var infos as string[] = ["Cool1", "Cool2"];
    return infos;
};
```

游戏中 : ![icon](https://github.com/XHL315/ZentutorialPhotos/blob/master/Photos/extraInfo.png)

### getMiningSpeed 函数

导包

```csharp
import mods.tconstruct.traits.MiningSpeed;
```

破坏方块时调用

此函数不需要返回值

* [Trait](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Tinkers_Construct/Trait/) 类的 `thisTrait`
* [IItemStack](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemStack/) 类的 `tool`
* [PlayerBreakSpeedEvent](https://docs.blamejared.com/1.12/en/Vanilla/Events/Events/PlayerBreakSpeed/) 类型的 `event`

函数写法 :

```csharp
myTrait.getMiningSpeed = function(thisTrait, tool, event) {
    //Code
};
```

### beforeBlockBreak 函数

导包

```csharp
import mods.tconstruct.traits.BeforeBlockBreak;
```

方块被破坏之前调用

此函数不需要返回值

* [Trait](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Tinkers_Construct/Trait/) 类的 `thisTrait`
* [IItemStack](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemStack/) 类的 `tool`
* [BlockBreakEvent](https://docs.blamejared.com/1.12/en/Vanilla/Events/Events/BlockBreak/) 类型的 `event`

函数写法 :

```csharp
myTrait.beforeBlockBreak = function(thisTrait, tool, event) {
    //Code
};
```

### afterBlockBreak 函数

导包

```csharp
import mods.tconstruct.traits.AfterBlockBreak;
```

方块被破坏之后调用

此函数不需要返回值

* [Trait](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Tinkers_Construct/Trait/) 类的 `thisTrait`
* [IItemStack](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemStack/) 类的 `tool`
* [IWorld](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Vanilla/Types/World/IWorld/) 类的 `world`
* [IBlockState](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Vanilla/Types/Block/ICTBlockState/) 类的 `blockstate`
* [IBlockPos](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Vanilla/Types/Block/IBlockPos/) 类的 `pos`
* [IEntityLivingBase](https://docs.blamejared.com/1.12/en/Vanilla/Entities/IEntityLivingBase/) 类的 `miner`
* boolean 类型的 `wasEffective`

函数写法 :

```csharp
myTrait.afterBlockBreak = function(thisTrait, tool, world, blockstate, pos, miner, wasEffective) {
    //Code
};
```

### onBlockHarvestDrops 函数

导包

```csharp
import mods.tconstruct.traits.BlockHarvestDrops;
```

方块被破坏且将要生成掉落物时调用

此函数不需要返回值

* [Trait](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Tinkers_Construct/Trait/) 类的 `thisTrait`
* [IItemStack](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemStack/) 类的 `tool`
* [BlockHarvestDropsEvent](https://docs.blamejared.com/1.12/en/Vanilla/Events/Events/BlockHarvestDrops/) 类型的 `event`

函数写法 :

```csharp
myTrait.onBlockHarvestDrops = function(thisTrait, tool, event) {
    //Code
};
```

### onUpdate 函数  

导包

```csharp
import mods.tconstruct.traits.Update;
```

此函数每 Tick 都会调用

此函数不需要返回值

* [Trait](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Tinkers_Construct/Trait/) 类的 `thisTrait`
* [IItemStack](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemStack/) 类的 `tool`
* [IWorld](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Vanilla/Types/World/IWorld/) 类的 `world`
* [IEntity](https://docs.blamejared.com/1.12/en/Vanilla/Entities/IEntity/) 类的 `entity` (实际使用时这个对象可能是为 [IPlayer](https://docs.blamejared.com/1.12/en/Vanilla/Players/IPlayer/), [IEntityLivingBase](https://docs.blamejared.com/1.12/en/Vanilla/Entities/IEntityLivingBase/), 只是被自动转型为 [IEntity](https://docs.blamejared.com/1.12/en/Vanilla/Entities/IEntity/), 可以 instanceof 判断之后就向下强转)
* int 类型的 `itemSlot`
* boolean 类型的 `isSelected`  

函数写法 :

```csharp
myTrait.onUpdate = function(thisTrait, tool, world, entity, itemSlot, isSelected) {
    //Code
};
```

### afterHit 函数

导包

```csharp
import mods.tconstruct.traits.AfterHit;
```

实体受到伤害后调用  

此函数不需要返回值

* [Trait](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Tinkers_Construct/Trait/) 类的 `thisTrait`
* [IItemStack](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemStack/) 类的 `tool`
* [IEntityLivingBase](https://docs.blamejared.com/1.12/en/Vanilla/Entities/IEntityLivingBase/) 类的 `attacker`
* [IEntityLivingBase](https://docs.blamejared.com/1.12/en/Vanilla/Entities/IEntityLivingBase/) 类的 `target`
* float 类型的 `damageDealt`
* boolean 类型的 `wasCritical`
* boolean 类型的 `wasHit`

函数写法 :

```csharp
mytrait.afterHit = function(trait, tool, attacker, target, damageDealt, wasCritical, wasHit) {
    //Code
};
```

### onHit 函数

导包

```csharp
import mods.tconstruct.traits.OnHit;
```

即将对实体造成伤害之前调用, 在此函数调用时所有的伤害都计算完毕 (简单来说就是最后一步)

此函数不需要返回值

* [Trait](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Tinkers_Construct/Trait/) 类的 `thisTrait`
* [IItemStack](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemStack/) 类的 `tool`
* [IEntityLivingBase](https://docs.blamejared.com/1.12/en/Vanilla/Entities/IEntityLivingBase/) 类的 `attacker`
* [IEntityLivingBase](https://docs.blamejared.com/1.12/en/Vanilla/Entities/IEntityLivingBase/) 类的 `target`
* float 类型的 `damage`
* boolean 类型的 `isCritical`

函数写法 :

```csharp
myTrait.onHit = function(thisTrait, tool, attacker, target, damage, isCritical) {
    //Code
};
```

### onBlock 函数  

导包

```csharp
import mods.tconstruct.traits.OnBlock;
```

玩家阻挡攻击时调用, 否则调用 [onPlayerHurt](#onplayerhurt-han-shu) 函数

此函数不需要返回值

* [Trait](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Tinkers_Construct/Trait/) 类的 `thisTrait`
* [IItemStack](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemStack/) 类的 `tool`
* [IPlayer](https://docs.blamejared.com/1.12/en/Vanilla/Players/IPlayer/) 类的 `attacker`
* [EntityLivingHurtEvent](https://docs.blamejared.com/1.12/en/Vanilla/Events/Events/EntityLivingHurt/) 类型的 `event`

函数写法 :

```csharp
myTrait.onBlock = function(thisTrait, tool, attacker, event) {
    //Code
};
```

### onPlayerHurt 函数

导包

```csharp
import mods.tconstruct.traits.OnPlayerHurt;
```

玩家未阻挡攻击时调用, 否则调用 [onBlock](#onblock-han-shu) 函数

此函数不需要返回值

* [Trait](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Tinkers_Construct/Trait/) 类的 `thisTrait`
* [IItemStack](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemStack/) 类的 `tool`
* [IPlayer](https://docs.blamejared.com/1.12/en/Vanilla/Players/IPlayer/) 类的 `player`
* [IEntityLivingBase](https://docs.blamejared.com/1.12/en/Vanilla/Entities/IEntityLivingBase/) 类的 `attacker`
* [EntityLivingHurtEvent](https://docs.blamejared.com/1.12/en/Vanilla/Events/Events/EntityLivingHurt/) 类型的 `event`

函数写法 :

```csharp
myTrait.onPlayerHurt = function(thisTrait, tool, player, attacker, event) {
    //Code
};
```

### calcCrit 函数

导包

```csharp
import mods.tconstruct.traits.IsCriticalHit;
```

对实体造成伤害之前调用以确定此次攻击是否暴击，返回值为 `false` 并不会取消已经是暴击的伤害

此函数需要返回一个 bool

* [Trait](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Tinkers_Construct/Trait/) 类的 `thisTrait`
* [IItemStack](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemStack/) 类的 `tool`
* [IEntityLivingBase](https://docs.blamejared.com/1.12/en/Vanilla/Entities/IEntityLivingBase/) 类的 `attacker`
* [IEntityLivingBase](https://docs.blamejared.com/1.12/en/Vanilla/Entities/IEntityLivingBase/) 类的 `target`

函数写法 :

```csharp
myTrait.calcCrit = function(thisTrait, tool, attacker, target) {
    //Code 
    return true; //或 false
};
```

### calcDamage 函数

导包

```csharp
import mods.tconstruct.traits.Damage;
```

攻击一个实体时调用，但在造成伤害和计算暴击加成之前调用, 此函数用于计算暴击伤害的加成

此函数需要返回一个 float 以确定伤害加成

* [Trait](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Tinkers_Construct/Trait/) 类的 `thisTrait`
* [IItemStack](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemStack/) 类的 `tool`
* [IEntityLivingBase](https://docs.blamejared.com/1.12/en/Vanilla/Entities/IEntityLivingBase/) 类的 `attacker`
* [IEntityLivingBase](https://docs.blamejared.com/1.12/en/Vanilla/Entities/IEntityLivingBase/) 类的 `target`
* float 类型的 `originalDamage`
* float 类型的 `currentDamage`
* boolean 类型的 `isCritical`

函数写法 :

```csharp
myTrait.calcDamage = function(thisTrait, tool, attacker, target, originalDamage, currentDamage, isCritical) {
    //Code 
    return currentDamage; //或者修改后的值
};
```

### calcKnockBack 函数

导包

```csharp
import mods.tconstruct.traits.KnockBack;
```

攻击实体后调用, 以修改实体受到的击退

此函数需要返回一个 float 以确定击退距离

* [Trait](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Tinkers_Construct/Trait/) 类的 `thisTrait`
* [IItemStack](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemStack/) 类的 `tool`
* [IEntityLivingBase](https://docs.blamejared.com/1.12/en/Vanilla/Entities/IEntityLivingBase/) 类的 `attacker`
* [IEntityLivingBase](https://docs.blamejared.com/1.12/en/Vanilla/Entities/IEntityLivingBase/) 类的 `target`
* float 类型的 `damage`
* float 类型的 `knockback`
* float 类型的 `newKnockback`
* boolean 类型的 `isCritical`

函数写法 :

```csharp
myTrait.calcKnockBack = function(thisTrait, tool, attacker, target, damage, knockback, newKnockback, isCritical) {
    //Code  
    return newKnockback; //或者修改后的值
};
```

### onToolDamage 函数

导包

```csharp
import mods.tconstruct.traits.OnToolDamage;
```

工具降低耐久度之前调用  

此函数需要返回一个 int 以确定工具耐久

* [Trait](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Tinkers_Construct/Trait/) 类的 `thisTrait`
* [IItemStack](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemStack/) 类的 `tool`
* int 类型的 `damage`
* int 类型的 `newDamage`
* [IEntityLivingBase](https://docs.blamejared.com/1.12/en/Vanilla/Entities/IEntityLivingBase/) 类的 `entity`

函数写法 :

```csharp
myTrait.onToolDamage = function(thisTrait, tool, damage, newDamage, entity) {
    //Code  
    return newDamage; //或者修改后的值
};
```

### calcToolHeal 函数

导包

```csharp
import mods.tconstruct.traits.OnToolHeal;
```

工具提高耐久度之前调用

此函数需要返回一个 int 以确定工具耐久

* [Trait](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Tinkers_Construct/Trait/) 类的 `thisTrait`
* [IItemStack](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemStack/) 类的 `tool`
* int 类型的 `damage`
* int 类型的 `newDamage`
* [IEntityLivingBase](https://docs.blamejared.com/1.12/en/Vanilla/Entities/IEntityLivingBase/) 类的 `entity`

函数写法 :  

```csharp
myTrait.calcToolHeal = function(thisTrait, tool, damage, newDamage, entity) {
    //Code  
    return newDamage; //或者修改后的值
};
```

### onToolRepair 函数

导包

```csharp
import mods.tconstruct.traits.OnToolRepair;
```

使用材料修复工具前调用, 请勿与 [calcToolHeal](#calctoolheal-han-shu) 函数混淆, 如果不止一次修复这个物品，此函数将被调用多次

此函数不需要返回值

* [Trait](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Tinkers_Construct/Trait/) 类的 `thisTrait`
* [IItemStack](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemStack/) 类的 `tool`
* int 类型的 `amount`

函数写法 :  

```csharp
myTrait.onToolRepair = function(thisTrait, tool, amount) {
    //Code
};
```
