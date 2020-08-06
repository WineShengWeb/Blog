# axios 封装

安装 `axios`

```npm
npm install axios
```

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

进阶版

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
