# Electron + BetterSQLite3 踩坑记

Electron 没法直接用 BetterSQLite3，得重新编译

```jsx
Verbose logs are written to:
c:\Users\HyFran\AppData\Roaming\Code\logs\20251114T090023\window1\exthost\ms-vscode.js-debug\vscode-debugadapter-c9fc53fc.json
"XXX/node_modules/.bin/electron.cmd" --serve . --remote-debugging-port=9876
(node:32732) UnhandledPromiseRejectionWarning: Error: The module '\\?\XXX\node_modules\better-sqlite3\build\Release\better_sqlite3.node'
warning:56
was compiled against a different Node.js version using
warning:56
NODE_MODULE_VERSION 137. This version of Node.js requires
warning:56
NODE_MODULE_VERSION 135. Please try re-compiling or re-installing
warning:56
the module (for instance, using `npm rebuild` or `npm install`).
warning:56
    at process.func [as dlopen] (node:electron/js2c/node_init:2:2569)
warning:56
    at Module._extensions..node (node:internal/modules/cjs/loader:1930:18)
warning:56
    at Object.func [as .node] (node:electron/js2c/node_init:2:2569)
warning:56
    at Module.load (node:internal/modules/cjs/loader:1472:32)
warning:56
    at Module._load (node:internal/modules/cjs/loader:1289:12)
warning:56
    at c._load (node:electron/js2c/node_init:2:17950)
warning:56
    at TracingChannel.traceSync (node:diagnostics_channel:322:14)
warning:56
    at wrapModuleLoad (node:internal/modules/cjs/loader:242:24)
warning:56
    at Module.require (node:internal/modules/cjs/loader:1494:12)
warning:56
    at require (node:internal/modules/helpers:135:16)
warning:56
(Use `electron --trace-warnings ...` to show where the warning was created)
warning:56
(node:32732) UnhandledPromiseRejectionWarning: Unhandled promise rejection. This error originated either by throwing inside of an async function without a catch block, or by rejecting a promise which was not handled with .catch(). To terminate the node process on unhandled promise rejection, use the CLI flag `--unhandled-rejections=strict` (see https://nodejs.org/api/cli.html#cli_unhandled_rejections_mode). (rejection id: 1)
```

根据 [Electron官方指引](https://www.electronjs.org/zh/docs/latest/tutorial/using-native-node-modules)，安装 electron-rebuild 重新编译 better-sqlite3 模块

```jsx
# 安装
npm install --save-dev @electron/rebuild
# 在当前 npm 项目运行eletron-rebuild 检测需要重新编译的模块
npx electron-rebuild -f -w bettersqlite3

或者在package.json 添加一个script
"rebuild": "electron-rebuild -f -w better-sqlite3"
```

electron-rebuild -f -w 的 option 见 [electron-rebuild 的 GitHub 仓库](https://github.com/electron/rebuild)