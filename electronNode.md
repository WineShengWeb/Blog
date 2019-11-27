<!--
 * @Author: guoxinggang<guoxinggang@gsaxns.com>
 * @Version: 1.0
 * @Date: 2019-09-02 16:50:40
 * @LastEditTime: 2019-09-10 17:47:25
 * @Description: 
 -->

# Electron 学习笔记

#### 简介

Electron是一个使用js来开发跨平台桌面端软件的一个框架，可以通过一套代码在不同的平台打包成不同的桌面应用程序。

比较著名的产品包括：VS code、skype、atom、钉钉、SwitchHosts!

#### 特点

- electron的原理是把chromium的v8引擎和node的运行时结合到了一起。

- 架构还是前后端分离

- 前端按照web开发的方式正常开发

- 通信原理：每一个前端窗口是一个进程，后端单独是一个进程。electron提供前后端进程间通信的接口。

#### 原理

基于Chromium和node.js开发。

Chromium：利用chromium内核执行HTML、CSS、JS代码，可以得到一个图形化界面。

node.js：提供功能，执行一些功能性的js脚本代码，可以读写文件。

因为Electron使用的是Chromium内核，所以开发者不用考虑兼容问题。

示意图：
![示意图](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91c2VyLWdvbGQtY2RuLnhpdHUuaW8vMjAxOS82LzEwLzE2YjNkMWM5NzdkOGQ3MjI)

#### 开发流程

1. 安装Electron

- windows 环境变量设置
    在开始安装前，先设置好环境变量，直接安装会报错，因为是国外资源，在国内访问不到，需要换成国内的淘宝镜像。

    鼠标右击我的电脑————>属性————>高级系统设置————>高级————>环境变量————>新建————>变量名设置为：ELECTRON_MIRROR；变量值：http：//npm.taobao.org/mirror/electron/————>确定。

```
// 安装
npm install -g electron

// 检测是否安装成功
electron -v
```

- Mac环境变量设置

    在用户目录文件中找到 .bash_profile文件(没有的话可以新建),添加以下内容:
    ```
    export ELECTRON_MIRROR=http://npm.taobao.org/mirrors/electron/
    ```

2. electron官方新手入门实例

    2.1 从GitHub上下载实例代码：
    ```
    git clone https://github.com/electron/electron-quick-start
    ```
    2.2 进入到electron-quick-start目录下

    ```
    cd electron-quick-start
    ```

    目录结构如下：
    ![图片](https://ss0.baidu.com/6ONWsjip0QIZ8tyhnq/it/u=1652161416,1996876583&fm=173&app=49&f=JPEG?w=603&h=199&s=8912CD1293F14823504DF0CA000050B1)

    2.3 安装依赖

    ```
    npm install
    ```

    2.4 启动项目

    ```
    npm start
    ```

    出现如下界面,则表示成功:
    ![图片](https://ss0.baidu.com/6ONWsjip0QIZ8tyhnq/it/u=1926442056,2345770979&fm=173&app=49&f=JPEG?w=640&h=480&s=48A63C72471A646D5A7510DA0000C0B2)

    2.5 解读main.js文件

    ```
    main.js文件是electron在启动时会通过node.js去执行mian.js文件，也就是electron的入口文件。

    // 导入electron模块,该模块为electron的内置模块
    const electron = require('electron');

    // APP模块控制整个应用程序的生命周期
    const APP = electron.app;

    // 绑定事件,当桌面应用创建完成时触发,调用createWindow函数
    APP.on('ready',createWindow);

    // 创建浏览器窗口
    const BrowserWindow = electron.BrowserWindow;

    // 声明变量
    let mainWindow

    function createWindow(){
        // 创建一个800*600的浏览器窗口
        mainWindow = new BrowserWindow({width:800,height:600});

        // 访问的页面,${ _dirname }为具体地址,可更换为baidu.com试试.
        mainWindow.loadURL( 'file://${ _dirname }/index.html' );

        // 启动时打开开发人员工具
        mainWindow.webcontents,openDevTools();
    }
    ```

3. 结构分析

    3.1 主进程

    electron在运行时会创建一个主进程(main process)，main.js在主进程中执行，而一个主进程下又有多个渲染进程(renderer process)。

    3.2渲染进程

    electron运行时，通过main.js文件中的new BrowserWindow创建新窗口,窗口中载入html文件,载入的html文件中js代码就属于渲染进程(renderer process)。

4. 将项目打包成可运行的桌面应用程序

    1、使用webpack将代码进行混编

    2、使用electron-builder对项目进行打包

    注：进行electron桌面应用程序开发时，最主要的依据就是参考electron的官方文档进行开发，官方文档里的讲解，很是详细。
