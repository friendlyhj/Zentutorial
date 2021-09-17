---
description: 需要附属mod LootTweaker
---

# 进阶

在阅读此页面前, 强烈建议先阅读 [战利品表修改(LootTweaker-基础)](/easy/loottweaker-easy.md) 页面.

## ZenScript 类型

### LootTweaker

* 全名 : ```loottweaker.LootTweaker```.

#### 方法

##### getTable(String tableName)

* tableName - LootTable 的名称.
如没有对应 LootTable 时, 返回错误.

正常时返回对应的 LootTable 对象.

##### newTable(String tableName)

* tableName - LootTable 的名称.
如已存在同名 LootTable, 返回错误.

如使用了 ```minecraft``` 命名空间, 返回警告. (可在 LootTweaker 配置中关闭此警告.)

正常时返回对应名称的空 LootTable 对象.

### LootTable

* 全名 : ```loottweaker.vanilla.loot.LootTable```.

#### 方法

##### clear()

清除所有此 LootTable 中的物品, 包括在调用此方法前使用脚本添加的。无返回值。

##### addPool(String poolName, float minRolls, float maxRolls, float minBonusRolls, float maxBonusRolls)

创建一个名称为 指定名称的 pool.

* poolName - pool 的名称.
* minRolls - 最低被抽取次数.
* maxRolls - 最高被抽取次数.
* minRolls - 最低额外被抽取次数.
* maxRolls - 最高额外被抽取次数.
如已存在同名 pool, 返回错误.

正常时返回对应名称的空 pool 对象.

##### removePool(String poolName)

移除指定名称对应的 pool.

* poolName - pool 的名称.

如指定名称对应的 pool 不存在, 返回错误.

正常时返回 void.

##### getPool(String poolName)

* poolName - pool 的名称.

如指定名称对应的 pool 不存在, 返回错误.

正常时返回指定名称对应的 pool.

#### pool 名称

所有 pool 都有一个名字. 第一个, 默认的 pool 名为 main. 接连的 pool 的命名格式为 ```poolN```, N 是一个从 ```1``` 递进的整数.


### LootPool

* 全名 : ```loottweaker.vanilla.loot.LootPool```.

#### Map 自动转换

0.2.1 及以上版本的 LootTweaker 会自动将 JSON 格式 Map 转换为 LootCondition/LootFunction. 即所有 LootFunction/LootCondition 参数都同样可以接受 JSON 格式 Map.

#### 方法

##### addConditions(LootCondition[] conditions)

为 pool 添加条件.

* conditions - LootCondition 实例数组.

无返回值。

##### removeEntry(String entryName)

移除 pool 中指定名称对应的 entry.

* entryName - entry 的名称.

pool 中不存在指定名称对应的 entry 时, 返回错误.

无返回值。

##### addItemEntry(IItemStack iStack, int weight, int quality, LootFunction[] functions, LootCondition[] conditions, @Optional String name)

向指定 pool 中添加一个 ```item``` 类型的 entry.

* iStack - 此 entry 产生的物品堆. LootTweaker 会在 ```functions``` 中不包含同名 LootFunction 时基于此堆自动生成 ```set_nbt```, ```set_damage/set_data``` 和 ```set_count``` 参数.
* weight - 此 entry 的生成权重, 越高生成的机率越大.
* quality - 此 entry 的稀有度, 即幸运效果影响此 entry 的程度, 越高受幸运效果影响就越大.
* functions - 影响此 entry 生成的参数.
* conditions - 此 entry 生成的条件.
* name - (可选) 此 entry 的名称, 必须在 pool 范围中唯一.

如指定 pool 中已存在同名 entry, 返回错误.

正常时返回 void.

##### addItemEntry(IItemStack stack, int weightIn, int qualityIn, @Optional String name)

向指定 pool 中添加一个 ```item``` 类型的 entry.

* stack - 此 entry 产生的物品堆. LootTweaker 会基于此堆自动生成 ```set_nbt```, ```set_damage/set_data``` 和 ```set_count``` 参数.
* weightIn - 此 entry 的生成权重, 越高生成的机率越大.
* qualityIn - 此 entry 的稀有度, 即幸运效果影响此 entry 的程度, 越高受幸运效果影响就越大.
* name - (可选) 此 entry 的名称, 必须在 pool 范围中唯一.

如指定 pool 中已存在同名 entry, 返回错误.

正常时返回 void.

##### addItemEntry(IItemStack stack, int weightIn, @Optional String name)

向指定 pool 中添加一个 ```item``` 类型的 entry.

* stack - 此 entry 产生的物品堆. LootTweaker 会在 ```functions``` 中不包含同名 LootFunction 时基于此堆自动生成 ```set_nbt```, ```set_damage/set_data``` 和 ```set_count``` 参数.
* weightIn - 此 entry 的生成权重, 越高生成的机率越大.
* name - (可选) 此 entry 的名称, 必须在 pool 范围中唯一.

如指定 pool 中已存在同名 entry, 返回错误.

正常时返回 void.

##### addLootTableEntry(String tableName, int weightIn, int qualityIn, LootCondition[] conditions, @Optional String name)

向指定 pool 中添加一个 ```loot_table``` 类型的 entry.

* tableName - 此 entry 用于读取并生成战利品的 LootTable 的名称.
* weight - 此 entry 的生成权重, 越高生成的机率越大.
* quality - 此 entry 的稀有度, 即幸运效果影响此 entry 的程度, 越高受幸运效果影响就越大.
* conditions - 此 entry 生成的条件.
* name - (可选) 此 entry 的名称, 必须在 pool 范围中唯一.

如指定 pool 中已存在同名 entry, 返回错误.

正常时返回 void.

##### addLootTableEntry(String tableName, int weightIn, int qualityIn, @Optional String name)

向指定 pool 中添加一个 ```loot_table``` 类型的 entry.

* tableName - 此 entry 用于读取并生成战利品的 LootTable 的名称.
* weight - 此 entry 的生成权重, 越高生成的机率越大.
* quality - 此 entry 的稀有度, 即幸运效果影响此 entry 的程度, 越高受幸运效果影响就越大.
* name - (可选) 此 entry 的名称, 必须在 pool 范围中唯一.

如指定 pool 中已存在同名 entry, 返回错误.

正常时返回 void.

##### addLootTableEntry(String tableName, int weightIn, @Optional String name)

向指定 pool 中添加一个 ```loot_table``` 类型的 entry.

* tableName - 此 entry 用于读取并生成战利品的 LootTable 的名称.
* weight - 此 entry 的生成权重, 越高生成的机率越大.
* name - (可选) 此 entry 的名称, 必须在 pool 范围中唯一.

如指定 pool 中已存在同名 entry, 返回错误.

正常时返回 void.

##### addEmptyEntry(int weight, int quality, LootCondition[] conditions, @Optional String name)

向指定 pool 中添加一个 ```empty``` 类型的 entry.

* weight - 此 entry 的生成权重, 越高生成的机率越大.
* quality - 此 entry 的稀有度, 即幸运效果影响此 entry 的程度, 越高受幸运效果影响就越大.
* conditions - 此 entry 生成的条件.
* name - (可选) 此 entry 的名称, 必须在 pool 范围中唯一.

如指定 pool 中已存在同名 entry, 返回错误.

正常时返回 void.

##### addEmptyEntry(int weight, int quality, @Optional String name)

向指定 pool 中添加一个 ```empty``` 类型的 entry.

* weight - 此 entry 的生成权重, 越高生成的机率越大.
* quality - 此 entry 的稀有度, 即幸运效果影响此 entry 的程度, 越高受幸运效果影响就越大.
* name - (可选) 此 entry 的名称, 必须在 pool 范围中唯一.

如指定 pool 中已存在同名 entry, 返回错误.

正常时返回 void.

##### addEmptyEntry(int weight, @Optional String name)

向指定 pool 中添加一个 ```empty``` 类型的 entry.

* weight - 此 entry 的生成权重, 越高生成的机率越大.
* name - (可选) 此 entry 的名称, 必须在 pool 范围中唯一.

如指定 pool 中已存在同名 entry, 返回错误.

正常时返回 void.

##### setRolls(float min, float max)

设置指定 pool 被抽取次数的最大最小值

* min - 被抽取次数的最小值
* max - 被抽取次数的最大值

正常时返回 void.

##### setBonusRolls(float min, float max)

设置指定 pool 额外被抽取次数的最大最小值

* min - 被抽取次数的最小值
* max - 被抽取次数的最大值

正常时返回 void.

##### clearConditions()

清除此 pool 的所有条件.

被绑定在子 entry 上的条件不受影响.

正常时返回 void.

##### clearEntries()

清除此 pool 中的所有 entry.

正常时返回 void.

### Conditions

* 全名 : ```loottweaker.vanilla.loot.Conditions```.

JSON 格式偶尔很难写, 此类型提供部分创建简单战利品条件的便利方法, 但如果想创建复杂战利品条件, 写 JSON 格式仍然是最佳选择.

```minecraft:entity_properties``` 和 ```minecraft:entity_scores``` 是没有任何便利方法的, 因为它们太复杂了.

此分类下的所有方法, 除了 ```parse()``` 会创建一个参数等效于等效战利品条件的参数的原版战利品条件. 所有的原版战利品条件都将被在下方列出.

战利品函数对应的类型是 ```Conditions```.

#### 方法


##### randomChance(float chance)

等价于 ```minecraft:random_chance```.

* chance - 随机概率.

##### randomChanceWithLooting(float chance, float lootingMult)

等价于 ```minecraft:random_chance_with_looting```.

* chance - 随机概率.
* lootingMult - 多战利品概率

##### killedByPlayer()

等价于 ```minecraft:killed_by_player```.

##### killedByNonPlayer()

等价于 ```inverse``` 值设置为 ```true``` 的 ```minecraft:killed_by_player```.

##### parse(DataMap json)

将一个 ```DataMap``` 转换为 LootCondition.

* json - ```DataMap``` 格式的 LootCondition.

##### zenscript(loottweaker.CustomLootCondition zenFunction)

将一个 ```zenFunction``` 转换为 ```LootCondition```.

* zenFunction - 一个附带了 ```IRandom``` 和 ```LootContext``` 参数, 且返回 ```Boolean``` 值的 ZenScript 自定义函数.

如提供的 ZenScript 自定义函数返回 true, 返回一个 LootCondition.

### Functions

* 全名 : ```loottweaker.vanilla.loot.Functions```.

JSON 格式偶尔很难写, 此类型提供部分创建简单战利品函数的便利方法, 但如果想创建复杂战利品函数, 写 JSON 格式仍然是最佳选择.

```minecraft:set_attributes``` 是没有任何便利方法的, 因为它太复杂了.

此分类下的所有方法, 除了 ```parse()``` 会创建一个参数等效于等效战利品条件的参数的原版战利品参数. 所有的原版战利品参数都将被在下方列出.

战利品条件对应的类型是 ```Functions```.

#### 方法


##### enchantRandomly(String[] enchantIDList)

等价于 : ```minecraft:enchant_randomly```.

* enchantIDList - 需要匹配的附魔的 ID.

当 ID 对应的附魔不存在时, 返回错误.

##### enchantWithLevels(int min, int max, boolean isTreasure)

等价于 : ```minecraft:enchant_with_levels```.

* min - 最低等级
* max - 最大等级
* isTreasure - 是否为宝藏附魔

##### lootingEnchantBonus(int min, int max, int limit)

等价于 : ```minecraft:looting_enchant```.

* min - 最低等级
* max - 最大等级
* limit - 额外限制量

##### setCount(int min, int max)

等价于 : ```minecraft:set_count```.

* min - 最低值
* max - 最大值

##### setDamage(float min, float max)

等价于 : ```minecraft:set_damage```.

* min - 最低值
* max - 最大值

当 ```max``` 大于 ```1.0``` 时, 返回错误.

##### setMetadata(int min, int max)

等价于 : ```minecraft:set_data```.

* min - 最低值
* max - 最大值

##### setNBT(DataMap nbtData)

等价于 : ```minecraft:set_nbt```.

* nbtData - 需要设置的 NBT.

当 nbtData 不为 ```compound``` 标签时, 返回错误.

##### smelt()

等价于 : ```minecraft:furnace_smelt```.

##### parse(DataMap json)


将一个 ```DataMap``` 转换为 LootFunction.

* json - ```DataMap``` 格式的 LootFunction.

##### zenscript(loottweaker.CustomLootCondition zenFunction)


将一个 ```zenFunction``` 转换为 ```LootFunction```.

* zenFunction - 一个附带了 ```IItemStack```, ```IRandom``` 和 ```LootContext``` 参数, 且返回 ```IItemStack``` 的 ZenScript 自定义函数.

如提供的 ZenScript 自定义函数返回 true, 返回一个 LootFunction.

### LootFunction

* 全名 : ```loottweaker.vanilla.loot.LootFunction```.

#### 方法

##### addConditions(LootCondition[] conditions)

为此 LootFunction 添加 LootCondition.

* conditions - 一个 LootCondition 实例数组.

返回被调用在在的 LootFunction.

### LootContext

* 全名 : ```loottweaker.LootContext```.

战利品生成的场景对象.

#### 方法

##### lootedEntity()

返回生成战利品的实体, ```IEntity``` 类型, 可能为空.

##### killerPlayer()

返回触发生成战利品的玩家, ```IPlayer``` 类型, 可能为空.

##### killer()

返回触发生成战利品的实体, ```IEntity``` 类型, 可能为空.

##### luck()

返回此战利品生成的幸运等级, ```float``` 类型.

##### world()

返回战利品生成在的世界, ```IWorld``` 类型, 可能为空.

##### lootingModifier()

返回此战利品生成的掠夺附魔等级. ```int``` 类型.
