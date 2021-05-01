# 高级运用

## 实例

请看[这](https://ikexing.gitbook.io/crt/)

## 运用于 MaterialBuilder 对象的函数

### ItemLocalizer函数

该函数用于计算材料名称  

 * [Material](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Tinkers_Construct/Material/) 类的 `thisMaterial`
 * String 类型的 `itemName`

例子 :
```javascript
myMat.itemLocalizer = function(thisMaterial, itemName) {
    return "Cool " + itemName;
};
```

结果 : 在名字前面加上 Cool

## 运用于 TraitBuilder 对象的函数

### CanApplyTogether 函数

此函数可以使特性或附魔不能同存  

 * [Trait](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Tinkers_Construct/Trait/) 类的 `thisTrait`
 * String 类型的 `otherTrait`

例子1 :
```javascript
myTrait.canApplyTogetherTrait = function(thisTrait, otherTrait) {
    return otherTrait != 特性名称(也就是 identifier)
};
```

 * [IEnchantmentDefinition](https://docs.blamejared.com/1.12/en/Vanilla/Enchantments/IEnchantmentDefinition/) 类的 `thisTrait`
 * String 类型的 `enchantmentDefinition`

例子2 :
```javascript
myTrait.canApplyTogetherEnchantment = function(thisTrait, enchantmentDefinition) {
    return enchant != 附魔名称(不要傻傻的填个"附魔名称")
};
```

### Extra info 函数

可以在工具装配台看到额外信息

 * [Trait](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Tinkers_Construct/Trait/) 类的 `thisTrait`
 * [IItemStack](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemStack/) 类的 `item`
 * [IData](https://docs.blamejared.com/1.12/en/Vanilla/Data/IData/) 类的 `tag`

例子 :
```javascript
myTrait.extraInfo = function(thisTrait, item, tag){
    val infos as string[] = ["1", "2"];
    for info in infos {
        return "Cool" ~ info;
    }
};
```

结果 : 工具装配台右侧显示 Cool1, Cool2

### getMiningSpeed 函数

此函数将在破坏方块时调用

注意 :  CrT 的 [PlayerBreakSpeedEvent](https://docs.blamejared.com/1.12/en/Vanilla/Events/Events/PlayerBreakSpeed/) 事件也监听此 MC 事件(所以如果 zs 脚本也写了这个事件, 那这个函数可能会被影响)

* [Trait](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Tinkers_Construct/Trait/) 类的 `thisTrait`
* [IItemStack](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemStack/) 类的 `tool`
* [PlayerBreakSpeedEvent](https://docs.blamejared.com/1.12/en/Vanilla/Events/Events/PlayerBreakSpeed/) 类型的 `event`

此函数不需要返回值(想在一些不满足条件的情况下结束代码怎么办? 不需要返回值的函数用 return 就可以了)

函数写法 :
```javascript
myTrait.getMiningSpeed = function(thisTrait, tool, event) {
    //Code
};
```

### beforeBlockBreak 函数

此函数将在方块被破坏之前调用

此函数将

* [Trait](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Tinkers_Construct/Trait/) 类的 `thisTrait`
* [IItemStack](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemStack/) 类的 `tool`
* [BlockBreakEvent](https://docs.blamejared.com/1.12/en/Vanilla/Events/Events/BlockBreak/) 类型的 `event`

此函数不需要返回值(想在一些不满足条件的情况下结束代码怎么办? 不需要返回值的函数用 return 就可以了)

函数写法 :
```javascript
myTrait.beforeBlockBreak = function(thisTrait, tool, event) {
    //Code
};
```

### afterBlockBreak 函数

此函数将在方块被破坏之后调用

* [Trait](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Tinkers_Construct/Trait/) 类的 `thisTrait`
* [IItemStack](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemStack/) 类的 `tool`
* [IWorld](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Vanilla/Types/World/IWorld/) 类的 `world`
* [IBlockState](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Vanilla/Types/Block/ICTBlockState/) 类的 `blockstate`
* [IBlockPos](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Vanilla/Types/Block/IBlockPos/) 类的 `pos`
* [IEntityLivingBase](https://docs.blamejared.com/1.12/en/Vanilla/Entities/IEntityLivingBase/) 类的 `miner`
* boolean 类型的 `wasEffective`

此函数不需要返回值(想在一些不满足条件的情况下结束代码怎么办? 不需要返回值的函数用 return 就可以了)

函数写法 :
```javascript
myTrait.afterBlockBreak = function(thisTrait, tool, world, blockstate, pos, miner, wasEffective) {
    //Code
};
```

### onBlockHarvestDrops 函数

此函数将当方块被破坏并且将要生成掉落物时调用

注意 :  CrT 的 [BlockHarvestDropsEvent](https://docs.blamejared.com/1.12/en/Vanilla/Events/Events/BlockHarvestDrops/) 事件也监听此 MC 事件(所以如果 zs 脚本也写了这个事件, 那这个函数可能会被影响)

* [Trait](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Tinkers_Construct/Trait/) 类的 `thisTrait`
* [IItemStack](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemStack/) 类的 `tool`
* [BlockHarvestDropsEvent](https://docs.blamejared.com/1.12/en/Vanilla/Events/Events/BlockHarvestDrops/) 类型的 `event`

此函数不需要返回值(想在一些不满足条件的情况下结束代码怎么办? 不需要返回值的函数用 return 就可以了)

函数写法 :
```javascript
myTrait.onBlockHarvestDrops = function(thisTrait, tool, event) {
    //Code
};
```

### onUpdate 函数  

此函数每 Tick 都会调用

* [Trait](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Tinkers_Construct/Trait/) 类的 `thisTrait`
* [IItemStack](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemStack/) 类的 `tool`
* [IWorld](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Vanilla/Types/World/IWorld/) 类的 `world`
* [IEntity](https://docs.blamejared.com/1.12/en/Vanilla/Entities/IEntity/) 类的 `entity` (实际使用时这个对象可能是为 [IPlayer](https://docs.blamejared.com/1.12/en/Vanilla/Players/IPlayer/), [IEntityLivingBase](https://docs.blamejared.com/1.12/en/Vanilla/Entities/IEntityLivingBase/), 只不过被强转为 [IEntity](https://docs.blamejared.com/1.12/en/Vanilla/Entities/IEntity/))
* int 类型的 `itemSlot`
* boolean 类型的 `isSelected`  

此函数不需要返回值(想在一些不满足条件的情况下结束代码怎么办? 不需要返回值的函数用 return 就可以了)

函数写法 :
```javascript
myTrait.onUpdate = function(thisTrait, tool, world, entity, itemSlot, isSelected) {
    //Code
};
```

### onHit 函数

在对实体即将造成伤害之前调用, 在此函数调用时所有的伤害都计算完毕(简单来说就是最后一步)

* [Trait](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Tinkers_Construct/Trait/) 类的 `thisTrait`
* [IItemStack](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemStack/) 类的 `tool`
* [IEntityLivingBase](https://docs.blamejared.com/1.12/en/Vanilla/Entities/IEntityLivingBase/) 类的 `attacker`
* [IEntityLivingBase](https://docs.blamejared.com/1.12/en/Vanilla/Entities/IEntityLivingBase/) 类的 `target`
* float 类型的 `damage`
* boolean 类型的 `isCritical`

此函数不需要返回值(想在一些不满足条件的情况下结束代码怎么办? 不需要返回值的函数用 return 就可以了)

函数写法 :
```javascript
myTrait.onHit = function(thisTrait, tool, attacker, target, damage, isCritical) {
    //Code
};
```

### afterHit 函数

在实体受到伤害后调用  

* [Trait](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Tinkers_Construct/Trait/) 类的 `thisTrait`
* [IItemStack](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemStack/) 类的 `tool`
* [IEntityLivingBase](https://docs.blamejared.com/1.12/en/Vanilla/Entities/IEntityLivingBase/) 类的 `attacker`
* [IEntityLivingBase](https://docs.blamejared.com/1.12/en/Vanilla/Entities/IEntityLivingBase/) 类的 `target`
* float 类型的 `damageDealt`
* boolean 类型的 `wasCritical`
* boolean 类型的 `wasHit`

此函数不需要返回值(想在一些不满足条件的情况下结束代码怎么办? 不需要返回值的函数用 return 就可以了)

函数写法 :
```javascript
mytrait.afterHit = function(trait, tool, attacker, target, damageDealt, wasCritical, wasHit) {
    //Code
};
```

### onBlock 函数  

当持有具有此函数的工具的玩家阻挡攻击时调用
否则调用 [onHit](https://youyi580.gitbook.io/zentutorial/contenttweaker/tinkers-construct-addon/advanced-functions#onhit-han-shu) 函数

* [Trait](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Tinkers_Construct/Trait/) 类的 `thisTrait`
* [IItemStack](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemStack/) 类的 `tool`
* [IPlayer](https://docs.blamejared.com/1.12/en/Vanilla/Players/IPlayer/) 类的 `attacker`
* [EntityLivingHurtEvent](https://docs.blamejared.com/1.12/en/Vanilla/Events/Events/EntityLivingHurt/) 类型的 `event`

此函数不需要返回值(想在一些不满足条件的情况下结束代码怎么办? 不需要返回值的函数用 return 就可以了)

函数写法 :
```javascript
myTrait.onBlock = function(thisTrait, tool, attacker, event) {
    //Code
};
```

### onPlayerHurt 函数

当持有具有此函数的工具的玩家未阻挡攻击时调用
否则调用 [onBlock](https://youyi580.gitbook.io/zentutorial/contenttweaker/tinkers-construct-addon/advanced-functions#onblock-han-shu) 函数

* [Trait](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Tinkers_Construct/Trait/) 类的 `thisTrait`
* [IItemStack](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemStack/) 类的 `tool`
* [IPlayer](https://docs.blamejared.com/1.12/en/Vanilla/Players/IPlayer/) 类的 `player`
* [IEntityLivingBase](https://docs.blamejared.com/1.12/en/Vanilla/Entities/IEntityLivingBase/) 类的 `attacker`
* [EntityLivingHurtEvent](https://docs.blamejared.com/1.12/en/Vanilla/Events/Events/EntityLivingHurt/) 类型的 `event`

此函数不需要返回值(想在一些不满足条件的情况下结束代码怎么办? 不需要返回值的函数用 return 就可以了)

函数写法 :
```javascript
myTrait.onPlayerHurt = function(thisTrait, tool, player, attacker, event) {
    //Code
};
```

### onToolRepair 函数

在使用材料修复工具前调用, 请勿将此函数与 [calcToolHeal](https://youyi580.gitbook.io/zentutorial/contenttweaker/tinkers-construct-addon/advanced-functions#ontoolrepair-han-shu) 函数混淆, 如果不止一次修复这个物品，此函数将被调用多次

* [Trait](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Tinkers_Construct/Trait/) 类的 `thisTrait`
* [IItemStack](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemStack/) 类的 `tool`
* int 类型的 `amount`

此函数不需要返回值(想在一些不满足条件的情况下结束代码怎么办? 不需要返回值的函数用 return 就可以了)

函数写法 :  
```javascript
myTrait.onToolRepair = function(thisTrait, tool, amount) {
    //Code
};
```

### calcCrit 函数

对实体造成伤害之前调用以确定它是否造成暴击，返回值为 `false` 也不会取消已经确定是暴击的伤害

* [Trait](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Tinkers_Construct/Trait/) 类的 `thisTrait`
* [IItemStack](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemStack/) 类的 `tool`
* [IEntityLivingBase](https://docs.blamejared.com/1.12/en/Vanilla/Entities/IEntityLivingBase/) 类的 `attacker`
* [IEntityLivingBase](https://docs.blamejared.com/1.12/en/Vanilla/Entities/IEntityLivingBase/) 类的 `target`

此函数需要返回值, 返回 `true` 或者 `false`

函数写法 :
```javascript
myTrait.calcCrit = function(thisTrait, tool, attacker, target) {
    //Code 
    return true; //或 false
};
```

### calcDamage 函数

当一个实体被击中时调用，但在造成伤害和暴击伤害加成之前调用  
此函数用于计算暴击伤害的加成

* [Trait](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Tinkers_Construct/Trait/) 类的 `thisTrait`
* [IItemStack](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemStack/) 类的 `tool`
* [IEntityLivingBase](https://docs.blamejared.com/1.12/en/Vanilla/Entities/IEntityLivingBase/) 类的 `attacker`
* [IEntityLivingBase](https://docs.blamejared.com/1.12/en/Vanilla/Entities/IEntityLivingBase/) 类的 `target`
* float 类型的 `originalDamage`
* float 类型的 `currentDamage`
* boolean 类型的 `isCritical`

此函数需要返回值, 返回 float 类型的新伤害或者返回 `currentDamage`

函数写法 :
```javascript
myTrait.calcDamage = function(thisTrait, tool, attacker, target, originalDamage, currentDamage, isCritical) {
    //Code 
    return currentDamage; //或者修改后的值
};
```

### calcKnockBack 函数

此函数在实体被命中后调用, 以修改实体受到的击退

* [Trait](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Tinkers_Construct/Trait/) 类的 `thisTrait`
* [IItemStack](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemStack/) 类的 `tool`
* [IEntityLivingBase](https://docs.blamejared.com/1.12/en/Vanilla/Entities/IEntityLivingBase/) 类的 `attacker`
* [IEntityLivingBase](https://docs.blamejared.com/1.12/en/Vanilla/Entities/IEntityLivingBase/) 类的 `target`
* float 类型的 `damage`
* float 类型的 `knockback`
* float 类型的 `newKnockback`
* boolean 类型的 `isCritical`

此函数需要返回一个 float 类型的击退数值, 或者返回 `newKnockback`

函数写法 :
```javascript
myTrait.calcDamage = function(thisTrait, tool, attacker, target, damage, knockback, newKnockback, isCritical) {
    //Code  
    return newKnockback; //或者修改后的值
};
```

### onToolDamage 函数

此函数在工具降低耐久度之前调用  

* [Trait](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Tinkers_Construct/Trait/) 类的 `thisTrait`
* [IItemStack](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemStack/) 类的 `tool`
* [IEntityLivingBase](https://docs.blamejared.com/1.12/en/Vanilla/Entities/IEntityLivingBase/) 类的 `entity`
* int 类型的 `damage`
* int 类型的 `newDamage`

此函数需要返回一个 int 类型的耐久或者返回 `newDamage`

函数写法 :
```javascript
myTrait.onToolDamage = function(thisTrait, tool, damage, newDamage, entity) {
    //Code  
    return newDamage; //或者修改后的值
};
```

### calcToolHeal 函数

此函数在工具提高耐久度之前调用

* [Trait](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Tinkers_Construct/Trait/) 类的 `thisTrait`
* [IItemStack](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemStack/) 类的 `tool`
* [IEntityLivingBase](https://docs.blamejared.com/1.12/en/Vanilla/Entities/IEntityLivingBase/) 类的 `entity`
* int 类型的 `damage`
* int 类型的 `newDamage`

此函数需要返回一个 int 类型的耐久或者返回 `newDamage`

函数写法 :  
```javascript
myTrait.onToolDamage = function(thisTrait, tool, damage, newDamage, entity) {
    //Code  
    return newDamage; //或者修改后的值
};
```
