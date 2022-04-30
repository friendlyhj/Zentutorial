# 数组与集合

## 数组

- 数组是一个容器，一个数组存储的元素的数据类型都是相同的。

- 你可以往数组里存取数据，也可以修改数组里的数据。

- 你可以为数组指定初始元素，也可以不指定。

- 数组里的元素具有顺序，可重复。

```csharp
var int_array1 as int[] = [];
// 定义一个 int 类型的数组，没有初始元素

var int_array2 as int[] = [10,20,30];
// 定义一个 int 类型的数组，有三个初始元素

var strings as string[] = ["apple","carrot"];
// 定义一个 string 类型的数组，有两个初始元素

var items as IItemStack[] = [<minecraft:apple>,<minecraft:carrot>];
// 定义一个 IItemStack 类型的数组，有两个初始元素
```

- 数组里的元素都具有下标，你可以通过下面的方式为数组添加元素，或修改数据。

- 数组里第一个元素的下标为 `0`。

```csharp
var numbers as int[] = [10,20,20]; // 定义一个数组
numbers[2] = 30; // 将下标为 2 的元素修改为 30 
numbers += 40; // 往数组的末尾添加一个元素
```

- 数组有一个`length`属性，返回数组的元素个数。

```csharp
var array as int[] = [2,4,6,8];
print(array.length); // array 的元素个数为 4，输出 4
```

## 多维数组

你用过`recipes.addShaped()`吗？它的参数里面就有一个多维数组。准确的来说，是一个二维数组。

```csharp
var gold as IItemStack = <minecraft:gold_ingot>;
var apple as IItemStack = <minecraft:apple>;

recipes.addShaped("golden_apple", <minecraft:golden_apple>,
    [[gold,gold,gold],
     [gold,apple,gold],
     [gold,gold,gold]]
);
```

在上面的示例中，二维数组的第一个元素，是一个一维数组，即九宫格的第一行`[gold,gold,gold]`。

二维数组的操作和一维数组的操作相似。

```csharp
var array as int[][] = [ //  定义一个二维数组
    [1,2,3],
    [4,5,6],
    [7,8,9]
];
// 如何获取第二行第三个数，即 6 呢？

print(array[1][2]); // 输出 6

// 二维数组第二个元素的下标为 1，这个元素同时也是一个数组，它的第三个元素下标为 2
```
