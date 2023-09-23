# Math包

只有加减乘除取余乘方的运算，是远远不能满足需求的。CraftTweaker 4.1.20.688 添加了 Math 包提供了一系列数学函数。

需要用`import crafttweaker.util.Math;`导入

| 方法名 | 参数要求 | 用途 |
| :--- | :--- | :--- |
| max | 2个double/float/int/long | 取最大值\(与max全局函数区别为允许double/float\) |
| min | 2个double/float/int/long | 取最小值\(与max全局函数区别为允许double/float\) |
| floor | 1个double | 向下取整\(返回int\) |
| ceil | 1个double | 向上取整\(返回int\) |
| abs | 1个double/float/int/long | 取绝对值 |
| sin | 1个double | 正弦（弧度制） |
| cos | 1个double | 余弦（弧度制） |
| tan | 1个double | 正切（弧度制） |
| asin | 1个double | 反正弦（弧度制） |
| acos | 1个double | 反余弦（弧度制） |
| atan | 1个double | 反正切（弧度制） |
| sinh | 1个double | 双曲正弦（弧度制） |
| cosh | 1个double | 双曲余弦（弧度制） |
| tanh | 1个double | 双曲正切（弧度制） |
| sqrt | 1个double | 开方 |
| log  | 1个double | 自然对数 |
| log10 | 1个double | 常用对数 |
| round | 1个double | 四舍五入取整 |
| clamp | 三个double/float/int/long参数 | 区间限制函数，见下例 |

```csharp
import crafttweaker.util.Math;

// Math.clamp(x, min, max)
// 将数字限制在一个范围内
// 若 x 在 min 与 max 之间，则返回 x
// 若 x 小于 min，则返回 min
// 若 x 大于 max，则返回 max

// 15 在 10 与 19 之间，返回 15
print(Math.clamp(15, 10, 19));

// 10 不在 12 与 19 之间，返回 12
print(Math.clamp(10, 12, 19));
```
