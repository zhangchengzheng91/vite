# 如何解析 script 文件

所有 js，tsx，scss，vue，node_modeules 相关的文件，都会进入这个函数

## transformRequest


## doTransform



## loadAndTransform

直接 load 源文件，不做任何处理先

将文件通过 pluginContainer.transform 进行 transform 转换

在 transform 转换的过程中，核心工作就是将 code 在所有的 plugin.transform 的函数走一遍。便利的顺序和 plugin 在config 中的顺序保持一致。

