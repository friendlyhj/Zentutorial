# 物品

需要`import mods.contenttweaker.Item;`导入有关包。原版加工厂包也需要导入！

用`val testItem as Item = VanillaFactory.createItem(字符串物品ID);`呼出一个物品类的一个实例，并存储在某个变量中，以做接下来的修改。物品ID必须全小写，可以包含数字和下划线\_ ，必须字母开头。

然后你对这个对象用一堆ZenProperties\(既是ZenSetter，也是ZenGetter\)设置这个物品的一些定义信息。最后用register方法将这个物品注册进游戏，注意注册后你不能对该物品再次修改，这样一个自定义物品就做好了。材质放在\resources\contenttweaker\textures\items文件夹，文件名与物品ID一致。

本地化key为`item.contenttweaker.物品ID.name`

以下为基础的ZenProperties（剩余的基本无用或需要函数参数，为高级运用，将在之后讲解）

| 名称 | 类型 | 默认值 | 描述 |
| :--- | :--- | :--- | :--- |
| beaconPayment | bool | false | 是否可以丢进信标里 |
| creativeTab | ICreativeTab | 杂项创造标签 | 设置物品所在创造标签，记得/ct creativetab指令 |
| glowing | bool | false | 是否有附魔光芒 |
| maxDamage | int | -1 | 设置物品耐久，小于0则为普通物品，大于0将会被当作工具 |
| maxStackSize | int | 64 | 设置物品最大堆叠数 |
| rarity | EnumRarity | COMMON | 设置物品稀有度，会影响物品显示名称的颜色，可以使用\(“COMMON”, “UNCOMMON”, “RARE”, “EPIC”\)以下某一个 |
| toolClass | string | null | 设置这是什么工具（pickaxe镐 axe斧等等）貌似sword剑不能 |
| toolLevel | int | -1 | 设置工具挖掘等级 |

示例脚本

```csharp
#loader contenttweaker
import mods.contenttweaker.VanillaFactory;
import mods.contenttweaker.Item;

val zsItem as Item = VanillaFactory.createItem("zs_item");
zsItem.maxDamage = 8848;
zsItem.rarity = "rare";
zsItem.creativeTab = <creativetab:tools>;
zsItem.toolClass = "pickaxe";
zsItem.toolLevel = 5;
zsItem.beaconPayment = true;
zsItem.register();
```
