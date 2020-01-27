# 样式代码



当然了，CrT中也可以用原版的§。具体用法见[wiki](https://minecraft-zh.gamepedia.com/%E6%A0%B7%E5%BC%8F%E4%BB%A3%E7%A0%81)

但是CrT也提供了format关键词，用颜色的名字表示该颜色，而不是§0到§f

```text
/* 可用的样式代码
format.black
format.darkBlue
format.darkGreen
format.darkAqua
format.darkRed
format.darkPurple
format.gold
format.gray
format.darkGray
format.blue
format.green
format.aqua
format.red
format.lightPurple
format.yellow
format.white
format.obfuscated
format.bold
format.strikethrough
format.underline
format.italic
*/
<minecraft:stick>.addTooltip(format.green("这不是绳子。"));
<minecraft:stick>.addShiftTooltip(format.strikethrough("不是好事。"));
<minecraft:stick>.addTooltip(format.green(format.italic("这不是绳子。")));
<minecraft:stick>.addTooltip(format.green(format.italic("这不是绳子。") + " with " + format.strikethrough("text")) + "不是么好事。");
```

