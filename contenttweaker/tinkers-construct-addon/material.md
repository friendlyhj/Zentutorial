# 材料  

## 导包

```csharp
import mods.contenttweaker.tconstruct.Material;
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

## 方法

| 方法 | 描述 |
| :---- | :---- |
| addItem(ingredient as [IIngredient](https://docs.blamejared.com/1.12/en/Vanilla/Variable_Types/IIngredient/), amountNeeded as int, amountMatched as int) | 使 `ingredient` 可以在工具装配台为匠魂工具添加此特性, `amountNeeded` 为需求数量, `amountMatched` 为匹配数量, 后两个参数选填, 默认为 1 |
| addTrait(trait as string, @Optional String dependencies) | 第一个参数为特性名 (identifier), 第二个参数为部件名 (可不填) |
| addTrait(trait as [Trait](trait.md), @Optional String dependencies) | 第一个参数为特性, 第二个参数为部件名 (可不填) |
