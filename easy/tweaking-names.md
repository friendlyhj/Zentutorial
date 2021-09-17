# 物品名称修改

使用`物品ID.displayName = "xxx";`来修改一个物品的名称。

例如`<minecraft:grass>.displayName = "充满力量的方块";` 将草方块重命名为充满力量的方块。

但是有可能在某种情况下，物品还是会显示旧名称，可以直接改本地化。

基本格式`game.setLocalization(languageCode, unlocalizedName, newName);`

* languageCode是字符串，同时也可选，选择语言。比如"en\_us"为英文，"zh\_cn"为中文。
* unlocalizedName是lang文件的key

  例如`game.setLocalization("tile.chest.name","StorageBox Deluxe");`

  说白了就是可以在zs中修改语言文件的一部分内容。
