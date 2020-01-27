# 配方函数与配方事件

我们再一次看回最基本的合成添加语句：`recipes.addShaped(recipeName, output, inputBox);`。然而事实上，这个语句还有两个可选参数——配方函数和配方事件。

`recipes.addShaped(recipeName, output, inputBox, recipeFunction, recipeAction);`

这两个都是用函数来处理的。配方函数用来决定配方输出结果，配方事件用于决定合成后会发生什么。

