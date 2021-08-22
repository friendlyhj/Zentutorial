# ZenClass

前面已经说过，ZenScript 是一门面向对象的语言。作为面向对象的语言，怎么不能自定义类呢？ZenScript 是一个基于 Java 的语言，它的类 ZenClass 本质上就是一个 Java 类。

## 所需的关键词

| 关键词     | 描述                   |
| ---------- | ---------------------- |
| `zenClass` | 告诉编译器要新建一个类，需要在后面指定自定义类的名字 |
| `zenConstructor` | 声明这个类的构造函数，之后调用该函数会返回该类的一个全新的实例。 |
| `val` 和 `var` | 声明这个类的字段。`val` 关键词声明的字段为 `final` 的，不可再次赋值。 |
| `static` | 声明这个类的静态字段。静态字段针对整个类，而不仅仅只是这个类的一个实例。 |
| `function` | 声明这个类的一个方法，在 ZenScript 中，你不可以声明静态方法。 |
| `this` | 指代对象本身，只在声明方法和构造器时有效。 |

## 声明例子

```csharp
zenClass MyClass { // 声明一个叫做 MyClass 的类
    zenConstructor(arg as string, arg1 as int) { // 声明构造函数
        myValue = arg;
        myValueTwo = arg1;
        // 一般这里填的都是给新的实例设置字段值
        print("new MyClass");
    }

    zenConstructor(arg as string) { // 你可以声明多个构造函数，但不可互相调用，而且参数表不能相同。
        myValue = arg;
        myValueTwo = 25;
    }

    // 设置该类的字段
    val myValue as string; // 在这里你可以不设初值，而在构造函数内给其赋值
    val myValueTwo as int;
    var myValueThree as int;
    static myStaticValue as int = 233;

    // 声明该类的叫做 getMyValue 的方法，返回字符串
    function getMyValue() as string {
        return this.myValue; // this指代该对象，这行即为返回该对象的 myValue 字段的值
    }

    function setMyValueThree(arg as int) as MyClass {
        this.myValueThree = arg; // 由于 myValueThree 字段由 var 关键词声明，可以多次赋值
        return this; // 返回该对象本身
    }

    function method() as string {
        return this.myValue ~ this.myValueTwo;
    }
}
```

## 使用例子

假如前文的脚本保存在 `./scripts/Class.zs`中。

```csharp
import scripts.Class.MyClass; //导入该类

val obj as MyClass = MyClass("abc", 1); // 构建该类的实例，调用构建函数

print(obj.getMyValue()); // 调用 getMyValue 方法，将会打印 "abc"
print(obj.myValueTwo); // 获取该实例 myValueTwo 字段的值，将会打印 1

print(MyClass.myStaticValue); // 调用 myStaticValue 字段的值，针对整个类（可以看见前面是 MyClass 类名）

val test as MyClass = MyClass("test");
test.myStaticValue = 3;
print(test.myStaticValue); // 也可以针对一个实例调用静态字段
```
