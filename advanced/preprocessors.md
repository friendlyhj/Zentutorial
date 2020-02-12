---
description: 正如其名，预处理器将会在脚本加载前启动。预处理器需要放在脚本最前端。
---

# 预处理器

可用的预处理器

| 预处理器 | 用途 |
| :--- | :--- |
| `#debug` | 打开debug模式，基本不会用到 |
| `#ignoreBracketErrors` | 忽略尖括号引用错误（当物品ID什么的打错不会报错，而是改为`null`） |
| `#loader loaderName` | 设定脚本加载器，默认脚本自带`#loader crafttweaker` |
| `#modloaded modID` | 只有指定的mod加载时这个脚本才会加载，可以设定多个modID，甚至可以取非 |
| `#norun` | 脚本将不会加载，虽然`/ct syntax`还是会检测其的语法错误 |
| `#priority number` | 设定脚本加载优先级，优先级越高越先加载。优先度一样的脚本，将按字母顺序依次加载 |
| `#ikwid` | 该脚本不会产生Warning |

