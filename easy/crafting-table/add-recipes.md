# 添加配方

## **添加有序合成**

基本格式：`recipes.addShaped(recipeName, output, inputbox);`

1.12中Mojang修改了合成的注册系统，每个配方以一个json文件储存，同时每个配方有一个ID。当你打开高级提示框（F3+H\)时，可以在JEI中看见每一个配方的ID。但实际上，你也可以省略配方ID，就像旧版本那样，这样CrT会使用hash值自动指定配方ID。配方名不能重复。

output即为配方输出。inputbox即为需要的物品。比如我们拿铁护腿举个例子。

![](https://i.loli.net/2019/08/11/2cLOkKTdjmiM81w.png)

它在CrT是这么表示的

```text
 //配方名略去
 recipes.addShaped(<minecraft:iron_leggings>,
 [[<ore:ingotIron>, <ore:ingotIron>, <ore:ingotIron>],
 [<ore:ingotIron>, null, <ore:ingotIron>],
 [<ore:ingotIron>, null, <ore:ingotIron>]]);
```

用中文翻译，即为

配方包.添加有序合成\(原版铁护腿，

\[\[铁锭矿辞，铁锭矿辞，铁锭矿辞\]，

\[铁锭矿辞， 空的，铁锭矿辞\]，

\[铁锭矿辞，也是空的，铁锭矿辞\]\]\);

第一层\[\]表示inputbox这一整体，第二层每个\[\]表示一行，自然最多只能包含三个物品。

如果输出物品是多个怎么办？

把`<minecraft:stick>`写成`<minecraft:stick> * 4`这样就可以了。之后物品数量大多以这样表示。

其他特殊的配方——镜像合成（一种特殊的有序配方，可以水平或竖直翻转材料，如原版弓的合成）和隐藏合成（JEI看不见的配方）。

可以用`recipes.addShapedMirrored(recipeName, output, inputBox);`和`recipes.addHiddenShaped(recipeName, output, inputBox);`添加。

## **添加无序合成**

基本格式`recipes.addShapeless(recipeName, output, inputbox);`

以末影之眼举个例子

![](https://i.loli.net/2019/08/11/LlFrkM3RnWSdVCa.png)

在CrT这么表示

```text
 //配方名略去
 recipes.addShapeless(<minecraft:ender_eye>,
 [<minecraft:ender_pearl>,<minecraft:blaze_power>]);
```

这里个inputbox只有一层\[\]，因为是无序配方，无所谓物品放在哪一行，自然没有表示形状的第二层\[\]了。

可用`recipes.addHiddenShapeless(recipeName, output, inputBox);`添加隐藏无序合成。

