# IBlockProPerties

## 导入

`import crafttweaker.block.IBlockProperties;`

## 可用ZenGetter

| 名称 | 类型 | 是否有同名ZenSetter | 描述 |
| :--- | :--- | :--- | :--- |
| canProvidePower | bool | ✘ |  |
| mobilityFlag | [IMobilityFlag](https://youyi580.gitbook.io/zentutorial/crafttweaker-lib/block/imobilityflag) | ✘ |  |
| material | [IMaterial](https://youyi580.gitbook.io/zentutorial/crafttweaker-lib/block/imaterial) | ✘ |  |
| causesSuffocation | bool | ✘ |  |
| hasCustomBreakingProgress | bool | ✘ |  |
| blockNormalCube | bool | ✘ |  |
| fullBlock | bool | ✘ |  |
| fullCube | bool | ✘ |  |
| normalCube | bool | ✘ |  |
| opaqueCube | bool | ✘ |  |
| useNeighborBrightness | bool | ✘ |  |

## 可用方法

`int getLightValue(IBlockAccess access, IBlockPos pos);`

`int getWeakPower(IBlockAccess access, IBlockPos pos, IFacing facing);`

`int getComparatorInputOverride(IWorld world, IBlockPos pos);`

`boolean canEntitySpawn(IEntity entity);`

`boolean doesSideBlockRendering(IBlockAccess access, IBlockPos pos, IFacing facing);`

`IBlockState getActualState(IBlockAccess access, IBlockPos pos);`

`float getBlockHardness(IWorld world, IBlockPos pos);`

`int getLightOpacity(IBlockAccess access, IBlockPos pos);`

`float getPlayerRelativeBlockHardness(IPlayer player, IWorld world, IBlockPos pos);`

`int getStrongPower(IBlockAccess access, IBlockPos pos, IFacing facing);`

`boolean isSideSolid(IBlockAccess access, IBlockPos pos, IFacing facing);`

