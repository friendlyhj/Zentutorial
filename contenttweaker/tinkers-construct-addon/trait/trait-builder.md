# 构建特性

## 导包

```csharp
import mods.contenttweaker.tconstruct.TraitBuilder;
```

## 构建器

**记得导包!**

```csharp
var myTrait as TraitBuilder = TraitBuilder.create(identifier as string);
```

## 可自定义参数

| 字段 | 值类型 | 描述 |
| :---- | :---- | :---- |
| identifier | string | 特性名称 |
| color | int | 特性显示的颜色 |
| maxLevel | int | 特性最高等级 (默认为 1) |
| hidden | bool | 是否隐藏此特性 |
| countPerLevel | int | 设置升级到下一级需要多少 countPerLevel |
| localizedDescription | string | 本地化描述 |
| localizedName | sting | 本地化名称 |

## 方法

| 方法 | 描述 |
| :---- | :---- |
| addItem(ingredient as [IIngredient](https://docs.blamejared.com/1.12/en/Vanilla/Variable_Types/IIngredient/), amountNeeded as int, amountMatched as int) | 使 `ingredient` 可以在工具装配台为匠魂工具添加此特性, `amountNeeded` 为需求数量, `amountMatched` 为匹配数量, 后两个参数选填, 默认为 1 |
| removeItem(itemStack as [IItemStack](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemStack/)) | 使 itemStack 不能制作此特性 |

## 注册特性

最后记得调用一下 `register` 零参方法, 否则游戏内会无反应

## 本地化

本地化为上文的 `localizedDescription` 和 `localizedName`

## 实例

```csharp
#loader contenttweaker //别忘加这行否则无法添加特性
import mods.contenttweaker.tconstruct.TraitBuilder; // 导入 TraitBuilder 包

var testTrait = TraitBuilder.create("kindlich_test");
testTrait.color = 0xffaadd;
testTrait.maxLevel = 100;
testTrait.countPerLevel = 20;
testTrait.addItem(<item:minecraft:iron_pickaxe>); // <item:minecraft:iron_pickaxe> 为铁镐
testTrait.addItem(<item:minecraft:iron_block>, 4, 2); // <item:minecraft:iron_block> 为铁块
testTrait.localizedName = "实例特性";
testTrait.localizedDescription = "独创的特性!";
//此函数将在高级运用讲解
testTrait.afterHit = function(thisTrait, tool, attacker, target, damageDealt, wasCrit, wasHit) {
    if(!attacker.world.remote) {
        attacker.heal(damageDealt);
    }
};
testTrait.register();
```

上文函数内的代码为什么要用 `world.remote` ? 看 [**!world.remote保证事件只在服务端处理**](../../advanced/event-overview/tips#worldremote-bao-zheng-shi-jian-zhi-zai-fu-wu-duan-chu-li)