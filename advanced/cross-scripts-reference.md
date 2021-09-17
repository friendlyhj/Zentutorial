# 跨脚本引用

跨脚本调用主要是针对静态变量，但自定义函数和类也需要它！

* 跨脚本调用需要以`scripts.`开头
* 匹配相对路径
* 先匹配目录，再匹配脚本和值

比如，两个脚本，a.zs和b.zs

a.zs

```text
static myVal as string = "myVal";
function makeLine() {
    print("---------------");
}
```

b.zs

```text
print(scripts.a.myVal);
scripts.a.makeLine();
```

你甚至可以使用import导入脚本

c.zs

```csharp
import scripts.a;

print(a.myVal);
a.makeLine();
```
