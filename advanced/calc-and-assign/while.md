# while



While循环只要后面的条件为`true`就会循环执行给定的代码。 另外，可以使用`break`关键字结束循环。

```javascript
var i as int = 0;

//会输出 0 - 9 ，因为在下一轮循环中，i等于10，因此 i<10 判断结果为false 
while (i < 10) {
    print(i);
    i += 1;
}

print("After loop: " + i);


//会输出 10 - 6, 因为在下一轮循环中 i等于5 ,使循环中断
while (i > 0) {
    if (i == 5) {
        break;
    }
    print(i);
    i -= 1;
}

print("After loop 2: " + i);


for k in 1 .. 10 {
    if (k == 5)
        break;
    print(k);
}
```

