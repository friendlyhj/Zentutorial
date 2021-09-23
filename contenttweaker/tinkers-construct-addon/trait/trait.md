# 特性 (Trait)

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
var ecological as string = <ticontrait:ecological>.commandString;
print(ecological); //输出的结果为 <ticontrait:cactus>
```

## 尖括号调用

可以访问游戏中匠魂或者 CoT 自定义的特性

如果找到特性则返回 [Trait](trait.md) 对象, 否则返回 null

### 访问方法

```cscsharp
<ticontrait:特性名>
```

## 访问特性的数据

此方法一般在 `TraitBuilder` 的函数内调用

### 访问例子

```csharp
var myTraitData as TraitDataRepresentation = myTrait.getData(itemWithTrait);
```

- myTrait as Trait 为被访问的特性
- itemWithTrait as [IItemStack](https://docs.blamejared.com/1.12/en/Vanilla/Items/IItemStack/) 为带特性的物品

关于 `TraitDataRepresentation` 类的信息请看[特性数据](traitDataRepresentation.md)
