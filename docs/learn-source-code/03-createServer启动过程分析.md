# createServer 启动过程分析

1. 收集所有配置

  ```js
  config = {
    css: {}, // 自定义 css 配置
    resolve: {
      alias: [
        {
          find: 'Common',
          replacement: '/packages/common_package'
        }
      ]
    },
    build: {
      input: {}
    },
    plugins: [  // 所有插件
      {
        name: 'vite:pre-alias'
      }, {
        name: 'alias',
      }, {
        name: 'xxx',
        enforce: 'pre', // 自定义前置插件
      }, {
        name: 'vite:modulepreload-polyfill',
      }, {
        name: 'vite:optimized-deps'
      }, {
        name: 'vite:resolve',
      }, {
        name: 'vite:html-inline-proxy',
      }, {
        name: 'vite:css',
      }, {
        name: 'vite:esbuild',
      }, {
        name: 'vite:json'
      }, {
        name: 'vite:wasm-helper',
      }, {
        name: 'vite:worker',
      }, {
        name: 'vite:asset',
      }, {
        name: 'xxx', // 自定义插件
      }, {
        name: 'vite:wasm-fallback'
      }, {
        name: 'vite:css-post',
      }, {
        name: 'vite:worker-import-meta-url',
      }, {
        name: 'vite:dynamic-import-vars',
      }, {
        name: 'vite:import-glob',
      }, {
        name: 'vite:client-inject',
      }, {
        name: 'vite:import-analysis',
      }
    ],
    server: {},
    configFile: '', // --config 文件的绝对路径
    optimizeDeps: '',
    configFileDependencies: [],
    inlineConfig: { // 命令行参数
      configFile: '', // --config
      logLevel: undefined,
      server: {
        force: true, // 依赖不使用缓存
      }
    },
    root: '',
    base: '',
    publicDir: '',
    cacheDir: '/Users/bytedance/workspace/business_platform/node_modules/.vite',
    command: 'serve',
    mode: 'development',
    ssr: {},
    isWorker: false,
    mainConfig: null,
    isProduction: false,
    preview: {},
    env: {
      BASE_URL: '/',
      MODE: 'development',
      DEV: true,
      PROD: false
    },
    assetsInclude: 'function',
    logger: {
      hasWarned: false,
      info: 'info',
      warn: 'warn',
      warnOnce: 'warnOnce',
      error: 'error',
      clearScreen: 'clearScreen',
      hasErrorLogged: 'hasErrorLogged'
    },
    packageCache: Map,
    createResolver: 'function',
    worker: {
      format: 'iife',
      plugins: [], // 默认 plugin，不包含 config 文件中的 plugin
      rollupOptions: {},
      getSortedPlugins: 'function',
      getSortedPluginHooks: 'function'
    },
    appType: 'spa',
    experimental: {
      importGlobRestoreExtension: false,
      hmrPartialAccept: false
    },
    getSortedPlugins: 'function',
    getSortedPluginHooks: 'function'
  }
  ```

1. vite 中的 server
　
vite 中的 server 是基于 nodejs 原生的 api 创建的

/vite/packages/vite/src/node/http.ts -> resolveHttpServer

1. 服务请求之后，开始处理请求

viteServer 的核心中间件：transformMiddleware.

/vite/packages/vite/src/node/server/middlewares/transform.ts


为什么会请求 map 文件呢？

clearUrl 可能存在的问题：

如果前端的 url 是用 hash 实现的，这里会不会有坑？

/vite/packages/vite/src/node/utils.ts -> clearUrl
