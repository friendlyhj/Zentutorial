# 食物

食物是一种特殊的物品。

## 导入包

`import mods.contenttweaker.ItemFood;` 原版加工厂包也需要导入！

## 创建

用`val testItem as ItemFood = VanillaFactory.createItemFood(字符串物品ID, 整数可恢复饥饿值);`呼出一个物品类的一个实例，并存储在某个变量中，以做接下来的修改。物品ID必须全小写，可以包含数字和下划线\_ ，必须字母开头。

食物是一种特殊的物品，接下来的操作与物品差不多。（注册、设置信息、设置本地化、材质与添加物品一致）[传送门](https://youyi580.gitbook.io/zentutorial/contenttweaker/vanilla-factory/item)

## 可用ZenProperties

创建物品时可用的ZenProperties，食物也能用！

以下为食物特有的

| 名称 | 类型 | 默认值 | 描述 |
| :--- | :--- | :--- | :--- |
| healAmount | int |  | 该食物可恢复的饥饿值 |
| alwaysEdible | bool | false | 该食物在玩家饥饿值满时是否还可以吃 |
| wolfFood | bool | false | 该食物是否可喂给狼 |
| saturation | float | 0.6 | 该食物的相对饱和度，实际饱和度为相对饱和度 * 饥饿值 |
| onItemFoodEaten | IItemFoodEaten | null | 吃下该食物后会发生什么\(见下文\) |

## 吃食物给药水效果

我知道你在想什么。这是事件高级运用，但你肯定想要，对吧？

```javascript
food.onItemFoodEaten = function(stack, world, player) { // 框架
    if (!world.remote) { // 框架
        //以下一行可改，格式为
        //player.addPotionEffect(药水ID.makePotionEffect(时间, 等级));
        //时间的单位为tick 1秒 = 20ticks
        //药水ID可用/ct potions 指令查看
        //想要加多个buff，就把下面这行多写几次就行
        player.addPotionEffect(<potion:minecraft:weakness>.makePotionEffect(60, 1)); // 吃食物给3s虚弱效果
    }  // 框架
}; // 框架
```

## 例子

```javascript
#loader contenttweaker

import mods.contenttweaker.VanillaFactory;
import mods.contenttweaker.ItemFood;

var soup as ItemFood = VanillaFactory.createItemFood("sweet_soup", 4);

soup.saturation = 0.8;
soup.alwaysEdible = true;
soup.onItemFoodEaten = function(stack, world, player) {
    if (!world.remote) {
        player.addPotionEffect(<potion:minecraft:speed>.makePotionEffect(100, 1));
        player.addPotionEffect(<potion:minecraft:strength>.makePotionEffect(200, 2));
    }
};
soup.register();
```

