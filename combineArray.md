<!--
 * @Author: gxg<18215084858@163.com>
 * @Date: 2021-11-06 12:37:54
 * @LastEditors: gxg<18215084858@163.com>
 * @LastEditTime: 2022-06-27 17:31:39
 * @Description:
-->

# JavaScript 多个数组组合

```js
// JavaScript 多个数组组合且不重复
var arr = [
  ["张三", "李四"],
  ["男", "女"],
  ["北京大学", "清华大学", "人民大学"],
  ["A", "B", "C", "D"],
];

function combine_arr(arr, split_str) {
  // split_str 为分隔符
  var sarr = [[]];
  for (var i = 0; i < arr.length; i++) {
    var tarr = [];
    for (var j = 0; j < sarr.length; j++) {
      for (var k = 0; k < arr[i].length; k++) {
        // tarr.push(sarr[j].concat(split_str + arr[i][k]).toString());
        tarr.push(sarr[j].concat(arr[i][k]));
      }
    }
    sarr = tarr;
  }
  return sarr;
}

console.log(combine_arr(arr));
// 0: (4) ['张三', '男', '北京大学', 'A']
// 1: (4) ['张三', '男', '北京大学', 'B']
// 2: (4) ['张三', '男', '北京大学', 'C']
// 3: (4) ['张三', '男', '北京大学', 'D']
// 4: (4) ['张三', '男', '清华大学', 'A']
// 5: (4) ['张三', '男', '清华大学', 'B']
// 6: (4) ['张三', '男', '清华大学', 'C']
// 7: (4) ['张三', '男', '清华大学', 'D']
// 8: (4) ['张三', '男', '人民大学', 'A']
// 9: (4) ['张三', '男', '人民大学', 'B']
// 10: (4) ['张三', '男', '人民大学', 'C']
// 11: (4) ['张三', '男', '人民大学', 'D']
// 12: (4) ['张三', '女', '北京大学', 'A']
// 13: (4) ['张三', '女', '北京大学', 'B']
// 14: (4) ['张三', '女', '北京大学', 'C']
// 15: (4) ['张三', '女', '北京大学', 'D']
// 16: (4) ['张三', '女', '清华大学', 'A']
// 17: (4) ['张三', '女', '清华大学', 'B']
// 18: (4) ['张三', '女', '清华大学', 'C']
// 19: (4) ['张三', '女', '清华大学', 'D']
// 20: (4) ['张三', '女', '人民大学', 'A']
// 21: (4) ['张三', '女', '人民大学', 'B']
// 22: (4) ['张三', '女', '人民大学', 'C']
// 23: (4) ['张三', '女', '人民大学', 'D']
// 24: (4) ['李四', '男', '北京大学', 'A']
// 25: (4) ['李四', '男', '北京大学', 'B']
// 26: (4) ['李四', '男', '北京大学', 'C']
// 27: (4) ['李四', '男', '北京大学', 'D']
// 28: (4) ['李四', '男', '清华大学', 'A']
// 29: (4) ['李四', '男', '清华大学', 'B']
// 30: (4) ['李四', '男', '清华大学', 'C']
// 31: (4) ['李四', '男', '清华大学', 'D']
// 32: (4) ['李四', '男', '人民大学', 'A']
// 33: (4) ['李四', '男', '人民大学', 'B']
// 34: (4) ['李四', '男', '人民大学', 'C']
// 35: (4) ['李四', '男', '人民大学', 'D']
// 36: (4) ['李四', '女', '北京大学', 'A']
// 37: (4) ['李四', '女', '北京大学', 'B']
// 38: (4) ['李四', '女', '北京大学', 'C']
// 39: (4) ['李四', '女', '北京大学', 'D']
// 40: (4) ['李四', '女', '清华大学', 'A']
// 41: (4) ['李四', '女', '清华大学', 'B']
// 42: (4) ['李四', '女', '清华大学', 'C']
// 43: (4) ['李四', '女', '清华大学', 'D']
// 44: (4) ['李四', '女', '人民大学', 'A']
// 45: (4) ['李四', '女', '人民大学', 'B']
// 46: (4) ['李四', '女', '人民大学', 'C']
// 47: (4) ['李四', '女', '人民大学', 'D']
```
