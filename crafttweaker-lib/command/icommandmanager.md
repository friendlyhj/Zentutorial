# ICommandManager

## 导入

`import crafttweaker.command.ICommandManager;`

## 可用ZenGetter

| 名称 | 类型 | 是否有同名ZenSetter | 描述 |
|-----|------|------|------|
|commands|ICommand[string]|✘||

## 可用方法

`int executeCommand(ICommandSender sender, String rawCommand);`

`string列表 getTabCompletions(ICommandSender sender, String input, @Optional IBlockPos pos);`

`ICommand列表 getPossibleCommands(ICommandSender sender);`
