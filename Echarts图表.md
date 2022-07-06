# Echarts 图表

### 安装 Echarts

> 在项目中安装 Echarts

```node
// 以下内容按需安装即可
npm install echarts // Echarts 图表库
npm install echarts-gl // Echarts 3D图表库
npm install echarts-liquidfill // Echarts 水球图
```

### 引入 Echarts

> 在 main.js 文件中写入以下代码

```javascript
// 引入echarts
import * as echarts from "echarts";
import "echarts-gl"; // 3d图表库
import "echarts-liquidfill";

Vue.prototype.$echarts = echarts;
```

### 使用 Echarts 绘制图表

> 创建图表页面组件，在指定位置直接引入改图表组件;

```vue
<template>
  <div ref="myChart" :style="{ width: 100%, height: 100%,  }"></div>
</template>

<script>
export default {
  data() {
    return {
      myChart: null,
      dataSource: [],
    };
  },

  mounted() {
    this.reloadChart();
    // 监听重载图表
    window.addEventListener("resize", () => {
      this.reloadChart();
    });
  },

  beforeDestroy() {
　　// 销毁图表
　　this.disposeChart()
　}

  methods: {
    // 重载图表
    reloadChart() {
      this.disposeChart();
      this.initChart(this.dataSource);
    },
    // 销毁图表
    disposeChart() {
      if (this.myChart) {
        this.myChart.dispose();
      }
    },
    // 初始化图表
    initChart(data) {
      // 初始化 echart
      this.myChart = this.$echarts.init(this.$refs.myChart, "tdTheme");

      // 图表的配置项
      let options = {
        // 添加配置项
      };

      // 设置图表 option
      this.myChart.setOption(options, true);
    },
  },
};
</script>

<style scoped lang="scss"></style>
```

> 或者对图表页面组件进行封装，直接传值进行图表显示。

- 封装 Echarts 图表组件

```vue
<template>
  <div
    :id="id"
    :class="className"
    :style="{ height: height, width: width }"
  ></div>
</template>

<script>
import tdTheme from "./theme.json"; // 引入默认主题
import "../map/china.js";
export default {
  name: "echart",
  props: {
    className: {
      type: String,
      default: "chart",
    },
    id: {
      type: String,
      default: "chart",
    },
    width: {
      type: String,
      default: "100%",
    },
    height: {
      type: String,
      default: "100%",
    },
    options: {
      type: Object,
      default: () => ({}),
    },
  },
  data() {
    return {
      chart: null,
    };
  },
  watch: {
    options: {
      handler(options) {
        // 设置true清空echart缓存
        this.chart.setOption(options, true);
      },
      deep: true,
    },
  },
  mounted() {
    this.$echarts.registerTheme("tdTheme", tdTheme); // 覆盖默认主题
    // this.initChart();
    this.reloadChart();
    // 监听重载图表
    window.addEventListener("resize", () => {
      this.reloadChart();
    });
  },
  methods: {
    // 字体大小
    WidthAdaptive(res) {
      var windth = window.innerWidth;
      let fontSize = windth / 1920;
      return fontSize * res;
    },
    // 重载图表
    reloadChart() {
      this.disposeChart();
      this.initChart();
    },
    // 销毁图表
    disposeChart() {
      if (this.myChart) {
        this.myChart.dispose();
      }
    },
    initChart() {
      // 初始化echart
      this.chart = this.$echarts.init(this.$el, "tdTheme");
      this.chart.setOption(this.options, true);
    },
  },
};
</script>

<style scoped lang="scss"></style>
```

- theme.json

```json
{
  "color": ["#2d8cf0", "#19be6b", "#ff9900", "#E46CBB", "#9A66E4", "#ed3f14"],
  "backgroundColor": "rgba(0,0,0,0)",
  "textStyle": {},
  "title": {
    "textStyle": {
      "color": "#516b91"
    },
    "subtextStyle": {
      "color": "#93b7e3"
    }
  },
  "line": {
    "itemStyle": {
      "normal": {
        "borderWidth": "2"
      }
    },
    "lineStyle": {
      "normal": {
        "width": "2"
      }
    },
    "symbolSize": "6",
    "symbol": "emptyCircle",
    "smooth": true
  },
  "radar": {
    "itemStyle": {
      "normal": {
        "borderWidth": "2"
      }
    },
    "lineStyle": {
      "normal": {
        "width": "2"
      }
    },
    "symbolSize": "6",
    "symbol": "emptyCircle",
    "smooth": true
  },
  "bar": {
    "itemStyle": {
      "normal": {
        "barBorderWidth": 0,
        "barBorderColor": "#ccc"
      },
      "emphasis": {
        "barBorderWidth": 0,
        "barBorderColor": "#ccc"
      }
    }
  },
  "pie": {
    "itemStyle": {
      "normal": {
        "borderWidth": 0,
        "borderColor": "#ccc"
      },
      "emphasis": {
        "borderWidth": 0,
        "borderColor": "#ccc"
      }
    }
  },
  "scatter": {
    "itemStyle": {
      "normal": {
        "borderWidth": 0,
        "borderColor": "#ccc"
      },
      "emphasis": {
        "borderWidth": 0,
        "borderColor": "#ccc"
      }
    }
  },
  "boxplot": {
    "itemStyle": {
      "normal": {
        "borderWidth": 0,
        "borderColor": "#ccc"
      },
      "emphasis": {
        "borderWidth": 0,
        "borderColor": "#ccc"
      }
    }
  },
  "parallel": {
    "itemStyle": {
      "normal": {
        "borderWidth": 0,
        "borderColor": "#ccc"
      },
      "emphasis": {
        "borderWidth": 0,
        "borderColor": "#ccc"
      }
    }
  },
  "sankey": {
    "itemStyle": {
      "normal": {
        "borderWidth": 0,
        "borderColor": "#ccc"
      },
      "emphasis": {
        "borderWidth": 0,
        "borderColor": "#ccc"
      }
    }
  },
  "funnel": {
    "itemStyle": {
      "normal": {
        "borderWidth": 0,
        "borderColor": "#ccc"
      },
      "emphasis": {
        "borderWidth": 0,
        "borderColor": "#ccc"
      }
    }
  },
  "gauge": {
    "itemStyle": {
      "normal": {
        "borderWidth": 0,
        "borderColor": "#ccc"
      },
      "emphasis": {
        "borderWidth": 0,
        "borderColor": "#ccc"
      }
    }
  },
  "candlestick": {
    "itemStyle": {
      "normal": {
        "color": "#edafda",
        "color0": "transparent",
        "borderColor": "#d680bc",
        "borderColor0": "#8fd3e8",
        "borderWidth": "2"
      }
    }
  },
  "graph": {
    "itemStyle": {
      "normal": {
        "borderWidth": 0,
        "borderColor": "#ccc"
      }
    },
    "lineStyle": {
      "normal": {
        "width": 1,
        "color": "#aaa"
      }
    },
    "symbolSize": "6",
    "symbol": "emptyCircle",
    "smooth": true,
    "color": ["#2d8cf0", "#19be6b", "#f5ae4a", "#9189d5", "#56cae2", "#cbb0e3"],
    "label": {
      "normal": {
        "textStyle": {
          "color": "#eee"
        }
      }
    }
  },
  "map": {
    "itemStyle": {
      "normal": {
        "areaColor": "#f3f3f3",
        "borderColor": "#516b91",
        "borderWidth": 0.5
      },
      "emphasis": {
        "areaColor": "rgba(165,231,240,1)",
        "borderColor": "#516b91",
        "borderWidth": 1
      }
    },
    "label": {
      "normal": {
        "textStyle": {
          "color": "#000"
        }
      },
      "emphasis": {
        "textStyle": {
          "color": "rgb(81,107,145)"
        }
      }
    }
  },
  "geo": {
    "itemStyle": {
      "normal": {
        "areaColor": "#f3f3f3",
        "borderColor": "#516b91",
        "borderWidth": 0.5
      },
      "emphasis": {
        "areaColor": "rgba(165,231,240,1)",
        "borderColor": "#516b91",
        "borderWidth": 1
      }
    },
    "label": {
      "normal": {
        "textStyle": {
          "color": "#000"
        }
      },
      "emphasis": {
        "textStyle": {
          "color": "rgb(81,107,145)"
        }
      }
    }
  },
  "categoryAxis": {
    "axisLine": {
      "show": true,
      "lineStyle": {
        "color": "#cccccc"
      }
    },
    "axisTick": {
      "show": false,
      "lineStyle": {
        "color": "#333"
      }
    },
    "axisLabel": {
      "show": true,
      "textStyle": {
        "color": "#fff"
      }
    },
    "splitLine": {
      "show": false,
      "lineStyle": {
        "color": ["#eeeeee"]
      }
    },
    "splitArea": {
      "show": false,
      "areaStyle": {
        "color": ["rgba(250,250,250,0.05)", "rgba(200,200,200,0.02)"]
      }
    }
  },
  "valueAxis": {
    "axisLine": {
      "show": true,
      "lineStyle": {
        "color": "#cccccc"
      }
    },
    "axisTick": {
      "show": false,
      "lineStyle": {
        "color": "#333"
      }
    },
    "axisLabel": {
      "show": true,
      "textStyle": {
        "color": "#fff"
      }
    },
    "splitLine": {
      "show": false,
      "lineStyle": {
        "color": ["#eeeeee"]
      }
    },
    "splitArea": {
      "show": false,
      "areaStyle": {
        "color": ["rgba(250,250,250,0.05)", "rgba(200,200,200,0.02)"]
      }
    }
  },
  "logAxis": {
    "axisLine": {
      "show": true,
      "lineStyle": {
        "color": "#cccccc"
      }
    },
    "axisTick": {
      "show": false,
      "lineStyle": {
        "color": "#333"
      }
    },
    "axisLabel": {
      "show": true,
      "textStyle": {
        "color": "#999999"
      }
    },
    "splitLine": {
      "show": true,
      "lineStyle": {
        "color": ["#eeeeee"]
      }
    },
    "splitArea": {
      "show": false,
      "areaStyle": {
        "color": ["rgba(250,250,250,0.05)", "rgba(200,200,200,0.02)"]
      }
    }
  },
  "timeAxis": {
    "axisLine": {
      "show": true,
      "lineStyle": {
        "color": "#cccccc"
      }
    },
    "axisTick": {
      "show": false,
      "lineStyle": {
        "color": "#333"
      }
    },
    "axisLabel": {
      "show": true,
      "textStyle": {
        "color": "#999999"
      }
    },
    "splitLine": {
      "show": true,
      "lineStyle": {
        "color": ["#eeeeee"]
      }
    },
    "splitArea": {
      "show": false,
      "areaStyle": {
        "color": ["rgba(250,250,250,0.05)", "rgba(200,200,200,0.02)"]
      }
    }
  },
  "toolbox": {
    "iconStyle": {
      "normal": {
        "borderColor": "#999"
      },
      "emphasis": {
        "borderColor": "#666"
      }
    }
  },
  "legend": {
    "textStyle": {
      "color": "#fff"
    }
  },
  "tooltip": {
    "axisPointer": {
      "lineStyle": {
        "color": "#ccc",
        "width": 1
      },
      "crossStyle": {
        "color": "#ccc",
        "width": 1
      }
    }
  },
  "timeline": {
    "lineStyle": {
      "color": "#8fd3e8",
      "width": 1
    },
    "itemStyle": {
      "normal": {
        "color": "#8fd3e8",
        "borderWidth": 1
      },
      "emphasis": {
        "color": "#8fd3e8"
      }
    },
    "controlStyle": {
      "normal": {
        "color": "#8fd3e8",
        "borderColor": "#8fd3e8",
        "borderWidth": 0.5
      },
      "emphasis": {
        "color": "#8fd3e8",
        "borderColor": "#8fd3e8",
        "borderWidth": 0.5
      }
    },
    "checkpointStyle": {
      "color": "#8fd3e8",
      "borderColor": "rgba(138,124,168,0.37)"
    },
    "label": {
      "normal": {
        "textStyle": {
          "color": "#8fd3e8"
        }
      },
      "emphasis": {
        "textStyle": {
          "color": "#8fd3e8"
        }
      }
    }
  },
  "visualMap": {
    "color": ["#516b91", "#59c4e6", "#a5e7f0"]
  },
  "dataZoom": {
    "backgroundColor": "rgba(0,0,0,0)",
    "dataBackgroundColor": "rgba(255,255,255,0.3)",
    "fillerColor": "rgba(167,183,204,0.4)",
    "handleColor": "#a7b7cc",
    "handleSize": "100%",
    "textStyle": {
      "color": "#333"
    }
  },
  "markPoint": {
    "label": {
      "normal": {
        "textStyle": {
          "color": "#eee"
        }
      },
      "emphasis": {
        "textStyle": {
          "color": "#eee"
        }
      }
    }
  }
}
```

- 父页面进行组件引入

```vue
<template>
  <div class="chartBox">
    <Echart :id="'myChart'" :options="option" />
  </div>
</template>

<script>
import Echart from "@/components/echart";
export default {
  components: {
    Echart,
  },
  data() {
    return {
      option: {},
    };
  },
  mounted() {
    let dataSource = ["138", "1190", "1425"];
    this.setEchartOption(dataSource);
  },
  methods: {
    /**
     * data 为传入的数据
     */
    setEchartOption(data) {
      this.option = {
        // 添加配置项
      };
    },
  },
};
</script>

<style scoped lang="scss">
.chartBox {
  width: 100%;
  height: 300px;
}
</style>
```
