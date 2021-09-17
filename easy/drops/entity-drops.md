# 生物掉落物

可用`/ct entities`指令查看所有实体ID。

```text
val entity = <entity:minecraft:sheep>;

//addDrop(item,min,max,chance);
//添加掉落（战利品表条目），min max chance均为可选参数
entity.addDrop(<minecraft:apple>);

//addDrop(weightedItem, min, max);
//添加掉落（战利品表条目）的另一种写法
entity.addDrop(<minecraft:stone> % 20);

//addPlayerOnlyDrop(item,min,max,chance);
//添加只有玩家杀死才能掉落的物品，min max chance均为可选参数
entity.addPlayerOnlyDrop(<minecraft:gold_ingot>, 10, 64);

//addPlayerOnlyDrop(weightedItem, min, max);
//添加只有玩家杀死才能掉落的物品的另一种写法
entity.addPlayerOnlyDrop(<minecraft:iron_ingot> % 20, 1, 3);

//removeDrop(item);
//删除某一个掉落物
entity.removeDrop(<minecraft:wool>);

//clearDrops
//删除所有掉落物
entity.clearDrops();
```
