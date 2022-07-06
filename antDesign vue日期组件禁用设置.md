# antDesign vue 日期组件禁用设置

### vue 部分

```vue
<a-date-picker
  :key="key"
  v-model="dateValue"
  :value="moment(dateValue, attrBute.format)"
  @change="onChange"
  @openChange="openChange"
  :format="attrBute.format"
  :disabled="newdisabled == '' ? attrBute.disabled : newdisabled"
  :allowClear="attrBute.allowClear"
  :size="attrBute.size"
  :showTime="attrBute.showTime"
  :placeholder="getPlaceHolder()"
  :disabledDate="getDisabledDate"
  :getCalendarContainer="getContainer"
  :locale="history"
/>
```

### JavaScript 部分

需要引入 `moment` 库

```JavaScript
getDisabledDate(val) {
    if (this.disabledInfo && this.disabledInfo.type == 1) {
    // 当前时间之前不可选
    let startTime = this.moment(this.disabledInfo.time, this.attrBute.format);
    return val.valueOf() < startTime.valueOf();
    } else if (this.disabledInfo && this.disabledInfo.type == 2) {
    // 当前时间之后不可选
    let startTime = this.moment(this.disabledInfo.time, this.attrBute.format);
    return val.valueOf() > startTime.valueOf();
    } else if (this.disabledInfo && this.disabledInfo.type == 3) {
    // 当前区间内不可选
    let startTime = this.moment(this.disabledInfo.start, this.attrBute.format);
    let endTime = this.moment(this.disabledInfo.end, this.attrBute.format);
    return val.valueOf() > startTime.valueOf() && endTime.valueOf() > val.valueOf();
    } else if (this.disabledInfo && this.disabledInfo.type == 4) {
    // 当前区间外不可选
    let startTime = this.moment(this.disabledInfo.start, this.attrBute.format);
    let endTime = this.moment(this.disabledInfo.end, this.attrBute.format);
    return val.valueOf() < startTime.valueOf() || endTime.valueOf() <= val.valueOf();
    } else if (this.disabledInfo && this.disabledInfo.type == 5) {
    // 固定日期禁止
    let oldStr = new Date(val).Format("yyyy-MM-dd");
    let formatL = this.attrBute.format.length;
    let newStr = oldStr.substr(0, formatL);
    if (this.disabledInfo.times.indexOf(newStr) > -1) {
        return true;
    } else {
        return false;
    }
    } else if (this.disabledInfo && this.disabledInfo.type == 6) {
    // 只有周末可以选
    let oldStr = new Date(val);
    let sd = oldStr.getDay() == 0 ? 7 : oldStr.getDay();
    if (sd == 6 || sd == 7) return false;
    else return true;
    } else {
    return false;
    }
}
```

### 配置信息

```js
data() {
    return {
        attrBute: {
            format: 'YYYY-MM-DD'
        },
        disabledInfo: [
            {
                type: 1, // 当前时间之前不可选
                time: "2020-04-10"
            },
            {
                type: 2, // 当前时间之后不可选
                time: "2020-04-10"
            },
            {
                type: 3, // start 和 end 区间内不可选
                start: "2020-04-10",
                end: "2020-04-15"
            },
            {
                type: 4, // start 和 end 区间外不可选
                start: "2020-04-10",
                end: "2020-04-15"
            },
            {
                type: 5, // 固定日期不可选
                times: ["2020-04-15", "2020-04-10"]
            },
            {
                type: 6 // 只有周末可以选
            }
        ]
    }
}
```
