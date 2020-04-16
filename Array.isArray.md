# Array.isArray() 判断是否是数组

##### demo

```javascript
var arr = [];
var str = "string";

console.log(Array.isArray(arr)); // true
console.log(Array.isArray(str)); // false
```

##### 使用 `Array.isArray()` 多维数组降维

```JavaScript
// 多维数组
var arr = [[1, 2, 8, [6, 7]], 3, [3, 6, 9], 4]

function getNewArr(arr) {
  // 定义新数组用于存储所有元素
  var newArr = []
  // 遍历原数组中的每个元素
  for (var i = 0; i < arr.length; i++) {
    // 判断当前元素是否为数组
    if (Array.isArray(arr[i])) {
      // 若当前元素为数组时，调用函数本身继续判断，通过 concat 方法连接函数返回的数组
      newArr = newArr.concat(getNewArr(arr[i]))
    } else { // 若不是数组直接将当前元素追加到新数组的末尾
      newArr.push(arr[i])
    }
  }
  // 循环结束将新数组返回
  return newArr
}

console.log(arr) // [[1, 2, 8, [6, 7]], 3, [3, 6, 9], 4]
console.log(getNewArr(arr)) // [1, 2, 8, 6, 7, 3, 3, 6, 9, 4]
```
