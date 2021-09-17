# Math包

只有加减乘除取余乘方的运算，是远远不能满足需求的。CrT本身并没有Math包。其附属mod [CraftTweaker Utils\(ctutils\)](https://www.curseforge.com/minecraft/mc-mods/crafttweaker-utils)提供了Math包。该包有多个方法提供数学运算。

需要用`import mods.ctutils.utils.Math;`导入

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
| random | 无参数 | 返回0到1之间的随机数 |
| round | 1个double | 四舍五入取整 |
| clamp | 三个double/float/int/long参数 | 区间限制函数，见下例 |

```csharp
import mods.ctuils.utils.Math;

// Math.clamp(x, min, max)
// 将数字限制在一个范围内
// 若 x 在 min 与 max 之间，则返回 x
// 若 x 小于 min，则返回 min
// 若 x 大于 max，则返回 max

// 12 在 14 与 19 之间，返回 12
print(Math.clamp(12, 14, 19));

// 10 不在 12 与 19 之间，返回 12
print(Math.clamp(10, 12, 19));
```
