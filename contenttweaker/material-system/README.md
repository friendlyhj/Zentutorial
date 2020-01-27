# 材料系统

材料系统是CoT一个特殊的包。允许像1.7.10AOBD/1.12.2 JAOPCA一样，一次性添加多个金属的不同部件。比如一次性添加各种金属的小撮粉。

需要`import mods.contenttweaker.MaterialSystem;`导入材料系统包。

一个MaterialPart\(材料部件\)类的对象将会根据其的PartType自动进行相应的注册。我们需要的只是构建出需要的MaterialPart。

以小撮铜粉为例，我们需要的就是铜和小撮粉。所以我们需要一个Material类和一个Part类。下文将对这两个进行讲解。

