---
description: >-
  关联数组（又称映射）与普通数组极为类似，也是用来存储多条数据的。但是它的key（键）可以自定义，而不是0 1 2 3 ...
  在我的实际运用中，关联数组一般用于制作数据库，在之后的循环调用。
---

# 关联数组\(映射\)

你需要用`{ }`和`:`来声明一个映射数组。

```javascript
import crafttweaker.item.IItemStack
val test as IItemStack[string] = {
    "dirt" : <minecraft:dirt>,
    "iron" : <minecraft:iron_ingot>
};
```

需要注意的是

* 你可以用ZenScript的任何类型作为key或值
* 不可使用变量作为key，变量名会被解释为字符串
* 不可用数组作为key，值可以。
* 不可以直接遍历用数组作为值的关联数组。

你可以用下标访问数组的某个元素，与普通数组不同，关联数组使用你事先定义的key来访问元素。比如上文例子的关联数组可用`test["iron"]`访问到`<minecraft:iron_ingot>`。如果key为字符串，也可以用`test.iron`

数组的某个键对应的元素可以随时覆盖，与普通数组不同，你可以用一个新的key来添加一个新的条目。

```javascript
val changingArray as string[IItemStack] = {
    <minecraft:dirt> : "这是我",
    <minecraft:gold_ingot> : "我讨厌他"
};

val gg = <minecraft:gold_ingot>;

//覆盖 gold_ingot 的 值
changingArray[gg] = "我喜欢他";

//添加一个新的条目
changingArray[<minecraft:grass>] = "力量！";
```

既然有了数组，我们需要遍历。你可以使用key遍历和key - value遍历。

* key 遍历法：遍历 key，只需要传入一个参数。
* key-value 遍历法：同时遍历 key 和 value，需要传入两个参数。

```javascript
val test as int[string] = {
    "one" : 1,
    "two" : 2,
    "three" : 3,
    "four" : 4
}

//key遍历法
//将会依次打印该映射数组的key one two three four
for key in test {
    print(key);
}
//key-value遍历法
for key, value in test {
    print("The key is " ~ key);
    print(value * 125);
}
```

关联数组提供了如下ZenGetter

```javascript
//获取映射数组的所有key，返回包含所有key的普通数组，可以使用如下的其中一个
AssocArray.keySet  //返回列表
AssocArray.keys  
//获取映射数组的所有值，返回包含所有值的普通数组，可以使用如下的其中一个
AssocArray.values
AssocArray.valueSet
//获取映射数组的所有条目，返回包含所有条目的普通数组
AssocArray.entrySet
//每个条目有key和value两个Getter获取这个条目的键和值
val Entry = AssocArray.entrySet[0];
Entry.key;
Entry.value;
```

