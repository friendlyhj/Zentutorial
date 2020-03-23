# tooltips



你肯定会见到一些物品，名称下面还有一段叙述文字。CrT同样可以做到。

```text
//item.addTooltip(tip);
//item可以是物品，也可以是OD
<minecraft:chest>.addTooltip("这个方块可以存东西");
<ore:ingotTin>.addTooltip("这是锡锭。");
//用多行tips
<minecraft:grass>.addTooltip("这个泥土上长了草");
<minecraft:grass>.addTooltip("充满了力量");
//item.addShiftTooltip(tip);
//按住Shift才会显示的tooltip
<minecraft:chest>.addShiftTooltip("可以存27组物品！！！！");
//按住Shift显示更多
<minecraft:shears:*>.addShiftTooltip("可以用于剪羊毛", "按住Shift键显示更多");
//item.clearTooltip();
//清除该物品所有tooltip
```

