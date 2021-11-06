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

console.log(combine_arr(arr))
```