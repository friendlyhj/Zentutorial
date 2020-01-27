# if



If 关键字是书写条件语句判定条件的部分，只有判定条件为 true 才会执行接下来的代码块。

注意！**两个等号** 才是比较运算符（一个等号是赋值运算符！）

```javascript
val test = 0;

if(test == 0){ //true
    print("Test 等于0！");
}
```

Else 关键字可以作为条件语句的后半部分，当 if 语句处条件为 false 时候，就会执行此处的代码块。

```javascript
var test as int = 0;

if(test == 0){//true
    //当 test 为 0 时候，执行此处语句
    print("Test 等于 0！");
} else {
    //当 test 不为 0 时候，执行此处语句
    print("Test 不等于 0！");
}

test = 1
if(test == 0){//false
    //当 test 为 0 时候，执行此处语句
    print("现在 test 等于 0！");
} else {
    //当 test 不为 0 时候，执行此处语句
    print("现在 test 不等于 0！");
}
```

