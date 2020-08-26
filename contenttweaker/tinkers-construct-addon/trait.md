# 特性

## 导入
通过`import mods.contenttweaker.tconstruct.Trait;`导入Trait对象  
通过`import mods.contenttweaker.tconstruct.TraitBuilder;`导入TraitBuilder对象  
通过`import mods.contenttweaker.tconstruct.TraitDataRepresentation;`导入TraitDataRepresentation对象  

## 特性构建器
`val myTrait = mods.contenttweaker.tconstruct.TraitBuilder.create(String identifier, int color, @Optional int maxLevel, @Optional int countPerLevel);`  
**其实你填完第一个参数就可以不填,剩下的由Setter方法填也是可以的。**

## 设定参数
**你可以通过一下方法设定特性的参数**
| 参数 | 设定值类型 | 参数描述 |
| :---- | :---- | :---- |
| identifier | string | 设定名称(一般在写构建器的时候就写了,不会用到) |
| color | int | 设定颜色 |
| maxLevel | int | 最高等级 |
| countPerLevel | int | 设定升级到第二级(前提是有,无就不需要写)需要多少个countPerLevel |
| hidden | bool | ? | 
| localizedDescription | string | 本地化描述 |
| localizedName | sting | 本地化名称 |

## CanApplyTogether函数
**可以使特性(附魔)不能同存**  
例子1:`myTrait.canApplyTogetherTrait = function(TraitRepresentation thisTrait, String otherTrait){return otherTrait != 特性名称(identifier)};`  
例子2:`myTrait.canApplyTogetherEnchantment = function(TraitRepresentation thisTrait, IEnchantmentDefinition enchant){return enchant != 附魔名称};`

## Extra info函数
**可以在工具装配台看到额外信息**  
例子:
```javascript
myTrait.extraInfo = function(TraitRepresentation thisTrait, IItemStack item, IData tag){
    val infos as string[] = ["1","2"];
    for i, info in infos {
        return "Cool" ~ info;
    }
};
```
结果,额外信息显示Cool1,Cool2  

## 访问特性数据
例子:`(val myTraitData = )myTrait.getData(itemWithTrait);`  
**myTrait指特性,itemWithTrait指工具**
