---
description: >-
  IData具有很多子类，但在其中，最重要的是DataMap，因为你获取到的物品、方块、玩家的NBT都是IData中的DataMap。Map即为映射，与上文的映射数组有些类似，不同的是，值可以是不同的类（其实值都是IData），而key只能为字符串。
---

# DataMap



声明一个DataMap的方法与IData其他子类的声明不同。

```javascript
import crafttweaker.data.IData;

val myFirstMap as IData = {key1: "value1",
                  key2: "value2",
                  key3: 3};
```

你甚至可以嵌套，NBT大多也是这样

```javascript
val nestedMap as IData = { key1: 
                    {
                        key1: "hello"
                    }
                };
```

然而IDataMap的元素不能直接修改，你也可以用key检索其中的元素，将会返回这个key对应的值，均以IData形式返回。

```javascript
val mySecondMap as IData = {key1: "value1",
                   key2: "value2",
                   key3: 3};

// 检索叫做 "key1" 的成员
var k1 as IData = mySecondMap.key1;
print(k1.asString());

// 检索叫做 "key2" 的成员
var k2 as IData = mySecondMap.memberGet("key2");
print(k2.asString());
```

你可以用`+`来合并两个IDataMap和`-`来裁剪IDataMap。合并时，相同key的值后者会覆盖前者（这是你唯一可以修改值的方法）。裁剪可以去除特定key的元素。

```javascript
val map1 as IData = {
    key1 : "hello",
    key3 : "test",
};

val map2 as IData = {
    key2 : "bye",
    key3 : "override"
};

print((map1 + map2).asString()); // 打印出 {key1 : "hello", key2 : "bye", key3 : "override"}



val map3 as IData = {
    key1 : "two",
    key2 : "two",
    key3 : "three"
};

print((map3 - "key1").asString()); // 打印出 {key2 : "two", key3 : "three"}

val map4 as IData = {
    key3 : "anything"
};

print((map3 - map4).asString()); // 打印出 {key1 : "two", key2 : "two"}
```

