# IContainer

## 导入

`import crafttweaker.container.IContainer;`

## tips

`IContainer` 是一个 `Iterable<IItemStack>` 。

这意味着你可以直接用for循环，遍历其内所有物品

## 可用ZenGetter

| 名称 | 类型 | 是否有同名ZenSetter | 描述 |
|-----|------|------|------|
|containerSize|int|✘||

## 可用方法

`IItemStack getStack(int i);`

`void setStack(int i, IItemStack stack);`

`String asString();`
