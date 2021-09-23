# 特性数据

获取特性更多的信息, 也可以通过此类设置 `Trait` 的一些参数

## 导包

```csharp
import mods.contenttweaker.tconstruct.TraitDataRepresentation;
```

## 参数

| 参数 | 是否有 ZenGetter | 是否有 ZenSetter | 值类型 | 描述 |
| :---- | :---- | :---- | :---- | :---- |
| identifier | √ | √ | string | 特性名称 |
| extraInfo | √ | √ | string | 特性额外信息 |
| info | √ | × | string | 特性信息 |
| colorString | √ | × | string | 返回 string 类型的 color |
| level | √ | √ | int | 特性等级 |
| color | √ | √ | int | 特性颜色 |
| current | √ | √ | int | 特性当前等级的值 |
| max | √  | √ | int | 特性当前等级可强化的最大值 |
