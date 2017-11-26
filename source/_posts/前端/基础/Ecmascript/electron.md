---
title: electron
toc: true
date: 2017-10-30  10:56:50
tags: [前端, electron, JS基础]
---

## electron

### 知识点

electron

### 背景资料

> 使用 JavaScript，HTML 和 CSS 构建跨平台桌面应用程序.基于 Node.js 和 Chromium 开发的, Atom editor 以及很多其他的 apps 就是使用 electron 编写的。

> 集成 Node 来授予网页访问底层系统的权限。



### electron入门

全局安装 electron

 ` npm install electron -g `
 
 ` yarn add electron -g `

##### 主进程

主进程，通常是一个命名为 main.js 的文件，该文件是每个 electron 应用的入口。它控制了应用的生命周期（从打开到关闭）。它既能调用原生元素，也能创建新的（多个）渲染进程。另外，Node API 是内置其中的。

![imgn](http://haoqiao.qiniudn.com/1460000007503499.png)

#### 渲染进程

 > 由于 electron 使用 Chromium 来展示页面，所以 Chromium 的多进程结构也被充分利用。每个 electron 的页面都在运行着自己的进程，这样的进程我们称之为渲染进程。在一般浏览器中，网页通常会在沙盒环境下运行，并且不允许访问原生资源。然而，electron 用户拥有在网页中调用 io.js 的 APIs 的能力，可以与底层操作系统直接交互。

渲染进程是应用的一个浏览器窗口。与主进程不同，它能存在多个（注：一个 electron 应用只能存在一个主进程）并且相互独立（它也能是隐藏的）。主窗口通常被命名为 index.html。它们就像典型的 HTML 文件，但 electron 赋予了它们完整的 Node API。因此，这也是它与浏览器的区别.

![imgn](http://haoqiao.qiniudn.com/1460000007503500.png)

#### 主进程与渲染进程的区别

主进程使用 BroswerWindow 实例创建网页。每个 BroswerWindow 实例都在自己的渲染进程里运行着一个网页。当一个 BroswerWindow 实例被销毁后，相应的渲染进程也会被终止。主进程管理所有页面和与之对应的渲染进程。每个渲染进程都是相互独立的，并且只关心他们自己的网页。由于在网页里管理原生 GUI 资源是非常危险而且容易造成资源泄露，所以在网页面调用 GUI 相关的 APIs 是不被允许的。如果你想在网页里使用 GUI 操作，其对应的渲染进程必须与主进程进行通讯，请求主进程进行相关的 GUI 操作。

![imgn](http://haoqiao.qiniudn.com/1460000007503501.png)

#### 相互通讯

>由于主进程和渲染进程各自负责不同的任务，而对于需要协同完成的任务，它们需要相互通讯。IPC就为此而生，它提供了进程间的通讯。但它只能在主进程与渲染进程之间传递信息（即渲染进程之间不能进行直接通讯）。

![imgn](http://haoqiao.qiniudn.com/1460000007503502.png)

`主进程和渲染进程各自拥有一个 IPC 模块。`


![imgn](http://haoqiao.qiniudn.com/1460000007503503.png)

### 开发环境配置

调试工具[ DevTools ](https://github.com/electron/devtron)

官网提供[ Quick Start ](https://github.com/electron/electron-quick-start)

但是我们项目都是根据自己采用的框架和库来开发。

因此不建议使用，推荐社区已经封装好的[ boilerplates ](https://electron.atom.io/community/#boilerplates)

或者直接根据你的需求去 GitHub 上搜索对应的开发环境。

#### 打包

应用构建完成后，可以通过 命令行工具 electron-packager 对其打包为适用于 Mac 、Windows 和 Linux 的应用。当然，你可以在 package.json 添加该命令行。查看下面相关资源，学习如何将应用发布到 Mac 和 Windows 的 App Store。


> [Mac App Store Electron Guide](http://electron.atom.io/docs/tutorial/mac-app-store-submission-guide/)


> [Windows App Store Electron Guide](http://electron.atom.io/docs/tutorial/windows-store-guide/)


### 从零构建一个多平台应用

直接 clone React 的[开发环境](electron-react-boilerplate)

```

First, clone the repo via git:

git clone --depth=1 https://github.com/chentsulin/electron-react-boilerplate.git your-project-name
And then install dependencies with yarn.

$ cd your-project-name
$ yarn

```

这个过程很慢，而且有时候你需要全局翻墙0-0

然后会发现卡在 ` electron node install.js `上

解决方案如下:

```

编辑 ~/.npmrc 加入下面内容

electron_mirror=https://npm.taobao.org/mirrors/electron/

```

安装完成之后执行` yarn run dev `

![imgn](http://haoqiao.qiniudn.com/electron1.gif)

### 小结

electron 虽然也能开发一些应用，但是环境配置实在蛋疼，而且开发环境不稳定。因此使用还需谨慎~作为玩具它也很让人糟心~

### 资料

> [ electron 官方中文文档](https://github.com/electron/electron/tree/master/docs-translations/zh-CN)

> [通过 electron 开发一个简单地桌面应用](https://juejin.im/entry/56aae5e4a633bd0257ae4ab8)

> [用 electron 打造跨平台前端 App](http://web.jobbole.com/86509/)

> [ electron 深度实践总结](https://changkun.us/archives/2017/03/217/)

