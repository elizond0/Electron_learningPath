# Electron_learningPath

## 1. [Electron 官方中文文档](https://electronjs.org/docs)

## 2. 初始化与安装

- Electron 可以使用 npm 或 yarn 包管理工具进行安装或者初始化

```js
// 初始化项目，生成package.json
npm init

// 项目内安装
npm install electron --save-dev

// 全局安装,需要配环境变量
npm install electron -g
```

- 自定义镜像:使用 electron-download 的网址

```js
// 淘宝镜像：
ELECTRON_MIRROR = "https://npm.taobao.org/mirrors/electron/";
url = ELECTRON_MIRROR + ELECTRON_CUSTOM_DIR + "/" + ELECTRON_CUSTOM_FILENAME;
```

- 本地缓存，手动下载相应版本的 zip 压缩包，放入以下文件中

  - Linux: \$XDG_CACHE_HOME or ~/.cache/electron/
  - MacOS: ~/Library/Caches/electron/
  - Windows: \$LOCALAPPDATA/electron/Cache or ~/AppData/Local/electron/Cache/
  - 在使用旧版本 Electron 的环境中，也可以在~/.electron 中找到缓存。（例如 windows，C:\用户\用户名\\.electron）

- 配置 package，在 package.json 中修改 scripts 对象，例如配置字段名 start，对应值"electron ."，如果是 node 应用则改成"node ."
- main.js 作为入口文件，如果没有查找到 main，则会自动寻找 index.js，main 中应该要创建窗口并且配置 html 首页
- 在 main.js 中配置的 html 首页中，可以写入 html/css/js 代码，就如同网页应用那样。

## 3. 应用程序打包

- 第三方打包工具：[electron-forge](https://electronforge.io/) 和 [electron-builder](https://github.com/electron-userland/electron-builder)

## 4. VS code 调试

- 添加一个 .vscode/launch.json 文件并使用以下配置：

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Debug Main Process",
      "type": "node",
      "request": "launch",
      "cwd": "${workspaceRoot}",
      "runtimeExecutable": "${workspaceRoot}/node_modules/.bin/electron",
      "windows": {
        "runtimeExecutable": "${workspaceRoot}/node_modules/.bin/electron.cmd"
      },
      "args": ["."],
      "outputCapture": "std"
    }
  ]
}
```

- 在入口 main.js 文件中，设置断点，启动 VS code 调试功能即可
