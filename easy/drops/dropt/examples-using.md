# Dropt - 使用示例

## 前言
此页面列出大量 Dropt 使用实例以供参考.

导包:
```csharp
import mods.dropt.Dropt;
```

想要使用 Dropt 添加一个掉落规则, 首先要创建一个 ``RuleList``, 接着向 ``RuleList`` 中添加 ``Rule``, 再为 ``Rule`` 定义 ``Match`` 条件和 ``Drop`` 掉落.

Dropt 会检测并应用所有被创建的 ``RuleList``, 空的也是.

不会被复用的规则和条件一般会直接在 ``RuleList`` 部分的本体中被现学现卖, 可能会造成混淆, 如:
```csharp
import mods.dropt.Dropt;

Dropt.list("list_name")

  .add(Dropt.rule()
      .matchBlocks(["minecraft:stone"])
      .addDrop(Dropt.drop()
          .items([<minecraft:string>])
      )
  );
```
实际上等价于:
```csharp
import mods.dropt.Dropt;
import mods.dropt.Rule;
import mods.dropt.Drop;
import mods.dropt.RuleList;

val gblList = Dropt.list("list_name") as RuleList;

val gblRule = Dropt.rule() as Rule;
gblRule.matchBlocks(["minecraft:stone"]);

val gblDrop = Dropt.drop() as Drop;
gblDrop.items([<minecraft:string>]);

gblRule.addDrop(gblDrop);
gblList.add(gblRule);
```

简而言之, Dropt 有着很强的模块性, 这点在需要复用等进阶用途时十分重要.


## 正文

请注意在阅读示例时, 不要因为因添加注释增加的空行忽视链式调用.

### 基础替换
将 ```"minecraft:stone"``` 的所有掉落替换为 ```1``` 个 ```<minecraft:string>```.

```csharp
import mods.dropt.Dropt;

// 创建一个名称为 "basic_replacement" 的 RuleList 对象
Dropt.list("basic_replacement")

  // 为父 RuleList 对象添加规则
  .add(
      
      // 创建一个 Rule 对象
      Dropt.rule()
      
      // 为父 Rule 对象添加匹配破坏  "minecraft:stone" 的条件
      .matchBlocks(["minecraft:stone"])

      // 为父 Rule 对象添加掉落
      .addDrop(
          
          // 创建一个 Drop 对象
          Dropt.drop()

          // 为父 Drop 对象添加掉落物 <minecraft:string>
          .items([<minecraft:string>])
      )
  );
```


### 选择性替换
阻止 ```<minecraft:cobblestone>``` 在 ```<minecraft:stone>``` 或 ```<minecraft:cobblestone>``` 被破坏时掉落.

此脚本要求 Dropt 匹配 ```"minecraft:stone"``` 或 ```"minecraft:cobblestone"``` 被破坏时掉落 ```<minecraft:cobblestone>```. 替换策略会替换所有匹配上述条件的掉落为一个新的, 空的 ```Drop 对象```. 由于目标规则中仅有一个空掉落池, 此空池总是会被选中.

```csharp
import mods.dropt.Dropt;

// 创建一个名称为 "selective_removal" 的 RuleList 对象
Dropt.list("selective_removal")

  // 为父 RuleList 对象添加规则
  .add(

      // 创建一个 Rule 对象
      Dropt.rule()

      // 为父 Rule 对象添加匹配破坏 "minecraft:stone" 或 "minecraft:cobblestone" 的条件
      .matchBlocks(["minecraft:stone", "minecraft:cobblestone"])

      // 为父 Rule 对象添加匹配掉落 <minecraft:cobblestone> 的条件
      .matchDrops([<minecraft:cobblestone>])

      // 将父 Rule 对象的替换策略从默认的 "REPLACE_ALL" 切换为 "REPLACE_ITEMS"
      .replaceStrategy("REPLACE_ITEMS")

      // 为父 Rule 对象添加掉落
      .addDrop(
          
          // 创建一个 Drop 对象
          Dropt.drop()
      )
  );
```


### 打草掉落
在破坏高草丛时, 有 15% 的概率掉落 ```<minecraft:string>```.

注意 Dropt 不提供直接的设置概率概率方法, 于是此处同时添加了一个权重为 ```85``` 的空掉落, 此掉落仍会被选择, 但什么也不掉落, 即可实现概率掉落.

```csharp
import mods.dropt.Dropt;

// 创建一个名称为 "grass_drop" 的 RuleList 对象
Dropt.list("grass_drop")

  // 为父 RuleList 对象添加规则
  .add(
      
      // 创建一个 Rule 对象
      Dropt.rule()

      // 为父 Rule 对象添加匹配破坏 "minecraft:tallgrass:*" 的条件 (使用 META 通配符匹配所有高草丛)
      .matchBlocks(["minecraft:tallgrass:*"])

      // 将父 Rule 对象的替换策略从默认的 "REPLACE_ALL" 切换为 "ADD"
      .replaceStrategy("ADD")

      // 为父 Rule 对象添加掉落
      .addDrop(
          
          // 创建一个 Drop 对象
          Dropt.drop()

          // 为父 Rule 对象定义一个选择器
          .selector(
              
              // 设置父选择器的权重为 85
              Dropt.weight(85)
          )
      )

      // 为父 Rule 对象添加掉落
      .addDrop(
          
          // 创建一个 Drop 对象
          Dropt.drop()

          // 为父 Rule 对象定义一个选择器
          .selector(

              // 设置父选择器的权重为 15
              Dropt.weight(15)
          )

          // 为父 Drop 对象添加掉落物 <minecraft:string>
          .items([<minecraft:string>])
      )
  );
```


### 树叶掉落
在破坏树叶时, 掉落 ```<minecraft:stick>```.

树叶方块在是否检测消散时有不同的 ```blockstate```, 使得其很难通过 META 检测其是否应被匹配

此时, 使用 Dropt 提供的 ```/dropt verbose``` 指令即可打开/关闭 verbose 模式, 此模式下会将所有被破坏的方块的信息打印到日志中, 便于提取准确的所需信息.

```csharp
import mods.dropt.Dropt;

// 创建一个名称为 "leaf_drops" 的 RuleList 对象
Dropt.list("leaf_drops")

  // 为父 RuleList 对象添加规则
  .add(
      
      // 创建一个 Rule 对象
      Dropt.rule()

      // 为父 Rule 对象添加匹配破坏 "minecraft:leaves:*" 的条件 (使用 META 通配符匹配所有种类的树叶)
      .matchBlocks(["minecraft:leaves:*"])

      // 为父 Rule 对象添加掉落
      .addDrop(
          
          // 创建一个 Drop 对象
          Dropt.drop()

          // 为父 Drop 对象添加掉落物 <minecraft:stick>
          .items([<minecraft:stick>])
      )
  );
```


### 工具限制
当玩家挖掘泥土时没有使用铲子, 则什么都不会掉落.

此处的
```csharp
.mainHand("BLACKLIST", [], "shovel;0;-1")
```
起了主要作用. 即将所有没有 ```shovel``` 工具类型的, 且挖掘等级小于 ```0``` 的主手物品列入黑名单. 最后设置当此规则被匹配时, 将泥土的掉落替换为一个空的 Drop 对象 (默认替换策略即是 ```"REPLACE_ALL"```).

```csharp
import mods.dropt.Dropt;

// 创建一个名称为 "tool_restriction" 的 RuleList 对象
Dropt.list("tool_restriction")

  // 为父 RuleList 对象添加规则
  .add(
      
     // 创建一个 Rule 对象
      Dropt.rule()

      // 为父 Rule 对象添加匹配破坏 "minecraft:dirt:*" 的条件 (使用 META 通配符匹配所有种类的泥土)
      .matchBlocks(["minecraft:dirt:*"])

      // 为父 Rule 对象添加一个采掘者匹配条件
      .matchHarvester(
          
          // 创建一个 Harvester 对象
          Dropt.harvester()

          // 将父 Harvester 对象的匹配类型设置为 "PLAYER" (真假玩家)
          .type("PLAYER")

          // 将所有没有 shovel 工具类型的, 且挖掘等级小于0 的主手物品列入父 Harvester 对象的匹配黑名单
          .mainHand("BLACKLIST", [], "shovel;0;-1")
      )

      // 为父 Rule 对象添加掉落
      .addDrop(
          
          // 创建一个 Drop 对象
          Dropt.drop()
      )
  );
```

### 进阶幸运修正
幸运等级越高, 挖掘 ```"minecraft:quartz_ore"``` 得到的 ```<minecraft:quartz>``` 数量越多.

通过权重设置, 将就算拥有幸运三效果仍会匹配到最低数量 (1~2 个) 的理论可能性减小到了 ```1/1111```.

重点在于使用 ```selector``` 方法的 ```fortuneLevelRequired``` 参数匹配幸运等级. 示例脚本因为直观展示需求, 并非是实现此目的的最优解.

```csharp
import mods.dropt.Dropt;

// 创建一个名称为 "advanced_fortune" 的 RuleList 对象
Dropt.list("advanced_fortune")

  // 为父 RuleList 对象添加规则
  .add(
      
      // 创建一个 Rule 对象
      Dropt.rule()

      // 为父 Rule 对象添加匹配破坏 "minecraft:quartz_ore" 的条件
      .matchBlocks(["minecraft:quartz_ore"])

      // 为父 Rule 对象添加掉落
      .addDrop(
          
          // 创建一个 Drop 对象
          Dropt.drop()

          // 为父 Drop 对象添加掉落物 1~2 个 <minecraft:quartz>
          .items([<minecraft:quartz>], Dropt.range(1, 2))
      )

      // 为父 Rule 对象添加掉落
      .addDrop(
          
          // 创建一个 Drop 对象
          Dropt.drop()

          // 为父 Rule 对象定义一个选择器
          .selector(

              // 设置父选择器的权重为 15, 无视精准采集效果, 需求最低 1 级的幸运效果
              Dropt.weight(10), "ANY", 1
          )

          // 为父 Drop 对象添加掉落物 4~8 个 <minecraft:quartz>
          .items([<minecraft:quartz>], Dropt.range(4, 8))
      )

      // 为父 Rule 对象添加掉落
      .addDrop(
          
          // 创建一个 Drop 对象
          Dropt.drop()

          // 为父 Rule 对象定义一个选择器
          .selector(

              // 设置父选择器的权重为 100, 无视精准采集效果, 需求最低 2 级的幸运效果
              Dropt.weight(100), "ANY", 2
          )

          // 为父 Drop 对象添加掉落物 16~32 个 <minecraft:quartz>
          .items([<minecraft:quartz>], Dropt.range(16, 32))
      )

      // 为父 Rule 对象添加掉落
      .addDrop(
          
          // 创建一个 Drop 对象
          Dropt.drop()

          // 为父 Rule 对象定义一个选择器
          .selector(

              // 设置父选择器的权重为 1000, 无视精准采集效果, 需求最低 3 级的幸运效果
              Dropt.weight(1000), "ANY", 3
          )

          // 为父 Drop 对象添加掉落物 32~64 个 <minecraft:quartz>
          .items([<minecraft:quartz>], Dropt.range(32, 64))
      )
  );
```


### 精准采集
当使用精准采集效果破坏 ```<minecraft:stone>```, 掉落 ```1``` 个 ```<minecraft:string>```.

此处使用了 ```REPLACE_ALL_IF_SELECTED``` 替换策略, 即仅在掉落池中物品被选中时, 才替换方块掉落物. 又因为添加的唯一一个掉落池定义了需要精准采集的选择器, 所以只有在方块被使用精准采集效果破坏时才会替换方块掉落物.

```csharp
import mods.dropt.Dropt;

// 创建一个名称为 "silk_touch" 的 RuleList 对象
Dropt.list("silk_touch")

  // 为父 RuleList 对象添加规则
  .add(
      
      // 创建一个 Rule 对象
      Dropt.rule()

      // 为父 Rule 对象添加匹配破坏 "minecraft:stone" 的条件
      .matchBlocks(["minecraft:stone"])

      // 将父 Rule 对象的替换策略从默认的 "REPLACE_ALL" 切换为 "REPLACE_ALL_IF_SELECTED"
      .replaceStrategy("REPLACE_ALL_IF_SELECTED")

      // 为父 Rule 对象添加掉落
      .addDrop(
          
          // 创建一个 Drop 对象
          Dropt.drop()

          // 为父 Rule 对象定义一个选择器
          .selector(
              
              // 设置父选择器的权重为 1, 需要精准采集效果
              Dropt.weight(1), "REQUIRED"
          )

          // 为父 Drop 对象添加掉落物 <minecraft:string>
          .items([<minecraft:string>])
      )
  );
```


### 等数替换
掉落多少个 ```<minecraft:redstone>```, 就将掉落替换为多少个 ```<minecraft:dirt>```.

```csharp
import mods.dropt.Dropt;

// 创建一个名称为 "match_quantity" 的 RuleList 对象
Dropt.list("match_quantity")

  // 为父 RuleList 对象添加规则
  .add(
      
      // 创建一个 Rule 对象
      Dropt.rule()

      // 为父 Rule 对象添加匹配掉落 <minecraft:redstone> 的条件
      .matchDrops([<minecraft:redstone>])

      // 为父 Rule 对象添加掉落
      .addDrop(
          
          // 创建一个 Drop 对象
          Dropt.drop()

          // 为父 Drop 对象添加掉落物 <minecraft:dirt>
          .items([<minecraft:dirt>])

          // 为父 Drop 对象添加匹配掉落的 <minecraft:redstone> 的数量的条件
          .matchQuantity([<minecraft:redstone>])
      )
  );
```


### 出生距离匹配
当采掘地点在距世界出生点 ```32``` 格内, 将所有 ```"minecraft:cobblestone"``` 的掉落物替换为 ```<minecraft:dirt>```.

```csharp
import mods.dropt.Dropt;

// 创建一个名称为 "distance" 的 RuleList 对象
Dropt.list("distance")

  // 为父 RuleList 对象添加规则
  .add(
      
      // 创建一个 Rule 对象
      Dropt.rule()

      // 为父 Rule 对象添加匹配破坏 "minecraft:cobblestone" 的条件
      .matchBlocks(["minecraft:cobblestone"])

      // 为父 Rule 对象添加匹配距离世界出生点距离为 0~32 格的条件
      .matchSpawnDistance("WHITELIST", 0, 32)

      // 为父 Rule 对象添加掉落
      .addDrop(
          
          // 创建一个 Drop 对象
          Dropt.drop()

          // 为父 Drop 对象添加掉落物 <minecraft:dirt>
          .items([<minecraft:dirt>])
      )
  );
```


### NBT 匹配
匹配手持物品是否包含指定 NBT.

是的, Dropt 支持匹配手持物品的 NBT, 也支持掉落带有 NBT 的物品.

如果玩家将物品重命名, 附魔等, NBT 可能会不再匹配.

另外使用 ```/dropt hand``` 指令打印如下所示的信息 (留意 ```RepairCost:0```).

```JSON
"minecraft:diamond_pickaxe:*#{RepairCost:0,display:{Name:\"Pick Astley\"}}"
```

但在 CrT 加持下, 使用 ```/ct hand``` 打印的 ```withTag``` 结果即可.

```csharp
import mods.dropt.Dropt;

// 创建一个名称为 "nbt" 的 RuleList 对象
Dropt.list("nbt")

  // 为父 RuleList 对象添加规则
  .add(
      
      // 创建一个 Rule 对象
      Dropt.rule()

      // 为父 Rule 对象添加匹配破坏 "minecraft:stone" 的条件
      .matchBlocks(["minecraft:stone"])

      // 为父 Rule 对象添加一个采掘者匹配条件
      .matchHarvester(
          
          // 创建一个 Harvester 对象
          Dropt.harvester()

          // 将父 Harvester 对象的匹配类型设置为 "PLAYER" (真假玩家)
          .type("PLAYER")

          // 匹配玩家主手手持带有 {RepairCost: 0, display: {Name: "Pick Astley"}} 标签的, 任意耐久的 <minecraft:diamond_pickaxe>
          .mainHand([
              <minecraft:diamond_pickaxe:*>.withTag({RepairCost: 0, display: {Name: "Pick Astley"}})
          ])
      )

      // 为父 Rule 对象添加掉落
      .addDrop(
          
          // 创建一个 Drop 对象
          Dropt.drop()

          // 掉落如下物品
          .items([
              <minecraft:cobblestone>.withTag({display: {Name: "Never"}}),
              <minecraft:cobblestone>.withTag({display: {Name: "Gonna"}}),
              <minecraft:cobblestone>.withTag({display: {Name: "Give"}}),
              <minecraft:cobblestone>.withTag({display: {Name: "You"}}),
              <minecraft:cobblestone>.withTag({display: {Name: "Stone"}})
          ])
      )
  );
```


### 游戏阶段匹配
当 ```"minecraft:stone"``` 被一个同时拥有 ```"stage_A"``` 和 ```"stage_B"``` 阶段的玩家破坏时, 将所有掉落替换为 ```<minecraft:string> * 1```.

```csharp
import mods.dropt.Dropt;

// 创建一个名称为 "gamestages" 的 RuleList 对象
Dropt.list("gamestages")

  // 为父 RuleList 对象添加规则
  .add(
      
      // 创建一个 Rule 对象
      Dropt.rule()

      // 为父 Rule 对象添加匹配破坏 "minecraft:stone" 的条件
      .matchBlocks(["minecraft:stone"])


      // 为父 Rule 对象添加一个采掘者匹配条件
      .matchHarvester(
          
          // 创建一个 Harvester 对象
          Dropt.harvester()

         
        // 为父 Harvester 对象添加白名单匹配拥有 "stage_A" 和 "stage_B" 两个阶段
        .gameStages("WHITELIST", "ALL", ["stage_A", "stage_B"])
      )


      // 为父 Rule 对象添加掉落
      .addDrop(
          
          // 创建一个 Drop 对象
          Dropt.drop()

          // 为父 Drop 对象添加掉落物 <minecraft:string>
          .items([<minecraft:string>])
      )
  );
```


### 强制掉落
当破坏 ```"minecraft:stone"``` 时, 永远掉落 ```<minecraft:string> * 1```, 且有 ```25%``` 的概率掉落一个 ```<minecraft:diamond>```.

```csharp
import mods.dropt.Dropt;

// 创建一个名称为 "forced_drops" 的 RuleList 对象
Dropt.list("forced_drops")

  // 为父 RuleList 对象添加规则
  .add(
      
      // 创建一个 Rule 对象
      Dropt.rule()

      // 为父 Rule 对象添加匹配破坏 "minecraft:stone" 的条件
      .matchBlocks(["minecraft:stone"])

      // 为父 Rule 对象添加掉落
      .addDrop(
          
          // 创建一个 Drop 对象
          Dropt.drop()

          // 将父 Drop 对象设置为强制掉落模式
          .force()

          // 为父 Drop 对象添加掉落物 <minecraft:string>
          .items([<minecraft:string>])
      )

      // 为父 Rule 对象添加掉落
      .addDrop(
          
          // 创建一个 Drop 对象
          Dropt.drop()

          // 为父 Rule 对象定义一个选择器
          .selector(
              
              // 设置父选择器的权重为 75
              Dropt.weight(75))
      )

      // 为父 Rule 对象添加掉落
      .addDrop(
          
          // 创建一个 Drop 对象
          Dropt.drop()

          // 为父 Rule 对象定义一个选择器
          .selector(
              
              // 设置父选择器的权重为 25
              Dropt.weight(25))

          // 为父 Drop 对象添加掉落物 <minecraft:diamond>
          .items([<minecraft:diamond>])
      )
  );
```

### 全部掉落替换
当破坏 ```"minecraft:stone"``` 时, 将所有掉落替换为 ```<minecraft:string> * 100``` 与 ```<minecraft:diamond> * 10```.

要达成此目的实际上有两种解法. 两个物品都可以被单独定义在两个 ```RuleList``` 对象中并单独定义 ```dropCount``` 为 ```2```, ```dropStrategy``` 为 ```UNIQUE```. 而另一种方法, 也是此处使用的方法则是将两个掉落定义在同一 ```RuleList``` 对象中, 并使用 ```ALL``` 掉落规则表策略, 且在此情况下就算掉落了多个物品, 多个掉落物也会被视为一次掉落.

```csharp
import mods.dropt.Dropt;

// 创建一个名称为 "drop_all" 的 RuleList 对象
Dropt.list("drop_all")

  // 为父 RuleList 对象添加规则
  .add(
      
      // 创建一个 Rule 对象
      Dropt.rule()

      // 为父 Rule 对象添加匹配破坏 "minecraft:stone" 的条件
      .matchBlocks(["minecraft:stone"])

      // 为父 Rule 对象添加掉落
      .addDrop(
          
          // 创建一个 Drop 对象
          Dropt.drop()

          // 为父 Drop 对象添加 <minecraft:string> * 100 和 <minecraft:diamond> * 10 的两个掉落物
          .items("ALL", [<minecraft:string> * 100, <minecraft:diamond> * 10])
      )
  );
```

### BlockState 替换
当破坏 ```"minecraft:stone"``` 时, 将所有内容为 ```<minecraft:cobblestone> * 1``` 的掉落替换为将原方块随机替换为一块朝向各不同的橡木, 云杉或白桦原木(```"oak"```, ```"spruce"``` 或 ```"birch"```)

```csharp
import mods.dropt.Dropt;

// 创建一个名称为 "blockstate_replacement" 的 RuleList 对象
Dropt.list("blockstate_replacement")

  // 为父 RuleList 对象添加规则
  .add(
      
      // 创建一个 Rule 对象
      Dropt.rule()

      // 为父 Rule 对象添加匹配破坏 "minecraft:stone" 的条件
      .matchBlocks(["minecraft:stone"])

      // 为父 Rule 对象添加掉落
      .addDrop(
          
          // 创建一个 Drop 对象
          Dropt.drop()

          // 为父 Rule 对象定义一个选择器
          .selector(
              
              // 设置父选择器的权重为 2
              Dropt.weight(2)
          )

          // 为父 Drop 对象添加掉落物 <minecraft:cobblestone>
          .items([<minecraft:cobblestone>])

          // 为父 Drop 对象添加方块替换 "minecraft:log", Propreties 为 {axis: "y", variant: "oak"}
          .replaceBlock("minecraft:log", {axis: "y", variant: "oak"})
      )

      // 为父 Rule 对象添加掉落
      .addDrop(
          
          // 创建一个 Drop 对象
          Dropt.drop()

          // 为父 Drop 对象添加掉落物 <minecraft:cobblestone>
          .items([<minecraft:cobblestone>])

          // 为父 Drop 对象添加方块替换 "minecraft:log", Propreties 为 {axis: "x", variant: "spruce"}
          .replaceBlock("minecraft:log", {axis: "x", variant: "spruce"})
      )

      // 为父 Rule 对象添加掉落
      .addDrop(
          
          // 创建一个 Drop 对象
          Dropt.drop()

          // 为父 Drop 对象添加掉落物 <minecraft:cobblestone>
          .items([<minecraft:cobblestone>])

          // 为父 Drop 对象添加方块替换 "minecraft:log", Propreties 为 {axis: "z", variant: "birch"}
          .replaceBlock("minecraft:log", {axis: "z", variant: "birch"})
      )
  );
```

### 落空匹配
当一个 ```Rule``` 对象启用了 ```fallthrough``` 时, Dropt 将试图为对应方块匹配另一个 ```Rule``` 对象. 即继续为该方块匹配父 ```RuleList``` 中其余的规则，直到匹配到一个没有启用 ```fallthrough``` 的 ```Rule``` 对象或父 ```RuleList``` 中没有更多匹配对应方块的 ```Rule``` 对象.

```csharp
import mods.dropt.Dropt;


Dropt.list("fallthrough_test")


  // 为父 RuleList 对象添加规则
  .add(
      
      // 创建一个 Rule 对象
      Dropt.rule()

      // 将父 Drop 对象设置为落空匹配模式
      .fallthrough()

      // 为父 Rule 对象添加匹配破坏 "minecraft:dirt" 的条件
      .matchBlocks(["minecraft:dirt"])

      // 为父 Rule 对象添加掉落
      .addDrop(
          
          // 创建一个 Drop 对象
          Dropt.drop()

          // 为父 Drop 对象添加掉落物 <minecraft:diamond>
          .items([<minecraft:diamond>])
      )
  )

  // 为父 RuleList 对象添加规则
  .add(
      
      // 创建一个 Rule 对象
      Dropt.rule()

      // 为父 Rule 对象添加匹配破坏 "minecraft:dirt" 的条件
      .matchBlocks(["minecraft:dirt"])

      // 将父 Rule 对象的替换策略从默认的 "REPLACE_ALL" 切换为 "ADD"
      .replaceStrategy("ADD")

      // 为父 Rule 对象添加掉落
      .addDrop(
          
          // 创建一个 Drop 对象
          Dropt.drop()

          // 为父 Drop 对象添加掉落物 <minecraft:emerald>
          .items([<minecraft:emerald>])
      )
  );
```
