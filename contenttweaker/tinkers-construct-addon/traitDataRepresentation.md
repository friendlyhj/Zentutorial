# 特性数据表示  

## 导入

通过`import mods.contenttweaker.tconstruct.TraitDataRepresentation;`导入TraitDataRepresentation类  

## 参数

| 参数 | 是否有ZenGetter | 是否有ZenSetter | 返回(设定)值类型 | 参数描述 |
| :---- | :---- | :---- | :---- | :---- |
| identifier | √ | √ | string | 特性名称 |
| extraInfo | √ | √ | string | 特性额外信息 |
| info | √ | × | string | ? |
| colorString | √ | × | string | ? |
| level | √ | √ | int | 特性等级 |
| color | √ | √ | int | 特性颜色 |
| current | √ | √ | int | ? |
| max | √  | √ | int | ? |

## 注意事项

* 请不要直接把材料(特征)直接使用此类的方法
* 请使用了getData()方法之后,对getData()方法的结果使用此类的方法
