# Map（映射、关联数组）

Map 是集合的一种，也称作映射、关联数组等。特点是存储的数据为键值对(Key-Value)，key（键）和 value（值）一一对应。

> - Map 没有下标，取代下标的是 key（键）
> - 你可以用 ZenScript 的任何类型作为 key
> - 键值对的形式为 key: value，键在前，值在后
> - 不可使用变量作为 key，变量名会被解释为字符串
> - 数组可以作为 value，但不可以作为 key

当然如果你的映射只是为了遍历就不用担心这个了。

## 定义与访问

```csharp
// 定义一个 Map 集合，key 为 int 类型，value 为 string 类型
var map1 as string[int] = {
    1 : "一",
    2 : "二",
    3 : "三"
};

// 通过 2 来访问 map1 中的 二， 输出 二
print(map1[2]);

// 定义一个 Map 集合，key 为 string 类型，value 为 IItemStack 类型
var map2 as IItemStack[string] = {
    gold : <minecraft:gold_ingot>,
    iron : <minecraft:iron_ingot>,
    diamond : <minecraft:diamond>
};

// 通过 iron 来访问 map2 中的 <minecraft:iron_ingot>
print(map2["iron"].displayName);

// 特别的，key 为 string 类型时可以通过点来访问 value
print(map2.iron.displayName);
```

## 修改

你可以修改一个键对应的值，也可以给 Map 添加新的键值对。

```csharp
var map as string[int] = {
    1 : "一",
    2 : "二",
    3 : "三",
};

map[1] = "one"; // 修改
map[2] = "two"; // 修改
map[3] = "three"; // 修改
map[4] = "four"; // 添加
map[5] = "five"; // 添加

```

## 遍历

可以通过增强 for 循环来遍历一个 Map 中的 key , key-value 和 entry。

```csharp
var map as string[int] = {
    1 : "一",
    2 : "二",
    3 : "三",
    4 : "四"
}

// key 遍历法
for key in map {
    print(key); // 输出 1, 2, 3, 4
}

// key-value 遍历法
for key, value in map {
    print(key ~ "-->" ~ value); // 输出 1-->一, 2-->二, 3-->三, 4-->四
}

// entry 遍历法
for entry in map.entrySet {
    print(entry.key ~ "-->" ~ entry.value); // 输出 1-->一, 2-->二, 3-->三, 4-->四
}
```

## Set 与 Entry

keySet, valueSet, entrySet

```csharp
map.keySet   // Returns the map's keySet.
map.keys     // Returns the map's keySet.
map.values   // Returns the map's valueSet.
map.valueSet // Returns the map's valueSet.
map.entrySet // Returns the map's entrySet.

entry.key;   // Returns the entry's key.
entry.value; // Returns the entry's value.
```
