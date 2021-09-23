# 材料 (Material)

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
var wood as string = <ticonmaterial:wood>.commandString;
print(wood); //输出的结果为 <ticonmaterial:wood>
```

## 尖括号调用

可以访问游戏中匠魂或者 CoT 自定义的材料

如果找到特性则返回 [Material](material.md) 对象, 否则返回 null

### 访问方法

```cscsharp
<ticonmaterial:材料名>
```

## 方法

| 方法 | 描述 |
| :---- | :---- |
| addItem(ingredient as [IIngredient](https://docs.blamejared.com/1.12/en/Vanilla/Variable_Types/IIngredient/), amountNeeded as int, amountMatched as int) | 使 `ingredient` 可以在工具装配台为匠魂工具添加此特性, `amountNeeded` 为需求数量, `amountMatched` 为匹配数量, 后两个参数选填, 默认为 1 |
| addTrait(trait as string, @Optional String dependencies) | 第一个参数为特性名 (identifier), 第二个参数为部件名 (可不填) |
| addTrait(trait as [Trait](trait.md), @Optional String dependencies) | 第一个参数为特性, 第二个参数为部件名 (可不填) |
