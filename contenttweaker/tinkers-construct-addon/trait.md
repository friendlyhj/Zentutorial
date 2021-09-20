# 特性

在游戏中的特性就是这个类的实例啦

## 导包

```csharp
import mods.contenttweaker.tconstruct.Trait;
```

## Getters

| Getter | 返回类型 | 描述 |
| :---- | :---- | :---- |
| identifier | string | 特性名称 |
| commandString | string | 见下 |

### 关于 commandString

```csharp
var cactus as string = <ticontrait:cactus>.commandString;
// <ticontrait:trait> 是一个尖括号调用
//返回找到的特性 (返回值为 Trait 类)
print(cactus); //输出的结果为 <ticontrait:cactus>
```

## 访问特性的数据

此方法一般在 `TraitBuilder` 的函数内调用

### 访问例子

```csharp
val myTraitData as TraitDataRepresentation = myTrait.getData(itemWithTrait);
```

- myTrait as Trait 为被访问的特性
- itemWithTrait as [IItemStack](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemStack/) 为带特性的物品

关于 `TraitDataRepresentation` 类的信息请看[特性数据](traitDataRepresentation.md)
