---
description: >-
  ZenScript是由MT/CrT提供的新的脚本语言，便于新人使用，也给高级玩家自由发挥的空间。ZenScript是顺序读取，从上往下读取，这意味着。import在脚本最前面，声明变量在脚本较上部。顺便一说，CrT修复了MT脚本不能使用中文的bug。
---

# Zenscript

### scripts文件夹

当你安装了CrT后，你可以在.minecraft文件夹下新建scripts文件夹，里面就是存放你的魔改脚本的地方。这里可以放无限多的脚本，其子文件夹里的脚本也能加载。魔改脚本以zs为后缀名。zs文件是纯文本文件，你可以用任何文本编辑器编辑（notepad++啊，visual studio code啊，等等都可以，不推荐windows自带的记事本），文本编码应为UTF-8（不带BOM），里面标点应该为英文标点。

### print 语句

经典老梗

```javascript
print("hello,world!");
```

print语句将会把里面的内容打印到minecraft文件夹下的crafttweaker.log中，这个文件是crafttweaker的日志文件，能有助于检测错误。在之后的脚本编写中，你应该要使日志只有INFO，没有ERROR和WARN。

### 指令

CraftTweaker的指令可以以`/crafttweaker`、`/ct`、`/minetweaker`和`/mt`中任一个开头

以下为常用的指令

| 命令 | 用途 |
| :--- | :--- |
| /ct help | 查看指令帮助 |
| /ct conflict | 在日志中打印冲突配方 |
| /ct docs | 打开CrT的wiki |
| **/ct hand** | 打印你手中的物品ID和所在矿辞，以zs的尖括号引用方式，同时将物品ID导入剪贴板 |
| **/ct syntax** | 检查脚本是否有错误（能检测语法错误，少部分空指针异常和类型转换异常） |
| /ct reload | 重载脚本功能已死，勿念（会指向一个链接，说为啥重载脚本没了）现在重新加载脚本只能重启游戏。 |
| **/ct inventory** | 打印物品栏的所有物品ID至日志 |
| **/ct liquids** | 打印所有流体及其信息至日志 |
| /ct seeds | 打印所有打草掉落物及其权重至日志 |
| /ct names display | 打印所有物品ID及其名称至日志 |

### 注释

注释能使你的脚本更易读。

单行注释以// 或 \#（建议用//，\#可能与预处理器冲突）开头，区块注释以`/*`开头，`*/`结尾

```javascript
// 我是一行单行注释.
// print("green");  <= 注释会使语句不再加载。
# 我也是一行单行注释
/* 我是
区块
注释哒！
*/
```

### 编排脚本的建议

建议把不同mod的物品的合成修改放在不同mod。比如Vanilla.zs ic2.zs mekanism.zs thermal.zs等等。由于一些特殊原因，也会分开脚本。实际按照个人喜好和具体情况而定。

