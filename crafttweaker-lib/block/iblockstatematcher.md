# IBlockStateMatcher

## 导入

`import crafttweaker.block.IBlockStateMatcher;`

## 可用ZenGetter

| 名称 | 类型 | 是否有同名ZenSetter | 描述 |
|-----|------|------|------|
|commandString|string|✘||

## 可用方法

`Collection<IBlockState> getMatchingBlockStates();`

`IBlockStateMatcher allowValuesForProperty(String name, String[] values);`

`IBlockStateMatcher withMatchedValuesForProperty(String name, String[] values);`

`string列表 getMatchedValuesForProperty(String name);`

`string[][string] getMatchedProperties();`

`boolean isCompound();`

## 可用操作符

* `in/has`
* `|`
