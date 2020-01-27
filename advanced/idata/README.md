---
description: IData是一个数据接口，用来操纵各种数据。
---

# IData 类型



IData是一个数据接口，用来操纵各种数据。

通过IData接口你可以将任意基础类型（短整型，双精度，字符串，整型），甚至数组类型转换为数据类型（IData）。使用`as IData`转换。

如果要使用本接口你需要导入 `crafttweaker.data.IData;`包

以下为所有的IData子类和其可用的操作符

| 二元操作符 | `+` | `-` | `*` | `/` | `%` | `&` | \` | \` | `^` | `in` | `==` | `<, >, <=, >=` |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| DataBool | ✘ | ✘ | ✘ | ✘ | ✘ | ✔ | ✔ | ✔ | ✔ | ✔ | ✘ | ✘ |
| DataByte | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| DataByte\[\] | ✘ | ✘ | ✘ | ✘ | ✘ | ✘ | ✘ | ✘ | ✔ | ✔ | ✘ | ✘ |
| DataDouble | ✔ | ✔ | ✔ | ✔ | ✔ | ✘ | ✘ | ✘ | ✔ | ✔ | ✔ | ✔ |
| DataFloat | ✔ | ✔ | ✔ | ✔ | ✔ | ✘ | ✘ | ✘ | ✔ | ✔ | ✔ | ✔ |
| DataInt | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| DataInt\[\] | ✔ | ✘ | ✘ | ✘ | ✘ | ✘ | ✘ | ✘ | ✔ | ✔ | ✘ | ✘ |
| DataList | ✔ | ✘ | ✘ | ✘ | ✘ | ✘ | ✘ | ✘ | ✔ | ✔ | ✘ | ✘ |
| DataLong | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| [DataMap](https://crafttweaker.readthedocs.io/zh_CN/latest/Vanilla/Data/DataMap) | ✔ | ✔ | ✘ | ✘ | ✘ | ✘ | ✘ | ✘ | ✔ | ✔ | ✘ | ✘ |
| DataShort | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| DataString | ✔ | ✘ | ✘ | ✘ | ✘ | ✘ | ✘ | ✘ | ✔ | ✔ | ✔ | ✔ |

| 一元操作符 | `-` 取反 | `!` 取否 |
| :--- | :--- | :--- |
| DataBool | ✘ | ✔ |
| DataByte | ✔ | ✔ |
| DataByte\[\] | ✘ | ✘ |
| DataDouble | ✔ | ✘ |
| DataFloat | ✔ | ✘ |
| DataInt | ✔ | ✔ |
| DataInt\[\] | ✘ | ✘ |
| DataList | ✘ | ✘ |
| DataLong | ✔ | ✔ |
| [DataMap](https://crafttweaker.readthedocs.io/zh_CN/latest/Vanilla/Data/DataMap) | ✘ | ✘ |
| DataShort | ✔ | ✔ |
| DataString | ✘ | ✘ |

| 索引与成员 | `[i]` | `[i]=v` | `.member` | `.member=v` | `.length` | `.immutable` | `.update(v)` |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| DataBool | ✘ | ✘ | ✘ | ✘ | returns `0` | ✔ | ✔ |
| DataByte | ✘ | ✘ | ✘ | ✘ | returns `0` | ✔ | ✔ |
| DataByte\[\] | ✔ | ✔ | ✘ | ✘ | ✔ | ✔ | ✔ |
| DataDouble | ✘ | ✘ | ✘ | ✘ | returns `0` | ✔ | ✔ |
| DataFloat | ✘ | ✘ | ✘ | ✘ | returns `0` | ✔ | ✔ |
| DataInt | ✘ | ✘ | ✘ | ✘ | returns `0` | ✔ | ✔ |
| DataInt\[\] | ✔ | ✔ | ✘ | ✘ | ✔ | ✔ | ✔ |
| DataList | ✔ | ✔ | ✘ | ✘ | ✔ | ✔ | ✔ |
| DataLong | ✘ | ✘ | ✘ | ✘ | returns `0` | ✔ | ✔ |
| DataMap | ✘ | ✘ | ✔ | ✔ | ✔ | ✔ | ✔ |
| DataShort | ✘ | ✘ | ✘ | ✘ | returns `0` | ✔ | ✔ |
| DataString | ✔ | ✘ | ✘ | ✘ | ✔ | ✔ | ✔ |

你可以将 IData 转换成特殊的类型：`data.asType()` → `data.asInt();`

你也可以使用数据接口来转换类型：`("1" as IData).asInt();`

| 类型由 ↓ 转换成 → | bool | byte | byte\[\] | double | float | int | int\[\] | list | long | [Map](https://crafttweaker.readthedocs.io/zh_CN/latest/AdvancedFunctions/Associative_Arrays) | short | string |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| DataBool | `≡` | ✔ | `null` | ✔ | ✔ | ✔ | `null` | `null` | ✔ | `null` | ✔ | ✔ |
| DataByte | ✘ | `≡` | `null` | ✔ | ✔ | ✔ | `null` | `null` | ✔ | `null` | ✔ | ✔ |
| DataByte\[\] | ✘ | ✘ | `≡` | ✘ | ✘ | ✘ | ✔ | ✔ | ✘ | `null` | ✘ | ✔ |
| DataDouble | ✘ | ✔ | `null` | `≡` | ✔ | ✔ | `null` | `null` | ✔ | `null` | ✔ | ✔ |
| DataFloat | ✘ | ✔ | `null` | ✔ | `≡` | ✔ | `null` | `null` | ✔ | `null` | ✔ | ✔ |
| DataInt | ✘ | ✔ | `null` | ✔ | ✔ | `≡` | `null` | `null` | ✔ | `null` | ✔ | ✔ |
| DataInt\[\] | ✘ | ✘ | ✔ | ✘ | ✘ | ✘ | `≡` | ✔ | ✘ | `null` | ✘ | ✔ |
| DataList | ✘ | ✘ | ✔ | ✘ | ✘ | ✘ | ✔ | `≡` | ✘ | `null` | ✘ | ✔ |
| DataLong | ✘ | ✔ | `null` | ✔ | ✔ | ✔ | `null` | `null` | `≡` | `null` | ✔ | ✔ |
| DataMap | ✘ | ✘ | `null` | ✘ | ✘ | ✘ | `null` | `null` | ✘ | `≡` | ✘ | ✔ |
| DataShort | ✘ | ✔ | `null` | ✔ | ✔ | ✔ | `null` | `null` | ✔ | `null` | `≡` | ✔ |
| DataString | ✘ | ✔ | `null` | ✔ | ✔ | ✔ | `null` | `null` | ✔ | `null` | ✔ | `≡` |

