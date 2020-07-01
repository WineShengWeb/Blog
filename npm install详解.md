# npm install、npm install --save 与 npm install --save-dev 区别

##### 1、相同点

三者都会本地安装包到项目的 `node_modules` 目录中

##### 2、指定依赖包

指定包取决于你的项目，你需要在 `package.json` 文件中列出你需要使用的包，有两种包可以选择：

-   “dependencies”： 这些包都是你的应用程序在生产环境中所需要的。
-   “devDepedencies”：这些包只是在开发和测试中需要的。

##### 3、区别

区别在于对项目 `package.json` 的修改，`npm install` 不会修改 `package.json`，而后两者会将依赖添加进 `package.json`，后两者的区别请看下文循序渐进。

###### 3.1、npm install X:

-   会把 X 包安装到 `node_modules` 目录中

-   不会修改 `package.json`

-   之后运行 `npm install` 命令时，不会自动安装 X

###### 3.2、npm install X –save:

-   会把 X 包安装到 `node_modules` 目录中

-   会在 `package.json` 的 `dependencies` 属性下添加 X

-   之后运行 `npm install` 命令时，会自动安装 X 到 `node_modules` 目录中

-   之后运行 `npm install –production` 或者注明 `NODE_ENV` 变量值为 `production` 时，会自动安装 `msbuild` 到 `node_modules` 目录中

###### 3.3、npm install X –save-dev:

-   会把 X 包安装到 `node_modules` 目录中

-   会在 `package.json` 的 `devDependencies` 属性下添加 X

-   之后运行 `npm install` 命令时，会自动安装 X 到 `node_modules` 目录中

-   之后运行 `npm install –production` 或者注明 `NODE_ENV` 变量值为 `production` 时，不会自动安装 X 到 `node_modules` 目录中

###### 3.4、使用原则:

-   运行时需要用到的包使用`–save`，否则使用`–save-dev`。

##### 4、`npm i` 和 `npm install` 的区别

在一次项目开发中安装依赖时用 `npm i` 来安装，一直报错，试了好几次，都是一样。后来换成了 `npm install` 来安装，一次就安装好了。原因如下：

**实际使用的区别点主要如下(windows 下)：**

-   1.用 `npm i` 安装的模块无法用 `npm uninstall` 删除，用 `npm uninstall i` 才卸载掉；
-   2.`npm i` 会帮助检测与当前 `node` 版本最匹配的 `npm` 包版本号，并匹配出来相互依赖的 `npm` 包应该提升的版本号；
-   3.部分 `npm` 包在当前 `node` 版本下无法使用，必须使用建议版本；
-   4.安装报错时 `intall` 肯定会出现 `npm-debug.log` 文件，npm i 不一定。
