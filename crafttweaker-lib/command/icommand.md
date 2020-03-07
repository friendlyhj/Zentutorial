# ICommand

## 导入

`import crafttweaker.command.ICommand;`

## 可用ZenGetter

| 名称 | 类型 | 是否有同名ZenSetter | 描述 |
| :--- | :--- | :--- | :--- |
| name | string | ✘ | 获取该对象参数的命令名（如 `/gamemode 1` 中的 `gamemode` \) |
| aliases | string\[\] | ✘ |  |

## 可用方法

`String getUsage(ICommandSender sender);`

`void execute(IServer server, ICommandSender sender, String[] args);`

`boolean checkPermission(IServer server, ICommandSender sender);`

`string[] getTabCompletions(IServer server, ICommandSender sender, String[] args, @Optional IBlockPos targetPos);`

`boolean isUsernameIndex(String[] args, int index);`

## 可用操作符

* `==`
* `!=`

