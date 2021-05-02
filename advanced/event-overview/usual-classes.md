# 常用类



你需要监听一些事件，获得一些信息，若满足什么条件，执行一些操作。有一些类，是你经常用到的。

我不列出各种类的信息，wiki上都有。链接指向英文wiki。

* [IPlayer](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Players/IPlayer/) ：指定玩家，包含玩家的各种信息。IPlayer继承 [IEntityLivingBase](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Entities/IEntityLivingBase/#ientitylivingbase) 类
* [IEntityLivingBase](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Entities/IEntityLivingBase/#ientitylivingbase)：指定一个Mob 继承 [IEntity](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Entities/IEntity/) 类
* [IEntity](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Entities/IEntity/) ：指定一个实体
* [IWorld](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/World/IWorld/#iworld)：包含世界中的一个维度的信息，包含天气效果、方块信息、服务端客户端等信息。可以用来在世界中召唤一个实体
* [IBlockPos](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/World/IBlockPos/) ：指定世界中一个坐标，常用这个获取或更改一个IWorld的指定坐标的IBlockState
* [ICommandSender](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Commands/ICommandSender/) ：指令发送者，如果想用zs发送指令需要用这个，但也要注意权限，推荐用`mods.ctutils.commands.Commands.getServerCommandSender()`获取服务端对应的CommandSender
* [IBlock](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Blocks/IBlock/) ：方块

