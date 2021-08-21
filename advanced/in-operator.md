# in/has 操作符

你可以用in/has 操作符来判断A是否包含B。这里的示例中的`in`均可以替换为`has`

```csharp
//检测加载模组
if (loadedMods in "thermalfoundation") {
    print("热力基本mod已被加载");
}
//检测材料对象
if (<ore:ingotIron> in <minecraft:iron_ingot>) {
    print("铁锭的矿物词典是正确的！");
}
```

请注意分清左右两个参数： 只有当所有在 `in` 之后的对象可以在 `in` 之前的对象找到时，结果才为真。用`has`可能更便于理解。

