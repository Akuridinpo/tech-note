# 写入  
## 异步工作模式 `fs.writeFile()`
```js
const vs = require('fs');//导入fs模块
fs.writeFile('./something.txt', 'some data', err => {

  if (err) throw err;

  console.log('It\'s saved!');

})//后输出
console.log('end');//先输出
```

## 同步工作模式 `fs.writeFileSync()`
```js
const fs = require('fs');

fs.writeFileSync('./something.txt', 'some data', err => {

  if (err) throw err;

  console.log('It\'s saved!');

});//写入文件但不答应

console.log('end');//打印
```
+ 不打印的原因是 `writeFileSync () ` 不接受回调函数