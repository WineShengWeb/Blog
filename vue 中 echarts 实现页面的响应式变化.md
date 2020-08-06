# vue 中 echarts 实现页面的响应式变化

echarts 图表本身提供了一个 resize 函数，当浏览器页面发生 resize 事件的时候，让表格触发 echats 的 resize 事件，然后重绘 canvas

页面只有一个 echarts 图表时，用 window.onresize = myChart.resize;即可完成自适应
当一个页面有多个 echarts 图表时，使用时间绑定方法 addEvebtListener 可以解决

```js
window.addEventListener("resize", () => {
    this.myChart.resize();
    this.myChart2.resize();
    this.myChart3.resize();
});
```

在 vue 中使用响应式图表，可以直接对单独的表格对象添加事件；

```js
myCharts.setOption(option);
window.addEventListener("resize", () => {
    myCharts.resize();
});

myCharts2.setOption(option);
window.addEventListener("resize", () => {
    myCharts2.resize();
});
```
