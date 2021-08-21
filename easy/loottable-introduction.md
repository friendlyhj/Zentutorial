# LootTable : 导论

LootTable(战利品表) 是原版概念, 用于决定各个情况下生成什么物品, 比如自然生成的容器的内容物, 破坏方块时的掉落物, 杀死实体时的掉落物, 钓鱼时可以钓上的物品等. 它不会影响经验的掉落和不掉落物品的实体, 比如大型史莱姆产生的史莱姆和被虫蚀的方块中的蠹虫.

## 简介
对于箱子, 陷阱箱, 漏斗, 运输矿车, 漏斗矿车, 发射器, 投掷器, 潜影盒, 木桶而言, 包含一个 LootTable 本体和一个 LootTableSeed.

对生物而言, 其根标签下包含一个 DeathLootTable 和一个 DeathLootTableSeed.

一个 LootTable(战利品表) 中可能有多个 pool(随机池), 但一般只有一个, 且名称为 main. 一个 pool(随机池) 中可能有多个 entry(被抽出项). 这三个概念是从属关系, 移除一个 LootTable 自然会移除属于其的所有 pool, 移除一个 pool 自然会移除属于其的所有 entry.

一个 pool 将视其 rolls(被抽取数) 和 bonus_rolls(额外被抽取数, 被幸运效果影响) 数值被抽取多次, 一个 entry 将视其 weight(权重) 数值为权重被抽取.

每个 LootTable, pool, entry 都可以拥有多个 function(函数), 每个 function 可拥有多个 condition(函数被应用条件).

# 引用
部分内容, 说明来自 [Minecraft Wiki](https://minecraft.fandom.com/zh/wiki/%E6%88%98%E5%88%A9%E5%93%81%E8%A1%A8), 原文在[CC BY-NC-SA 3.0](https://www.fandom.com/zh/licensing-zh)许可协议下提供. 
