# npm i 和 npm install 的区别

本人在一次项目中安装依赖时用npm i 来安装，一直报错，试了好几次，都是一样。后来换成了npm install 来安装，一次就安装好了。原因如下：

**实际使用的区别点主要如下(windows下)：**

- 1.用npm i安装的模块无法用npm uninstall删除，用npm uninstall i才卸载掉；
- 2.npm i会帮助检测与当前node版本最匹配的npm包版本号，并匹配出来相互依赖的npm包应该提升的版本号；
- 3.部分npm包在当前node版本下无法使用，必须使用建议版本；
- 4.安装报错时intall肯定会出现npm-debug.log 文件，npm i不一定。
