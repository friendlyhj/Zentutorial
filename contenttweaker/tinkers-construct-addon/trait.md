# 特性

## 导入

通过 `import mods.contenttweaker.tconstruct.Trait;` 导入Trait类  
通过 `import mods.contenttweaker.tconstruct.TraitBuilder;` 导入TraitBuilder类

## 特性构建器

具有 @Optional 注解的参数为可选参数

```javascript
val myTrait as TraitBuilder = mods.contenttweaker.tconstruct.TraitBuilder.create(identifier as string, color as int, @Optional maxLevel as int, @Optional countPerLevel as int);
```

可以只设置 identifier 剩下的由 TraitBuilder类 提供的 setter 设置

## 设定参数

此为 TraitBuilder 类里的参数(在 TraitBuilder 对象上使用)
| 参数 | 设定值类型 | 参数描述 |
| :---- | :---- | :---- |
| identifier | string | 设置名称 |
| color | int | 设定颜色 |
| maxLevel | int | 最高等级(默认为1) |
| countPerLevel | int | 设置升级到下一级(前提是有, 没有就不需要写)需要多少个 countPerLevel |
| hidden | bool | 隐藏此特性 |
| localizedDescription | string | 本地化描述 |
| localizedName | sting | 本地化名称 |

此为 Trait 类里的参数(在 Trait 对象上使用)
| 参数 | 设定值类型 | 参数描述 |
| :---- | :---- | :---- |
| identifier | string | 设置名称 |
| commandString | string | 见下 |

关于 commandString : 
```javascript
var cactus as string = <ticontrait:cactus>.commandString;
print(cactus); //输出的结果为 <ticontrait:cactus>
```

## 访问特性数据

例子 : 
```javascript
val myTraitData as TraitDataRepresentation = myTrait.getData(itemWithTrait);
```  

关于 TraitDataRepresentation 类的信息请看[这](https://youyi580.gitbook.io/zentutorial/contenttweaker/tinkers-construct-addon/traitdatarepresentation)

myTrait 对象为 Trait 类, itemWithTrait 对象为 [IItemStack](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemStack/) 类(不要在不是 Trait 类的对象用此方法)

## 注册特性

最后记得调用一下 `register` 零参方法, 否则游戏内会无反应  

## 本地化

本地化为上文的 `localizedDescription` 和 `localizedName`  

## 例子

```javascript
#loader contenttweaker
#modloaded tconstruct

val testTrait = mods.contenttweaker.tconstruct.TraitBuilder.create("kindlich_test");
testTrait.color = 0xffaadd;
testTrait.maxLevel = 100;
testTrait.countPerLevel = 20;
testTrait.addItem(<item:minecraft:iron_pickaxe>); // <item:minecraft:iron_pickaxe> 为铁镐
testTrait.addItem(<item:minecraft:iron_block>, 4, 2); // <item:minecraft:iron_block> 为铁块
testTrait.localizedName = "测试特性";
testTrait.localizedDescription = "这是一个特性";
//此函数将在高级运用讲解
testTrait.afterHit = function(thisTrait, tool, attacker, target, damageDealt, wasCrit, wasHit) {
    if(!attacker.world.remote) {
        attacker.heal(damageDealt);
    }
};
testTrait.register();
```

上文函数内的代码为什么要用 world.remote ? 看[这](https://youyi580.gitbook.io/zentutorial/advanced/event-overview/tips#worldremote-bao-zheng-shi-jian-zhi-zai-fu-wu-duan-chu-li)