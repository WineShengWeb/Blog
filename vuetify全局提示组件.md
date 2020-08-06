# vuetify 全局提示组件

elment 有一个 Message 可以全局提示的控件很是羡慕，但是作为一位后端人员又不想搞太多前端 css，喜欢用 vuetify，但是没有全局 Message，只好自己动手实现一个了。

接下来让我们一步步实现
首先在 src/commponents/下创建 Message 目录，并在 Message 目录下创建
Message.vue 和 index.js 文件，文件位置如下：

Message.vue 的代码如下：

```vue
<template>
    <transition name="message-fade">
        <div class="message" :class="typeClass" role="alert" v-show="visible">
            <p class="message__content">
                <v-icon large :color="color" small="true">{{ icon }}</v-icon>
                &nbsp;{{ message }}
            </p>
        </div>
    </transition>
</template>

<script>
export default {
    name: "message",

    data() {
        return {
            visible: false,
            duration: 2000,
            message: "",
            timer: null,
            closed: false,
            color: "",
            icon: "",
            typeClass: "",
        };
    },

    watch: {
        closed(val) {
            if (val) {
                this.visible = false;
                this.$el.addEventListener("transitionend", this.destroyElement);
            }
        },
    },

    methods: {
        destroyElement() {
            this.$el.removeEventListener("transitionend", this.destroyElement);
            this.$destroy(true);
            this.$el.parentNode.removeChild(this.$el);
        },

        startTimer() {
            if (this.duration > 0) {
                this.timer = setTimeout(() => {
                    if (!this.closed) {
                        this.close();
                    }
                }, this.duration);
            }
        },

        close() {
            this.closed = true;
        },
    },

    mounted() {
        // 开始定时器
        this.startTimer();
    },
};
</script>

<style scoped>
.message {
    min-width: 380px;
    box-sizing: border-box;
    border-radius: 4px;
    border-width: 1px;
    border-style: solid;
    /* border-color: #ebeef5; */
    position: fixed;
    left: 50%;
    top: 20px;
    transform: translateX(-50%);
    /* background-color: #edf2fc; */
    transition: opacity 0.3s, transform 0.4s;
    overflow: hidden;
    padding: 15px 15px 15px 20px;
    display: flex;
    align-items: center;
}

.message--success {
    background-color: #f0f9eb;
    border-color: #e1f3d8;
    color: #67c23a;
}

.message--error {
    background-color: #ffccff;
    border-color: #ffccff;
    color: #cc0033;
}

.message p {
    margin: 0;
}

.message__content {
    padding: 0;
    font-size: 14px;
    line-height: 1;
}

.message-fade-enter,
.message-fade-leave-active {
    opacity: 0;
    transform: translate(-50%, -100%);
}
</style>
```

index 中的代码如下：

```js
import Vue from "vue";
import Main from "./Message.vue";

let MessageConstructor = Vue.extend(Main);

let instance;
let instances = [];
let seed = 1;
const Message = function (options, color, icon, typeClass) {
    options = options || {};
    if (typeof options === "string") {
        options = {
            message: options,
            color: color,
            icon: icon,
            typeClass: typeClass,
        };
    }
    let id = "message_" + seed++;
    instance = new MessageConstructor({
        data: options,
    });
    instance.id = id;
    instance.vm = instance.$mount();
    document.body.appendChild(instance.vm.$el);
    instance.vm.visible = true;
    instance.dom = instance.vm.$el;
    instance.dom.style.zIndex = 10000;
    instances.push(instance);
    return instance.vm;
};

Message.success = function (option) {
    Message(option, "#67c23a", "beenhere", "message--success");
};
Message.error = function (option) {
    Message(option, "#CC0033", "mdi-backspace", "message--error");
};

Message.close = function (id) {
    for (let i = 0, len = instances.length; i < len; i++) {
        if (id === instances[i].id) {
            instances.splice(i, 1);
            break;
        }
    }
};

Message.closeAll = function () {
    for (let i = instances.length - 1; i >= 0; i--) {
        instances[i].close();
    }
};

export default Message;
```

由于某些原因未实现警告框，如果需要添加，请在 Message.vue 中的 style 添加如下:【请改变下列颜色，不要原封不动】

```css
.message--alert {
    //背景颜色
    background-color: #f0f9eb;
    //边框颜色
    border-color: #e1f3d8;
    //文字颜色
    color: #67c23a;
}
```

index.js 中添加如下，

```js
Message.alert = function (option) {
    //请更改第二个和第三个参数，第三个参数是图标，就像success的‘√’，第二个参数是图标的颜色
    Message(option, "#67c23a", "beenhere", "message--alert");
};
```

不过，警告框好像没什么作用，那么如上就当作我在帮忙讲解一下这些内容吧，接下来讲一下怎么用

首先需要在 main.js 中注册

```js
import Message from "./components/Message/index.js";
//引入这个是为了解决有时候图标展示不正常，可以先注释了尝试一下
import "material-design-icons-iconfont/dist/material-design-icons.css";

Vue.prototype.$message = Message;
```

第二个参数亲测不加会有些图标展示不正常或者不出现，详细解决办法请参考部分图标展示不正常
也可以先不解决这个问题，看一下正常不，不正常在返回来解决这个问题，也很简单【温馨提示：在进入上述链接执行 npm 命令后我会出现 node_modules 中 axios 引用被删除的问题，本着不求甚解的精神，为了以防万一，建议首先将这个文件夹复制出来，在执行之后如果被删除，粘贴进去即可！】
接下来就可以在想使用的地方使用了：如下

```js
//成功提示
this.$message.success(`success这是一条消息`);
//失败提示
this.$message.error(`error这是一条消息`);
```

还有一个问题，在使用拦截器 interceptors 的时候，做统一异常处理的时候回调用 this.\$message.error(error 这是一条消息) 的时候没有效果，这个是因为 this 都找不到，这个时候如下操作：

```js
//导入/components/Message/index.js
import Message from "../components/Message/index.js";
```

然后可以使用 Message.error();来进行调用。
