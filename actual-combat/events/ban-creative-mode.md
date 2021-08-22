# 禁止开创造

```csharp
import crafttweaker.events.IEventManager;
import crafttweaker.event.CommandEvent;

events.onCommand(function(event as CommandEvent){
   if (!event.commandSender.world.remote && event.command.name == "gamemode" 
       && (event.parameters in "1" || event.parameters in "creative")) {
       // event.command.name 获取命令名
       // event.parameters 为包含命令参数的字符串数组
       // in操作符检查一个字符串数组是否有某个元素
       event.cancel(); //取消事件
   } 
});
```

