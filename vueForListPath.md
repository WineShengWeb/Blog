<!--
 * @Author: guoxinggang<guoxinggang@gsaxns.com>
 * @Version: 1.0
 * @Date: 2019-11-21 15:05:05
 * @LastEditTime: 2019-11-21 16:16:17
 * @Description: 
 -->
# vue使用for循环给导航栏批量添加路径

## 配置路由

router.js中配置好对应的路由表

HTML代码

```html
<template>
    <div class="header">
        <nav>
            <div class="name">
                <h2>***技术有限公司</h2>
            </div>
            <ul class="nav">
                <li v-for="(item,index) in nav" :key="index">
                    <router-link :to="{ path:item.path }">{{ item.name }}</router-link>
                    <div class="list">
                        <div class="arrows"></div>
                        <div class="hide_list">
                            <ul>
                                <li v-for="(index,item) in item.list" :key="item">
                                    <router-link :to='{ path:index.path }'>{{ index.name }}</router-link>
                                </li>
                            </ul>
                        </div>
                    </div>
                </li>
            </ul>
        </nav>
    </div>
</template>
```

js代码

```html
<script>
export default {
  data () {
    return {
      nav: [
        {
          name: '首页',
          path: '/',
          list: []
        },
        {
          name: '安全研究',
          path: '/mobile',
          list: [
            {name: '移动互联网安全', path: '/mobile'},
            {name: '云计算环境安全', path: '/cloud'},
            {name: '工业控制系统安全', path: '/industrial'}
          ]
        },
        {
          name: '安全服务',
          path: '/securityService',
          list: [
            {name: '等级保护测评服务', path: '/securityService'},
            {name: '风险评估服务', path: '/exposureRating'},
            {name: '渗透测试服务', path: '/penetrationTesting'},
            {name: '安全运维服务', path: '/securityOperations'},
            {name: '应急响应服务', path: '/emergencyResponse'}
          ]
        },
        {
          name: '新闻中心',
          path: '/news',
          list: [
            {name: '公司动态', path: '/news'},
            {name: '行业资讯', path: '/industryInformation'},
            {name: '技术交流', path: '/technicalExchange'}
          ]
        },
        {
          name: '关于我们',
          path: '/aboutUs',
          list: [
            {name: '公司简介', path: '/aboutUs'},
            {name: '资质荣誉', path: '/qualificationHonor'},
            {name: '诚聘英才', path: '/Recruitment'},
            {name: '联系我们', path: '/contactUs'}
          ]
        }
      ]
    }
  }
}
</script>
```
