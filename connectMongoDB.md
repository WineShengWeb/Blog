# vue 连接本地 MongoDB 数据库

##### 后端服务

-   初始化

```js
// 项目初始化
npm init

// package.json文件
package name: (nodeapp) app //可以直接回车默认
version: (1.0.0) // 回车
description: // 回车
entry point: (index.js) server.js // 入口文件名称，默认为index.js
test command: // 回车
git repository: // 回车
keywords: // 回车
author: JSGuo // 作者 可以直接回车
license: // 回车
Is this OK? (yes) yes // 输入yes后回车
```

-   安装 `express` 和 `mongoose`

```nodejs
npm install express
npm install mongoose
```

-   引入 `express` 和 `mongoose`

新建 `server.js` 文件

```JavaScript
// server.js

// 引入express
const express = require("express");

// 引入mongoose
const mongoose = require("mongoose");

// 实例化express
const app = express();

// 引入DB config
const db = require("./config/keys").mongoURI;

// 连接MongoDB数据库
mongoose
  .connect(db, { useNewUrlParser: true, useUnifiedTopology: true })
  .then(() => console.log("MongoDB Connected"))
  .catch(err => console.log(err));

// 设置本地端口号为5000
const port = process.env.PORT || 5000;

app.listen(port, () => {
  console.log(`Server running on port ${port}`); // 此处使用``进行输出，如果使用""、''会被原样输出
});
```

```javascript
// config/keys.js

// URL
module.exports = {
    mongoURI: "mongodb://localhost:27017/test",
    secretOrKey: "secret",
};
```

##### 前端

-   配置 `vue.config.js`

```js
module.exports = {
    devServer: {
        open: true,
        host: "localhost",
        port: 8081,
        https: false,
        hotOnly: false,
        proxy: {
            // 配置跨域
            "/api": {
                target: "http://localhost:5000/api/",
                ws: true,
                changOrigin: true,
                pathRewrite: {
                    "^/api": "",
                },
            },
        },
        before: (app) => {},
    },
};
```
