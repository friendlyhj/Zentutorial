---
description: 真正要有mod的样，应该有属于自己的创造标签。
---

# 创造标签



需要`import mods.contenttweaker.CreativeTab;`导入相关包，原版加工厂包也需要导入！

用`val testTab as CreativeTab = VanillaFactory.createCreativeTab(字符串创造标签ID, 一个东西表示图标);`

图标可以用以下三个类中其中之一（还有个IItemStackSupplier是函数高级运用，跳过）

* IItemStack：物品堆。注意CoT表示IItemStack的尖括号调用，开头必须为item:，不可省略。
* Item：CoT注册物品
* Block：CoT注册方块

本地化key为`itemGroup.创造标签ID`

之后你就可以用\，来给添加的物品方块指定创造标签了。

实例脚本

```javascript
#loader contenttweaker
import mods.contenttweaker.CreativeTab;
import mods.contenttweaker.VanillaFactory;
import mods.contenttweaker.Item;

val zsTab as CreativeTab = VanillaFactory.createCreativeTab("contenttweaker", <item:minecraft:dragon_egg>);
zsTab.register();

val zsItem as Item = VanillaFactory.createItem("test_item");
zsItem.creativeTab = <creativetab:contenttweaker>;
zsItem.register();
```

