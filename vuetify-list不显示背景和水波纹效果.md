# vuetify 框架使用中 list 组件悬浮变色和水波纹效果的解决办法

##### 问题：list 组件悬浮变色和水波纹效果丢失

在日常开发中，遇到 vuetify 框架中把 list 组件中的代码 copy 到项目中时，list 组件悬浮变色和水波纹效果丢失，以下代码中是 list 组件的使用：

```
<v-menu v-model="value" offset-y nudge-bottom="8px" left>
    <template v-slot:activator="{ on, attrs }">
        <v-btn class="mx-2" icon fab dark v-bind="attrs" v-on="on">
            <v-icon dark>mdi-plus</v-icon>
        </v-btn>
    </template>
    <v-list>
        <v-list-item v-for="(item, index) in items" :key="index">
            <v-list-item-title @click="release(item.path)">
                <svg-icon :icon-class="item.icon" class="icon"></svg-icon>
                {{ item.title }}
            </v-list-item-title>
        </v-list-item>
    </v-list>
</v-menu>
```

组件是可以正常使用，但当鼠标移上去时，当前项没有悬浮变色，点击当前项是也没有水波纹效果。

##### 解决办法：向组件中添加 <v-list-item-group></v-list-item-group> 标签

把 list 组件中的内容用 <v-list-item-group></v-list-item-group> 标签包裹起来，也就是放到一个组中，代码如下：

```
<v-list>
    <v-list-item-group>
        <v-list-item v-for="(item, index) in items" :key="index">
            <v-list-item-title @click="release(item.path)">
                    <svg-icon :icon-class="item.icon" class="icon"></svg-icon>
                    {{ item.title }}
            </v-list-item-title>
        </v-list-item>
    </v-list-item-group>
</v-list>
```

问题完美解决。
