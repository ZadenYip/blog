# Angular-Electron VSCode 调试配置

之前写 Angular-Electron 相关的项目的时候，上游更新 Angular 版本后，从 Angular 相关文件的打包工具从 webpack 改为了官方的打包工具，但是配置和 VSCode 调试没对应更新，打断点没生效，误打误撞解决了，见[PR](https://github.com/maximegris/angular-electron/pull/849)。  

感觉有时间得研究下 VSCode tasks 的配置和 launch 的配置，小众的项目有时很难找到现成的 VSCode 配置模版（

2026-01-02


继上次后断点其实依然存在一点问题，但是这次是极大概率的偶发性的断点没生效，修复见 [commit](https://github.com/ZadenYip/Todo-Project/commit/2592ab48131c4faf263e1824953e7fa4c42c72a3)

```
    "configurations": [
        {
            "name": "Renderer",
            "type": "chrome",
            "request": "attach",
            "port": 9876,
            "sourceMaps": true,
            "urlFilter": "http://localhost:4200*", // 主要是这一栏
            "timeout": 20000,
            "trace": true,
            "preLaunchTask": "Build.Renderer",
        },
```
给渲染进程的 attach，原本配置是 `url:http://localhost:4200`，但是调试启动 Electron 和 Angular 短时间就关闭了，然后又重新启动，此时断点会有极大概率不生效，非常玄学，但是把这个`url`配置删掉或者改为`"urlFilter": "http://localhost:4200*"`就会正常不受影响了。

2026-01-30