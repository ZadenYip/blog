# VS Code 与多个 tsconfig 文件管理的文件的语法提示隔离

## 背景

最近写的项目遇到 VSCode 语法提示的问题。例如，对于 spec.ts 文件，我希望 vitest 的 describe，it 和 expect 等函数使用不用显式 import 而是以注入全局变量的方式，就要给 tsconfig CompilerOptions 的 types 引入 vitest/globals。

然而，全局注入会影响我的其他 ts 文件，就得另外创子 tsconfig 去管理。

此时，项目结构如下：
```
angular-electron/
├── tsconfig.json                      (根配置)
├── app/
│   ├── tsconfig.electron.json
│   └── tsconfig.electron.spec.json
└── src/
    ├── tsconfig.app.json
    └── tsconfig.spec.json
```

接着发现 VSCode TS语法提示只会读取跟目录的 tsconfig.json，可是 TypeScript 使用子 tsconfig 编译时是正常的，没出现 VSCode 语法提示的那些错误。  

## 解决方案

在根目录的 tsconfig.json 添加对所有子 tsconfig 的 references，在子 tsconfig compilerOptions 打开 composite。

tsconfig.json：
```
{
  ...
  "declaration": true, // 使用 refrences (项目引用)，父子 tsconfig 都必须打开这个
  "references": [
    { "path": "./app/tsconfig.electron.json" },
    { "path": "./app/tsconfig.electron.spec.json" },
    { "path": "./src/tsconfig.app.json" },
    { "path": "./src/tsconfig.spec.json" }
  ],
  ...
}
```

各种子 tsconfig：
```
{
  "compilerOptions": {
    "composite": true,
    ...
  }
}
```

配置好后，只要子 tsconfig include 和 files 包含的文件方式是正确的，此时 VS Code 的 TypeScript 语法提示就能正常工作，打开一个文件的类型，函数等提示就是对应的 tsconfig 的设置了。