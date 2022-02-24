# node服务器端开发

## 一、模块化

### 1.系统模块

 	node的是由JavaScript和一些附带API组成，除此之外还提供了一些模块。JavaScript由ECMAScript、DOM、BOM组成，局限于浏览器，因此他不能如Java、C语言那般对计算机的硬件资源进行访问。而node提供的系统模块可以是JavaScript对计算机的一些硬件资源进行访问，如fs模块、path模块可以对计算机资源的访问路径进行拼接以及解析。

#### 常用模块：

fs模块：对计算机的文件进行读写的模块

API：

```javascript
fs.readFile(资源路径，编码)
fs.writeFile(资源路径，编码)
```

path模块：对计算机资源进行拼接以及解析

http模块：网络资源开放接口，该模块用于构建nodejs服务器

url模块：对GET请求的参数进行解析

```javascript
url.parse(url地址，true)
```

queryString模块：

```javascript
queryString(url地址，true)
```

### 2.第三方模块

 	第三方模块是由node以外的第三方提供的模块，方便快速开发，这些模块主要是对已有的功能进行封装，使其更加易用，简捷。

####  常用模块：

nodemon模块：一个命令模块，方便运行js文件

```
nodemon js文件		#运行js文件
```

nrm模块：资源下载地址管理，也是一个命令模块，主要方便切换资源下载地址

```
nrm ls		 #列出所有资源下载地址
nrm use 下载地址		#切换资源下载地址
```

gulp模块：对资源文件进行任务处理，一个对象。

MySQL模块：一个对象，用于连接数据库对数据库资源进行访问，提供一系列的API。

```javascript
//数据库连接，API：createPool返回一个连接对象
const db = mysql.createPool({
    host: 'localhost',			//主机
    user: 'root',				//用户名
    password: 'root',			//密码
    database: 'myigou'			//数据库
});

const getCateNames = `SELECT * FROM category ORDER BY category_id desc`;

//sql语句执行，API：query
db.query(getHomeStr, (err, data) => {
    if (err) {
        console.log(err);
        res.status(500).send('database err').end();
    } else {
        if (data.length == 0) {
            res.status(500).send('no datas').end();
        } else {
            res.send(data);
        }
    }
});
```

mime模块：可以对资源的类型进行判断

```javascript
mime.getType(资源)		//判断资源类型
```

mongoose模块：建立与mongoose数据库的连接并执行语句并调取资源

body-Parser： post请求参数解析

formidable：表单数据解析

### 3.模块导入与导出

#### 导入：

 	1.require： nodejs提供的模块导入API

```javascript
require("fs")		//导入模块
```

 	2.import： ES6规范提供关键字，用户模块的导入

```javascript
import 模块名 from '模块路径'		//整体导入
import { s1,s2... } from '模块路径'		//模块按需导入
```

#### 导出：

 	1.module.exports： nodejs提供的模块成员导出对象

```javascript
module.exports.getting = 成员		//添加导出成员
```

 	2.exports： nodejs提供的模块成员导入对象

```javascript
exports.add = 成员		//添加导出成员
```

 	3.export： ES6提供的模块成员导出关键字

```javascript
export default {		//默认导出
    成员1,
    成员2
}

export 成员1;		//按需导出
export 成员2;		//按需导出
export 成员3;		//按需导出
```



## 二、构建node服务器

### 1.服务器构建

```javascript
const http = require("http")		//导入http模块
const app = http.createServer()		//使用createServerAPI创建一个服务对象
```

### 2.请求处理

请求：由客户端向服务器端发送资源请求

http模块

url模块

queryString模块

#### 1.获取请求方式：

```javascript
const http = require("http")		//引入http模块
const app = http.createServer()		//创建web服务对象
app.on('request',(req,res) => {		//注册请求事件，用户接受用户请求
    console.log(req.method)			//获取请求方式
})
```

#### 2.获取请求头

```javascript
const http = require("http")
const app = http.createServer()
app.on('request',(req,res) => {
	console.log(req.headers)		//获取请求头
})
```

#### 3.请求参数处理

GET：

```JavaScript
const http = require("http")
const app = http.createServer()
const url = require('url')		//GET参数解析模块
app.on('request',(req,res) => {
	let { query,pathname } = url.parse(req.url,true)		//左边对象解构，右边参数解析
	console.log(query)		//打印参数对象
})
```

POST：

```javascript
const http = require("http")
const app = http.createServer()
const queryString = require('queryString')		//POST参数解析模块
app.on('request',(req,res) => {
    let queryPlaceholder
    req.on('data', params =(){
    	queryPlaceholder += data
    })
    req.on('end',()=> {
		let { query,pathname } = queryString.parse( queryPlaceholder )
        						//左边对象解构，右边参数解析
		console.log(query)		//打印参数对象
    })
})
//post数据会分为多次传输
```

### 3.响应处理

#### 1.响应

```javascript
const http = require("http")
const app = http.createServer()
app.on('request',(req,res) => {
    res.end()
})
```

#### 2.状态码

```javascript
const http = require("http")
const app = http.createServer()
app.on('request',(req,res) => {
    res.writeHead(状态码,{})
    res.end()
})
```

#### 3.响应头

```javascript
const http = require("http")
const app = http.createServer()
app.on('request',(req,res) => {
    res.writeHead(状态码,{
        请求头
    })
    res.end()
})
```

#### 4.响应体

```javascript
const http = require("http")
const app = http.createServer()
app.on('request',(req,res) => {
    res.writeHead(状态码,{
        "content-Type":"text/palin;charset=utf8"	//输出为纯文本并解决响应中文乱码问题
    })
    res.end(`<h1>你好</h1>`)			//响应内容
})
```

#### 5.静态资源处理

```javascript
const http = require("http")
const app = http.createServer()
const mime = require("mime")		//用于获取静态资源的类型
const path = require('path')
app.on('request',(req,res) => {
    let realpath = path.join(__dirname,'public',req.url)
    let Type = mime.getType(realpath)
    fs.readFile(realpath, (error,result) => {
        if(error != null){
            res.writeHead(200,{
                "content-Type":'text/palin;charset=utf8'
            })
            res.end("获取资源失败")
        } else {
            res.writeHead(200,{
                "content-Type":Type + ";charset=utf8"
            })
            res.end(result)
        }
    })
})
```

### 4.异步编程

1.异步API

2.回调地狱

3.promise对象

## 三、框架开发（Express）

 	Express是基于node环境来搭建Web服务器的框架，其是对node的http进行封装，主要是通过提供的中间件的路由来构造供外界访问的接口，

### 1.中间件

 	中间件主要是对请求的中间处理，类似于过滤器，Express框架的中间件是由app.get、app.post、app.use三种，
 	
 	每个中间件都有其独特的特性：

app.get：处理get请求

```javascript
app.get('/index',(req,res,next) => {
	next()		//中间件的传递
})
```

app.post：处理post请求

```javascript
app.post('/index',(req,res,next) => {
	next()		//中间件的传递
})
```

app.use：处理post和get请求

```javascript
app.use('/index',(req,res,next) => {
	next()		//中间件的传递
})
```

特殊的app.use：当use没有请求路径时，默认处理该服务器上的所有请求

```javascript
app.use((req,res,next) => {
	next()
})
```

### 2.路由

 	路由与中间件大致一致，不同的是，中间件的中间处理，而路由则是一个请求的最终处理；通过中间的中间处理，传递给路由做最终处理，而后响应结果给客户端；
 	
 	路由由两个API，一个是app.get、app.post

app.get：

```javascript
app.get('/index',(req,res) => {
	res.send()
})
```

app.post：

```javascript
app.post('/index',(req,res) => {
	res.send()
})
```



### 3.模块路由

 	模块路由，可以理解为定义二级路由，为了好维护，进行路由模块化管理，避免路由之间相互交叉，缠绕。模块路由是通过Express框架的Router API实现的，使用Router API构造一个router对象，用其router.get、router.post两个API来创建二级路由。

创建模块路由对象：

```javascript
const express = require('Express')
const app = express()
const router = express.Router()
```

创建模块路由：

```javascript
router.get('/children',(req,res) => {
	res.send()
})

router.post('/children',(req,res) => {
    res.send()
})
```

### 4.获取请求参数

 	创建中间件、路由、和子路由可以接受请求，在接受请求的同时还要对其请求参数做相应的处理，主要是POST请求，post请求有两种参数类型，需要使用第三方模块（body-parser）对参数进行解析，而GET请求Express框架已经封装了解析函数。

GET：

```javascript
//获取请求参数
app.get('/index',(req,res) => {
    console.log(req.query)
})
```

POST：

```javascript
const bodyParser = require('body-parser')
app.use(bodyParser.urlencoded({ extended:false }))		
		//解析application/x-www-form-urlencoded类型的参数
app.use(bodyParser.json())		
		//解析application/json类型的参数
app.post('/index',(req,res) => {
    console.log(req.body)
})
```

路由参数接收：

```javascript
//请求示例：http://localhost:3000/index/3/zhangsan
app.get('/index/:id/:name',(req,res) => {
    console.log(req.params)
})
```

### 5.设置响应信息

 	在路由处理完请求后，便需要将处理完后的数据响应到客户端，在这里以GET请求为例

```javascript
app.get('/index',(req,res) => {
    const array = [
        { name: "lisi", age: 20 },
        { name: "wangwu", age: 22 },
        { name: "zhangsan", age: 15}
    ]
    res.setHeader('content-Type','application/json')		//设置响应头
    res.send(array)		//设置响应头
})
```

### 6.静态文件处理

```javascript
const express = require('express')
const app = express()
app.use(express.static('public'))		//public为静态资源目录
```

## 四、Ajax交互

 	ajax(asynchronous JavaScript and XML，异步的JavaScript和XML)是浏览器提供的一种网页开发技术，实现了网页无刷新更新数据，主要是用来向后端发送请求。

创建Ajax对象：

```javascript
var xhr = new XMLHttpRequest()
```

发送Ajax请求：

```javascript
var xhr = new XMLHttpRequest()
xhr.open('get','http://localhost:3000/index')
xhr.send()
```

接受响应数据：

```javascript
var xhr = new XMLHttpRequest()
xhr.open('get','http://localhost:3000/index')
//方式一
xhr.onload = function(data){
    console.log(data)
}
//方式二
xhr.onreadystatechange = function(data) {
    console.log(data)
}
xhr.send()
```

### 1.请求行

 	请求行是用于指定发送请求的方式和url地址，这里通过open API指定

```javascript
var xhr = new XMLHttpRequest()
xhr.open('get','http://localhost:3000/index')
xhr.send()
```

 	参数一为请求的方式，主要为POST和GET，参数二则为请求的url地址，参数三为可选参数，用来指定ａｊａｘ异步API，默认为ｔｒｕｅ

### 2.请求头

　	请求头中指定了请求的相关信息，Ajax中使用的是setRequestHeader API

```javascript
var xhr = new XMLHttpRequest()
xhr.open('post','http://localhost:3000/index')
xhr.setRequestHeader('content-Type','application/json')
xhr.send()
```

### 3.请求参数

#### 1.GET请求参数传递

 	使用GET请求方式传递参数时，将参数拼接在url地址的后面，使用的是字符串传递的方式

```javascript
var xhr = new XMLHttpRequest()
xhr.open('get','http://localhost:3000/index?name=zhangsan&&age=30')
xhr.send()
```



#### 2.POST请求参数传递

```javascript
var xhr = new XMLHttpRequest()
xhr.open('post','http://localhost:3000/index')
//方式一
var username = 'zhangsan'
var age = 20
var params = 'name='+username+'&age='+age
xhr.setRequestHeader('content-Type','application/x-www-form-urlencoded')
xhr.send(params)

//方式二
var username = 'zhangsan'
var age = 20
var params = 'name='+username+'&age='+age
xhr.setRequestHeader('content-Type','application/json')
xhr.send(JSON.stringify(params))
```



### 4.Ajax函数封装

```javascript
function ajax(options) {
    var defaults = {
    	type:'get',
        url:'',
        data:''
    	contentType:'application/x-www-form-urlencoded',
        success:function(data){
            console.log(data)
        },
        error:function(data){
            console.log(data)
        }
	}
	Object.assign(defaults,options)
	var xhr = new XMLHttpRequest()
    var params = ''
    for(var attr in defaults.data){
        params += attr + '=' + defaults.ddata[attr] + '&'
    }
	params = params.substr(0,params.length-1)
    if(defaults.type == 'get'){
        defaults.url = defaults.url + '?' + params
    }
    xhr.open(defaults.type,defaults.url)
    if(defaults.type == 'post'){
        if(defaults.contentType == 'application/x-www-form-urlencoded'){
            xhr.setRequestHeader('content-Type','application/x-www-form-urlencoded')
            xhr.send(params)
        } else if(defaults.contentType == 'application/json') {
            xhr.setRequestHeader('content-Type','application/json')
            xhr.send(JSON.stringify(params))
        }
    }
	xhr.onload = function(data){
        var contentType = xhr.getRequestHeader('content-Type')
        var responseText = xhr.responseText
        if(contentType.includes('application/json')){
            responseText = JSON.parser(responseText)
        }
        if(xhr.status == 200){
            defaults.success(data)
        } else {
            defaults.error(data)
        }
    }
	xhr.send()
}
```



### 5.form数据传递

### 6.Ajax同源策略

### 7.跨域处理

### 6.JQuery的Ajax

## 五、数据库

## 六、关键字（术语）

请求：由客户端向服务器端发送资源请求

响应：由服务器端向客户端响应资源