# 流体

需要`import mods.contenttweaker.Fluid;`导入有关包。原版加工厂包也需要导入！

用`val testFluid as Fluid = VanillaFactory.createFluid(字符串流体ID, int表示RGB模式颜色);`呼出一个流体类的一个实例，并存储在某个变量中，以做接下来的修改。ID必须全小写，可以包含数字和下划线\_ ，必须字母开头。

流体的材质会根据所给的用颜色参数进行染色，让你方便制作出各种颜色的“水”或“熔岩”，而不用设定材质。

本地化的key为`fluid.流体ID`

可用的ZenProperties

| 名称 | 类型 | 默认值 | 描述 |
| :--- | :--- | :--- | :--- |
| density | int | 1000 | 密度，决定实体在其游泳速度，水为1000，熔岩为3000 |
| luminosity | int | 0 | 流体亮度 |
| temperature | int | 300 | 流体温度，水为300，熔岩为1300 |
| viscosity | int | 1000 | 流体黏度，决定流体流动速度，水为1000，熔岩为3000 |
| vaporize | bool | false | 在下界是否会蒸发 |
| colorize | bool | true | 实际材质是否受颜色参数影响 |
| stillLocation | string | "contenttweaker:fluids/fluid" | 设定源头材质路径，建议类似水的设置为"base:fluids/liquid"，类似熔岩设置为"base:fluids/molten" |
| flowingLocation | string | "contenttweaker:fluids/fluid\_flow" | 设定流动流体的材质路径，建议类似水的设置为"base:fluids/liquid\_flow"，类似熔岩设置为"base:fluids/molten\_flowing" |
| material | IMaterialDefinition | `<blockmaterial:water>` | 建议类似水的设置为`<blockmaterial:water>`，类似熔岩设置为`<blockmaterial:lava>` |
| gaseous | bool | false | 流体是否反重力流动 |

示例脚本

```csharp
#loader contenttweaker
import mods.contenttweaker.VanillaFactory;
import mods.contenttweaker.Fluid;

var zsFluid as Fluid = VanillaFactory.createFluid("zs_fluid", 0xFF69B4);
zsFluid.temperature = 500;
zsFluid.viscosity = 1500;
zsFluid.density = 1500;
zsFluid.luminosity = 4;
zsFluid.stillLocation = "base:fluids/liquid";
zsFluid.flowingLocation = "base:fluids/liquid_flow";
zsFluid.register();
```

