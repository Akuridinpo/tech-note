```node
const express = require('express');
//引入工具包express
const app = express();
//定义app实例，赋予其使用express工具的许可
app.use(express.json());
//app使用express中的方法，使其能接受json格式的请求
let tasks = [{id:1, title:'一段简单的node.js代码'}];
//定义一个数组，简单存放数据
app.get('/',(req,res)=>{
	res.send('欢迎使用任务管理系统！访问/api/tasks 查看任务')
});
//app使用get方法获取请求，当请求位置处于'/'时，使用箭头函数发送一段字符串
app.get('/api/tasks', (req, res) => { res.json(tasks);
});
//app使用get方法获取请求，将tasks数组以json格式返回

app.post('/api/tasks', (req, res) => {
	const newTask = {id: tasks.length + 1, title: req.body.title};
	tasks.push(newTask);
	res.status(201).json(newTask);
});
//app使用post方法新增资源，将用户请求体的title新增到临时数据数组tasks中，使用push方法将数据置于数组的最后，并返回状态码201表示返回成功，同时将newTask的内容以json格式返回，让用户确认。

app.listen(3000, () => { console.log('一段简单的node代码') });
//app使用listen方法启用服务器并监听端口，返回一段字符串表示启用成功。
```
