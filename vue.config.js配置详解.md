# `vue.config.js` 配置详解

```js
module.exports={
    //部署应用包时的基本url。
    //baseUrl:"/",//从 Vue CLI 3.3 起已弃用
    publicPath: process.env.NODE_ENV === "production" ? "./" : "./",
    publicPath:"/"，
    //默认情况下，Vue CLI 会假设你的应用是被部署在一个域名的根路径上，例如 https://www.my-app.com/。
    //如果应用被部署在一个子路径上，你就需要用这个选项指定这个子路径。例如，如果你的应用被部署在 https://www.my-app.com/my-app/，则设置 publicPath 为 /my-app/。
    //这个值也可以被设置为空字符串 ('') 或是相对路径 ('./')，这样所有的资源都会被链接为相对路径，这样打出来的包可以被部署在任意路径，也可以用在类似 Cordova hybrid 应用的文件系统中。
    //也可以使用三元运算符配置开发和正式环境上不同的路径

    outputDir:"dist",//打包后生成的生产环境构建文件的目录，dist是默认值。默认情况下每次打包都会清空上次打包文件（构建时传入 --no-clean 可关闭该行为）。
    //官方提示:始终使用outputDir，而不要修改 webpack 的 output.path。
    assetsDir:"",//放置生成的静态资源 (js、css、img、fonts) 的 (相对于 outputDir 的) 目录
    indexPath:"index.html",//指定生成的 index.html 的输出路径 (相对于 outputDir)。也可以是一个绝对路径。
    filenameHashing:true,//默认情况下，生成的静态资源在它们的文件名中包含了 hash 以便更好的控制缓存。然而，这也要求 index 的 HTML 是被 Vue CLI 自动生成的。如果你无法使用 Vue CLI 生成的 index HTML，你可以通过将这个选项设为 false 来关闭文件名哈希。

    //默认是undefined，配置类型是Object，这也是多页面应用的所需要配置的（具体方式，请先找度娘）
    pages:{
        index:{
          // page 的入口
          entry: 'src/index/main.js',
          // 模板来源
          template: 'public/index.html',
          // 在 dist/index.html 的输出
          filename: 'index.html',
          // 当使用 title 选项时，
          // template 中的 title 标签需要是 <title><%= htmlWebpackPlugin.options.title %></title>
          title: 'Index Page',
          // 在这个页面中包含的块，默认情况下会包含
          // 提取出来的通用 chunk 和 vendor chunk。
          chunks: ['chunk-vendors', 'chunk-common', 'index']
        },
        // 当使用只有入口的字符串格式时，
        // 模板会被推导为 `public/subpage.html`
        // 并且如果找不到的话，就回退到 `public/index.html`。
        // 输出文件名会被推导为 `subpage.html`。
        subpage: 'src/subpage/main.js'
    },

    lintOnSave:true,//在保存后eslint检查代码。将值设置为'error'是把错误直接输出为编译错误。process.env.NODE_ENV !== 'production'，在生产环境上设为false。


    runtimeCompiler:false,//是否使用包含运行时编译器的 Vue 构建版本。设置为 true 后你就可以在 Vue 组件中使用 template 选项了，但是这会让你的应用额外增加 10kb 左右。
    transpileDependencies:[],//默认情况下 babel-loader 会忽略所有 node_modules 中的文件。如果你想要通过 Babel 显式转译一个依赖，可以在这个选项中列出来。
    productionSourceMap:true,//如果你不需要生产环境的 source map，可以将其设置为 false 以加速生产环境构建。
    //在打包完成后文件夹中有.map文件，他的作用是在打包完成后，如果运行时报错，没有.map文件不能找到报错信息的准确位置。

    crossorigin:undefined,//设置类型是Sring，设置生成的 HTML 中 <link rel="stylesheet"> 和 <script> 标签的 crossorigin 属性。需要注意的是该选项仅影响由 html-webpack-plugin 在构建时注入的标签 - 直接写在模版 (public/index.html) 中的标签不受影响。
    integrity:false,//在生成的 HTML 中的 <link rel="stylesheet"> 和 <script> 标签上启用 Subresource Integrity (SRI)。如果你构建后的文件是部署在 CDN 上的，启用该选项可以提供额外的安全性。
    //需要注意的是该选项仅影响由 html-webpack-plugin 在构建时注入的标签 - 直接写在模版 (public/index.html) 中的标签不受影响。
    //另外，当启用 SRI 时，preload resource hints 会被禁用，因为 Chrome 的一个 bug 会导致文件被下载两次。
    configureWebpack:Object|Function,//如果这个值是一个对象，则会通过 webpack-merge 合并到最终的配置中。
    //如果这个值是一个函数，则会接收被解析的配置作为参数。该函数及可以修改配置并不返回任何东西，也可以返回一个被克隆或合并过的配置版本。

    chainWebpack:Function,//是一个函数，会接收一个基于 webpack-chain 的 ChainableConfig 实例。允许对内部的 webpack 配置进行更细粒度的修改。

    //css.loaderOptions:{},//Object,默认是{},向 CSS 相关的 loader 传递选项
    css: {
        modules:false,//默认情况下，只有 *.module.[ext] 结尾的文件才会被视作 CSS Modules 模块。设置为 true 后你就可以去掉文件名中的 .module 并将所有的 *.(css|scss|sass|less|styl(us)?) 文件视为 CSS Modules 模块。
        extract:Boolean,//生产环境下是 true，开发环境下是 false,是否将组件中的 CSS 提取至一个独立的 CSS 文件中 (而不是动态注入到 JavaScript 中的 inline 代码)。
        //同样当构建 Web Components 组件时它总是会被禁用 (样式是 inline 的并注入到了 shadowRoot 中)。
        //当作为一个库构建时，你也可以将其设置为 false 免得用户自己导入 CSS。
        //提取 CSS 在开发环境模式下是默认不开启的，因为它和 CSS 热重载不兼容。然而，你仍然可以将这个值显性地设置为 true 在所有情况下都强制提取。
        sourceMap:false,//Boolean,是否为 CSS 开启 source map。设置为 true 之后可能会影响构建的性能。
        loaderOptions: {
          css: {
            // 这里的选项会传递给 css-loader
          },
          postcss: {
            // 这里的选项会传递给 postcss-loader
          }
        }
     }
     //支持的 loader 有：css-loader,postcss-loader,sass-loader,less-loader,stylus-loader

    devServer:{
        clientLogLevel:'silent' | 'trace' | 'debug' | 'info' | 'warn' | 'error' | 'none' | 'warning',//使用内联模式时，DevTools中的控制台将显示消息，例如在重新加载之前，错误之前或启用热模块更换时。默认为info
        historyApiFallback: true,//使用HTML5历史记录API时，index.html可能必须提供该页面以代替任何404回复。devServer.historyApiFallback默认情况下禁用。通过传递启用它
        hot: true,//热模块替换，就是热更新页面
        compress: true,//为所服务的一切启用gzip压缩
        host: 'localhost',//指定要使用的主机。默认情况下这是localhost。
        port: 8080//端口号，
        //所有 webpack-dev-server 的选项都支持。注意：
        //有些值像 host、port 和 https 可能会被命令行参数覆写。
        //有些值像 publicPath 和 historyApiFallback 不应该被修改，因为它们需要和开发服务器的 publicPath 同步以保障正常的工作。

        //proxy:"url地址",//前端应用和后台API服务没有运行在一个主机上，设置此项在开发环境下代理到API服务器。
        proxy:{//配置不同的后台API地址
            '/api': {
                target: '<url>',
                ws: true,
                changeOrigin: true,
                pathRewrite: {
                  "^/api": "/"
                }
              },
              '/foo': {
                target: '<other_url>'
              }
        }
    }，

    parallel:require('os').cpus().length > 1,//Boolean,是否为 Babel 或 TypeScript 使用 thread-loader。该选项在系统的 CPU 有多于一个内核时自动启用，仅作用于生产构建。

   pwa:{},//向 PWA 插件传递选项。

   pluginOptions:{},//一个不进行任何 schema 验证的对象，因此它可以用来传递任何第三方插件选项


}
```
