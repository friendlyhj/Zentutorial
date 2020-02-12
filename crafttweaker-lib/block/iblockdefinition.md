# IBlockDefinition

## 导入

`import crafttweaker.block.IBlockDefinition;`

## 可用ZenGetter

| 名称 | 类型 | 是否有同名ZenSetter | 描述 |
|-----|------|------|------|
|id|string|✘||
|displayName|string|✘||
|lightOpacity|int|只有ZenSetter，无ZenGetter||
|lightLevel|int|只有ZenSetter，无ZenGetter||
|resistance|float|只有ZenSetter，无ZenGetter||
|hardness|float|✔||
|tickRandomly|bool|✔||
|harvestLevel|int|✘||
|harvestTool|string|✘||
|canSpawnInBlock|bool|✘||
|unlocalizedName|string|✘||
|creativeTab|[ICreativeTab](crafttweaker-lib/creativetabs/icreativetab.md)|✔||
|defaultState|[IBlockState](crafttweaker-lib/block/IBlockState.md)|✘||
|defaultSlipperiness|float|只有ZenSetter，无ZenGetter||

## 可用方法

`void setUnbreakable();`

`void setHarvestLevel(String toolClass, int level);`

`boolean canPlaceBlockOnSide(IWorld world, IBlockPos pos, IFacing facing);`

`boolean canPlaceBlockAt(IWorld world, IBlockPos pos);`

`float getSlipperiness(IBlockState state, IBlockAccess access, IBlockPos pos, @Optional IEntity entity);`
