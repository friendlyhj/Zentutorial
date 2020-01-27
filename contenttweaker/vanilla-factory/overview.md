# 概论

原版加工厂提供了添加物品、方块、食物、流体、创造标签等原版东西的方法。

需要用`import mods.contenttweaker.VanillaFactory;`导入原版加工厂包。

当你添加了物品、方块等其他内容后，你需要提供语言文件、材质、BlockState、Model（如果你需要建模的话）。保存在游戏根目录\resources\contenttweaker目录下，这块内容类似于材质包制作，我不讲解。

CoT疑似集成了[Resource Loader](https://www.curseforge.com/minecraft/mc-mods/resource-loader)这个mod，本来是这个mod才提供了resources文件夹，不过我还是推荐再添加这个mod。RL有个屑特性，resources文件夹内的语言文件会被自动改编码，导致本地化时zh\_cn.lang不可用，会乱码。943汉化天空树厂4就遇到这个问题，你可以用u码转义防止编码改掉的影响，或者直接尝试用zs本地化。（见基本运用--物品名称修改 章）用zs本地化的脚本加载器是CraftTweaker，记得分脚本！

