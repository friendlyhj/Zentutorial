# Dropt - 方法速查

## 前言

Dropt 所有的 ZenClass, 均在 ``mods.dropt`` 下, 本文将分为 ``主体 (Dropt)``, ``规则列表 (RuleList)``, ``规则 (Rule)``, ``掉落 (Drop)`` 和 ``采掘者 (Harvester)`` 五部分列出.

## 正文

### Dropt

#### 导包

```csharp
import mods.dropt.Dropt;
```

#### list()

```java
static RuleList list(string name);
```

返回一个新的, 可被配置的 RuleList 对象.

再次使用相同 ``name`` 调用此方法会返回同一对象.

#### rule()

```java
static Rule rule();
```

返回一个新的, 可被配置的 Rule 对象.

#### harvester()

```java
static Harvester harvester();
```

返回一个新的, 可被配置的 Harvester 对象.

#### drop()

```java
static Drop drop();
```

返回一个新的, 可被配置的 Drop 对象.

#### range(int fixed)

```java
static Range range(int fixed);
```

返回一个仅有一个固定值的 Range 对象.

#### range(int min, int max)

```java
static Range range(int min, int max);
```

返回一个包含最大值和最小值的 Range 对象.

#### weight(int weight)

```java
static Weight weight(int weight);
```

返回一个 Weight 对象.

#### weight(int weight, int fortuneModifier)

```java
static Weight weight(int weight, int fortuneModifier);
```

返回一个带有幸运效果修正的 Weight 对象.

### RuleList

#### 导包

```csharp
import mods.dropt.RuleList;
```

#### priority(int priority)

```java
RuleList priority(int priority);
```

为此 RuleList 设置优先级, 默认为 ``0``.

优先级值越大, 相应 RuleList 就越先被匹配.

#### add(Rule rule)

```java
RuleList add(Rule rule);
```

为此 RuleList 添加一个规则.

### Rule

#### 导包

```csharp
import mods.dropt.Rule;
```

#### debug()

```java
Rule debug();
```

为此规则启用调试日志输出.

请确保在调试结束后禁用调试, 调试模式会在 Dropt 日志中打印大量输出.

#### matchBlocks(string[] blockStrings)

```java
Rule matchBlocks(string[] blockStrings);
```

此规则将匹配的方块. (白名单)

支持 META 匹配, 多个 META 匹配和 META 通配.

如``["minecraft:dirt", "minercaft:glass:2", "tconstruct:slime_dirt:1,2", "minecraft:wool:*"]``.

注: 此方法匹配 ``blockStates``, 不能使用矿物词典.

#### matchBlocks(string type, string[] blockStrings)

```java
Rule matchBlocks(string type, string[] blockStrings);
```

此规则将匹配的方块. (白名单)

``type`` 可用的参数: ``WHITELIST``, ``BLACKLIST``.

支持 META 匹配, 多个 META 匹配和 META 通配.

如``["minecraft:dirt", "minercaft:glass:2", "tconstruct:slime_dirt:1,2", "minecraft:wool:*"]``.

注: 此方法匹配 ``blockStates``, 不能使用矿物词典.

#### matchDrops(IIngredient[] items)

```java
Rule matchDrops(IIngredient[] items);
```

此规则将匹配的掉落物. (白名单)

支持 META 匹配, 多个 META 匹配, META 通配和矿物词典.

如``[<minecraft:dirt>, <minercaft:glass:2>, <tconstruct:slime_dirt:1,2>, <minecraft:wool:*>, <ore:ingotIron>]``.

#### matchDrops(string type, IIngredient[] items)

```java
Rule matchDrops(string type, IIngredient[] items);
```

此规则将匹配的掉落物. (白名单)

``type`` 可用的参数: ``WHITELIST``, ``BLACKLIST``.

支持 META 匹配, 多个 META 匹配, META 通配和矿物词典.

如``[<minecraft:dirt>, <minercaft:glass:2>, <tconstruct:slime_dirt:1,2>, <minecraft:wool:*>, <ore:ingotIron>]``.

#### matchHarvester(Harvester harvester)

```java
Rule matchHarvester(Harvester harvester);
```

此规则将匹配的采掘者对象. (白名单)

有关采掘者对象, 详见 ```### Harvester```.

#### matchBiomes(string[] ids)

```java
Rule matchBiomes(string[] ids);
```

此规则将匹配的生物群系. (白名单)

如 ```["minecraft:birch_forest_hills", "minecraft:extreme_hills"]```.

#### matchBiomes(string type, string[] ids)

```java
Rule matchBiomes(string type, string[] ids);
```

此规则将匹配的生物群系. (白名单)

``type`` 可用的参数: ``WHITELIST``, ``BLACKLIST``.

如 ```["minecraft:birch_forest_hills", "minecraft:extreme_hills"]```.

#### matchDimensions(int[] ids)

```java
Rule matchDimensions(int[] ids);
```

此规则将匹配的维度. (白名单)

如 ```[0, 1]```.

#### matchDimensions(string type, int[] ids)

```java
Rule matchDimensions(string type, int[] ids);
```

此规则将匹配的维度. (白名单)

``type`` 可用的参数: ``WHITELIST``, ``BLACKLIST``.

如 ```[0, 1]```.

#### matchVerticalRange(int min, int max)

```java
Rule matchVerticalRange(int min, int max);
```

此规则将匹配的垂直高度距离, 默认为匹配全部高度. (白名单)

#### matchSpawnDistance(int min, int max)

```java
Rule matchSpawnDistance(int min, int max);
```

此规则将匹配的距离世界出生点的距离, 默认为匹配全部距离. (白名单)

#### matchSpawnDistance(string type, int min, int max)

```java
Rule matchSpawnDistance(string type, int min, int max);
```

此规则将匹配的距离世界出生点的距离, 默认为匹配全部距离.

``type`` 可用的参数: ``WHITELIST``, ``BLACKLIST``.

#### replaceStrategy(string strategy)

```java
Rule replaceStrategy(string strategy);
```

此规则将使用的替换掉落物策略, 默认为 ```REPLACE_ALL```, 可用的参数:

* ```REPLACE_ITEMS```: 移除所有现存的已定义物品掉落.
* ```REPLACE_ITEMS_IF_SELECTED```: 当掉落物被从当前规则中选择时, 移除所有现存的已定义物品掉落.
* ```REPLACE_ALL```: 所有现存的已定义物品掉落将被本规则中定义的物品掉落替换.
* ```REPLACE_ALL_IF_SELECTED```: 当掉落物被从当前规则中选择时, 所有现存的已定义物品掉落将被本规则中定义的物品掉落替换.
* ```ADD```: 从当前规则添加一个物品掉落, 不影响其他任何掉落. 如果规则被匹配但规则中没有任何物品被选中, 则不会掉落任何物品.

#### dropStrategy(string strategy)

```java
Rule dropStrategy(string strategy);
```

此规则将使用的掉落物政策, 默认为 ```REPEAT```, 可用的参数:

* ```REPEAT```: 当加权选择器选择掉落物时, 此规则中的所有掉落可能被多次选中.
* ```UNIQUE```: 当加权选择器选择掉落物时, 此规则中的所有掉落只可能被选中一次.

#### dropCount(Range range)

```java
Rule dropCount(Range range);
```

此规则将被加权拣选器将从中选择几次掉落物, 默认为 ```1```.

注: 此方法不会影响强制掉落.

#### addDrop(Drop drop)

```java
Rule addDrop(Drop drop);
```
为当前规则添加掉落.

#### fallthrough(boolean fallthrough)

```java
Rule fallthrough(boolean fallthrough);
```

是否在当前规则被匹配过后继续匹配规则, 默认为 ```false```.

### Harvester

#### 导包

```csharp
import mods.dropt.Harvester;
```

#### type(string type)

```java
Harvester type(string type);
```

匹配被破坏类型, 默认为 ```ANY```, 可用的参数:

* ```PLAYER```: 必须被玩家破坏. (真假皆可)
* ```NON_PLAYER```: 必须被非玩家破坏.
* ```ANY```: 任何方式皆可. 如果是被玩家破坏且定义了 ```heldItemMainHand```, ```gamestages``` 或 ```playerName```, 则以上参数会被检查匹配.
* ```EXPLOSION```: 必须被爆炸破坏.  注: 部分物品可能会被爆炸炸没.
* ```REAL_PLAYER```: 必须被真玩家采掘.
* ```FAKE_PLAYER```: 必须被假玩家采掘.

#### mainHand(string harvestLevel)

```java
Harvester mainHand(string harvestLevel);
```

匹配采掘者主手物品的挖掘等级. (白名单)

#### mainHand(IItemStack[] items)

```java
Harvester mainHand(IItemStack[] items);
```

匹配采掘者的主手物品. (白名单)

#### mainHand(string type, IItemStack[] items)

```java
Harvester mainHand(string type, IItemStack[] items);
```

匹配采掘者的主手物品.

``type`` 可用的参数: ``WHITELIST``, ``BLACKLIST``.

#### mainHand(string type, IItemStack[] items, string harvestLevel)

```java
Harvester mainHand(string type, IItemStack[] items, string harvestLevel);
```

匹配采掘者的主手物品和挖掘等级.

``type`` 可用的参数: ``WHITELIST``, ``BLACKLIST``.

#### offHand(string harvestLevel)

```java
Harvester offHand(string harvestLevel);
```

匹配采掘者副手物品的挖掘等级. (白名单)

#### offHand(IItemStack[] items)

```java
Harvester offHand(IItemStack[] items);
```

匹配采掘者的副手物品. (白名单)

#### offHand(string type, IItemStack[] items)

```java
Harvester offHand(string type, IItemStack[] items);
```

匹配采掘者的副手物品.

``type`` 可用的参数: ``WHITELIST``, ``BLACKLIST``.

#### offHand(string type, IItemStack[] items, string harvestLevel)

```java
Harvester offHand(string type, IItemStack[] items, string harvestLevel);
```

匹配采掘者的副手物品和挖掘等级.

``type`` 可用的参数: ``WHITELIST``, ``BLACKLIST``.

#### gameStages(string[] stages)

```java
Harvester gameStages(string[] stages);
```

匹配采掘者是否已解锁指定游戏阶段. (白名单)

#### gameStages(string require, string[] stages)

```java
Harvester gameStages(string require, string[] stages);
```

匹配采掘者是否已解锁指定游戏阶段. (白名单)

``require`` 可用的参数:

* ```ANY```: 采掘者需要拥有列表中的任意阶段.
* ```ALL```: 采掘者需要拥有列表中的所有阶段.

#### gameStages(string type, string require, string[] stages)

```java
Harvester gameStages(string type, string require, string[] stages);
```

匹配采掘者是否已解锁指定游戏阶段.

``type`` 可用的参数: ``WHITELIST``, ``BLACKLIST``.

``require`` 可用的参数:

* ```ANY```: 采掘者需要拥有列表中的任意阶段.
* ```ALL```: 采掘者需要拥有列表中的所有阶段.

#### playerName(string[] names)

```java
Harvester playerName(string[] names);
```

匹配采掘玩家的名称. (白名单)

#### playerName(string type, string[] names)

```java
Harvester playerName(string type, string[] names);
```

匹配采掘玩家的名称.

``type`` 可用的参数: ``WHITELIST``, ``BLACKLIST``.

### Drop

#### 导包

```csharp
import mods.dropt.Drop;
```

#### force()

```java
Drop force();
```

强制当前掉落总是掉落, 忽略选择器.

#### selector(Weight weight)

```java
Drop selector(Weight weight);
```

为当前掉落定义选择器.

#### selector(Weight weight, string silkTouch)

```java
Drop selector(Weight weight, string silkTouch);
```

为当前掉落定义选择器.

```silkTouch``` 默认值为 ```ANY```, 可用参数:

* ```REQUIRED```: 必须有精准采集.
* ```EXCLUDED```: 必须没有精准采集.
* ```ANY```: 忽略精准采集.

#### selector(Weight weight, string silkTouch, int fortuneLevelRequired)

```java
Drop selector(Weight weight, string silkTouch, int fortuneLevelRequired);
```

为当前掉落定义选择器.

```silkTouch``` 默认值为 ```ANY```, 可用参数:

* ```REQUIRED```: 必须有精准采集.
* ```EXCLUDED```: 必须没有精准采集.
* ```ANY```: 忽略精准采集.

#### items(IItemStack[] items)

```java
Drop items(IItemStack[] items);
```

为当前掉落定义掉落物.

#### items(string drop, IItemStack[] items)

```java
Drop items(string drop, IItemStack[] items);
```

为当前掉落定义掉落物.

```drop``` 默认值为 ```ONE```, 可用参数

* ```ONE```: 从输入的 ```IItemStack[]``` 中随机选取一个物品掉落.
* ```ALL```: 掉落输入的 ```IItemStack[]``` 中的所有物品.

#### items(IItemStack[] items, Range range)

```java
Drop items(IItemStack[] items, Range range);
```

为当前掉落定义掉落物.

#### items(string drop, IItemStack[] items, Range range)

```java
Drop items(string drop, IItemStack[] items, Range range);
```

为当前掉落定义掉落物.

```drop``` 默认值为 ```ONE```, 可用参数

* ```ONE```: 从输入的 ```IItemStack[]``` 中随机选取一个物品掉落.
* ```ALL```: 掉落输入的 ```IItemStack[]``` 中的所有物品.

#### matchQuantity(IItemStack[] drops)

```java
Drop matchQuantity(IItemStack[] drops);
```

为当前掉落定义掉落物数量.

#### xp(string replace, Range amount)

```java
Drop xp(string replace, Range amount);
```

为当前掉落定义经验掉落, ```replace``` 默认为 ```ADD```.

```replace``` 可用的参数:

* ```ADD```: 添加经验掉落，不影响任何现存经验掉落.
* ```REPLACE```: 替换所有现存的经验掉落.

#### replaceBlock(string block)

```java
Drop replaceBlock(string block);
```

定义一个用于替换的 ``blockstate``.

#### replaceBlock(string block, Map properties)

```java
Drop replaceBlock(string block, Map properties);
```

定义一个用于替换的 ``blockstate``.
