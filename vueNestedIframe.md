# vue 嵌套 iframe 页面

#### 嵌套页面

```html
<iframe class="iframeBox" ref="myiframe" src="/flowChart/verification.html"  frameborder="0" scrolling="no"></iframe>
```

#### 父页面向子页面传递数据

```js
// FrameName.window.childMethod();
this.$refs.myiframe.contentWindow.childMethod(data)
```

#### 子页面向父页面传递数据

```js
// parent.window.parentMethod();
// 子页面发送数据
var guideModal = {
    type: 'guideModal',
    isOpen: true,
    step: 1,
    isDisable: false,
    tips: '欢迎使用流程图向导模式，点按钮开始！'
}
window.parent.postMessage(guideModal, '*');

// 父页面接收数据
window.addEventListener('message', (event) => {
    console.log('event', event.data)
})
```