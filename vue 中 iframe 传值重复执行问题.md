# vue 中 iframe 传值重复执行的问题

## 出现的问题

> 在 vue 页面中添加事件监听后,  message 弹框会重复执行多次，并且无法移除事件监听

#### 代码

```js
mounted() {
    let _this = this
    // 添加监听 iframe 消息
    window.addEventListener('message', this.eventListenerHandler, false)
    window.removeEventListener('message', this.eventListenerHandler, false)
}
```
> methods 里注册事件 

```js
// 监听 iframe 消息事件
eventListenerHandler(event) {
    let _this = this
    // 成功提示
    if (event.data.type == 'successMsg') {
    _this.spinning = false
    _this.$message.success(event.data.message)
    }

    // 错误提示
    if (event.data.type == 'errorMsg') {
    _this.spinning = false
    _this.$message.error(event.data.message)
    }
},
```

> 页面渲染时事件又重复绑定执行了，没有解绑成功




## 解决方案

> 在页面挂载时添加事件监听，在页面销毁时对删除事件监听

#### 添加监听事件

```js
mounted() {
// 添加监听 iframe 消息
window.addEventListener('message', this.eventListenerHandler, false)
},
```

#### 在生命周期结束时销毁

```js
// 页面销毁后
destroyed() {
// 销毁事件监听
// TODO：修复 iframe 弹框重复问题
window.removeEventListener('message', this.eventListenerHandler, false)
},
```

#### 完整文件

```vue
<template>
  <div class="flowBox">
    <iframe ref="myiframe" src="/flowChart/design.html" class="iframe" frameborder="0" scrolling="no"></iframe>
  </div>
</template>

<script>
export default {
  data() {
    return {
        spinning: false,
    }
  },
  mounted() {
    // 添加监听 iframe 消息
    window.addEventListener('message', this.eventListenerHandler, false)
  },
  // 页面销毁后
  destroyed() {
    // 销毁事件监听
    // TODO：修复 iframe 弹框重复问题
    window.removeEventListener('message', this.eventListenerHandler, false)
  },
  methods: {
    // 监听 iframe 消息事件
    eventListenerHandler(event) {
      let _this = this
      // 成功提示
      if (event.data.type == 'successMsg') {
        _this.spinning = false
        _this.$message.success(event.data.message)
      }

      // 错误提示
      if (event.data.type == 'errorMsg') {
        _this.spinning = false
        _this.$message.error(event.data.message)
      }
    },
  },
}
</script>
```

> 成功移除。