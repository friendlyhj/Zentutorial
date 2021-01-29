# 自定义材料类型

## 导论

假设你需要一个类似 TE 的硬化玻璃的方块，但有一个问题：玻璃是透明的，若要是透明方块的话。需要将 `blockLayer` 设置为 `"CUTOUT"`，还要把 `fullBlock` 属性设置为 `false` 、把 `translucent` 设置为 `true`。否则就算材质是透明的，但最终方块是会像 X 光方块一样透视。而材料系统的 block 材料类型只是一个普通方块，设置不了这些。这个时候我们就需要自定义材料类型。

## 导入

`import mods.contenttweaker.PartType;`

## 创建一个材料类型

创建一个材料类型非常简单，只需要调用 `MaterialSystem.createPartType`方法就行。这个方法会返回 PartType，你把它填进自定义部件时的 `setPartType` 方法就行。
这个方法需要两个参数：一个是材料类型的名字，第二个是 RegisterMaterialPart 函数。这个函数的指定比较麻烦，下章即对这个进行讲解。

## 实例脚本

摘自 wiki。这个脚本只是展示基本格式用法。这个例子由于 RegisterMaterialPart 函数是空的。这个脚本在游戏内不会产生任何变化。

```javascript
#loader contenttweaker

import mods.contenttweaker.MaterialSystem;

val ourType = MaterialSystem.createPartType("cool_type", function(materialPart){

});

//Use the new type to create a Part
val ourPart = mods.contenttweaker.MaterialSystem.getPartBuilder().setName("cool_part").setPartType(ourType).build();

//Create a new Material and register the newly created part.
val ourMaterial = MaterialSystem.getMaterialBuilder().setName("Lawrencium").setColor(15426660).build();
ourMaterial.registerPart(ourPart);
```
