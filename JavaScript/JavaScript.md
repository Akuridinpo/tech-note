## js基础用法及注意事项
html中 js脚本代码必须位于`<script>`与`</script>`标签之间。

js脚本代码可被放置在html中的`<`body`>`和`<head>`部分中。

外源性js文件中不包含任何html标签。

js中的函数和变量声明都会进行hoisting(声明提升)，自动将声明提升至方法体最顶部。`var x;//声明函数`
但是初始化部分不会提升。`var y = 7;//初始化函数`

比较运算中，`if(10=="10")`返回值为true，想要更严格的比较运算则需要用到`===`同时检查表达式的值与类型。
switch语句所执行的判断使用的就是恒等判断。
```js
<script>  
function myFunction(){  
    var x = document.getElementById("number").value;  
    switch(x){  
        case 1:alert("数字1");  
        break;  
        case "1":alert("字符串1");  
        break;  
        default:alert("其他");  
    }  
}
```
![[Pasted image 20240629111130.png]]

JavaScript 中的所有数据都是以 64 位**浮点型数据(float)** 来存储。
所有的编程语言，包括 JavaScript，对浮点型数据的精确度都很难确定
```js
	var x = 0.1;var y = 0.2;var z = x + y            
    // z 的结果为 0.30000000000000004if (z == 0.3)            
    // 返回 false
    var z = (x * 10 + y * 10) / 10;       // z 的结果为 0.3
```

字符串断行需要使用反斜杠(\)
```js
var x = "Hello 
\World!";
```
## js赋值
js中的赋值统一使用关键字var，无论赋值为整数，字符串，数组，对象。
```javascript
var array=[1,"2"];//赋值数组格式
var array1=new Array(1,"2");/*使用关键词new申明类型，此时array1是对
                              象而非数组*/
var object={attribute1:"1",attribute2:2};//赋值对象格式
array=null/*Undefined 这个值表示变量不含有值。
			可以通过将变量的值设置为 null 来清空变量。*/
```
如果不使用关键字声明，变量将会自动作为window的一个属性。
`value = 1`
在非严格模式下，value是全局对象(即使在函数内定义)的可配置属性，可以删除，但是并不推荐用这种方法设置全局变量。
`console.log(delete value)//true`
## js输出
- 使用 **window.alert()** 弹出警告框。
- 使用 **document.write()** 方法将内容写到 HTML 文档中。
	使用该方法会覆盖文档。
- 使用 **innerHTML** 写入到 HTML 元素。
- 使用 **console.log()** 写入到浏览器的控制台。

## js语句
JavaScript 语句是发给浏览器的命令。

## js数据结构
**值类型(基本类型)**：字符串（String）、数字(Number)、布尔(Boolean)、空（Null）、未定义（Undefined）、Symbol。

**引用数据类型（对象类型）**：对象(Object)、数组(Array)、函数(Function)，还有两个特殊的对象：正则（RegExp）和日期（Date）。
变量的数据类型可以使用 typeof 操作符来查看

## js对象
JavaScript 对象是键值对的容器，拥有属性和方法
创建方法：
```js
new Object(value);//构造函数形式
var myObject={key1:value1,
			  key2:value2};//字面量形式
function Object(attribute1,attribute2){
	this.attribute1=attribute1;
	this.attribute2=attribute2;
}//构造器，想在构造器外对构造器内部添加新的属性方法，需要使用prototype属性
```
访问方法:
```JavaScript
var object={attribute1:"1",attribute2:2};
object.attribute1;
object["attribute1"];
```
创建对象中的方法:
```js
method:function(){

}//字面量形式

this.funName=funName;
function funName(){}//构造函数形式
```
执行对象方法:
```js
objname.methodname();
//如果代码没加括号，则会返回函数的定义而不是执行方法
```
方法也可以是对象中的一个属性
```javascript
var object = {first:"1",
        second:2,
        merge:function(){
            return this.first + this.second;
        }};
        myFunction = function() {
            alert(object.merge());
        }
```
在 JavaScript 中，几乎所有的对象都是 Object 类型的实例，它们都会从 ==Object.prototype== 继承属性和方法。

Object 构造函数创建一个对象包装器。

Object 构造函数，会根据给定的参数创建对象，具体有以下情况：

- 如果给定值是 null 或 undefined，将会创建并返回一个空对象。
- 如果传进去的是一个基本类型的值，则会构造其包装类型的对象。
- 如果传进去的是引用类型的值，仍然会返回这个值，经他们复制的变量保有和源对象相同的引用地址。
- 当以非构造函数形式被调用时，Object 的行为等同于 new Object()。

 JavaScript 是面向对象的语言，但 JavaScript 不使用类。
在 JavaScript 中，不会创建类，也不会通过类来创建对象（就像在其他面向对象的语言中那样）。
JavaScript 基于 prototype，而不是基于类的。

可以使用 for... In 循环，遍历对象的属性

### Prototype (原型对象)
所有的 JavaScript 对象都会从一个 prototype（原型对象）中继承属性和方法：

- `Date` 对象从 `Date.prototype` 继承。
- `Array` 对象从 `Array.prototype` 继承。
- `Person` 对象从 `Person.prototype` 继承。
```js
function person(firstname, lastname) {  
    this.firstname = firstname;  
    this.lastname = lastname;  
    this.changeName = changeName;//this is a reference to the function  
    function changeName(name) {  
        this.firstname = name;  
    }  
}  
person.eyecolor = "blue";//不会被实例继承  
person.prototype.nationality = "English";//会被实例继承
```

## Js 类
创建类：使用关键字 class
```js
class myClass{
	counstructor(){}//构造器
}
```
## js函数
格式:
```js
function functionname(para1, para2)  
{  
    // 执行代码_  
}
```
可自带参数:
```js
function myfun(x,y=6){
return x+y;
}
myfun(1);//7
myfun(1,2);//3
```
### 箭头函数
格式:
```js
(par1,par2,para3)=>{//函数体
					};
```
特性：
+ 语法简洁
+ 没有箭头函数不绑定 this，因此在回调函数或者嵌套函数中包含箭头函数，箭头函数内的 this 值为捕获包含它的上下文的 this 值。
### 自调用函数
```js
(function myfun(){//函数体
})();//自调用函数，不需要其他语句调用也会自我执行一次。
```
### 函数自带对象
+ argument 对象：拥有类似数组的结构，在函数内部，可以通过 `arguments[x]` 来获取函数的第 x 个参数，也可以通过 `argument.length` 获得参数个数。箭头函数没有 `arguments` 对象。
### 函数自带方法
+ `toString ()`
+ `apply()`
+ `call()`
### 函数闭包
函数闭包可以在函数的作用域外，访问函数内部的内部变量，实现数据封装或私有变量。

## js事件
![[Pasted image 20240626181001.png]]

事件可以用于处理表单验证，用户输入，用户行为及浏览器动作:

- 页面加载时触发事件
- 页面关闭时触发事件
- 用户点击按钮执行动作
- 验证用户输入内容的合法性
- 等等 ...

可以使用多种方法来执行 JavaScript 事件代码：

- HTML 事件属性可以直接执行 JavaScript 代码
- HTML 事件属性可以调用 JavaScript 函数
- 你可以为 HTML 元素指定自己的事件处理程序
- 你可以阻止事件的发生。
- 等等 ...

## js字符串
![[Pasted image 20240626181409.png]]![[Pasted image 20240626181424.png]]
定义字符串时可以使用反引号\`\`，此为模版字面量，在中间可以任意使用单引号和双引号。
同时，模版字面量中，可以使用`${变量名}`的方式来直接引用变量，或者使用`${表达式}`的方式来直接返回表达式。
甚至可以直接当做html模版使用。

## js正则表达式
语法：
`/正则表达式主体/修饰符(可选)
例如：
`var patt = /example/i`

在 JavaScript 中，RegExp 对象是一个预定义了属性和方法的正则表达式对象。

JavaScript 中，正则表达式通常用于两个字符串方法 : search() 和 replace()。
**search()** 方法用于检索字符串中指定的子字符串，或检索与正则表达式相匹配的子字符串，并返回子串的起始位置。
```js
var string = "hello world";
var n = string.search(/world/i)//6
```
**replace()** 方法用于在字符串中用一些字符串替换另一些字符串，或替换一个与正则表达式匹配的子串。
```js
var string = "hello world";
var text = string.replace(/world/i, "universe");//hello universe
```
其他方法：
**test()** 方法用于检测一个字符串是否匹配某个模式，如果字符串中含有匹配的文本，则返回 true，否则返回 false。

**exec()** 方法用于检索字符串中的正则表达式的匹配。
该函数返回一个数组，其中存放匹配的结果。如果未找到匹配，则返回值为 null。

以下实例用于搜索字符串中的字符 "e"：
![[Pasted image 20240626183422.png]]![[Pasted image 20240626183602.png]]
## js异常
异常值可以是任意数据类型
语法:
```js
try{
...throw...
}catch(err){//将抛出的异常保存进err中
//异常的捕获和处理
}finally{
//一定会执行，结束处理
}
```
## js调试
使用`console.log()`方法调试，在浏览器f12控制台中查看打印值。
debugger和断点一样，使代码停止在debugger语句/断点处。

## js严格模式
"use strict" 指令在 JavaScript 1.8.5 (ECMAScript5) 中新增。
它不是一条语句，但是是一个字面量表达式，在 JavaScript 旧版本中会被忽略。
"use strict" 的目的是指定代码在严格条件下执行。
严格模式下：
+ 你不能使用未声明的变量。
+ 不允许删除变量，对象，函数。
+ 不允许变量重名。
+ 不支持八进制。
+ 不支持转义字符。
+ 不支持对只读属性赋值。
+ 不允许对`getter()`方法读取的属性赋值。
+ 不允许变量名使用`eval`，`arguments`字符串。
+ 不允许使用`with()`语句。
	 `with()`语句通常用于直接设置特定对象的作用域，在`with()`语句中可以直接访问对象内的属性和方法。
 + 不允许调用在作用域`eval()`创建的变量。
 + `eval()`方法是一个全局函数，其可以执行一段js代码表示的字符串。
 + 禁止`this`关键字指向全局对象。 因此，使用构造函数时，如果忘了加new，this不再指向全局对象，而是报错。
 ```js
	function f(){
    return !this;
} 
// 返回false，因为"this"指向全局对象，"!this"就是false

function f(){ 
    "use strict";
    return !this;
} 
// 返回true，因为严格模式下，this的值为undefined，所以"!this"为true。
function f(){
"use strict";
this.a=1;
};
f();//this未定义,报错

```

为什么使用严格模式:
- 消除 Javascript 语法的一些不合理、不严谨之处，减少一些怪异行为。
- 消除代码运行的一些不安全之处，保证代码运行的安全。
- 提高编译器效率，增加运行速度。
- 为未来新版本的Javascript做好铺垫。

"严格模式"体现了Javascript更合理、更安全、更严谨的发展方向，包括IE 10在内的主流浏览器，都已经支持它，许多大项目已经开始全面拥抱它。
另一方面，同样的代码，在"严格模式"中，可能会有不一样的运行结果；一些在"正常模式"下可以运行的语句，在"严格模式"下将不能运行。掌握这些内容，有助于更细致深入地理解Javascript，让你变成一个更好的程序员。
## js关键字
### this
面向对象语言中 this 表示当前对象的一个引用。

但在 JavaScript 中 this 不是固定不变的，它会随着执行环境的改变而改变。

- 在方法中，this 表示该方法所属的对象。
```js
<p id="demo"></p>  
<script>  
    var obj={  
        name:"John",  
        age:30,  
        city:"New York",  
        data: function(){  
            return this.name + " is " + this.age + " years old and lives in " + this.city;  
        },  
        myfunction: function(){  
            return this;  
        }  
    };  
    document.getElementById("demo").innerHTML = obj.myfunction();//[object object]
		    /*显示原因为返回了一个对象，而将对象设置为innerHTML时，js回调用toString方法，
			  toString方法对对象是用会返回[object object]*/
```
- 如果单独使用，this 表示全局对象。
`var x = this;`在浏览器中，window就是该全局对象为`[object window]`。
- 在函数中，this 表示全局对象。
- 在函数中，在严格模式下，this 是未定义的(undefined)。
- 在事件中，this 表示接收事件的元素。
- 类似` call()` 和 `apply()` 方法可以将 this 引用到任何对象。
		call()可以调用函数以及设置函数内部的this值。
```js
var obj1={  
    name:"John",  
    age:30,  
    city:"New York",  
    data: function(){  
        return this.name + " is " + this.age + " years old and lives in " + this.city;  
    }  
};  
var obj2={  
    name:"Mike",  
    age:25,  
    city:"Los Angeles"  
};  
function namefunction(){  
    return this.name;  
}
var txt =obj1.data.call(obj2);  
document.getElementById("demo").innerHTML =txt;//Mike is 25 years old and lives in Los Angeles
var text2 = namefunction.call(obj1);  
document.getElementById("demo1").innerHTML =text2;//john

```


### let
`let`只在块级作用域内生效。
```js
var x = 1;
var z = 0;
{
var x = 2;
let y = 3;
let z = 4;
}
//此处可以使用x,x=2,不可以使用y,可以使用z,z=0。
```
在循环体内也会使用`let`
```js
var i = 5;
for(let i = 0; i < 10; i++){
	//一些代码...
}
//此处i=5。
```
在函数体内部使用`let`和`var`效果类似，作用域都为函数体内部。
同时，在代码块外使用也类似，作用域都为全局。但区别是:
在HTML中，全局作用域针对window对象，`var`声明的全局作用域变量属于window对象，而==let声明的全局作用域变量不属于window对象。==
```js
var carName = "siu7";  
document.getElementById("demo").innerHTML = window.carName;
//输出siu7
let carName1 = "volvo";  
document.getElementById("demo1").innerHTML = window.carName1;
//输出undefined
```
关于重置变量：
使用 **var** 关键字声明的变量在任何地方都可以修改。
在相同的作用域或块级作用域中，不能使用 **let** 关键字来重置 **var** 关键字声明的变量。
在相同的作用域或块级作用域中，不能使用 **let** 关键字来重置 **let** 关键字声明的变量。
在相同的作用域或块级作用域中，不能使用 **var** 关键字来重置 **let** 关键字声明的变量。
**let** 关键字在不同作用域，或不同块级作用域中是可以重新声明赋值的。

|     | var      | let              |
| --- | -------- | ---------------- |
| var | 可在任何地方重置 | 只能在不同作用域或块级作用域重置 |
| let | 不可重置     | 只能在不同作用域或块级作用域重置 |
### const
`const`声明时必须进行初始化，且初始化后值不可再修改。
`const`定义常量与使用`let` 定义的变量相似：
- 二者都是块级作用域
- 都不能和它所在作用域内的其他变量或函数拥有相同的名称

两者还有以下两点区别：
- `const`声明的常量必须初始化，而`let`声明的变量不用
- const 定义常量的值不能通过再赋值修改，也不能再次声明。而 let 定义的变量值可以修改。

`const` 的本质: `const` 定义的变量并非常量，并非不可变，它定义了一个常量引用一个值。使用 const 定义的对象或者数组，其实是可修改或添加属性的。下面的代码并不会报错：
```js
// 创建常量对象
const car = {type:"Fiat", model:"500", color:"white"};
 
// 修改属性:
car.color = "red";
 
// 添加属性
car.owner = "Johnson";
```
但是我们不能对常量对象重新赋值：
```js
// 创建常量对象
const car = {type:"Fiat", model:"500", color:"white"};
car = {};//报错
```
数组同理。
关于重置变量：

|       | 相同作用域可修改 | 不同作用域可修改 |
| ----- | -------- | -------- |
| var   | var      | var,let  |
| let   |          | let      |
| const |          | const    |

### void
计算一个表达式但不返回值。
```js
<a href ="javascript:void(0)">nothing happen</a>
/*一个点了什么都不会发生的超链接。
  用户点击时，void计算为0，但是什么都不返回。*/
<button onclick="javascript:void(alert('Hello World!'))">Click me!</button>
//用户点击时执行alert('Hello World!')
```
## json
json(java script object notation),是一种轻量级的数据交换格式。
json是独立的语言，易于理解。
==JSON 使用 JavaScript 语法，但是 JSON 格式仅仅是一个文本。  
文本可以被任何编程语言读取及作为数据格式传递。==
### json实例
```json
{"cars":[  
    { "name":"Ford", "model":"Mustang" },  
    { "name":"BMW", "model":"X5" },  
    { "name":"Fiat", "model":"500" }  
]}
```
### json语法规则
+ 数据为键/值对
+ 由逗号分隔
+ 大括号保存对象
+ 方括号保存数组
### JSON字符串转化为js对象
首先读取JSON数据，创建为字符串：
```js
var car = `{"cars":[  
    { "name":"Ford", "model":"Mustang" },  
    { "name":"BMW", "model":"X5" },  
    { "name":"Fiat", "model":"500" }  
]}`;
```
接下来使用js内置函数`JSON.parse()`将字符串转化为JS对象：
`var obj = JSON.parse(car);`
此时，obj已经成为一个可使用的对象。

`JSON.stringify()`函数：将对象转化为JSON格式的字符串。

## js异步编程
### 异步编程：

+ 程序不按照编辑好的语句顺序严格执行，同步时一条语句未执行完则下一条不进行，而异步时在一个语句在执行过程中，程序不必阻塞等待，可以先处理不需要等待的操作，再回来继续执行相关任务。
### 什么时候使用异步编程：
+ 当程序需要进行I/O操作（网页请求，文件上传）时，一般耗时较长，此时，我们会通过回调函数来管理异步结果。
+ 在JS中，异步模型依赖于事件循环和回调队列。
   当执行一个异步操作时，该操作会被放入一个等待队列中，主线程继续执行后面的代码。
   一旦异步操作完成，它的回调函数会被放入回调队列中，此时事件循环会检查主线程是否空闲，如果空闲，就从回调队列中取回回调函数运行。
```js
setTimeout(function(){  
    document.getElementById("demo").innerHTML = "Hello world!";}  
, 3000);  //三秒后回调函数才会执行
    document.getElementById("demo1").innerHTML = "Hello JavaScript!";//直接执行
```
### AJAX
+ AJAX 是一种运用于网页上提供动态交互的技术，该技术可以允许用户在不重新加载整个网页的情况下与服务器进行交互。
#### AJAX 的核心：
+ XMLHttpRequest 对象：
  该对象允许网页在后台服务器交互。
#### AJAX 的使用：
```js
//首先，我们创建一个 XMLHttpRequest 对象  
var xhr = new XMLHttpRequest();  
//然后，我们用open方法初始化一个新的请求，GET表示请求数据，url表示请求的地址，true表示请求是异步的  
xhr.open('GET', 'https://api.github.com/users', true);  
//定义回调函数，当请求完成时调用  
xhr.onreadystatechange=function() {  
    //当请求完成且成功时  
    if (xhr.readyState == 4 && xhr.status == 200) {  
    /*readyState===4:请求完成且响应已经完全接受
      status===200:http状态码为200表示请求成功
    */
        console.log(JSON.parse(xhr.responseText));  
    }  
};  
//发送请求  
xhr.send();

```
### Promise
Promise 是一个构造函数，Promise 的参数是一个函数，该函数包含 resolve 参数和 reject 参数，这两个参数分别返回成功与失败信息并对应地改变 Promise 的状态。

```js
// 创建一个promise对象  
 var promise = new Promise((resolve, reject)=>{  
     /*promise是一个构造函数,接受一个函数作为参数,  
       (resolve, reject)=>{}是一个执行器函数,这个函数有两个函数参数,resolve和reject。  
     */     setTimeout(()=>{  
         // 通过resolve函数来改变promise的状态  
         if(Math.random() < 0.5) {  
             resolve('success');  
         }else{  
             reject('fail');  
         }  
     }, 300);  
 });  
promise.then(result=> {  
    console.log(result);  
}).catch(error=> {  
    console.log(error);  
});
```

`resolve` 和 `reject` 都是函数，正常时调用 `resolve `，异常则调用 ` reject `。
`resolve` 中的参数会传入 `. then`，`reject` 同理。
```js
var promise = new Promise(function(resolve, reject){  
    var a = 2, b = 1;  
    if(b==0) reject('Divide by zero');  
    else resolve(a/b);  
}).then(function(value){  
    console.log("a/b = " + value);  
}).catch(function(err){  
    console.log("Error: " + err);  
}).finally(function(){  
    console.log("End");  
});
```
+ Promise 包含了方法 `then， catch，fianlly`，其中 `then` 用于处理 Promise 成功后的回调函数，`catch` 处理失败的回调函数，`.fianlly ` 为一定执行。
+ Promise 可以包含多个 `.then `， `.then ` 传入的函数会按顺序依次执行，上一个 `.then ` 的返回 promise 对象的值会传入下一个 `.then ` 继续执行。有任何异常都会直接跳到 `.catch ` 序列。可以使用 ` throw ` 语句使 `.then ` 不继续执行，而是直接跳转至 `.catch `。
```js
// 创建一个promise对象  
var promise = new Promise(function(resolve, reject){  
    var a = 2, b = 1;  
    if(b==0) reject('Divide by zero');  
    else resolve(a/b);  
}).then(function(value) {  
    console.log("a/b = " + value);  
    return value+1;//返回一个promise对象  
}).then(function(value){//这里的value是上一个then返回的promise对象的值  
    console.log("a/b + 1 = " + value);  
}).catch(function(err){//捕获错误  
    console.log("Error: " + err);  
}).finally(function(){//无论如何都会执行  
    console.log("End");  
});
```
当 return 的不是一个值，而是一个新的 promise 对象时，下一个 then 会对这个对象进行操作。
```js
function print(delay,message){  
    return new Promise((resolve,reject)=>{  
        setTimeout(()=>{  
            console.log(message);  
            resolve();  
        },delay);  
    }).then(()=>{  
        return new Promise((resolve,reject)=>{  
            setTimeout(()=>{  
                console.log(message);  
                resolve();  
            },delay);  
    }).catch((error)=>{  
        console.log(error);  
    }).finally(()=>{  
        console.log('done');  
    });  
});  
}
```
```js
function print(message, delay){  
    return new Promise((resolve, reject)=>{  
        setTimeout(()=>{  
            console.log(message);  
            resolve();//resolve the promise  
        }, delay)  
    });  
}  
print('Hello', 1000).then(()=>{ //由于print函数返回的是一个Promise对象，所以可以使用.then方法
    return print('World', 1000);  
}).then(()=>{  
    return print('!', 1000);  
});

```
### Async
 异步函数 `async function fun()` 可以使用 `await` 指令。
 `await` 指令后面需要跟随一个 `promise` 函数，`await` 会让异步函数停止，等到 `promise` 完成后再继续运行。
 ```js
 async function printAll(){  
    await print('Hello', 1000);  
    await print('World', 500);  
    await print('!', 100);  
}
 ```
## DOM
+ document object model，文档对象模型。
+ dom 是一种数据结构，将HTML 或者 XML 文件以树状层次表现，并提供了丰富的接口，使编程语言可以操控 dom 中的元素。
+ dom 可以使开发者用编程的方式，动态地与网页交互。
### 常用的 dom 接口
#### 查找 HTML 元素
```js
document.getElementById("");//通过id获取元素
document.getElementByClass("");//通过类名获取元素，由于class的元素不唯一，所以获取的元素依次放入数组中。
document.getElementByTag("");//通过标签获取元素，同样由于标签不唯一，所以获取的元素依次放入数组中。
```
#### 修改 HTML 元素
```js
document.write();//直接动态创建HTML内容。
document.getElementById("").innerHTML="";//将获取的元素中的HTML文本直接修改
document.getElementsByTagName("p")[0].innerHTML = "";//同上
document.getElementsByTagName("img")[0].src="";//直接修改图片
```
### 修改 HTML 事件
```js
onclick = "this."//点击
onload = ""//进入网页时触发
onunload = ""//离开网页时触发
onchange = ""//离开输入框时触发
onmouseover = ""//鼠标移至该处触发
onmouseout = ""//鼠标移开触发
```
### 创建 HTML 元素
```js
<body>  
    <div id="div1">  
        <p id="p1">This is a paragraph.</p>  
        <p id="p2">This is another paragraph.</p>  
    </div><script>  
    var para=document.createElement("p");//create a new paragraph element  
    var node=document.createTextNode("This is new.");//create a text node  
    para.appendChild(node);//add the text node to the paragraph element  
    var element=document.getElementById("div1");//find an element with the id "div1"  
    element.appendChild(para);//add the paragraph element to the div element  
</script>
```

## NodeList 与 Collection 的区别
HTMLCollection 是 HTML 元素的集合。

NodeList 是一个文档节点的集合。

NodeList 与 HTMLCollection 有很多类似的地方。

NodeList 与 HTMLCollection 都与数组对象有点类似，可以使用索引 (0, 1, 2, 3, 4, ...) 来获取元素。

NodeList 与 HTMLCollection 都有 length 属性。

HTMLCollection 元素可以通过 name，id 或索引来获取。

NodeList 只能通过索引来获取。

只有 NodeList 对象有包含属性节点和文本节点。