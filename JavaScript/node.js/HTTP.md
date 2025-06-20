# 创建 HTTP 服务
+ `res. end() ` 括号内可以读取 buffer
```JS
const http = require('http');

  

const server = http.createServer((request, response) => {//request是请求报文的封装对象，response响应报文的封装

 response.setHeader('content-type', 'text/html;charset=utf-8');//响应头添加一个tontent-type键，告诉浏览器返回的为UTF-8字符集的HTML文件

  response.end('响应体');//设置响应体并结束响应

 

});//当服务接受到http请求时启用

  

server.listen(9000, ()=> {

  console.log
  
```
# 获得 HTTP 请求报文
+ 请求方法：`request.method`
+ HTTP 协议版本号：`request.httpVersion`
+ 请求头：`request.headers //返回一个对象`
+ 请求体：
```js
let body = '';

  request.on('data', chunk => {

    body += chunk.toString();//流式获取请求体中的数据，将缓冲块转为字符串存在body中

  })

  request.on('end', () => {

    console.log(body);

  })
```
+ 请求 url：`request.url //只包含路径与查询字符串`
+ 请求 url 的路径和查询字符串：

	方法一：
```js
const url = require('url');
//....
console.log(url.parse(request.url).pathname);
//parse是url的解析方法，返回一个对象，包括url的各种属性，pathname
console.log(url.parse(request.url,true).query.keyword);//查询字符串keyword键的值
//parse方法如果传入true参数，则会返回对象，对象中query的keyword的键和值分开储存，如果不加true则会直接返回`keyword=123`
```

	方法二（新方法，首选）：
```js
//不需要引入url接口

//...

  

  let parsedurl = new URL(request.url, "http://127.0.0.1");

  console.log(parsedurl.pathname);
  
  console.log(parsedurl.searchParams.get('keyword'));
  //实例化的URL对象中，有一个searchParams参数，他的值是包括keyword的键和值，我们用get方法就可以直接获得keyword的值
```
# 编写响应行/头/体
+ 响应头 `res.setHeader('键','值')`
+ 响应体 `res.write()`
# 常见问题
## 浏览器页面显示乱码？
```js
response.setHeader('content-type', 'text/html;charset=utf-8');//响应头添加一个tontent-type键，告诉浏览器返回的为UTF-8字符集的HTML文件
```
## `ERROR:address already in use 端口已被占用`
+ 除了改端口外，可以通过资源监视器-网络-侦听端口来找到端口被哪个应用程序占用

## 外部引入的 css，js 文件无法正常加载？
+ 如果用使用 `fs.readFile()` 将 HTML 文件写入响应体内，HTML 内部申请的外部 css 样式和 js 脚本都会被 node. Js 的回调函数响应，必须用请求路径返回相应结果才能正确调用外部文件。
```js
const http = require("http");
const fs = require("fs");
const path = require("path");
const mime = require("mime");

const server = http.createServer((req, res) => {
  let { pathname } = new URL(req.url, "http://127.0.0.1");
  let filepath = path.join(__dirname, "静态资源包", pathname);//请求路径名和文件名相同，所以将静态资源全部放在一个文件夹内，用path.join组成新的绝对路径即可

  

  let contType = mime.getType(pathname) + ";charset=utf-8"//用mime接口提供的getType方法获取请求资源所对应的mime类型,并限制字符集
  res.setHeader("content-type", contType);//添加进响应头
  
    fs.readFile(filepath, (err, data) => {
      if (err) {
        res.statusCode = 500;
        res.end("读取失败");
        throw err;
      }

      res.end(data);
    });
});
  

server.listen("9000", () => {
  console.log("start");
})
```