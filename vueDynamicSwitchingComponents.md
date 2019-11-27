<!--
 * @Author: guoxinggang<guoxinggang@gsaxns.com>
 * @Version: 1.0
 * @Date: 2019-11-21 14:34:39
 * @LastEditTime: 2019-11-21 16:16:43
 * @Description: 
 -->
# vue同页面动态切换组件

实现思路：在一个框架页面内左边循环添加导航栏并添加路径，路径在路由中定义好后再data里对象写入路径，右边给一个**<router-view></router-view>**标签让它动态切换显示组件

HTML代码

```html
// :to="{ path:item.path }"  要跳转的路径
// <router-view></router-view>  组件显示的地方
<template>
    <div class="demo">
        <!-- 左边循环导航栏并添加路径 -->
        <ul class="sideList">
            <li  @click="addClass(index)" :class="{'actives':i==index}" v-for="(item,index) in data" :key="index">
                <router-link :to="{ path:item.path }">{{ item.name }}</router-link>
            </li>
        </ul>
        <div class="right_side">
            <router-view></router-view>
        </div>
    </div>
</template>
```

js代码

```html
<script>
export default {
  name: 'demo',
  data () {
    return {
      i: 0,
      data: [
        { name: '公司简介', path: '/aboutUs' },
        { name: '资质荣誉', path: '/qualificationHonor' },
        { name: '诚聘英才', path: '/Recruitment' },
        { name: '联系我们', path: '/contactUs' }
      ]
    }
  },
  // 动态添加css样式
  methods: {
    addClass (index) {
      this.i = index
    }
  }
}
</script>
```

router.js文件

```javascript
{
    path: '/aboutUs',
    name: 'aboutUs',
    component: aboutUs,
    children: [
    {
        path: '/aboutUs', // 公司简介
        name: 'AboutUs',
        component: resolve => require(['@/view/aboutUs/components/AboutUs.vue'], resolve)
    },
    {
        path: '/qualificationHonor', // 资质荣誉
        name: 'qualificationHonor',
        component: resolve => require(['@/view/aboutUs/components/qualificationHonor.vue'], resolve)
    },
    {
        path: '/Recruitment', // 诚聘英才
        name: 'Recruitment',
        component: resolve => require(['@/view/aboutUs/components/Recruitment.vue'], resolve)
    },
    {
        path: '/contactUs', // 联系我们
        name: 'contactUs',
        component: resolve => require(['@/view/aboutUs/components/contactUs.vue'], resolve)
    }
    ]
}
```
