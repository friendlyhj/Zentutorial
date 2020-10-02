# RegisterMaterialPart

`RegisterMaterialPart` 是一个由 `MaterialPart` 为参数的函数。它用来告诉游戏如何把构建出的 `MaterialPart` 注册进游戏的实际内容。本文以一个金属框架为例。

注意：现在你是从头造轮子，所以现成的习以为常的功能，你需要从头写！下面会一一阐述。

它的结构在上章已经有所说明：

```javascript
function(materialPart){
    // ...
});
```

## 关于 MaterialPart

`MaterialPart` 是由 `Material` 和 `Part` 组成的。你可以用 `getMaterial` 和 `getPart` 来获取组成这个材料部件的材料和部件。
关于这个类，更多内容见[官方文档](https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Materials/Materials/MaterialPart/)

## 调用原版加工厂

想要往游戏里注册添加东西，那必须只能是原版加工厂了。我们现在需要框架，是个方块。 所以用 `createBlock` 方法。

```javascript
// import 和函数声明部分从略
val materialName as string = materialPart.getMaterial().getName();
val frame as Block = MaterialPart.createBlock("frame_" ~ materialName.toLowerCase(), <blockmaterial:iron>)
```

你会发现我们对方块 ID 进行了字符串拼接。很明显，我们添加的方块 ID 是不能重复的。最好的方法就是根据 `MaterialPart` 的材料的名字来给所要注册的物品/方块确定名字。例子所中的就是铜框架材料部件将会注册一个 ID 为 frame_copper 的方块。然后你就可以像添加普通方块修改所需的其他 ZenProperty.

## 确定基底材质以及染色

对的，材料系统最经典的功能，你需要从头再写。这里我们需要设定 `textureLocation` `itemColorSupplier` `blockColorSupplier` ZenProperties 来指定基底材质和染色。

```javascript
// 确定基底材质路径于 contenttweaker:blocks/frame.png
// 把所需的材质文件名为 frame.png 放到 /resources/contenttweaker/textures/blocks 中
frame.textureLocation = mods.contenttweaker.ResourceLocation.create("contenttweaker:blocks/frame");

// 设定物品染色器
// 需要返回一个 Color 对象
// @See {https://docs.blamejared.com/1.12/en/Mods/ContentTweaker/Vanilla/Types/Color/Color/}
// 我们直接返回材料部件的颜色就好
// 这个写法由于 CraftTweaker/CraftTweaker#972 的修复而成为了可能
// 如果你使用这个造成了游戏崩溃，请更新下你的 CrT
frame.itemColorSupplier = function(item, tintindex) {
    return materialPart.getCTColor();
};

// 设定方块染色器
// 与物品同理
// 当然如果你自定义的材料类型是个物品的话，就不需要这个了
frame.blockColorSupplier = function(state, access, pos, tintIndex) {
    return materialPart.getCTColor();
};
```

## 本地化

材料系统的另外一个特点，就是自动确定本地化名。你也会发现，我们是注册了一个个单独方块，有各自的 ID，不像预设的材料类型只占用一个 ID，而以 meta 区分。所以你会发现注册的方块的非本地化名（也就是本地化所需要的 key）也是不同的，跟随原版加工厂添加方块的本地化 key: `tile.contenttweaker.方块ID.name`

你自然可以再用语言文件进行本地化，但或许会过于繁琐了。用 CrT 自带的设定物品名称功能更好。(记得另开脚本！)

为了使用方便，使用了 [ZenUtils](https://www.curseforge.com/minecraft/mc-mods/zenutil)

```javascript
import mods.zenutils.StaticString;

for item in itemUtils.getItemsByRegexRegistryName("^contenttweaker:block_frame_.*") {
    val materialName as string = item.definition.id.substring("contenttweaker:block_frame_".length);
    item.displayName = StaticString.format(game.localize("contenttweaker.part.frame"), [game.localize("base.material." ~ materialName)]);
}
```
