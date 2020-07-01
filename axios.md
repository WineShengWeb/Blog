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
