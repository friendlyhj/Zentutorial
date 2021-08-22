# 修改方块掉落物

看似简单的修改，实则事件运用



```csharp
import crafttweaker.events.IEventManager;
import crafttweaker.event.BlockHarvestDropsEvent;
import crafttweaker.block.IBlock;
import mods.ctutils.utils.Math;

events.onBlockHarvestDrops(function(event as BlockHarvestDropsEvent) {
    // 该事件由方块破坏满足挖掘等级，将有掉落物时触发
    // event.drops为WeightedItemStack数组 ZenGetter & ZenSetter，修改其即可修改掉落物。
    // WeightedItemStack有stack ZenGetter 返回 IItemStack
    // 可用event.player获取挖掘的玩家对象
    // 可用event.isPlayer检测是否为玩家挖掘方块触发该事件，而不是TNT啥的。
    if (!event.world.remote) { // world.remote
        // 跳过挖方块无掉落和精准的情况
        if (event.drops.length == 0 || event.silkTouch) {
            return; 
        }
        val block as IBlock = event.block; // 获取所挖的方块
        if (block.definition.id == "minecraft:wool" && block.meta == 13) { // 检测方块ID与metadata
            event.drops = [<item:minecraft:apple> % 100]; // 修改方块掉落物
            event.addItem(<item:minecraft:arrow> * 2 % 20); // 添加方块掉落物
        } else if (<ore:oreIron> in event.drops[0].stack) { // 若所挖的方块符合一个矿辞，要求该方块原来是掉落其本身
            val fortune as int = event.fortuneLevel; // 时运附魔等级
            if (fortune == 0) {
                event.drops = [<item:minecraft:iron_ingot> % 100];
            } else {
                // 时运支持，这里的例子为掉落物品数量为1 ~ 附魔等级，你可以按照你想要的通过获取的附魔等级参数修改逻辑
                event.drops = [<item:minecraft:iron_ingot> * Math.ceil(Math.random() * fortune) % 100];
            }
        } /* else if(...) {
            ...  继续修改
        } */
    }
});
```

