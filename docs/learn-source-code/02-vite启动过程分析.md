# vite 启动过程分析

1. 寻找入口

   node_modules/.bin/vite

2. 获取执行文件路径

   source-code/vite/packages/vite/bin/vite.js

3. 执行启动函数

   start()

4. 导入命令行文件

   ```js
   import('./dist/node/cli.js')
   ```

5. 匹配模式

   cli.parse()

   [root]: start dev server
   build [root]: build for production
   optimize [root]: pre-bundle dependencies
   preview [root]: locally preview production build

   匹配到模式之后执行对应的 action

   this.runMatchedCommand();

6. 启动服务

   输出对应的 service 信息
