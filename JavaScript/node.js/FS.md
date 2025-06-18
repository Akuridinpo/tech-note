# FS 的相对路径参照命令行所在目录
+ 可使用 `__dirname` 当做路径，此路径为代码所在目录的绝对路径 
# 写入  
## 异步写入 `fs.writeFile()`
```js
const vs = require('fs');//导入fs模块
fs.writeFile('./something.txt', 'some data', err => {

  if (err) throw err;//err为null则写入成功

  console.log('It\'s saved!');

})//后输出
console.log('end');//先输出
```

## 同步写入 `fs.writeFileSync()`
```js
const fs = require('fs');

fs.writeFileSync('./something.txt', 'some data', err => {

  if (err) throw err;

  console.log('It\'s saved!');

});//写入文件但不答应

console.log('end');//打印
```
+ 不打印的原因是 `writeFileSync () ` 不接受回调函数


## 异步追加写入 `fs.appendFile ()`
```js
const fs = require('fs');

fs.writeFile('./something just like this.txt', 'I\'ve been reading book of old', err => {

  if (err) return console.log('it\'s not saved');//写入文件失败

  console.log('It\'s saved!');

});

fs.appendFile('./something just like this.txt', ' \r\nThe legend and the myths', err => {

  if (err) return console.log('it\'s not appended');

  console.log('It\'s appended!');

});
```
## 异步追加写入 `fs.writeFile({flag:'a'})`
```js
fs.writeFile('./something just like this.txt','\nAchillis and his gold',{flag:'a'}, err => {

  if (err) return console.log('it\'s not saved');//写入文件失败

  console.log('It\'s appended!');

});
```
## 流式写入 `fs.createwritestream`
+ 流式写入比较传统的追加写入可以减少开关文件次数
```js
const ws = fs.createWriteStream('./something just like this.txt');
ws.write('I\'ve been reading book of old');
ws.write('\nHercules and his gifts');
ws.close();
```
+ 会覆盖已写文件的内容，`write` 多少覆盖多少
```js
fs.writeFile('./love and peace.txt','love and peace', err => {

  if (err) return console.log('it\'s not saved');//写入文件失败

  console.log('It\'s saved!');

});

const ws = fs.createWriteStream('./love and peace.txt');

ws.write('test');

ws.close();

console.log('end');
//文件内味test and love
```
# 读取
## 异步读取 `fs.readFile()`
+ 语法: `fs.readFile(path,[,option],callback)`
	回调函数格式：`(err, data)`
```js
const fs = require('fs');

fs.readFile('./something just like this.txt', (err, data) => {

  if (err) throw err;

  console.log(data.toString());

  });
```
## 同步读取 `fs.readFileSync()`
```js
let data = fs.readFileSync('./something just like this.txt')

  console.log(data.toString());
```
## 流式读取 `createReadStream()`
+ 读取效率高
```js
const rs = fs.createReadStream('./CCUT.jpg');

rs.on('data', chunk => {

  console.log(chunk.length);

});//每次读取65536byte
rs.on('end', () => {

  console.log('end');

});
```
# 移动与重命名 `fs.rename`
+ 语法 `fs.rename(oldpath,newpath,err)`
+ 重命名
```js
const fs = require('fs');

fs.rename('something just like this.txt', 'new something.txt', (err) => {

  if (err) throw err;

  console.log('File renamed successfully');

})
```
+ 移动
```js
const fs = require('fs');

fs.rename('./new.txt', './new_folder/new.txt', (err) => {

  if (err) throw err;

  console.log('File renamed successfully');

})
```
# 删除 
## `fs.unlink()`
```js
const fs = require('fs');

fs.unlink('../resource/del.txt', err => {

  if (err) throw err;

  console.log("it\'s deleted");

});
```
##  `fs.rm`
```js
const fs = require('fs');

fs.rm('../resource/del2.txt', err => {

  if (err) throw err;

  console.log("it\'s deleted");

});
```
# 文件夹创建
## 创建单个文件夹 `fs.mkdir()`
```js
const fs = require('fs');

fs.mkdir('./new_Folder', err => {

  if (err) throw err;

  console.log("it\'s created")

  }

)
```
## 递归创建文件夹 `fs.mkdir(,{recursive:true})`
```js
const fs = require('fs');

fs.mkdir('./new_Folder/1/2',{recursive:true}, err => {

  if (err) throw err;

  console.log("it\'s created")

  }

)
```

# 文件夹读取
## 读取文件夹下一层 `fs.readDir()`
```js
const fs = require('fs');

let data = fs.readdirSync('./new_folder');

console.log(data);
```

## 递归读取文件夹 `fs.readdirSync(,{recursive:true});`
```js
const fs = require('fs');

let data = fs.readdirSync('./new_folder',{recursive:true});

console.log(data);
```

# 文件夹删除
## 删除无内容文件夹 `fs.rmdir()`
```js
const fs = require('fs');

fs.rmdirSync('./delFolder');
```
## 递归删除文件夹 `fs.rm({recursive:true})`
```js
const fs = require('fs');

fs.rmdirSync('./new_Folder',{recursive:true});
//DeprecationWarning: In future versions of Node.js, fs.rmdir(path, { recursive: true }) will be removed. Use fs.rm(path, { recursive: true }) instead

```

# 查看文件信息
## `fe.stat()`
```js
const fs = require('fs');

fs.stat('../resource/CCUT.jpg', (err, data) => {

  if (err) throw err;

  console.log(data);

  console.log(data.isDirectory());//是否是文件夹

  console.log(data.isFile());//是否是文件
  

})
```

# 练习
## 复制 `pipe()`
+ 先同步读取再同步写入
```js
const fs = require('fs');

const data = fs.readFileSync('./something just like this.txt');

fs.writeFileSync('copy of something just like this.txt', data);
```
+ 流式读取+流式写入（占用内存空间更少）
```js
const rs = fs.createReadStream('./something just like this.txt');

const ws = fs.createWriteStream('./(2)copy of something just like this.txt');

  

rs.on('data', chunk => {

    ws.write(chunk);

})

rs.on('end', () => {

  ws.end();

})
```
+ 使用管道 `pipe`

```js
rs.pipe(ws)
```
## 批量重命名（加上序号）
```js
const fs = require('fs');

const targetDir = __dirname + '/../src';

const files = fs.readdirSync(targetDir);

let i = 0;

files.forEach(file => {

  const oldPath = targetDir + '/' + file;

  const newName = `${i}_${file}`;

  const newPath = targetDir + '/' + newName;

  i++;

  console.log(`${file} to ${newName}`);

  fs.renameSync(oldPath, newPath);

});
```
## 批量重命名（序号小于十加上前缀零）
```js
const fs = require('fs');

const targetDir = __dirname + '/../src';

const files = fs.readdirSync(targetDir);

let i = 0;

files.forEach(file => {

  let sliptFile = file.split('_');

  let [num, name] = sliptFile;

  //;

  if (Number(num) < 10) {

    let newNum = '0' + num;

    let newName = newNum + '_' + name;

    let oldPath = targetDir + '/' + file;

    let newPath = targetDir + '/' + newName;

    fs.renameSync(oldPath,newPath);

  }

});
```
## 批量重命名（序号排序并补空）
```js
const fs = require('fs');

const path = require('path');

  

const targetDir = path.resolve(__dirname, '../src');

const files = fs.readdirSync(targetDir);

  

const numberList = files

  .filter(file => /^\d+_/.test(file))//选取数字开头的文件

  .map(file => parseInt(file.split('_')[0])) //提取数字

  .sort((a, b) => a - b);//排序

  

const missingNums = [];

const maxNum = numberList[numberList.length - 1];//找出最大元素

  

//将缺失元素找出

for (let i = 1; i < maxNum; i++){

  if (!numberList.includes(i)) {

    missingNums.push(i);

  }

}

  

//建立重新排序映射表

let cunt = 1;

const renumberMap = {};

files.forEach(file => {

  if (/^\d+_/.test(file)) {

    const [oldNum] = file.split('_');//直接取出file.split('_')的第0个元素赋予oldNum

    renumberMap[file] = cunt++;

  }

});

  

let renamedCount = 0;

files.forEach(file => {

  if (/^\d+_/.test(file)) {

    const newNum = renumberMap[file];//取出文件对应count

    const [, ...restParts] = file.split('_');//取出数字_以外所有部分（不加...则会忽略split第二部分以外的其他部分）

    const restName = restParts.join('_');//将剩余部分用_连接以保持原样

    const newName = `${newNum.toString().padStart(2, '0')}_${restName}`;//padStart(2,'0')指的是数字保证两位位，不满则以0开头

    const oldPath = path.resolve(targetDir, file);

    const newPath = path.resolve(targetDir, newName);

    console.log(oldPath + '=>' + newPath);

    fs.renameSync(oldPath, newPath);

  }
```