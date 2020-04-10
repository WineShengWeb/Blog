<!--
 * @Author: guoxinggang<guoxinggang@gsaxns.com>
 * @Version: 1.0
 * @Date: 2019-09-11 14:49:18
 * @LastEditTime: 2020-03-07 18:32:42
 * @Description: 
 -->
# Echarts入门教程

#### 一、引导语

echarts.js是百度团队推出的一款用于图表可视化的插件，用于以图表的形式展现数据，功能强大，上手简单。

#### 二、下载

1. 从[Echarts官方网站](https://www.echartsjs.com/zh/index.html)中下载所需的echarts.js文件，该文件因功能广泛，包体较大，可自行决定按需打包下载。开发环境建议下载源代码版本，包含了常见的错误提示和警告。

在 ECharts 的 GitHub 上下载最新的 release 版本，解压出来的文件夹里的 dist 目录里可以找到最新版本的 echarts 库。

npm install echarts --save

2. 在前端页面中引入echarts.js，后即可使用，如：

原生引入
```
<script src="js/echarts.min.js"></script>
```

通过 npm 上安装的 ECharts 和 zrender 会放在node_modules目录下。可以直接在项目代码中 require('echarts') 得到 ECharts。
```
var echarts = require('echarts');

// 基于准备好的dom，初始化echarts实例
var myChart = echarts.init(document.getElementById('main'));
// 绘制图表
myChart.setOption({
    title: {
        text: 'ECharts 入门示例'
    },
    tooltip: {},
    xAxis: {
        data: ['衬衫', '羊毛衫', '雪纺衫', '裤子', '高跟鞋', '袜子']
    },
    yAxis: {},
    series: [{
        name: '销量',
        type: 'bar',
        data: [5, 20, 36, 10, 10, 20]
    }]
});

// 按需引入

// 引入 ECharts 主模块
var echarts = require('echarts/lib/echarts');

// 引入柱状图
require('echarts/lib/chart/bar');

// 引入提示框和标题组件
require('echarts/lib/component/tooltip');
require('echarts/lib/component/title');
```

3. demo

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>echarts入门</title>
    </head>
    
    <script src="js/jquery-2.2.4.js"></script>
    <script src="js/echarts.min.js"></script>
    <style>
        
        .box{
            width:900px;
            height: 900px;
            border:4px double seagreen;
            margin: auto;
            float: left;
        }
        
        
    </style>
    
    
    <body>
            
                <div class="box"></div>
                <div class="box"></div>
                <div class="box"></div>
                <div class="box"></div>
                <div class="box"></div>
                <div class="box"></div>
                <div class="box"></div>
                <div class="box"></div>
        
    </body>
    
    <script>
        
        var myChart1 = echarts.init(document.getElementsByClassName('box')[0]);
        
        var myChart2 = echarts.init(document.getElementsByClassName('box')[1]);
        
        var myChart3 = echarts.init(document.getElementsByClassName('box')[2]);
        
        var myChart4 = echarts.init(document.getElementsByClassName('box')[3]);
        
        var myChart5 = echarts.init(document.getElementsByClassName('box')[4]);
        
        //指定图表的配置项和数据
        var option1 =  {
            title: {text:'商户营业状态'},

            tooltip : {
                trigger: 'item',
                formatter: "{a} <br/>{b} : {c} ({d}%)"
            },
            legend: {
                orient : 'vertical',
                x : 'right',
                y:'bottom',
                data:['营业中','未营业']
            },
            calculable : true,
            series : [
                {
                    name:'访问来源',
                    type:'pie',
                    radius : ['30%', '40%'],
                    itemStyle : {
                        normal : {
                            label : {
                                show : false
                            },
                            labelLine : {
                                show : false
                            }
                        },
                        emphasis : {
                            label : {
                                show : true,
                                position : 'center',
                                textStyle : {
                                    fontSize : '20',
                                    fontWeight : 'bold'
                                }
                            }
                        }
                    },
                    data:[
                        {value:635, name:'营业中'},
                        {value:310, name:'未营业'},
                    ]
                }
            ]
        };
                            
        
        var option2 =  {
            title:{
                text:'服装店销售统计'
            },
            //提示框组件
            tooltip:{
                //坐标轴触发，主要用于柱状图，折线图等
                trigger:'axis'
            },
            //图例
            legend:{
                data:['销量'],
                x:'right'
            },
            //横轴
            yAxis:{
                data:["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
            },
            //纵轴
            xAxis:{},
            //系列列表。每个系列通过type决定自己的图表类型
            series:[{
                name:'销量',
                //折线图
                type:'bar',
                data:[5, 20, 36, 10, 10, 20]
            }]
        };
        
        
        myChart1.setOption(option1);
        
        myChart2.setOption(option2);
        
    </script>
</html>
```

4. 效果图

![demo效果图](https://img2018.cnblogs.com/blog/1157406/201906/1157406-20190611101415483-966217337.png)

#### 三、API及配置项

[Echarts配置项](https://www.echartsjs.com/zh/option.html#title)

[EchartsAPI](https://echarts.apache.org/zh/api.html#echarts)

[Echarts案例参考](https://www.echartsjs.com/examples/zh/index.html)


