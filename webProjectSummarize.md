# 公司官网vue项目开发总结

### 项目中的问题及解决办法

#### 1、头部导航栏批量添加路径问题

- 问题描述：头部导航栏使用for循环出来后无法像原生页面一样添加跳转路径

- 解决方法：在数据中添加 **path** 路径，在循环时给 **routerlink** 的 **to** 属性循环绑定path路径，具体解决办法见以下代码：

**template模板代码**

```html
<template>
    <div class="header">
        <nav>
            <div class="name">
                <h2>某某科技有限公司</h2>
            </div>
            <ul class="nav">
                <li v-for="(item,index) in nav" :key="index">
                    <!-- 一级导航 -->
                    <router-link :to="{ path:item.path }">{{ item.name }}</router-link>
                    <!-- 下拉二级导航 -->
                    <div class="list">
                        <div class="arrows"></div>
                        <div class="hide_list">
                            <ul>
                                <li v-for="(index,item) in item.list" :key="item">
                                    <router-link :to='{ path:index.path }'>{{ index.name }}</router-link>
                                </li>
                            </ul>
                        </div>
                    </div>
                </li>
            </ul>
        </nav>
    </div>
</template>
```

**js代码**

```html
<script>
export default {
  data () {
    return {
      nav: [
        {
          name: '首页',
          path: '/',
          list: []
        },
        {
          name: '页面1',
          path: '/page1',
          list: [
            {name: '页面1.1', path: '/page1.1'},
            {name: '页面1.2', path: '/page1.2'},
            {name: '页面1.3', path: '/page1.3'}
          ]
        },
        {
          name: '页面2',
          path: '/page2',
          list: [
            {name: '页面2.1', path: '/page2.1'},
            {name: '页面2.2', path: '/page2.2'},
            {name: '页面2.3', path: '/page2.3'},
            {name: '页面2.4', path: '/page2.4'}
          ]
        }
      ]
    }
  }
}
</script>
```

#### 2、模板内动态切换组件问题

- 问题描述：在左右分栏的模板页面中点击左边菜单栏，动态替换掉右边显示的组件

- 解决办法：在左边循环菜单列表时，将路径一并循环添加进去，在右边指定切换区域写入 **routerview**标签即可。具体解决办法见以下代码：

**template模板代码**

```html
<template>
    <div class="research">
        <!-- 头部 -->
        <Header></Header>
        <main class="content">
            <!-- 左边菜单栏 -->
            <div class="left_side">
                <div class="side_nav">
                    <div class="nav_title">
                        <h4>新闻中心</h4>
                    </div>
                    <div class="nav_list">
                        <img src="@/assets/img/shadow_2.png" alt />
                        <ul class="sideList">
                            <li  @click="addClass(index)" :class="{'actives':i==index}" v-for="(item,index) in data" :key="index">
                                <router-link :to="{ path:item.path }">{{ item.name }}</router-link>
                            </li>
                        </ul>
                    </div>
                </div>
            </div>
            <!-- 右边显示区域 -->
            <div class="right_side">
                <router-view></router-view>
            </div>
        </main>
        <!-- 脚部 -->
        <Footer></Footer>
    </div>
</template>
```

js代码

```html
<script>
import Header from '@/components/header'
import Footer from '@/components/footer'
export default {
  name: 'research',
  data () {
    return {
      i: 0,
      data: [
        {name: '公司动态', path: '/news'},
        {name: '行业资讯', path: '/industryInformation'},
        {name: '技术交流', path: '/technicalExchange'}
      ]
    }
  },
  components: {
    Header,
    Footer
  },
  methods: {
    addClass (index) {
      this.i = index
    }
  }
}
</script>
```

#### 3、vue中使用百度地图定位的问题

- 问题描述：官网联系我们页面使用了百度地图定位功能，但由于生成的代码是原生的，无法直接放入vue中使用

- 解决办法：使用 [vue baidu map](https://dafrok.github.io/vue-baidu-map/#/) 实现地图定位功能。具体解决办法见以下代码：

**安装vue baidu map**

```node
npm install vue-baidu-map --save
```

**template模板代码**

```html
<template>
    <div class="contactUs">
        <!--百度地图容器-->
        <baidu-map class="bm-view" ak="YOUR_APP_KEY" :center="center" :zoom="zoom" :scroll-wheel-zoom="true">
            <bm-marker :position="center" :dragging="true" animation="BMAP_ANIMATION_BOUNCE" @click="infoWindowOpen">
                <!-- 缩放控件 -->
                <bm-navigation anchor="left"></bm-navigation>
                <!-- 比例尺控件 -->
                <bm-scale anchor="bottom" ></bm-scale>
                <!-- 缩略图 -->
                <bm-overview-map anchor="BMAP_ANCHOR_BOTTOM_RIGHT" :isOpen="true"></bm-overview-map>
                <!-- 定点提示框 -->
                <bm-info-window title="某某技术有限公司" :show="show" @close="infoWindowClose" @open="infoWindowOpen" class="address">地址：某某市某某区某某路1号</bm-info-window>
            </bm-marker>
        </baidu-map>
    </div>
</template>
```

js代码

```html
<script>
// 注册组件
import BaiduMap from 'vue-baidu-map/components/map/Map.vue'
import BmMarker from 'vue-baidu-map/components/overlays/Marker'
import BmInfoWindow from 'vue-baidu-map/components/overlays/InfoWindow'
import BmScale from 'vue-baidu-map/components/controls/Scale'
import BmNavigation from 'vue-baidu-map/components/controls/Navigation'
import BmOverviewMap from 'vue-baidu-map/components/controls/OverviewMap'

export default {
  data () {
    return {
      center: { lng: 103.876025, lat: 36.059423 },
      zoom: 18,
      show: true
    }
  },
  // 组件
  components: {
    BaiduMap,
    BmMarker,
    BmInfoWindow,
    BmScale,
    BmNavigation,
    BmOverviewMap
  },
  methods: {
    handler ({ BMap, map }) {
      this.center.lng = 103.875955
      this.center.lat = 36.059471
      this.zoom = 18
    },
    infoWindowClose () {
      this.show = false
    },
    infoWindowOpen () {
      this.show = true
    }
  }
}
</script>
```

css样式

```html
<style scoped>
.bm-view {
    width: 100%;
    height: 400px;
    border: #ccc solid 1px;
}
.address{
    font-size: 12px;
}
</style>
```

#### 4、项目打包后出现空白的问题

- 问题描述：在项目完成打包后，页面出现空白或者盘符索引。

- 解决办法：在项目完成打包后，需要在 **utils.js** 文件中添加 **publicPath: '../../'**；在 **webpack.prod.conf.js** 文件中添加 **publicPath: './'**；在 **config** 文件下的 **index.js** 文件中添加 **assetsPublicPath: './'**；在路由表中去掉 **mode: 'history'**，因为不管你用的是react，还是vue，都是用了H5 history api来做前端路由，经过静态文件服务器做处理之后，前端才能识别不同的路由，所以你直接打开文件看到404。具体解决办法见以下代码：


**utils.js**文件

```javascript
'use strict'
const path = require('path')
const config = require('../config')
const ExtractTextPlugin = require('extract-text-webpack-plugin')
const packageConfig = require('../package.json')

exports.assetsPath = function (_path) {
  const assetsSubDirectory = process.env.NODE_ENV === 'production'
    ? config.build.assetsSubDirectory
    : config.dev.assetsSubDirectory

  return path.posix.join(assetsSubDirectory, _path)
}

exports.cssLoaders = function (options) {
  options = options || {}

  const cssLoader = {
    loader: 'css-loader',
    options: {
      sourceMap: options.sourceMap
    }
  }

  const postcssLoader = {
    loader: 'postcss-loader',
    options: {
      sourceMap: options.sourceMap
    }
  }

  // generate loader string to be used with extract text plugin
  function generateLoaders (loader, loaderOptions) {
    const loaders = options.usePostCSS ? [cssLoader, postcssLoader] : [cssLoader]

    if (loader) {
      loaders.push({
        loader: loader + '-loader',
        options: Object.assign({}, loaderOptions, {
          sourceMap: options.sourceMap
        })
      })
    }

    // Extract CSS when that option is specified
    // (which is the case during production build)
    if (options.extract) {
      return ExtractTextPlugin.extract({
        use: loaders,
        fallback: 'vue-style-loader',
        // 在此处添加publicPath: '../../'
        publicPath: '../../'
      })
    } else {
      return ['vue-style-loader'].concat(loaders)
    }
  }

  // https://vue-loader.vuejs.org/en/configurations/extract-css.html
  return {
    css: generateLoaders(),
    postcss: generateLoaders(),
    less: generateLoaders('less'),
    sass: generateLoaders('sass', { indentedSyntax: true }),
    scss: generateLoaders('sass'),
    stylus: generateLoaders('stylus'),
    styl: generateLoaders('stylus')
  }
}

// Generate loaders for standalone style files (outside of .vue)
exports.styleLoaders = function (options) {
  const output = []
  const loaders = exports.cssLoaders(options)

  for (const extension in loaders) {
    const loader = loaders[extension]
    output.push({
      test: new RegExp('\\.' + extension + '$'),
      use: loader
    })
  }

  return output
}

exports.createNotifierCallback = () => {
  const notifier = require('node-notifier')

  return (severity, errors) => {
    if (severity !== 'error') return

    const error = errors[0]
    const filename = error.file && error.file.split('!').pop()

    notifier.notify({
      title: packageConfig.name,
      message: severity + ': ' + error.name,
      subtitle: filename || '',
      icon: path.join(__dirname, 'logo.png')
    })
  }
}
```

**webpack.prod.conf.js** 文件

```javascript
'use strict'
const path = require('path')
const utils = require('./utils')
const webpack = require('webpack')
const config = require('../config')
const merge = require('webpack-merge')
const baseWebpackConfig = require('./webpack.base.conf')
const CopyWebpackPlugin = require('copy-webpack-plugin')
const HtmlWebpackPlugin = require('html-webpack-plugin')
const ExtractTextPlugin = require('extract-text-webpack-plugin')
const OptimizeCSSPlugin = require('optimize-css-assets-webpack-plugin')
const UglifyJsPlugin = require('uglifyjs-webpack-plugin')

const env = require('../config/prod.env')

const webpackConfig = merge(baseWebpackConfig, {
  module: {
    rules: utils.styleLoaders({
      sourceMap: config.build.productionSourceMap,
      extract: true,
      usePostCSS: true
    })
  },
  devtool: config.build.productionSourceMap ? config.build.devtool : false,
  output: {
    // 在此处添加 publicPath: './'
    publicPath: './',
    path: config.build.assetsRoot,
    filename: utils.assetsPath('js/[name].[chunkhash].js'),
    chunkFilename: utils.assetsPath('js/[id].[chunkhash].js')
  },
  plugins: [
    // http://vuejs.github.io/vue-loader/en/workflow/production.html
    new webpack.DefinePlugin({
      'process.env': env
    }),
    new UglifyJsPlugin({
      uglifyOptions: {
        compress: {
          warnings: false
        }
      },
      sourceMap: config.build.productionSourceMap,
      parallel: true
    }),
    // extract css into its own file
    new ExtractTextPlugin({
      filename: utils.assetsPath('css/[name].[contenthash].css'),
      // Setting the following option to `false` will not extract CSS from codesplit chunks.
      // Their CSS will instead be inserted dynamically with style-loader when the codesplit chunk has been loaded by webpack.
      // It's currently set to `true` because we are seeing that sourcemaps are included in the codesplit bundle as well when it's `false`,
      // increasing file size: https://github.com/vuejs-templates/webpack/issues/1110
      allChunks: true
    }),
    // Compress extracted CSS. We are using this plugin so that possible
    // duplicated CSS from different components can be deduped.
    new OptimizeCSSPlugin({
      cssProcessorOptions: config.build.productionSourceMap
        ? { safe: true, map: { inline: false } }
        : { safe: true }
    }),
    // generate dist index.html with correct asset hash for caching.
    // you can customize output by editing /index.html
    // see https://github.com/ampedandwired/html-webpack-plugin
    new HtmlWebpackPlugin({
      filename: config.build.index,
      template: 'index.html',
      inject: true,
      minify: {
        removeComments: true,
        collapseWhitespace: true,
        removeAttributeQuotes: true
        // more options:
        // https://github.com/kangax/html-minifier#options-quick-reference
      },
      // necessary to consistently work with multiple chunks via CommonsChunkPlugin
      chunksSortMode: 'dependency'
    }),
    // keep module.id stable when vendor modules does not change
    new webpack.HashedModuleIdsPlugin(),
    // enable scope hoisting
    new webpack.optimize.ModuleConcatenationPlugin(),
    // split vendor js into its own file
    new webpack.optimize.CommonsChunkPlugin({
      name: 'vendor',
      minChunks (module) {
        // any required modules inside node_modules are extracted to vendor
        return (
          module.resource &&
          /\.js$/.test(module.resource) &&
          module.resource.indexOf(
            path.join(__dirname, '../node_modules')
          ) === 0
        )
      }
    }),
    // extract webpack runtime and module manifest to its own file in order to
    // prevent vendor hash from being updated whenever app bundle is updated
    new webpack.optimize.CommonsChunkPlugin({
      name: 'manifest',
      minChunks: Infinity
    }),
    // This instance extracts shared chunks from code splitted chunks and bundles them
    // in a separate chunk, similar to the vendor chunk
    // see: https://webpack.js.org/plugins/commons-chunk-plugin/#extra-async-commons-chunk
    new webpack.optimize.CommonsChunkPlugin({
      name: 'app',
      async: 'vendor-async',
      children: true,
      minChunks: 3
    }),

    // copy custom static assets
    new CopyWebpackPlugin([
      {
        from: path.resolve(__dirname, '../static'),
        to: config.build.assetsSubDirectory,
        ignore: ['.*']
      }
    ])
  ]
})

if (config.build.productionGzip) {
  const CompressionWebpackPlugin = require('compression-webpack-plugin')

  webpackConfig.plugins.push(
    new CompressionWebpackPlugin({
      asset: '[path].gz[query]',
      algorithm: 'gzip',
      test: new RegExp(
        '\\.(' +
        config.build.productionGzipExtensions.join('|') +
        ')$'
      ),
      threshold: 10240,
      minRatio: 0.8
    })
  )
}

if (config.build.bundleAnalyzerReport) {
  const BundleAnalyzerPlugin = require('webpack-bundle-analyzer').BundleAnalyzerPlugin
  webpackConfig.plugins.push(new BundleAnalyzerPlugin())
}

module.exports = webpackConfig
```

config文件下**index.js** 文件

```javascript
'use strict'
// Template version: 1.3.1
// see http://vuejs-templates.github.io/webpack for documentation.

const path = require('path')

module.exports = {
  dev: {

    // Paths
    assetsSubDirectory: 'static',
    assetsPublicPath: '/',
    proxyTable: {},

    // Various Dev Server settings
    host: 'localhost', // can be overwritten by process.env.HOST
    port: 8080, // can be overwritten by process.env.PORT, if port is in use, a free one will be determined
    autoOpenBrowser: false,
    errorOverlay: true,
    notifyOnErrors: true,
    poll: false, // https://webpack.js.org/configuration/dev-server/#devserver-watchoptions-

    // Use Eslint Loader?
    // If true, your code will be linted during bundling and
    // linting errors and warnings will be shown in the console.
    useEslint: true,
    // If true, eslint errors and warnings will also be shown in the error overlay
    // in the browser.
    showEslintErrorsInOverlay: false,

    /**
     * Source Maps
     */

    // https://webpack.js.org/configuration/devtool/#development
    devtool: 'cheap-module-eval-source-map',

    // If you have problems debugging vue-files in devtools,
    // set this to false - it *may* help
    // https://vue-loader.vuejs.org/en/options.html#cachebusting
    cacheBusting: true,

    cssSourceMap: true
  },

  build: {
    // Template for index.html
    index: path.resolve(__dirname, '../dist/index.html'),

    // Paths
    assetsRoot: path.resolve(__dirname, '../dist'),
    assetsSubDirectory: 'static',
    // 在此处的 assetsPublicPath: '/' 改为 assetsPublicPath: './'
    assetsPublicPath: './',

    /**
     * Source Maps
     */

    productionSourceMap: true,
    // https://webpack.js.org/configuration/devtool/#production
    devtool: '#source-map',

    // Gzip off by default as many popular static hosts such as
    // Surge or Netlify already gzip all static assets for you.
    // Before setting to `true`, make sure to:
    // npm install --save-dev compression-webpack-plugin
    productionGzip: false,
    productionGzipExtensions: ['js', 'css'],

    // Run the build command with an extra argument to
    // View the bundle analyzer report after build finishes:
    // `npm run build --report`
    // Set to `true` or `false` to always turn it on or off
    bundleAnalyzerReport: process.env.npm_config_report
  }
}
```

最后在 **路由表** 里将 **mode: 'history'** 注释掉或者删除。
