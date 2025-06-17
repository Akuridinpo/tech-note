# Buffer 创建
```node.js
let buf = new Buffer.alloc(10);//二进制数据缓冲区，归零

let buf_2 = new Buffer.allocUnsafe(10000);//二进制数据缓冲区，不归零,比alloc更快

let buf_3 = new Buffer.from(`hello`);//将数据转换为unicode编码的二进制数据缓冲区

let buf_4 = new Buffer.from([10,16]);//数组也可以转换为二进制数据缓冲区
```

# Buffer 转 String
```js
let buf_4 = new Buffer.from([105,108]);//数组也可以转换为二进制数据缓冲区

console.log(buf_4.toString());//将二进制数据缓冲区通过unicode编码转换为字符串
```

# Buffer 取用
```js
let buf_5 = new Buffer.from(`hello`);

console.log(buf_5[0].toString(2));//可以将buffer类型当做数组，取第一个byte输出，此时toString(2)指转为二进制

buf_5[0] = 85;//高于八位（255）部分会舍弃 
```