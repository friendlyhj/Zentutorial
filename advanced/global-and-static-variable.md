# 全局和静态变量

你肯定受够了局部变量只能在当前脚本使用，其他脚本需要再次声明。有什么方法可以调用其他脚本的变量呢？使用全局和静态变量，允许跨脚本调用！

声明全局和静态变量非常简单。注意as 类型名 不能省略，且全局静态变量之后不能再次声明，修改其类型。（但可以重新赋值）全局变量可以直接在其他脚本使用，静态变量还需要跨脚本调用。

```javascript
import crafttweaker.item.IItemStack;

global stone as IItemStack = <minecraft:stone>;
static dirt as IItemStack = <minecraft:dirt>;
```

* 含有全局变量的脚本需要用优先级预加载器保证其优先加载。
* 局部变量可以覆盖全局变量

