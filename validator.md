# 正则验证

#### 手机号码

```js
// 验证手机号
function validatorPhone(value) {
  if (/^1[3456789]\d{9}$/.test(value)) {
    console.log("手机号验证通过!");
    return true;
  } else {
    console.log("手机号格式不正确!");
    return false;
  }
}
```

#### 验证邮箱

```js
// 验证邮箱
function validatorEmail(value) {
  if (/^[a-zA-Z0-9_-]+@[a-zA-Z0-9_-]+(\.[a-zA-Z0-9_-]+)+$/.test(value)) {
    console.log("邮箱格式不正确!");
    return true;
  } else {
    console.log("邮箱格式不正确!");
    return false;
  }
}
```

#### 身份证号

```js
// 验证身份证号
function validatorIDNumber(value) {
  // let idre = /^[1-9]\d{5}(18|19|([23]\d))\d{2}((0[1-9])|(10|11|12))(([0-2][1-9])|10|20|30|31)\d{3}[0-9Xx]$/;
  if (
    /^([1-6][1-9]|50)\d{4}(18|19|20)\d{2}((0[1-9])|10|11|12)(([0-2][1-9])|10|20|30|31)\d{3}[0-9Xx]$/.test(
      value
    )
  ) {
    console.log("身份证号验证通过");
    return true;
  } else {
    console.log("身份证号验证未通过");
    return false;
  }
}
```

#### 银行卡号

```js
// 验证银行卡号
function validatorBankNumber(value) {
  if (/^([1-9]{1})(\d{14}|\d{18})$/.test(value)) {
    console.log("银行卡号验证通过!");
    return true;
  } else {
    console.log("银行卡号格式不正确!");
    return false;
  }
}
```
