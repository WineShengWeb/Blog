# v-resize Demo

# 安装

```node
npm install v-resize || yarn add v-resize
```

# 使用

```vue
<template>
    <div class="box" v-resize="options"></div>
</template>

<script>
import VResize from "v-resize";
export default {
    directives: {
        resize: VResize,
    },
    data() {
        return {
            options: {
                // 回调函数
                onResize(params) {
                    console.log(params);
                },
                // 方向
                directions: [
                    "top",
                    "bottom",
                    "left",
                    "right",
                    "left-top",
                    "bottom-right",
                    "right-top",
                    "bottom-left",
                ],
            },
        };
    },
};
</script>

<style scoped lang="scss">
.box {
    width: 100px;
    height: 500px;
    border-right: 1px solid #111;
}
</style>
```

详细配置请参考[官网](https://github.com/next-pieces/v-resize)
