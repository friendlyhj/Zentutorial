# 方块

需要`import mods.contenttweaker.Block;`导入有关包。原版加工厂包也需要导入！

用`val testBlock as Block = VanillaFactory.createBlock(字符串方块ID, BlockMaterial);`创建一个「即将」加入进游戏的方块，并存储在某个变量中，以做接下来的修改。ID必须全小写，可以包含数字和下划线\_ ，必须字母开头。 设定的BlockMaterial将会影响方块的一些特性。

接下来操作与物品类似。材质放在\resources\contenttweaker\textures\blocks文件夹，文件名与物品ID一致。

本地化key为`tile.contenttweaker.方块ID.name`

可用的ZenProperties\(其它基本无用，或为事件高级运用\)

| 名称 | 类型 | 默认值 | 描述 |
| :--- | :--- | :--- | :--- |
| axisAlignedBB | MCAxisAlignedBB | 完整方块 | 设置方块碰撞箱 |
| beaconBase | bool | false | 是否可作为信标基座 |
| blockHardness | float | 5.0 | 方块硬度 |
| blockLayer | string | "SOLID" | 可用“SOLID”, “CUTOUT\_MIPPED”, “CUTOUT”, “TRANSLUCENT”之一。渲染类似冰的半透明请用 TRANSLUCENT，类似玻璃的请用 CUTOUT_MIPPED 或 CUTOUT|
| blockResistance | float | 5.0 | 方块防爆等级 |
| blockSoundType | SoundType | `<soundtype:metal>` | 设置方块声音，方块放置破坏时的声音，记得记得/ct soundtype指令 |
| creativeTab | ICreativeTab | 杂项创造标签 | 设置物品所在创造标签，记得/ct creativetab指令 |
| dropHandler | IBlockDropHandler | null | 函数，用于设定方块掉落物 |
| entitySpawnable | bool | true | 生物是否可以在这个方块上生成 |
| enumBlockRenderType | string | "MODEL" | 可用“INVISIBLE”, “LIQUID”, “ENTITYBLOCK\_ANIMATED”, “MODEL” 其中之一，用于设定这个方块如何渲染 |
| fullBlock | bool | true | 是否为完整方块，用于渲染和光照计算 |
| gravity | bool | false | 是否受重力影响 |
| lightOpacity | bool | 如果fullBlock为true则为255，反之为0 | 设置不透明度，用于光照计算 |
| lightValue | int | 0 | 设置方块光照等级，最大为15 |
| passable | bool | 取决于设定的BlockMaterial | 玩家是否可通过这个方块 |
| replaceable | bool | 取决于设定的BlockMaterial | 玩家是否可直接替换这个方块，比如原版的草 |
| slipperiness | float | 0.6 | 设置方块滑度，冰为0.98 |
| toolClass | string | "pickaxe" | 设置方块需要什么工具挖掘 |
| toolLevel | int | 2 | 设置方块需要多少挖掘等级 |
| translucent | bool | false | 方块是否为（半）透明 |
| witherProof | bool | false | 方块是否可抵御凋灵爆炸 |

示例脚本

```csharp
#loader contenttweaker

import mods.contenttweaker.VanillaFactory;
import mods.contenttweaker.Block;

var antiIceBlock as Block = VanillaFactory.createBlock("anti_ice", <blockmaterial:ice>);
antiIceBlock.lightOpacity = 3;
antiIceBlock.LightValue = 0;
antiIceBlock.blockHardness = 1.0;
antiIceBlock.blockResistance = 5.0;
antiIceBlock.toolClass = "pickaxe";
antiIceBlock.toolLevel = 0;
antiIceBlock.blockSoundType = <soundtype:snow>;
antiIceBlock.slipperiness = 0.75;
antiIceBlock.register();
```
