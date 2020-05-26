# `vue` 中 `svg-sprite-loader` 的使用教程

##### 1、安装和配置 `svg-sprite-loader`:

安装命令

```node
npm install -D svg-sprite-loader
```

vue.config.js 文件配置：

```JavaScript
'use strict'
const path = require('path')

function resolve(dir) {
  return path.join(__dirname, dir)
}

module.exports = {
  chainWebpack(config) {
    // set svg-sprite-loader
    config.module
      .rule('svg')
      .exclude.add(resolve('src/icons'))
      .end()
    config.module
      .rule('icons')
      .test(/\.svg$/)
      .include.add(resolve('src/icons'))
      .end()
      .use('svg-sprite-loader')
      .loader('svg-sprite-loader')
      .options({
        symbolId: 'icon-[name]'
      })
      .end()
  },
  publicPath: './'
}

```

webpack 配置：

```JavaScript
{
    test: /\.svg$/,
    loader: 'svg-sprite-loader',
    include: [resolve('src/icons')],
    options: {
        symbolId: 'icon-[name]'
    }
},
{
    test: /\.(png|jpe?g|gif|svg)(\?.*)?$/,
    loader: 'url-loader',
    options: {
        limit: 10000,
        name: utils.assetsPath('img/[name].[hash:7].[ext]')
    },
    exclude: [resolve('src/icons')]
}
```

> 注意 url-loader 中要将 icons 文件夹排除, 不让 url-loader 处理该文件夹

##### 2、新建组件 `SvgIcon.vue`:

在 `components` 中新建 `SvgIcon` 文件夹， `SvgIcon` 文件夹写新建 `SvgIcon.vue` 组件:

```vue
<template>
    <svg :class="svgClass" aria-hidden="true">
        <use :xlink:href="iconName"></use>
    </svg>
</template>

<script>
export default {
    name: "svg-icon",
    props: {
        iconClass: {
            type: String,
            required: true,
        },
        className: {
            type: String,
        },
    },
    computed: {
        iconName() {
            return `#icon-${this.iconClass}`;
        },
        svgClass() {
            if (this.className) {
                return "svg-icon " + this.className;
            } else {
                return "svg-icon";
            }
        },
    },
};
</script>

<style scoped>
.svg-icon {
    width: 1em;
    height: 1em;
    vertical-align: -0.15em;
    fill: currentColor;
    overflow: hidden;
}
</style>
```

##### 3、新建 `icons` 文件夹

在 `src` 文件夹写新建 `icons` 文件，里面新建 `Svg` 文件夹（存放 `svg` 文件）和 `index.js` 文件：

```JavaScript
import Vue from 'vue'
import SvgIcon from '@/components/SvgIcon' // svg组件

// register globally
Vue.component('svg-icon', SvgIcon)

const requireAll = requireContext => requireContext.keys().map(requireContext)
const req = require.context('./svg', false, /\.svg$/)
requireAll(req)
```

##### 4、引入 `main.js`

将 `icons` 引入 `main.js` 文件中：

```JavaScript
import '@/icons'
```

##### 5、使用 `svg` 文件

在页面中使用：

```html
<svg-icon icon-class="eye"></svg-icon>
```

> 1、`icon-class` 的值是 `svg` 文件名；
> 2、可以加 `class` 控制和改变 `svg` 的大小和颜色；
> 3、如果需要改变 `svg` 的颜色，需要将对应 `svg` 文件里的 `fill="#2c2c2c"` 属性值 `#2c2c2c` 清空，否则颜色不可变。
