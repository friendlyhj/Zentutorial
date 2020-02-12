# IBlockState

## 导入

`import crafttweaker.block.IBlockState;`

## 拓展

IBlockState类拓展了[IBlockProperties](iblockproperties.md)和[IBlockStateMatcher](iblockstatematcher.md)类

## 可用ZenGetter

| 名称 | 类型 | 是否有同名ZenSetter | 描述 |
|-----|------|------|------|
|block|[IBlock](iblock.md)|✘||
|meta|int|✘||

## 可用方法

`boolean isReplaceable(IWorld world, IBlockPos blockPos);`

`IBlockState withProperty(String name, String value);`

`String列表 getPropertyNames();`

`String getPropertyValue(String name);`

`String列表 getAllowedValuesForProperty(String name);`

`string[string] getProperties();`

`IBlockStateMatcher matchBlock();`

`static IBlockState getBlockState(String blockname, String[] properties)`

## 可用操作符

`==`
