<!--
 * @Author: guoxinggang<guoxinggang@gsaxns.com>
 * @Version: 1.0
 * @Date: 2019-08-08 20:48:38
 * @LastEditTime: 2019-08-21 17:00:34
 * @Description:
 -->

# <center>vue 创建项目的方式</center>

## 1. 使用 vue init webpack my-project 创建

### 1.1 安装 node.js

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[node 下载地址](https://nodejs.org/zh-cn/download/)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;安装完成后，在 Windows 环境下，请打开命令提示符，然后输入：**node -v**和**npm -V**，如果安装正常，会看到 v7.6.0 这样的输出。

### 1.2 使用 node.js 安装 vue-cli

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;输入：**npm install -g vue-cli**，回车，等待安装...

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;安装成功后输入：**vue -V**检查 vue 版本，如果输出：**2.9.6**则脚手架安装成功。

### 1.3 创建项目

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;输入：**vue init webpack my-project**(my-project 为项目名称),回车,等待一会依次会出现以下操作项:

- Project name :项目名称 ，如果不需要更改直接回车就可以了。注意：这里不能使用大写；

- Project description:项目描述，默认为 A Vue.js project,直接回车，不用编写；

- Author：作者，如果你有配置 git 的作者，他会读取；

- Install vue-router? 是否安装 vue 的路由插件；

- Use ESLint to lint your code? 是否用 ESLint 来限制你的代码错误和风格。如果你是大型团队开发，最好是进行配置；

- setup unit tests with Karma + Mocha? 是否需要安装单元测试工具 Karma+Mocha；

- Setup e2e tests with Nightwatch?是否安装 e2e 来进行用户行为模拟测试。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;全部配置完后，等待创建项目...

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;项目创建完成后会出现:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**cd my-project**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**npm run dev**

### 1.4 运行项目

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在命令行输入:**cd my-project**进入到项目文件夹，再输入：**npm run dev**运行项目,等到出现：**http://localhost:8080**，打开浏览器，在地址栏输入：**http://localhost:8080**后就可以看到创建好的项目了。

## 2. 使用 vue create my-project 创建

<font color="red">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;注意：1.使用此方法请先将 vue-cli 升级为 3.x 版本;

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2.vue 检查版本命令: **vue -V**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2.vue 版本升级命令: **npm install -g @vue/cli**
</font>

### 2.1 创建项目

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在 Windows 环境下，请打开命令提示符，然后输入：**vue create my-project**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;选 default 后会自动开始创建项目。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;创建完成后会出现：**http://localhost:8080**，下边还会出现一个 IP 地址：**http://192.168.3.2:8080**，这个的好处就是，如果你做的是移动端，可以直接在手机浏览器里输入 IP 地址来查看项目。

## 3 使用图形界面创建项目

  <font color="red">
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;注意：此方法适用于vue-cli 3.x版本
  </font>

### 3.1 创建项目

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;此方法比较简单，在命令窗口输入：**vue ui** 会自动打开图形界面，之后一步一步按提示操作即可，在这里不作太多叙述。

## 4 vue init webpack demo 和 vue create demo 创建项目的区别

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;vue create 是 vue-cli3.x 的初始化方式，目前模板是固定的，模板选项可自由配置，创建出来的是 vue-cli3 的项目，与 cue-cli2 项目结构不同，配置方法不同，具体配置方法参考官方文档网页链接。vue init 是 vue-cli2.x 的初始化方式，可以使用 github 上面的一些模板来初始化项目，webpack 是官方推荐的标准模板名。vue-cli2.x 项目向 3.x 迁移只需要把 static 目录复制到 public 目录下，老项目的 src 目录覆盖 3.x 的 src 目录(如果修改了配置，可以查看文档，用 cli3 的方法进行配置)
