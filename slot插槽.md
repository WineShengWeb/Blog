# vue 中 slot 插槽详解

插槽含义：就是引入子组件后，在插入子组件元素中添加信息或者标签，使得子组件的指定位置插入信息或者标签

插槽有三种：默认插槽、具名插槽、作用域插槽，由于 vue2.6.0 后对插槽进行修改，但是兼容 2.6.0 前的版本，博文中只说明 2.6.0 后的插槽，vue3.0 后面会去除 2.60 前的版本兼容

##### 有什么用

> 调用组件时，写在组件标签内的内容，默认不会被渲染
> 有时，需要组件标签内的内容能被渲染出来，slot 插槽实现

##### slot 的基本使用

> 1、定义组件时想好要在哪个位置去渲染 slot 内容
> 2、在想好的位置哪里，放置一个 slot 标签 即可 <slot></slot>
> 3、slot 内容 就会自动去替换 slot 标签

##### 默认插槽

> 写在 slot 标签内的内容就是这个 slot 标签的默认内容

子组件定义插槽

```vue
<template>
    <div>
        <div>我是子组件</div>
        <slot></slot>
    </div>
</template>
```

父组件调用子组件

```vue
<template>
    <div>
        <children>
            <div>我是默认插槽</div>
        </children>
    </div>
</template>
```

##### 具名插槽

给 slot 标签 设置一个 name 属性。这时 slot 标签叫做 具名 slot 标签

> 1、slot 在一个组件内是可以使用多次的
> 2、给 slot 取了名字之后，slot 内容想要 渲染在哪个 slot，就需要设置 slot 属性。属性的值为某个 slot 的名

-   slot 有一个默认的名字，就叫做 default，<slot></slot> => <slot name="default"></slot>

子组件定义插槽

```vue
<template>
    <div>
        <div>我是子组件</div>
        <slot name="top"></slot>
        <slot></slot>
    </div>
</template>
```

父组件调用子组件

```vue
<template>
    <div>
        <children>
            <div>你好</div>
            <div slot="top">加油</div>
        </children>
    </div>
</template>
```

##### 作用域插槽

> 插槽内容 中使用 子组件中的作用域

```html
<div id="app">
    <hello>
        // xxxx 如何能够用上 hello 组件中 的 msg 数据
        <p>我是一个插槽内容。xxxx</p>
    </hello>
</div>
```

-   1.定义组件的 slot 的时候，将要在插槽内容中使用的数据，绑定在 slot 标签上
    `<slot :a="msg" :b="age" ></slot>`
-   2.在插槽内容的标签上，设置 slot-scope 属性。属性值随便写。这个属性值就是上一个步骤中绑定出来的数据的一个大对象
    `<p slot-scope="obj">我是一个插槽内容。msg, age</p>`
    `obj === { a: "hello", b: 19 }`

> 注意：不能绑定 name 属性。因为 name 属性有特殊用途。name 属性用来做具名插槽的。

```html
<div id="app">
    <hello>
        <p slot-scope="{a,b}">{{b}}{{a}}</p>
    </hello>
</div>
<script src="https://cdn.jsdelivr.net/npm/vue@2.6.11/dist/vue.js"></script>
<script>
    Vue.component("hello", {
        data: function () {
            return {
                msg: "hello",
                age: 2,
            };
        },
        template: `
                <div>
                    <slot :a='msg' :b='age'></slot>
                    <h1>1</h1>
                </div>
            `,
    });
    var vm = new Vue({
        el: "#app",
        data: {},
    });
</script>
```

##### v-slot

slot 插槽 在 2.6.0 这个版本的时候，做了更新。提供了一个新的指令叫做 v-slot。
后续实现具名插槽与作用域插槽都使用 v-slot 来实现

v-slot 语法
v-slot:xxxx=yyyy
xxxx 插槽名字
yyyy 作用域插槽数据

> 1、v-slot 必须用在 template 元素上。
> 2、如果插槽没有设置 name 名字的话： v-slot => v-slot:default
> 3、v-slot 简写 #：注意: 使用 简写时必须携带名字。默认的名字需要写成： ' #default '
> 4、插槽只有一个的情况下，可以不使用 template 去包裹插槽内容。而是直接将 v-slot 写在组件标签上。

```html
<div id="app">
    <helloworld2 #bottom>
        <p>加油</p>
    </helloworld2>
    <hr />
    <helloworld>
        <template #top>
            <p>我的天</p>
        </template>

        <template #default>
            <p>我的地</p>
        </template>
    </helloworld>

    <hr />

    <!-- 老语法的具名插槽使用 -->
    <hello>
        <p slot="top">我的天</p>

        <p slot="bottom">我的地</p>
    </hello>
    <!-- 新语法的具名插槽使用 -->
    <hello>
        <template #top>
            <p>我的天</p>
        </template>

        <template #bottom>
            <p>我的地</p>
        </template>
    </hello>

    <!-- 老语法的作用域插槽使用 -->
    <world>
        <p slot="top" slot-scope="{ msg, age }">
            我的天-{{ msg }} - {{ age }}
        </p>
    </world>

    <!-- 新语法的作用域插槽使用 -->
    <world>
        <template #top="obj">
            <p>
                我的天-{{ obj.msg }} - {{ obj.age }}
            </p>
        </template>
    </world>

    <!-- 新语法的作用域插槽使用 解构赋值-->
    <world>
        <template #top="{ msg, age }">
            <p>
                我的天-{{ msg }} - {{ age }}
            </p>
        </template>
    </world>
</div>

<script src="https://cdn.jsdelivr.net/npm/vue@2.6.11/dist/vue.js"></script>
<script>
    Vue.component("hello", {
        template: `
        <div>
        <slot name="top"></slot>
        <h1>hello</h1>
        <slot name="bottom"></slot>
        </div>
    `,
    });
    Vue.component("world", {
        data() {
            return {
                msg: "张三",
                age: 18,
            };
        },
        template: `
        <div>
        <slot name="top" :msg="msg" :age="age"></slot>
        <h1>world</h1>
        <slot name="bottom"></slot>
        </div>
    `,
    });
    Vue.component("helloworld", {
        template: `
        <div>
        <slot name="top"></slot>
        <h1>helloworld</h1>
        <slot></slot>
        </div>
    `,
    });
    Vue.component("helloworld2", {
        template: `
        <div>
        <h1>helloworld2</h1>
        <slot name="bottom"></slot>
        </div>
    `,
    });
    var vm = new Vue({
        el: "#app",
    });
</script>
```

将组件标签内的内容渲染出来，使用 slot 插槽
然后又想在插槽内使用组件内的数据：

1.先在 slot 标签上用动态属性的形式接收数据,例如:
:属性名='组件内的变量名'
`<slot :a='msg' :b='age'></slot>`

2.在插槽内容的标签上，设置 slot-scope
`<p slot-scope='{a,b}'>{{b}}{{a}}</p>`

3.新语法: v-slot 写在 template 上，
<template #top="{ msg, age }"> ====> v-slot= slot + slot-scope 具名+作用域'

4.默认：#default (default 不可省略)


### 插槽使用示例

#### 子组件中创建插槽

> 1、样式必须使用 `/deep/` 进行样式穿透，否则插槽内的内容没有样式；
>
> 2、父组件调用时不适用插槽，则该插槽不显示；
> 
> 3、传值的时候使用 `:data="data"` 的方式，父组件接收数据时使用 `v-slot:插槽名称="data"` ，使用数据时 `data.data.courseName`。

```html
<template>
  <div class="courseList">
    <!-- 数据列表 -->
    <div v-if="dataList != undefined && dataList.length > 0">
      <a-row type="flex" justify="start" :gutter="[16, 16]">
        <a-col :xs="24" :sm="24" :md="12" :lg="12" :xl="8" :xxl="6" v-for="(item, index) in dataList" :key="index">
          <div class="courseDataList">
            <!-- 有背景图 -->
            <div
              class="dataHeader"
              v-if="item.bgimage"
              :style="{
                backgroundImage: 'url(' + getbgimg(item.bgimage) + ') ',
                backgroundPosition: bgimgStyle(item.bgimageStyle),
              }"
            >
              <slot name="courseName" :data="item" />
              <slot name="describe" :data="item" />
              <slot name="isCompleteCourse" :data="item" />
            </div>
            <!-- 没有背景图，系统默认 -->
            <div class="head" v-else>
              <slot name="courseName" :data="item" />
              <slot name="describe" :data="item" />
              <slot name="isCompleteCourse" :data="item" />
            </div>
            <div class="courseInformation">
              <!-- 课程信息 -->
              <div class="courseContent">
                <slot name="courseContent" :data="item" />
              </div>
              <div class="courseCatalogue">
                <slot name="courseCatalogue" :data="item" />
              </div>
              <a-divider class="divider" />
              <!-- 我的 -->
              <div class="actionArea">
                <div class="source">
                  <!-- 课程来源 / 是否发布 / 创建时间 -->
                  <slot name="source" :data="item" />
                </div>
                <div class="action">
                  <!-- 操作按钮 -->
                  <slot class="action" name="actions" :data="item" :index="index" />
                </div>
              </div>
            </div>
          </div>
        </a-col>
      </a-row>
    </div>
    <!-- 空状态 -->
    <div class="empty" v-else>
      <a-empty />
    </div>
  </div>
</template>

<script>
export default {
  props: {
    dataList: {
      require: true,
      type: Array,
    },
  },
  data() {
    return {}
  },
  mounted() {
    // console.log(this.dataList)
  },
  computed: {
    // 课程id
    // quoteCourseId() {
    //   return this.$route.query.quoteCourseId
    // },
  },
  methods: {
    // 背景图样式
    bgimgStyle(value) {
      if (value == '00') {
        return '0px 0px'
      } else if (value == '01') {
        return '-400px 0px'
      } else if (value == '02') {
        return '-800px 0px'
      } else if (value == '10') {
        return '0px 0px'
      } else if (value == '11') {
        return '-400px 0px'
      } else if (value == '12') {
        return '-800px 0px'
      } else if (value == '20') {
        return '0px 0px'
      } else if (value == '21') {
        return '-400px 0px'
      } else if (value == '22') {
        return '-800px 0px'
      }
    },
    // 格式化背景图路径
    getbgimg(value) {
      let imgObj = JSON.parse(value)
      if (imgObj == null) {
        return false
      } else {
        return imgObj.visit + imgObj.filepath
      }
    },
  },
}
</script>

<style scoped lang="less">
.courseList {
  .courseDataList {
    width: 300px;
    margin-bottom: 20px;
    border: 1px solid #ccc;
    background: #fff;
    // 文字禁止复制 / 选中 start
    -moz-user-select: none; /*火狐*/
    -webkit-user-select: none; /*webkit浏览器*/
    -ms-user-select: none; /*IE10*/
    -khtml-user-select: none; /*早期浏览器*/
    user-select: none; /*open浏览器*/
    // 文字禁止复制 / 选中 end
    &:hover {
      box-shadow: 0 2px 4px rgba(0, 0, 0, 0.12), 0 0 6px rgba(0, 0, 0, 0.04);
    }
    .dataHeader,
    .head {
      position: relative;
      width: 100%;
      height: 200px;
      padding: 20px;
      border-bottom: 1px solid #ccc;
      // background: url('../../../../assets/bg.png');
      background-repeat: no-repeat;
      background-size: cover;
      display: flex;
      flex-wrap: wrap;
      align-items: flex-end;
      color: #fff;
      /deep/ .courseName {
        width: 220px;
        text-align: center;
        overflow: hidden;
        text-overflow: ellipsis;
        white-space: nowrap;
        font-size: 18px;
        font-weight: 600;
        color: #fff;
        cursor: pointer;
      }
      /deep/ .describe {
        // 文字多行隐藏无效
        // 文字3行显示 start
        overflow: hidden;
        text-overflow: ellipsis;
        display: -webkit-box;
        /* autoprefixer: off */
        -webkit-box-orient: vertical;
        /* autoprefixer: on */
        -webkit-line-clamp: 3;
        // 文字3行显示 end
        color: #fff;
      }
      /deep/ .isCompleteCourse {
        position: absolute;
        top: 0;
        right: 0;
        width: 0;
        height: 0;
        border-top: 80px solid #1890ff;
        border-left: 80px solid transparent;
        .completeCourse {
          position: absolute;
          top: -52px;
          right: -20px;
          width: 80px;
          font-size: 14px;
          color: #fff;
          display: inline-block;
          // 旋转
          transform: rotate(45deg);
          -ms-transform: rotate(45deg); /* IE 9 */
          -moz-transform: rotate(45deg); /* Firefox */
          -webkit-transform: rotate(45deg); /* Safari 和 Chrome */
          -o-transform: rotate(45deg);
        }
      }
    }
    .head {
      background-image: url('../../../../assets/bg.png') !important;
    }
    .courseInformation {
      padding: 16px 10px;
      .courseCatalogue,
      .courseContent,
      .actionArea {
        display: flex;
        align-items: center;
        margin-bottom: 16px;
        /deep/ .label {
          margin-right: 10px;
        }
        /deep/ .content {
          flex: 1;
          display: flex;
          justify-content: space-between;
          .unit {
            margin-right: 10px;
          }
          .node {
            margin: 0 auto;
          }
        }
      }
      .isreleaseBox{

      }
      .divider {
        margin: 16px 0;
        margin-bottom: 10px;
      }
      .actionArea {
        justify-content: space-between;
        margin-bottom: 0px;
        .source {
          display: flex;
        }
      }
    }
  }
  .empty {
    display: flex;
    align-items: center;
    justify-content: center;
  }
}
</style>
```

#### 父组件调用

> 子组件的方法可直接写在父组件中

```html
<template>
    <div class="dataList">
        <CourseDataList ref="CourseDataList" :dataList="dataSource" @changeDataSource="loadData">
          <!-- 课程名称 -->
          <template v-slot:courseName="data">
            <div class="courseName" @click="courseName(data.data, data.index)">
              {{ data.data.courseName }}
            </div>
          </template>
          <!-- 课程介绍 -->
          <template v-slot:describe="data">
            <div class="describe">课程介绍：{{ data.data.courseDesc }}</div>
          </template>
          <!-- 是否完整课程 -->
          <template v-slot:isCompleteCourse="data">
            <div class="isCompleteCourse" v-if="data.data.type == 1">
              <span class="completeCourse">完整课程</span>
            </div>
          </template>
          <!-- 课程信息 -->
          <template v-slot:courseContent="data">
            <div class="label">课程目录:</div>
            <div class="content">共 {{ data.data.unitNum || 0 }} 章</div>
          </template>
          <template v-slot:courseCatalogue="data">
            <div class="label">课程内容:</div>
            <div class="content">
              <span class="unit">共 {{ data.data.contentNum || 0 }} 个</span>
              <span v-if="data.data.isSyncKnowledge == 1" style="color: #1896FF;">已发布</span>
              <span v-else style="color: #ff4d4f;">未发布</span>
            </div>
          </template>
          <!-- 课程是否发布 -->
          <template v-slot:source="data">
            <div class="label">来源:</div>
            <div class="schoolName" v-if="data.data.field3">{{ data.data.field3 }}</div>
            <div class="schoolName" v-else>暂无</div>
          </template>
          <!-- 操作栏 -->
          <template v-slot:actions="data">
            <a-dropdown :trigger="['click']" placement="topLeft">
              <a style="color: #555555" @click="(e) => e.preventDefault()"> 更多 <a-icon type="dash" /> </a>
              <a-menu slot="overlay">
                <a-menu-item v-if="data.data.isSyncKnowledge == 1">
                  <a href="javascript:;" @click="cancelRelease(data.data)">取消发布</a>
                </a-menu-item>
                <a-menu-item v-else>
                  <a href="javascript:;" @click="release(data.data)">发布</a>
                </a-menu-item>
                <a-menu-item>
                  <a href="javascript:;" @click="clickEdit(data.data)">编辑</a>
                </a-menu-item>
                <a-menu-item>
                  <a href="javascript:;">复制</a>
                </a-menu-item>
                <a-menu-item>
                  <a href="javascript:;" @click="clickRemove(data.data, data.index)">删除</a>
                </a-menu-item>
                <a-menu-item>
                  <a href="javascript:;">下载</a>
                </a-menu-item>
              </a-menu>
            </a-dropdown>
          </template>
        </CourseDataList>
    </div>
</template>

<script>
import CourseDataList from '@/views/review/modules/knowledgeBase/courseDataList'
export default {
  components: {
    CourseDataList,
  },
  data() {
      return {
          ...
      }
  },
  methods: {
      ...
  }
}
</script>
```