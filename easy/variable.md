# 局部变量

使用一些变量存储常用的物品，让你不用打又臭又长的物品ID。

```text
 // 基本格式: var 变量名 (as 类型名) = 值;
 //用iron代替铁锭这个物品
 var iron = <minecraft:iron_ingot>;
 // var 变量可以再赋值，之后的脚本中iron代表石头。
 iron = <minecraft:stone>;
 //val 变量不可再次赋值。
 val gold = <minecraft:gold_ingot>;
 //gold = <minecraft:stone>; 
 //上一行是错误的，val变量不可再次赋值。
```

val/var 变量为局部变量，只可在所在脚本使用，另外的脚本不可使用，需要另外声明。

