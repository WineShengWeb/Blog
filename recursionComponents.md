# 递归组件

---

#### 父组件调用子组件

```vue
<template>
  <div>
    <div class="box">
      <div class="header">
        <div class="name">学科名称</div>
        <div class="type">学术类型</div>
      </div>
      <div class="list">
        <div class="forList" v-for="(item, index) in dataList" :key="index">
          <div class="listBox">
            <div class="checkBox">
              <a-checkbox @change="onChange(item)" :default-checked="item.value"> {{ item.name }} </a-checkbox>
            </div>
            <div class="sub_type">{{ item.type }}</div>
          </div>
          <div class="childrenList">
            <Children :dataList="item.children" :key="item.id" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Children from './children'
export default {
  name: 'direction',
  components: {
    Children,
  },
  data() {
    return {
      // 数据
      dataList: [
        {
          id: 1,
          name: '张三',
          value: true,
          type: '类型一',
          children: [
              {
                id: 1,
                name: '张三',
                value: true,
                type: '类型一',
                children: [
                    {
                      id: 1,
                      name: '张三',
                      value: true,
                      type: '类型一',
                      children: []
                    }
                ]
              }
          ]
        },
        {
          id: 2,
          name: '张三',
          value: false,
          type: '类型一',
          children: [
                {
                  id: 1,
                  name: '张三',
                  value: false,
                  type: '类型一',
                  children: []
                }
          ]
        }
      ],
    }
  },
  methods: {
    // 选中
    onChange(data) {
      this.dataList.map((item) => {
        if (item.id == data.id) {
          item.value = !item.value
        }
      })
    },
  },
}
</script>
```

#### 子组件

```vue
<template>
  <div class="childrenBox">
    <div class="list" v-for="(item, index) in dataList" :key="index">
      <div class="listBox">
        <div class="checkBox">
          <a-checkbox @change="onChange(item)" :default-checked="item.value"> {{ item.name }} </a-checkbox>
        </div>
        <div class="type">{{ item.type}}</div>
      </div>
      <div class="childrenListBox" v-if="item.value">
        <Children :dataList="item.children" :key="item.id" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Children',
  props: {
    dataList: {
      require: true,
      type: Array,
    },
  },
  data() {
    return {}
  },
  methods: {
    // 选中
    onChange(data) {
      this.dataList.map((item) => {
        if (item.id == data.id) {
          item.value = !item.value
        }
      })
    },
  },
}
</script>
```