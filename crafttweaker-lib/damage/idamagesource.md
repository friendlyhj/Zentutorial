# IDamageSource

## 导入

`import crafttweaker.damage.IDamageSource;`

## 尖括号引用

`<damagesource:type>`

如`<damageSource:IN_FIRE>;`

以下为游戏内已经有的damagesource类型

* IN_FIRE
* LIGHTNING_BOLT
* ON_FIRE
* LAVA
* HOT_FLOOR
* IN_WALL
* CRAMMING
* DROWN
* STARVE
* CACTUS
* FALL
* FLY_INTO_WALL
* OUT_OF_WORLD
* GENERIC
* MAGIC
* WITHER
* ANVIL
* FALLING_BLOCK
* DRAGON_BREATH
* FIREWORKS

如果引用的不在这其中，会创建一个全新的IDamageSource。

## 可用ZenGetter

| 名称 | 类型 | 是否有同名ZenSetter | 描述 |
|-----|------|------|------|
|harmInCreative|bool|✘||
|damageType|string|✘||
|hunderDamage|float|✘||
|immediateSource|[IEntity](https://youyi580.gitbook.io/zentutorial/crafttweaker-lib/entity/ientity)|✘||
|trueSource|IEntity|✘||
|creativePlayer|bool|✘||
|damageAbsolute|bool|✘||
|difficultyScaled|bool|✘||
|explosion|bool|✘||
|fireDamage|bool|✘||
|magicDamage|bool|✘||
|projectile|bool|✘||

## 可用方法

`String getDeathMessage(IEntity entity);`

`IDamageSource setDamageAllowedInCreativeMode();`

`IDamageSource setDamageBypassesArmor();`

`IDamageSource setDamageIsAbsolute();`

`IDamageSource setDifficultyScaled();`

`IDamageSource setExplosion();`

`IDamageSource setFireDamage();`

`IDamageSource setMagicDamage();`

`IDamageSource setProjectile();`

`static IDamageSource createMobDamage(IEntityLivingBase mob)`

`static IDamageSource createIndirectDamage(IEntity source, IEntityLivingBase indirectEntityIn)`

`static IDamageSourcecreatePlayerDamage(IPlayer player)`

`static IDamageSource createThrownDamage(IEntity source, @Optional IEntity indirectEntityIn)`

`static IDamageSource createIndirectMagicDamage(IEntity source, @Optional IEntity indirectEntityIn)`

`static IDamageSource createThornsDamage(IEntity source)`

`static IDamageSource createExplosionDamage(@Optional IEntityLivingBase entityLivingBaseIn)`

`static IDamageSource createOfType(String type)`
