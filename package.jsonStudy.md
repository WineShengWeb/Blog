## package.json 学习

#### package.json 文件简介

-   1、每个项目的根目录下面，一般都有一个 package.json 文件，定义了这个项目所需要的各种模块，以及项目的配置信息（比如名称、版本、许可证等元数据）。npm install 命令根据这个配置文件，自动下载所需的模块，也就是配置项目所需的运行和开发环境。

-   2、package.json 文件可以手工编写，也可以使用 npm init 命令自动生成。

-   3、npm 安装 package.json 时 直接转到当前项目目录下用命令 npm install 或 npm install --save-dev 安装即可，自动将 package.json 中的模块安装到 node-modules 文件夹下。

-   4、package.json 中添加中文注释会编译出错。

#### package.json 文件配置详解

文件示例

```json
* 真实的package.json没有注释（json文件不存在注释）
{
    "name": "my-demo", //项目名称
    "version": "1.0.0", //项目版本
    "description": "a project", //项目描述
    "main": "index.js", //主文件（比如默认是index.js，项目名称叫package。那么require(‘package’)将返回index.js返回的内容）es5编译入口文件
    "module": "./es/index", // es6编译入口文件
    "files": [
        // 包含在项目中的文件(夹)数组，可以声明一个.gitignore来忽略部分文件
        "lib",
        "es",
        "dist",
        "assets"
    ],
    "repository": "http://.../h5-components.git", // 项目代码存放的地方
    "homepage": "http://...", // 项目主页url，（包的官网）
    "scripts": {
        //scripts指定了运行脚本命令的npm命令行缩写，比如start指定了运行npm run start时，所要执行的命令。
        //npm run 可列出package.json中scripts的所有脚本命令
        "build": "weex-builder src dist",
        "build_plugin": "webpack --config ./tools/webpack.config.plugin.js --color",
        "dev": "weex-builder src dist -w",
        "serve": "serve -p 8080"
    },
    "config": {
        // 字段用于添加命令行的环境变量。
        "port": 8089,
        "entry": {
            "h5-components": ["./index.js"]
        }
    },
    "keywords": ["weex"],
    "author": "demo@gmail.com", //作者
    "license": "ISC", //协议/许可证，默认是ISC、有的默认是MIT
    "devDependencies": {
        // 在开发、测试环境中用到的依赖
        // devDependencies指定项目开发所需要的模块。
        "babel-core": "^6.14.0",
        "babel-loader": "^6.2.5",
        "babel-preset-es2015": "^6.18.0",
        "vue-loader": "^10.0.2",
        "eslint": "^3.5.0",
        "serve": "^1.4.0",
        "webpack": "^1.13.2",
        "weex-loader": "^0.3.3",
        "weex-builder": "^0.2.6"
    },
    "dependencies": {
        // 在生产环境中需要用到的依赖
        // dependencies字段指定了项目运行所依赖的模块
        "weex-html5": "^0.3.2",
        "weex-components": "*"
    },
    "sideEffects": ["*.scss"], // 如果没有这个值，打包时会出错，参照css issue
    "browserslist": [
        // 指定该模板供浏览器使用的版本
        "iOS >= 8",
        "Firefox >= 20",
        "Android > 4.2",
        "> 1%",
        "last 2 versions",
        "not ie <= 10"
    ]
    // bugs：填写一个bug提交地址，便于用户反馈
}
```

#### npm install 安装模块

-   1、npm install 本地安装

```
（1）将安装包放在 ./node_modules 下（运行 npm 命令时所在的目录），如果没有 node_modules 目录，会在当前执行 npm 命令的目录下生成 node_modules 目录。
（2）可以通过 require() 来引入本地安装的包。
```

-   2、npm install -g 全局安装

```
(1)将安装包放在你 node 的安装目录。
(2)可以直接在命令行里使用。
(3)不能使用 package.json 里列举的依赖进行全局安装
```

-   3、npm install --save 在生产环境中需要用到的依赖 ,发布之后还依赖的东西

```
(1)会把msbuild包安装到node_modules目录中
(2)会在package.json的dependencies属性下添加msbuild
(3)之后运行npm install命令时，会自动安装msbuild到node_modules目录中
(4)之后运行npm install --production或者注明NODE_ENV变量值为production时，会自动安装msbuild到node_modules目录中
```

-   4、npm install --save-dev 在开发、测试环境中用到的依赖 ,开发时依赖的东西

```
(1)会把msbuild包安装到node_modules目录中
(2)会在package.json的devDependencies属性下添加msbuild
(3)之后运行npm install命令时，会自动安装msbuild到node_modules目录中
(4)之后运行npm install --production或者注明NODE_ENV变量值为production时，不会自动安装msbuild到node_modules目录中
```
