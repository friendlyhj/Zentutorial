# 概述

本节将会详细地说明CrT的所有类，以及可以访问的ZenSetter、ZenGetter、ZenMethod。

本节内容为我翻源码而得，有些内容wiki并没有

其实也可以打指令/ct dumpzs &lt;输出方式&gt;\(可选log html json\)来查看

基本getter啥的没有描述，因为基本上名称就说明用处了。还是推荐与wiki配合使用。

A类拓展了B类，说明A类可以使用B类的所有getter setter和方法。需要B类作为参数的函数/方法，也可使用A类。如果是反过来，建议用`instanceof`关键字判断后进行类型转换。

```csharp
//导入类部分省略
events.onEntityLivingDeath(function(event as EntityLivingDeathEvent) {
    if (event.entityLivingBase instanceof IPlayer) { //event.entityLivingBase返回IEntityLivingBase类，IPlayer是它的拓展类
        val player as IPlayer = event.entityLivingBase;
        print("玩家" ~ player.name ~ "死了！");
    }
});
```

静态方法说明该方法针对包，而不是一个具体的对象、实例。

```csharp
import crafttweaker.block.IBlockState;

IBlockState.getBlockState("minecraft:wool", ["color=red"]); //getBlockState静态方法
```

方法用

`返回值类型 函数名(输入参数1类型 输入参数1名称, 输入参数2类型 输入参数2名称, @Optional 可选参数3类型 可选参数3名称, ...);`

来表示

静态方法会在返回值类型前有个 `static` 标识
