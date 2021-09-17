---
description: 函数可以用于计算结果也可以打包一系列操作。
---

# 自定义函数

## 基本格式

```csharp
function 函数名(参数表) as 返回类型名 {
    [代码]
    return 函数返回值;
}
```

然而事实上，只有`function`关键字是必要的，若是一个不需要参数的函数，则不需要参数表，只有一对小括号；若不需要返回值，只是打包一些操作的话，则不需要as 返回类型名和return；如果这个函数需要的代码只需要一行，直接写在return所在的一行即可，不需要其他代码；没有函数名的函数称为匿名函数，这经常匹配到特定的function类用于作为特定方法的输入参数（高级用法将会经常用到）。

return关键字将会把指定的值返回至函数的调用点上，执行后续操作。若函数处理时，碰到return后，程序将跳出函数，不再执行之后的函数内操作（跳出所有循环）。所以一般return会在函数代码的最下方。

## 例子

例子一：getItemName函数，返回输入的IItemStack的物品名

```csharp
function getItemName(input as IItemStack) as string {
    val id as string = input.definition.id;
    val meta as int = input.metadata;
    if (meta == 0){
        return id;
    } else return (id ~ ":" ~ meta);
}
```

例子二：将删合成和添加合成打包起来（打包操作不需要返回值）为了指定配方名用到了例子一的getItemName函数

```csharp
function recipeTweak(isShaped as bool, out as IItemStack, input as IIngredient[][]) {
    val recipeName as string = getItemName(out);
    recipes.remove(out,true);
    if (isShaped) {
        recipes.addShaped(recipeName,out,input);
    } else {
        recipes.addShapeless(recipeName,out,input[0]);
    }
}
```

例子三：构建一个全局函数

```csharp
global addition as function(int, int)int = function (a as int, b as int) as int {
    return a + b;
};
```
