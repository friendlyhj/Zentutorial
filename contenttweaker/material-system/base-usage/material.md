---
description: 材料是一个物品的材质。比如铜、锡、铁...  你需要通过MaterialBuilder对象构建Material类对象。
---

# 材料

## 导入

你需要通过`import mods.contenttweaker.MaterialBuilder;`导入MaterialBuilder对象

通过`import mods.contenttweaker.Material;`导入Material类。

## 获取材料构建器

用MaterialSystem包的getMaterialBuilder方法获取材料构建器。

```javascript
var mBuilder as MaterialBuilder = MaterialSystem.getMaterialBuilder();
```

## 指定参数

你可以用以下方法指定所构建的材料对象的参数

| 方法名 | 参数描述 | 功能 |
| :--- | :--- | :--- |
| setName\(id\) | id 为 字符串 | 设定材料的ID（貌似能用中文，但极不推荐，因为这个ID会影响所注册的材料部件的矿辞名，待会出个`gear铜`矿辞就过草） |
| setColor\(color\) | color为int或CTColor对象 | 设定材料的颜色\(int代表RGB颜色\) |
| setHasEffect\(hasEffect\) | hasEffect为布尔值 | 设定其将来所创建的材料部件是否有附魔光芒（这个方法有bug，只要你调用了这个方法，不管你的参数是什么，所创建的材料部件都会有光芒） |

## 构建

最后你需要对MaterialBuilder使用`build`方法来构建材料，这个方法将会返回一个Material对象。记得用变量储存，以便接下来构建材料部件！

## 实例脚本

```javascript
import mods.contentTweaker.MaterialSystem;
import mods.contenttweaker.MaterialBuilder;
import mods.contenttweaker.Material;

var builder as MaterialBuilder = MaterialSystem.getMaterialBuilder();
builder.setName("Urubuntu");
builder.setColor(0x000151);
builder.setHasEffect(false);
val urubuntu as Material = builder.build();

val arakantara as Material = MaterialSystem.getMaterialBuilder().setName("Arakantara").setColor(15592941).setHasEffect(true).build();
```

## 本地化

本地化key为`base.material.<材料ID>`，如铁的就是 `base.material.iron`

