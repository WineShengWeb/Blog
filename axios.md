# axios 学习笔记

#### 什么是 `axios`

> `axios` 是一个基于 `Promise` 用于浏览器和 `nodejs` 的 `HTTP` 客户端。简单的理解就是 `ajax` 的封装

#### 特征

-   从浏览器中创建 `XMLHttpRequest`
-   从 `node.js` 发出 http 请求
-   支持 `Promise API`
-   拦截请求和响应
-   转换请求和响应数据
-   取消请求
-   自动转换 `JSON` 数据
-   客户端支持防止 `CSRF/XSRF`

#### 安装 `axios`

`npm` 安装

```npm
npm install axios
```

bower

```bower
bower install axios
```

`CDN` 引入

```JavaScript
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
```

#### `axios` 中 `GET` 请求

```JavaScript
// 为给定 ID 的 user 创建请求
axios.get('/user?ID=12345')
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });

// 上面的请求也可以这样做
axios.get('/user', {
    params: {
      ID: 12345
    }
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });
```

#### `axios` 中 `POST` 请求

```JavaScript
axios.post('/user', {
    firstName: 'Fred',
    lastName: 'Flintstone'
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });
```

#### `axios` 中并发请求

```JavaScript
function getUserAccount() {
  return axios.get('/user/12345');
}

function getUserPermissions() {
  return axios.get('/user/12345/permissions');
}

axios.all([getUserAccount(), getUserPermissions()])
  .then(axios.spread(function (acct, perms) {
    // 两个请求现在都执行完成
  }));
```

#### 请求方法的别名

为方便起见，为所有支持的请求方法提供了别名

-   axios.request(config)
-   axios.get(url[, config])
-   axios.delete(url[, config])
-   axios.head(url[, config])
-   axios.options(url[, config])
-   axios.post(url[, data[, config]])
-   axios.put(url[, data[, config]])
-   axios.patch(url[, data[, config]])

###### 注意

> 在使用别名方法时， url、method、data 这些属性都不必在配置中指定。

#### 并发

处理并发请求的助手函数

-   axios.all(iterable)
-   axios.spread(callback)

#### 创建实例

可以使用自定义配置新建一个 `axios` 实例

-   axios.create([config])

```JavaScript
const instance = axios.create({
  baseURL: 'https://some-domain.com/api/',
  timeout: 1000,
  headers: {'X-Custom-Header': 'foobar'}
});
```

##### 实例方法

以下是可用的实例方法。指定的配置将与实例的配置合并。

-   axios#request(config)
-   axios#get(url[, config])
-   axios#delete(url[, config])
-   axios#head(url[, config])
-   axios#options(url[, config])
-   axios#post(url[, data[, config]])
-   axios#put(url[, data[, config]])
-   axios#patch(url[, data[, config]])

#### 请求配置

这些是创建请求时可以用的配置选项。只有 `url` 是必需的。如果没有指定 `method`，请求将默认使用 `get` 方法。

```JavaScript
{
   // `url` 是用于请求的服务器 URL
  url: '/user',

  // `method` 是创建请求时使用的方法
  method: 'get', // default

  // `baseURL` 将自动加在 `url` 前面，除非 `url` 是一个绝对 URL。
  // 它可以通过设置一个 `baseURL` 便于为 axios 实例的方法传递相对 URL
  baseURL: 'https://some-domain.com/api/',

  // `transformRequest` 允许在向服务器发送前，修改请求数据
  // 只能用在 'PUT', 'POST' 和 'PATCH' 这几个请求方法
  // 后面数组中的函数必须返回一个字符串，或 ArrayBuffer，或 Stream
  transformRequest: [function (data, headers) {
    // 对 data 进行任意转换处理
    return data;
  }],

  // `transformResponse` 在传递给 then/catch 前，允许修改响应数据
  transformResponse: [function (data) {
    // 对 data 进行任意转换处理
    return data;
  }],

  // `headers` 是即将被发送的自定义请求头
  headers: {'X-Requested-With': 'XMLHttpRequest'},

  // `params` 是即将与请求一起发送的 URL 参数
  // 必须是一个无格式对象(plain object)或 URLSearchParams 对象
  params: {
    ID: 12345
  },

   // `paramsSerializer` 是一个负责 `params` 序列化的函数
  // (e.g. https://www.npmjs.com/package/qs, http://api.jquery.com/jquery.param/)
  paramsSerializer: function(params) {
    return Qs.stringify(params, {arrayFormat: 'brackets'})
  },

  // `data` 是作为请求主体被发送的数据
  // 只适用于这些请求方法 'PUT', 'POST', 和 'PATCH'
  // 在没有设置 `transformRequest` 时，必须是以下类型之一：
  // - string, plain object, ArrayBuffer, ArrayBufferView, URLSearchParams
  // - 浏览器专属：FormData, File, Blob
  // - Node 专属： Stream
  data: {
    firstName: 'Fred'
  },

  // `timeout` 指定请求超时的毫秒数(0 表示无超时时间)
  // 如果请求话费了超过 `timeout` 的时间，请求将被中断
  timeout: 1000,

   // `withCredentials` 表示跨域请求时是否需要使用凭证
  withCredentials: false, // default

  // `adapter` 允许自定义处理请求，以使测试更轻松
  // 返回一个 promise 并应用一个有效的响应 (查阅 [response docs](#response-api)).
  adapter: function (config) {
    /* ... */
  },

 // `auth` 表示应该使用 HTTP 基础验证，并提供凭据
  // 这将设置一个 `Authorization` 头，覆写掉现有的任意使用 `headers` 设置的自定义 `Authorization`头
  auth: {
    username: 'janedoe',
    password: 's00pers3cret'
  },

   // `responseType` 表示服务器响应的数据类型，可以是 'arraybuffer', 'blob', 'document', 'json', 'text', 'stream'
  responseType: 'json', // default

  // `responseEncoding` indicates encoding to use for decoding responses
  // Note: Ignored for `responseType` of 'stream' or client-side requests
  responseEncoding: 'utf8', // default

   // `xsrfCookieName` 是用作 xsrf token 的值的cookie的名称
  xsrfCookieName: 'XSRF-TOKEN', // default

  // `xsrfHeaderName` is the name of the http header that carries the xsrf token value
  xsrfHeaderName: 'X-XSRF-TOKEN', // default

   // `onUploadProgress` 允许为上传处理进度事件
  onUploadProgress: function (progressEvent) {
    // Do whatever you want with the native progress event
  },

  // `onDownloadProgress` 允许为下载处理进度事件
  onDownloadProgress: function (progressEvent) {
    // 对原生进度事件的处理
  },

   // `maxContentLength` 定义允许的响应内容的最大尺寸
  maxContentLength: 2000,

  // `validateStatus` 定义对于给定的HTTP 响应状态码是 resolve 或 reject  promise 。如果 `validateStatus` 返回 `true` (或者设置为 `null` 或 `undefined`)，promise 将被 resolve; 否则，promise 将被 rejecte
  validateStatus: function (status) {
    return status >= 200 && status < 300; // default
  },

  // `maxRedirects` 定义在 node.js 中 follow 的最大重定向数目
  // 如果设置为0，将不会 follow 任何重定向
  maxRedirects: 5, // default

  // `socketPath` defines a UNIX Socket to be used in node.js.
  // e.g. '/var/run/docker.sock' to send requests to the docker daemon.
  // Only either `socketPath` or `proxy` can be specified.
  // If both are specified, `socketPath` is used.
  socketPath: null, // default

  // `httpAgent` 和 `httpsAgent` 分别在 node.js 中用于定义在执行 http 和 https 时使用的自定义代理。允许像这样配置选项：
  // `keepAlive` 默认没有启用
  httpAgent: new http.Agent({ keepAlive: true }),
  httpsAgent: new https.Agent({ keepAlive: true }),

  // 'proxy' 定义代理服务器的主机名称和端口
  // `auth` 表示 HTTP 基础验证应当用于连接代理，并提供凭据
  // 这将会设置一个 `Proxy-Authorization` 头，覆写掉已有的通过使用 `header` 设置的自定义 `Proxy-Authorization` 头。
  proxy: {
    host: '127.0.0.1',
    port: 9000,
    auth: {
      username: 'mikeymike',
      password: 'rapunz3l'
    }
  },

  // `cancelToken` 指定用于取消请求的 cancel token
  // （查看后面的 Cancellation 这节了解更多）
  cancelToken: new CancelToken(function (cancel) {
  })
}
```

#### 请求响应结构

某个请求的响应包含以下信息

```JavaScript
{
  // `data` 由服务器提供的响应
  data: {},

  // `status` 来自服务器响应的 HTTP 状态码
  status: 200,

  // `statusText` 来自服务器响应的 HTTP 状态信息
  statusText: 'OK',

  // `headers` 服务器响应的头
  headers: {},

   // `config` 是为请求提供的配置信息
  config: {},
 // 'request'
  // `request` is the request that generated this response
  // It is the last ClientRequest instance in node.js (in redirects)
  // and an XMLHttpRequest instance the browser
  request: {}
}
```

使用 `then` 时，你将接收下面这样的响应 :

```JavaScript
axios.get('/user/12345')
  .then(function(response) {
    console.log(response.data);
    console.log(response.status);
    console.log(response.statusText);
    console.log(response.headers);
    console.log(response.config);
  });
```

在使用 `catch` 时，或传递 `rejection` `callback` 作为 `then` 的第二个参数时，响应可以通过 `error` 对象可被使用。

#### 配置默认值

-   全局的 axios 默认值

```JavaScript
axios.defaults.baseURL = 'https://api.example.com';
axios.defaults.headers.common['Authorization'] = AUTH_TOKEN;
axios.defaults.headers.post['Content-Type'] = 'application/x-www-form-urlencoded';
```

-   自定义实例默认值

```JavaScript
// Set config defaults when creating the instance
const instance = axios.create({
  baseURL: 'https://api.example.com'
});

// Alter defaults after instance has been created
instance.defaults.headers.common['Authorization'] = AUTH_TOKEN;
```

-   配置的优先顺序

配置会以一个优先顺序进行合并。这个顺序是：在 lib/defaults.js 找到的库的默认值，然后是实例的 `defaults` 属性，最后是请求的 `config` 参数。后者将优先于前者。请看以下例子：

```JavaScript
// 使用由库提供的配置的默认值来创建实例
// 此时超时配置的默认值是 `0`
var instance = axios.create();

// 覆写库的超时默认值
// 现在，在超时前，所有请求都会等待 2.5 秒
instance.defaults.timeout = 2500;

// 为已知需要花费很长时间的请求覆写超时设置
instance.get('/longRequest', {
  timeout: 5000
});
```

#### 拦截器

在请求或响应被 `then` 或 `catch` 处理前拦截它们。

```JavaScript
// 添加请求拦截器
axios.interceptors.request.use(function (config) {
    // 在发送请求之前做些什么
    return config;
  }, function (error) {
    // 对请求错误做些什么
    return Promise.reject(error);
  });

// 添加响应拦截器
axios.interceptors.response.use(function (response) {
    // 对响应数据做点什么
    return response;
  }, function (error) {
    // 对响应错误做点什么
    return Promise.reject(error);
  });
```

如果你想在稍后移除拦截器，可以这样：

```JavaScript
const myInterceptor = axios.interceptors.request.use(function () {/*...*/});
axios.interceptors.request.eject(myInterceptor);
```

可以为自定义 `axios` 实例添加拦截器

```JavaScript
const instance = axios.create();
instance.interceptors.request.use(function () {/*...*/});
```

#### 错误处理

```JavaScript
axios.get('/user/12345')
  .catch(function (error) {
    if (error.response) {
      // The request was made and the server responded with a status code
      // that falls out of the range of 2xx
      console.log(error.response.data);
      console.log(error.response.status);
      console.log(error.response.headers);
    } else if (error.request) {
      // The request was made but no response was received
      // `error.request` is an instance of XMLHttpRequest in the browser and an instance of
      // http.ClientRequest in node.js
      console.log(error.request);
    } else {
      // Something happened in setting up the request that triggered an Error
      console.log('Error', error.message);
    }
    console.log(error.config);
  });
```

可以使用 `validateStatus` 配置选项定义一个自定义 `HTTP` 状态码的错误范围。

```JavaScript
axios.get('/user/12345', {
  validateStatus: function (status) {
    return status < 500; // Reject only if the status code is greater than or equal to 500
  }
})
```

#### 取消请求

使用 `cancel` `token` 取消请求

> Axios 的 cancel token API 基于 cancelable promises proposal，它还处于第一阶段。

可以使用 CancelToken.source 工厂方法创建 `cancel` `token`，像这样：

```JavaScript
const CancelToken = axios.CancelToken;
const source = CancelToken.source();

axios.get('/user/12345', {
  cancelToken: source.token
}).catch(function(thrown) {
  if (axios.isCancel(thrown)) {
    console.log('Request canceled', thrown.message);
  } else {
     // 处理错误
  }
});

axios.post('/user/12345', {
  name: 'new name'
}, {
  cancelToken: source.token
})

// 取消请求（message 参数是可选的）
source.cancel('Operation canceled by the user.');
```

还可以通过传递一个 `executor` 函数到 `CancelToken` 的构造函数来创建 `cancel` `token`：

```JavaScript
const CancelToken = axios.CancelToken;
let cancel;

axios.get('/user/12345', {
  cancelToken: new CancelToken(function executor(c) {
    // executor 函数接收一个 cancel 函数作为参数
    cancel = c;
  })
});

// cancel the request
cancel();
```

> 注意: 可以使用同一个 `cancel` `token` 取消多个请求

#### 使用 `application/x-www-form-urlencoded format`

默认情况下，`axios` 将 `JavaScript` 对象序列化为 `JSON`。 要以 `application / x-www-form-urlencoded` 格式发送数据，您可以使用以下选项之一。

-   浏览器
    在浏览器中，您可以使用 `URLSearchParams API`，如下所示：

```JavaScript
const params = new URLSearchParams();
params.append('param1', 'value1');
params.append('param2', 'value2');
axios.post('/foo', params);
```

> 请注意，所有浏览器都不支持 URLSearchParams（请参阅 caniuse.com），但可以使用 polyfill（确保填充全局环境）。

或者，您可以使用 `qs` 库编码数据：

```JavaScript
const qs = require('qs');
axios.post('/foo', qs.stringify({ 'bar': 123 }));
```

或者以另一种方式（ES6）

```JavaScript
import qs from 'qs';
const data = { 'bar': 123 };
const options = {
  method: 'POST',
  headers: { 'content-type': 'application/x-www-form-urlencoded' },
  data: qs.stringify(data),
  url,
};
axios(options);
```

-   `Node.js`
    在 `node.js` 中，您可以使用 `querystring` 模块，如下所示：

```JavaScript
const querystring = require('querystring');
axios.post('http://something.com/', querystring.stringify({ foo: 'bar' }));
```

您也可以使用 `qs` 库。

#### 在 `vue` 中封装 `axios`

初级版封装

```JavaScript
// 封装axios请求，官网：`https://www.npmjs.com/package/axios,axios`还可以同时处理多个接口请求，这里先不做介绍
// params是添加到url的请求字符串中的，用于get请求,例如`shinyway.com?key=params`
// 而data是添加到请求体（body）中的， 用于post请求,传递参数
import axios from 'axios'
import store from '@/store/index'
import qs from 'qs' // node.js的产物,序列化请求数据，视服务端的要求需不需要,暂且先用
import router from '@/router' // 用于在判断错误时的重定向页面，例如404页面等
import { getToken } from '@/utils/auth'

// 创建axios实例 axiso的一些基础参数配置,
const service = axios.create({
  baseURL: process.env.BASE_API, // 配置在config/prod.env里的baseApi
  timeout: 5000 // 超时时间
})
// 传参拦截器
service.interceptors.request.use(
  config => {
    //  打开loadding
    store.commit('CONTROL_LOADDING', true)
    if (store.getters.token) {
      config.headers['X-Token'] = getToken() // 让每个请求携带token--['X-Token']为自定义key 请根据实际情况自行修改
    }
    // 判断为post请求，序列化传来的参数
    if (config.method === 'post' || config.method === 'put' || config.method === 'delete') {
      config.data = qs.stringify(config.data)
    }
    return config
  }, error => {
    // 处理错误信息
    // alert(error.data.error.message)
    return Promise.reject(error)
  })

// 响应拦截器
service.interceptors.response.use(res => {
  // 请求成功时要做的处理

  // 对响应数据做些事，把loading动画关掉
  store.commit('CONTROL_LOADDING', false)
  // 对请求成功的值进行统一判断
  //   1.判空
  if (res.data === '' || res.data.length === 0 || res.data === 'undefined' || res.data === undefined) {
    console.log('后台传来的data为空/为undefined')
  }
  //   2.错误提示(前提是接口跑通了，只是对里边某些值做下详细判断。要先跟后台商定好，对某个固定的字段进行判断，并且确定固定字段来承接 错误信息，方便展示)
  // if (res.data && !res.data.success) {
  //  console.log(res.data.error.message)
  // }
  return res.data
}, error => {
  // 请求错误时做些事(接口错误、超时等)

  // 关闭loadding
  store.commit('CONTROL_LOADDING', false)
  console.log(error) // 打开控制台，可以看到error包含了几个对象:message, config, code, request, response,可以拿来请求超时等问题

  //  1.判断请求超时
  if (error.code === 'ECONNABORTED' && error.message.indexOf('timeout') !== -1) {
    console.log('根据你设置的timeout/真的请求超时 判断请求现在超时了，你可以在这里加入超时的处理方案')
    // return service.request(originalRequest);//例如再重复请求一次
  }
  //  2.需要重定向到错误页面
  const errorInfo = error.response
  console.log(errorInfo)
  if (errorInfo) {
    // error =errorInfo.data//页面那边catch的时候就能拿到详细的错误信息,看最下边的Promise.reject
    if (errorInfo.status === 403) {
      router.push({
        path: '/error/403'
      })
    }
    // if (errorInfo.status === 500) {
    //   router.push({
    //     path: "/error/500"
    //   });
    // }
    // if (errorInfo.status === 502) {
    //   router.push({
    //     path: "/error/502"
    //   });
    // }
    // if (errorInfo.status === 404) {
    //   router.push({
    //     path: "/error/404"
    //   });
    // }
  }
  return Promise.reject(error) // 在调用的那边可以拿到(catch)你想返回的错误信息
})
export default service

```

进阶版封装

```js
/**axios封装
 * 请求拦截、相应拦截、错误统一处理
 */

// 在http.js中引入axios
import axios from "axios";
// 引入qs模块，用来序列化post类型的数据
import QS from "qs";
// mint-ui的toast提示框组件，大家可根据自己的ui组件更改
import { Toast } from "mint-ui";
import store from "../store/index";

// 环境的切换
if (process.env.NODE_ENV === "development") {
    axios.defaults.baseURL = "http://www.dev.com";
} else if (process.env.NODE_ENV === "test") {
    axios.defaults.baseURL = "http://www.test.com";
} else if (process.env.NODE_ENV === "production") {
    axios.defaults.baseURL = "http://www.pro.com";
}

// 请求超时时间
axios.defaults.timeout = 10000;

// post请求头
axios.defaults.headers.post["Content-Type"] =
    "application/x-www-form-urlencoded;charset=UTF-8";

// 请求拦截器
axios.interceptors.request.use(
    (config) => {
        // 每次发送请求之前判断是否存在token，如果存在，则统一在http请求的header都加上token，不用每次请求都手动添加了
        // 即使本地存在token，也有可能token是过期的，所以在响应拦截器中要对返回状态进行判断
        const token = store.state.token;
        token && (config.headers.Authorization = token);
        return config;
    },
    (error) => {
        return Promise.error(error);
    }
);

// 响应拦截器
axios.interceptors.response.use(
    (response) => {
        if (response.status === 200) {
            return Promise.resolve(response);
        } else {
            return Promise.reject(response);
        }
    },
    // 服务器状态码不是200的情况
    (error) => {
        if (error.response.status) {
            switch (error.response.status) {
                // 401: 未登录
                // 未登录则跳转登录页面，并携带当前页面的路径
                // 在登录成功后返回当前页面，这一步需要在登录页操作。
                case 401:
                    router.replace({
                        path: "/login",
                        query: { redirect: router.currentRoute.fullPath },
                    });
                    break;
                // 403 token过期
                // 登录过期对用户进行提示
                // 清除本地token和清空vuex中token对象
                // 跳转登录页面
                case 403:
                    Toast("登录过期，请重新登录");
                    // 清除token
                    localStorage.removeItem("token");
                    store.commit("loginSuccess", null); // 不太懂的话可不对状态码进行操作
                    // 跳转登录页面，并将要浏览的页面fullPath传过去，登录成功后跳转需要访问的页面
                    setTimeout(() => {
                        router.replace({
                            path: "/login",
                            query: {
                                redirect: router.currentRoute.fullPath,
                            },
                        });
                    }, 1000);
                    break;
                // 404请求不存在
                case 404:
                    Toast("网络请求不存在");
                    break;
                // 其他错误，直接抛出错误提示
                default:
                    Toast(error.response.data.message);
            }
            return Promise.reject(error.response);
        }
    }
);
/**
 * get方法，对应get请求
 * @param {String} url [请求的url地址]
 * @param {Object} params [请求时携带的参数]
 */
export function get(url, params) {
    return new Promise((resolve, reject) => {
        axios
            .get(url, {
                params: params,
            })
            .then((res) => {
                resolve(res.data);
            })
            .catch((err) => {
                reject(err.data);
            });
    });
}
/**
 * post方法，对应post请求
 * @param {String} url [请求的url地址]
 * @param {Object} params [请求时携带的参数]
 */
export function post(url, params) {
    return new Promise((resolve, reject) => {
        axios
            .post(url, QS.stringify(params))
            .then((res) => {
                resolve(res.data);
            })
            .catch((err) => {
                reject(err.data);
            });
    });
}
```
