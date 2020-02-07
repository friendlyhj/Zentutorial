# 循环语句\(foreach循环\) / 普通数组

这里算简单还是高级呢？循环允许一个语句执行多次。用不到你一直复制粘贴，同时也能增强脚本的可读性。一个循环语句的基本样子：

```javascript
//导入包，为下面的定义数组作准备。
import crafttweaker.item.IItemStack;

var logs as IItemStack[] = [
    <minecraft:log>,
    <minecraft:log:1>,
    <minecraft:log:2>,
    <minecraft:log:3>,
    <minecraft:log:4>,
    <minecraft:log:5>
];  //定义一个IItemStack类数组
//var局部变量的 `as 类型名` 可以省略，但定义数组时决不能省略，中括号表示数组。
var planks as IItemStack[] = [
    <minecraft:planks>,
    <minecraft:planks:1>,
    <minecraft:planks:2>,
    <minecraft:planks:3>,
    <minecraft:planks:4>,
    <minecraft:planks:5>,
]; //两个数组要一一对应

//这个只是为了方便编写
var stoneAxe = <minecraft:stone_axe>.anyDamage().transformDamage();
var ironAxe = <minecraft:iron_axe>.anyDamage().transformDamage();
var goldenAxe = <minecraft:golden_axe>.anyDamage().transformDamage();
var diamondAxe = <minecraft:diamond_axe>.anyDamage().transformDamage();

for i, log in logs {   
//一个for循环，准确的说是foreach循环，遍历数组，i为一个变量，表示循环了几次（程序员数数是从0开始数的，第一次循环i=0，第二次为1....）
//log in logs 表示在logs数组中循环，并把log变量用来存储logs数组的每一个物品。
    var plank = planks[i]; //将plank赋值为myPlanks中i对应的物品
    recipes.removeShapeless(plank, [log]);
    recipes.addShapeless(plank * 2, [log]);
    recipes.addShapeless(plank * 3, [log, stoneAxe]);
    recipes.addShapeless(plank * 4, [log, ironAxe]);
    recipes.addShapeless(plank * 5, [log, goldenAxe]);
    recipes.addShapeless(plank * 6, [log, diamondAxe]);
}
```

> foreach是for语句的简化，但是foreach并不能替代for循环。可以这么说，任何foreach都能改写为for循环，但是反之则行不通。
>
> foreach不是一个关键字。foreach的循环对象一般是一个集合，List、ArrayList、LinkedList、Vector、数组等。

