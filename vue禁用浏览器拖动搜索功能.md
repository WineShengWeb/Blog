# 解决 vue 中使用 vue-draggable 组件时，火狐浏览器自动搜索的问题

### 问题

在项目中使用 vue-draggable 组件进行拖动排序时，会在火狐浏览器上会打开新窗口自动搜索所拖动的文字。但项目并不需要搜索功能，所以需要禁用。

### 解决办法

在vue实例生命周期的 created 或 mountend 中将以下代码放进去：

```js
/* 阻止火狐浏览器在  vue-draggable组件时拖动 打开新窗口 */
mounted() {
    document.body.ondrop = function (event) {
        event.preventDefault()
        event.stopPropagation()
    }
},
```

