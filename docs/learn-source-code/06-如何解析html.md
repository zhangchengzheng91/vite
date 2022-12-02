# 如何解析 html 文件

解析 html 文件所经历过的函数，已经具体所做的事情

## transformIndexHtml

/vite/packages/vite/src/node/server/index.ts

应用在 vite 构建过程中，和任意 html 插件转换。

## createDevHtmlTransformFn

/vite/packages/vite/src/node/server/middlewares/indexHtml.ts

dev 环境 html 转化。初始值未 null。

### preImportMapHook

检验 importmap 和 module 的位置

### 自定义 preHook

### devHtmlHook

在 vite 中注入 /@vite/client

源 html 文件解析完之后，会在 head 中插入 client

```html

<head>
  <script type="module" src="/@vite/client"></script>
</head>
```

在 client 中插入了 env.mjs 文件

```js
import '/@fs/Users/bytedance/source-code/vite/packages/vite/dist/client/env.mjs';
```

### postHook

### postImportMapHook

将 moduleScript 替换为 importMap/math

## applyHtmlTransforms

/vite/packages/vite/src/node/plugins/html.ts



