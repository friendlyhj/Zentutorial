---
description: 当你把ZenScript当作一种“编程”语言时……更广阔的天地等你探索！
---

# 基本类

[什么是OOP?](https://baike.baidu.com/item/%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1%E7%A8%8B%E5%BA%8F%E8%AE%BE%E8%AE%A1/24792)

最近github对ZenScript有了高亮支持，也算是一种语言了。为了给新手使用，zs没有使用类型安全，采用了IAny这一个弱类，这使得val/var局部变量可以省略as 类型名。但是在之后的使用中，这样会产生许许多多的问题，尽量不用省略类型名。那么，有多少类型名呢？

| 类名 | 解释 | 示例 | 导入 |
| :--- | :--- | :--- | :--- |
| 整型\(int\) | 任意整数\(范围为-2147483648~2147483647\) | `var test as int = 10;` |  |
| 布尔值\(bool\) | 真\(true\)或假\(false\) | `var test as bool = true;` |  |
| 长整型\(long\) | 范围更大的整数\(一般int就够了\) | `var test as long = 2147483648;` |  |
| 字符串\(string\) | 文本（注1：Java可用的string类的方法，ZenScript一样可用 注2：可用`==`判断是否相同，不需用equals方法） | `var test as string = "hello!";` |  |
| 单精度浮点数\(float\) | 小数 | `var test as float = 1.5;` |  |
| 双精度浮点数\(double\) | 也是小数，但是比float范围更大，有效数字更多 | `var test as double = 1.2345;` |  |
| 无类型\(void\) | 空，null，用于函数/方法表明该函数/方法无返回值 | `var test as void = null;` |  |
| 物品堆\(IItemStack\) | 一个物品 | `var test as IItemStack = <minecraft:stone>;` | `import crafttweaker.item.IItemStack;` |
| 材料\(IIngredient\) | 一个或多个物品（比如`<minecraft:stone>`和`<ore:ingotIron>`\) | `var test as IIngredient = <minecraft:stone>;` | `import crafttweaker.item.IIngredient;` |
| 矿物词典\(IOreDictEntry\) | 一个矿辞代表的多个物品 | `var test as IOreDictEntry = <ore:ingotIron>;` | `import crafttweaker.oredict.IOreDictEntry;` |
| 流体堆\(ILiquidStack\) | 一个流体 | `var test as ILiquidStack = <liquid:water>;` | `import crafttweaker.liquid.ILiquidStack` |

