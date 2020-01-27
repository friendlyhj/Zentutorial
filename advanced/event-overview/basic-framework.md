# 基本框架



最好先用`import crafttweaker.events.IEventManager;`导入有关包

你需要用一个函数描述事件，并告诉CraftTweaker要干什么。最重要的是**构建正确类型的事件**，否则你不能访问ZenGetter

```javascript
import crafttweaker.events.IEventManager; //导入事件管理器
import crafttweaker.event.PlayerCraftedEvent //导入玩家合成事件的类

//使用events全局关键词调用事件管理器，并使用一个ZenMethod指定使用的事件，在函数头将事件匹配至PlayerCraftedEvent
events.onPlayerCrafted(function(event as PlayerCraftedEvent){
    event.player.xp += 1; //玩家+1经验
});
```

你可以使用这些事件

| ZenMethod | 对应的类 |
| :--- | :--- |
| onAllowDespawn | [`crafttweaker.event.EntityLivingSpawnEvent`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/EntityLivingSpawn/) |
| onBlockBreak | [`crafttweaker.event.BlockBreak`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/BlockBreak/) |
| onBlockHarvestDrops | [`crafttweaker.event.BlockHarvestDrops`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/BlockHarvestDrops/) |
| onCheckSpawn | [`crafttweaker.event.EntityLivingExtendedSpawnEvent`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/EntityLivingSpawn/) |
| onCommand | [`crafttweaker.event.CommandEvent`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/CommandEvent/) |
| onEnderTeleport | [`crafttweaker.event.EnderTeleportEvent`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/EnderTeleport/) |
| onEntityLivingAttacked | [`crafttweaker.event.EntityLivingAttackedEvent`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/EntityLivingAttacked/) |
| onEntityLivingDeath | [`crafttweaker.event.EntityLivingDeathEvent`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/EntityLivingDeath/) |
| onEntityLivingDeathDrops | [`crafttweaker.event.EntityLivingDeathDropsEvent`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/EntityLivingDeathDrops/) |
| onEntityLivingFall | [`crafttweaker.event.EntityLivingFallEvent`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/EntityLivingFall/) |
| onEntityLivingHurt | [`crafttweaker.event.EntityLivingHurtEvent`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/EntityLivingHurt/) |
| onEntityLivingJump | [`crafttweaker.event.EntityLivingJumpEvent`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/EntityLivingJump/) |
| onEntityLivingUseItem | [`crafttweaker.event.EntityLivingUseItemEvent.All`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/LivingEntityUseItem/) |
| onEntityLivingUseItemFinish | [`crafttweaker.event.EntityLivingUseItemEvent.Finish`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/LivingEntityUseItem/) |
| onEntityLivingUseItemStart | [`crafttweaker.event.EntityLivingUseItemEvent.Start`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/LivingEntityUseItem/) |
| onEntityLivingUseItemStop | [`crafttweaker.event.EntityLivingUseItemEvent.Stop`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/LivingEntityUseItem/) |
| onEntityLivingUseItemTick | [`crafttweaker.event.EntityLivingUseItemEvent.Tick`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/LivingEntityUseItem/) |
| onEntityStruckByLightning | [`crafttweaker.event.EntityStruckByLightningEvent`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/EntityStruckByLightning/) |
| onItemExpire | [`crafttweaker.event.ItemExpireEvent`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/ItemExpire/) |
| onItemToss | [`crafttweaker.event.ItemTossEvent`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/ItemToss/) |
| onPlayerAdvancement | [`crafttweaker.event.PlayerAdvancement`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/PlayerAdvancement/) |
| onPlayerAnvilRepair | [`crafttweaker.event.PlayerAnvilRepair`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/PlayerAnvilRepair/) |
| onPlayerAttackEntity | [`crafttweaker.event.PlayerAttackEntityEvent`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/PlayerAttackEntity/) |
| onPlayerBonemeal | [`crafttweaker.event.PlayerBonemealEvent`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/PlayerBonemeal/) |
| onPlayerBreakSpeed | [`crafttweaker.event.PlayerBreakSpeed`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/PlayerBreakSpeed/) |
| onPlayerBrewedPotion | [`crafttweaker.event.PlayerBrewedPotion`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/PlayerBrewedPotion/) |
| onPlayerChangedDimension | [`crafttweaker.event.PlayerChangedDimensionEvent`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/PlayerChangedDimension/) |
| onPlayerCrafted | [`crafttweaker.event.PlayerCraftedEvent`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/PlayerCrafted/) |
| onPlayerDeathDrops | [`crafttweaker.event.PlayerDeathDropsEvent`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/PlayerDeathDrops/) |
| onPlayerDestroyItem | [`crafttweaker.event.PlayerDestroyItem`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/PlayerDestroyItem/) |
| onPlayerFillBucket | [`crafttweaker.event.PlayerFillBucketEvent`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/PlayerFillBucket/) |
| onPlayerInteract | [`crafttweaker.event.PlayerInteractEvent`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/PlayerInteract/) |
| onPlayerInteractBlock | [`crafttweaker.event.PlayerInteractBlockEvent`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/PlayerInteractBlock/) |
| onPlayerInteractEntity | [`crafttweaker.event.PlayerInteractEntityEvent`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/PlayerInteractEntity/) |
| onPlayerLoggedIn | [`crafttweaker.event.PlayerLoggedInEvent`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/PlayerLoggedIn/) |
| onPlayerLoggedOut | [`crafttweaker.event.PlayerLoggedOutEvent`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/PlayerLoggedOut/) |
| onPlayerOpenContainer | [`crafttweaker.event.PlayerOpenContainerEvent`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/PlayerOpenContainer/) |
| onPlayerPickupItem | [`crafttweaker.event.PlayerPickupItemEvent`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/PlayerPickupItem/) |
| onPlayerPickupXp | [`crafttweaker.event.PlayerPickupXpEvent`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/PlayerPickupXp/) |
| onPlayerRespawn | [`crafttweaker.event.PlayerRespawnEvent`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/PlayerRespawn/) |
| onPlayerSetSpawn | [`crafttweaker.event.PlayerSetSpawn`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/PlayerSetSpawn/) |
| onPlayerSleepInBed | [`crafttweaker.event.PlayerSleepInBedEvent`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/PlayerSleepInBed/) |
| onPlayerSmelted | [`crafttweaker.event.PlayerSmeltedEvent`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/PlayerSmelted/) |
| onPlayerTick | [`crafttweaker.event.PlayerTickEvent`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/PlayerTick/) |
| onPlayerUseHoe | [`crafttweaker.event.PlayerUseHoeEvent`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/PlayerUseHoe/) |
| onSpecialSpawn | [`crafttweaker.event.EntityLivingExtendedSpawnEvent`](https://crafttweaker.readthedocs.io/en/latest/#Vanilla/Events/Events/EntityLivingSpawn/) |

