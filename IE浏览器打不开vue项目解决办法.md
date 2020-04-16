### IE 浏览器中打不开 vue 项目的问题及解决办法

注：`vue` 最低兼容至 `IE9+`

##### 安装 babel-polyfill

```node
npm install babel-polyfill
```

##### 在入口 main.js 文件中引入

```JavaScript
import 'babel-polyfill'
```

##### 修改配置文件 webpack-base-config.js

```JavaScript
entry: {
    // app: './src/main.js'
    app: ["babel-polyfill", "./src/main.js"],
  },
// 路径是"../src/main.js"
```

##### 解决 IE 不显示内容代码

```html
<meta http-equiv="X-UA-Compatible" content="IE=edge" />
```
