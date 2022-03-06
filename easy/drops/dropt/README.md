# Dropt - 导言

## 前言
[Dropt](https://www.mcmod.cn/class/2195.html) 是一个强大, 灵活的方块掉落物替换系统, 可以在不使用[事件系统](/advanced/event-overview/README.md)的前提下简单的添加多条件的方块掉落物替换. 其在通过使用规则缓存 Blockstate 以显著提升性能的同时, 提供了大量条件匹配和判断, 同时链式调用的格式也提升了代码可读性, 对尤其是对事件系统不甚理解的新手非常友好. Dropt 本身提供 JSON, ZenScript 以及 Java DroptAPI 支持, 但本文将侧重 ZenScript 兼容. 

## Dropt 特性一览
Dropt 可以匹配:
* 方块 (META 值, META 通配, 多个 META 数值) (黑/白名单)
* 掉落物品 (META 值, META 通配, 多个 META 数值, 矿物词典) (黑/白名单)
* 采掘者 (玩家, 非玩家, 任意)
* 采掘者手持物品 (META 值, META 通配) (黑/白名单)
* 采掘者拥有的阶段 (需安装 GameStages 模组)
* 采掘者玩家名
* 生物群系 (黑/白名单)
* 维度 (黑/白名单)
* 垂直范围

Dropt 提供的可供使用的替换策略:
* 向现存掉落中添加
* 替换所有掉落
* 当掉落被选中时替换所有掉落
* 替换所有被匹配的掉落
* 当掉落被选中时替换所有被匹配的掉落

Dropt 提供的可供使用的掉落策略:
* 重复 (可多次选中同一掉落)
* 独特 (仅能选中一个掉落一次)

Dropt 提供的掉落物选择计数/掉落量策略:
* 固定值
* 指定范围内的随机值
* 幸运效果修正

Dropt 提供的其余掉落物选择策略:
* 幸运效果影响权重
* 所需最低幸运级别
* 精准采集效果需求 (需要, 不需要, 任意)

Dropt 提供的掉落策略:
* 可为每次掉落定义掉落表
* 可在掉落表中添加 META 通配
* 可在掉落表中添加矿词对象
* 可为掉落添加经验掉落 (兼容幸运效果修正和范围限制)
* 可在掉落表中添加包含 NBT 的对象


## 本章目录
本章节内容一览:

* [Dropt - 导言](/easy/drops/dropt/README.md)
  * [Dropt - 方法速查](/easy/drops/dropt/methods-overview.md)
  * [Dropt - 使用示例](/easy/drops/dropt/examples-using.md)


## 版权信息 Copyright Information

本 GitBook 相关内容中所有完全翻译自或引用 [Dropt 官方文档](https://dropt.readthedocs.io/en/latest/https://dropt.readthedocs.io/en/latest/) 的内容, 均以 [Dropt Contributor License Agreement Version 1.0.0](https://dropt.readthedocs.io/en/latest/cla/) 授权.


All related content fully translated or referenced from the [Dropt Official Document](https://dropt.readthedocs.io/en/latest/https://dropt.readthedocs.io/en/latest/) in this GitBook is licensed under the [Dropt Contributor License Agreement Version 1.0.0](https://dropt.readthedocs.io/en/latest/cla/).
