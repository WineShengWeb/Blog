# vue 中开发环境和生产环境的配置

##### 1、开发环境

所有的开发和配置在这个环境里进行。一般情况下，只有这个环境可以改配置和进行开发，并且一般不在这个环境下创建数据。（开发环境就是每个开发人员电脑上的开发环境，只有开发人员可以配置和开发，写数据测试放在测试环境）

在根目录下新建 `.env.development` 文件

```js
// VUE_APP_URL= url;
VUE_APP_URL = "http://192.168.1.106:8083/api/v1";
```

##### 2、生产环境

正式使用的系统环境。 一般情况下，一个环境对应一个服务器，也有一些公司把开发、测试等环境放到一个服务器的。（从 SVN 上通过 FTP 下载下来，然后在服务器上的 tomcat 部署、发布，服务器是 linux 的）

在根目录下新建 `.env.production` 文件

```js
// VUE_APP_URL = url;
VUE_APP_URL = "http://192.168.12.108:8883/api/v1";
```

##### 3、在 `axios` 中使用

```js
const service = axios.create({
    baseURL: process.env.BASE_API, // 配置在config/prod.env里的baseApi
    timeout: 5000, // 超时时间
});
```
