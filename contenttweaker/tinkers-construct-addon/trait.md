# 特性

## 导入
通过`import mods.contenttweaker.tconstruct.Trait;`导入Trait对象  
通过`import mods.contenttweaker.tconstruct.TraitBuilder;`导入TraitBuilder对象  
通过`import mods.contenttweaker.tconstruct.TraitDataRepresentation;`导入TraitDataRepresentation对象  

## 特性构建器
`val myTrait = mods.contenttweaker.tconstruct.TraitBuilder.create(String identifier, int color, @Optional int maxLevel, @Optional int countPerLevel);` 
其实你填完第一个参数就可以不填,剩下的由Setter方法填也是可以的。

## 设定参数
你可以通过一下方法设定特性的参数
| 参数 | 设定值类型 | 参数描述 |
| :---- | :---- | :---- |
| color | 
