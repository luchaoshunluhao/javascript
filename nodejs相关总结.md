## 一、Node快速体验

### 1、 Node介绍

#### （1） [Node.js](https://nodejs.org/en/)是什么

- `Node`  是一个基于` Chrome V8` 引擎的` JavaScript ` 运行环境。  
  - `Node`  不是一种独立的语言、
  - `Node`不是 `JavaScript ` 框架，
  - `Node`是一个**除了浏览器之外的、可以让` JavaScript ` 运行的环境**

#### （2） Node 能做什么

[知乎 - Node.js能做什么，该做什么？](https://www.zhihu.com/question/20796866)

- Web 服务器(重点)
- 命令行工具
- 网络爬虫:是一种按照一定的规则，自动地抓取网站信息的程序
- 桌面应用程序开发

#### （3） 一些资源

① 文档

[Node.js 官方文档](https://nodejs.org/en/docs/)
[Node.js 中文文档（非官方）](http://nodejs.cn/)

② 书籍

[深入浅出 Node.js](https://read.douban.com/ebook/12053349/)
[Node.js 权威指南](https://book.douban.com/subject/25892704/)
[Node.js 实战](https://book.douban.com/subject/25870705/)
[Node.js实战（第2季）](https://book.douban.com/subject/26642320/)

③ github资源

[Node.js 包教不包会](https://github.com/alsotang/node-lessons)
[ECMAScript 6 入门](http://es6.ruanyifeng.com/)
[七天学会 NodeJS](https://github.com/nqdeng/7-days-nodejs) 

④ 社区

**[Node.js 中文社区](https://cnodejs.org/)** 

### 2. Node起步

#### （1）安装Node

- 下载：https://nodejs.org/en/download/
- 历史版本：https://nodejs.org/en/download/releases/

> 对于已经装过的，重新安装就会升级
>
> 确认 Node 环境是否安装成功
>
> 打开命令行，输入 node --version
>
> 或者 node -v

#### （2）REPL环境(Read Eval Print Loop:交互式解释器：了解)

在命令行工具界面输入`node`  按回车 就进入到了`REPL` 环境

- read
- eval
- print
- loop

> 类似于浏览器中的 Console控制台 ，可以做一些代码测试。
>
> 按ctrl + 两次c 退出REPL环境
>
> 但是, 我们写代码肯定不是在控制台中写,而是写在一个单独的.js文件中.

#### （3）HelloWorld

1. 新建一个 `hello.js` 并写入以下示例代码

```js
var message = 'Hello World!'
console.log(message)
```

1. 打开命令行并定位到 `hello.js ` 文件所属目录
2. 在命令行中输入 `node hello.js ` 回车执行

```bash
node hello.js
```

#### （4）Node中的js

**node中的js和浏览器中的js不同:**

- 浏览器中的js
  - ECMAScript
  - DOM
  - BOM
- node中的js
  - ECMAScript
  - 自己的API
  - **没有DOM和BOM**

## 二、Node中的模块和包管理器npm

### 1、Node中的模块体验

#### （1）文件读写

文件读取：

```js
// 1、引用fs核心模块
var fs = require('fs');
// 2、读取文件
// fs.readFile中有两个参数：
//     path： 要读取文件的路径
//     callback：读取文件后面的回调函数
//          err: 读取文件异常的异常信息
//              如果文件读取出来err为null
//              如果文件读取失败err为失败信息
//          data: 文件中的内容
//              如果文件读取成功，那么将来data会是一个十六进制的Buffer数组
fs.readFile('./00.txt', function(err, data){
    // 输出文件中的内容
    console.log(err);
    console.log(data.toString());
});
```

文件写入：

> 注意：
>
> - 在写入时会覆盖已有的内容
>
> - 如果写入的文件不存在，会自动创建

```js
// 1、引用fs核心模块
var fs = require('fs');
// 2、向文件中写入内容
//  这个方法是用来覆盖原文件中的内容，
// fs.wirteFile(file, data, callback)
//      file：要写入内容的文件
//      data：要写入的数据（可以为utf-8）
//      callback：写入后的回调函数
//          err: 写入失败后面的异常信息     
fs.writeFile('./0000.txt', '天若有情天易老，人间正道是沧桑', function(err){
    if (err) {
        console.log(err.message);
    } else {
        console.log('写入成功');
    }
});
```

文件追加写：

```js
// 核心模块：fs
//      fs.readFile
//      fs.writeFile
//  思想：先读，然后追加，然后再写

var fs =require("fs");
// 1、读取
fs.readFile("./00.txt", function(err, data){
    if(err) {
        console.log(err.message);
    } else {
        // 2、追加
        var str = "小猪配奇身上纹，掌声送给社会人";
        str = data + str;
        fs.writeFile("./00.txt", str, function(err) {
            if(err) {
                console.log(err.message);
            } else {
                console.log("写入成功");
            }
        });
    }
});
```

#### （2）HTTP 服务

```js
// node把处理web服务器相关的功能 封装到了 http模块中
// 1、导入http模块
var http = require('http');
// 2、使用http这个模块中的createServer()创建一个服务器实例对象
var server = http.createServer();
// 3、给服务器对象注册一个request事件，当浏览器有请求发送过来时，服务器会接收，并且执行后面的回调函数
// 请求处理函数function(形参1,形参2){}
// 形参1:request请求对象 获取到当前请求的路径,方法等信息
// 形参2:response响应对象 发送响应数据
server.on('request', function(request, response) {
    console.log('有浏览器连接上来了!');
    // 向客户端页面返回字符串
    response.write("hello node");
    // 结束响应
    response.end();
});
// 4、绑定端口号,启动web服务器
server.listen(12345, function() {
    console.log(' 请访问http://localhost:12345');
});
```

> 注意: 
>
> 1. 注册request处理函数 有两个形参 request和response 不要搞混
> 2. 在写完服务器代码后 保存代码 ->在cmd中 `node 文件名` 然后回车执行
> 3. 每次修改代码后 要重新在cmd中 `node 文件名` 执行这个文件
> 4. !! 端口号尽量写的大一些 大于3000 否则容易和已经运行的软件所占用的接口相冲突!

### 2、小案例

#### （1）通过http模块写一个自己的服务器

需求：将来有请求链接上来以后，服务器需求响应一个hello world的内容回浏览器

```js
var http = require("http");
var server = http.createServer();
// 如果需要响应在requrest事件后面的回调函数中有两个参数：
//  request
//  response
// 参数：
//  request:浏览器发送到服务器的请求
//  response:服务器响应回浏览器的数据
//      方法：
//          write：向响应报文中写入一段要发送浏览器的数据，不会将数据立即响应回浏览器
//          end：将数据响应回浏览器
//          setHeader:设置响应头
server.on('request', function(request, response){
    // 响应数据回浏览器要借助response
    // response.write('hello');
    // response.write(' world');
    // response.end('hello world');
    // 设置响应报文的响应头
    response.setHeader("content-type", "text/html;charset=utf-8");
    response.end('<doctype><html><head></head><body></body></html>');
});
server.listen(3000, "192.168.81.1", function(){
    console.log('服务器开启成功');
});
```

#### （2）通过服务器响应一个完整的html页面回浏览器

js文件：

```js
var http = require("http");
// 引用fs模块
var fs = require('fs');
var server = http.createServer();
server.on('request', function(request, response){
    // response.setHeader("content-type","text/html;charset=utf-8");
    // response.end('');
    // 响应一个完整页面回浏览器的思路
    //  1、创建一个完整的html页面
    //  2、将这个页面中内容读取出来
    fs.readFile('./views/index.html', function(err, data){
        if(err) {
           return console.log(err.message);
        }
        //  3、将内容通过response.end响应回浏览器
        response.end(data);
    });
});
server.listen(3000, "192.168.81.1", function(){
    console.log('服务器开启成功');
});
```

html文件：./views/index.html

```html
<body>
    <h1>你好，世界！</h1>
</body>
```

#### （3）在上面基础上显示一张图片

js文件：

```js
var http = require("http");
var fs = require('fs');
var server = http.createServer();
// request:所有浏览器发送到服务器的请求数据
//    属性：
//      url  
server.on('request', function (request, response) {
    // 如果将来图片的请求过来服务器，服务器是没有作任何处理
    // 处理一个图片和页面的请求：
    //  约定：
    //      将来请求根目录时，是请求页面
    //      将来请求views/0.jpg时，是请求图片
    //  问题：如何得到请求的路径
    //      request.url
    // 判断：如果请求的 / ，响应页面回去
    //      如果请求的 /views/0.jpg响应图片回去
    if (request.url === '/') {
        fs.readFile('./views/index.html', function (err, data) {
            if (err) {
                return console.log(err.message);
            }
            response.end(data);
        });
    } else if (request.url === '/views/0.jpg') {
        fs.readFile("./views/0.jpg", function(err, data){
            if (err) {
                return console.log(err.message);
            }
            response.end(data);
        });
    }
});
server.listen(3000, "192.168.81.1", function () {
    console.log('服务器开启成功');
});
```

html文件：./views/index.html

```html
<body>
    <h1>你好，世界！</h1>
    <!-- 因为这个路径压根就没有在服务器中被解析过，是浏览器来解析，因此使用绝对路径 -->
    <img src="/views/0.jpg" id="img">
</body>
```

#### （4）在此基础上响应一个js文件

```js
var http = require("http");
var fs = require('fs');
var server = http.createServer();
server.on('request', function (request, response) {
    // 处理根目录的请求
    if (request.url === '/') {
        fs.readFile('./views/index.html', function (err, data) {
            if (err) {
                return console.log(err.message);
            }
            response.end(data);
        });
        // 处理了图片的请求
    } else if (request.url === '/views/0.jpg') {
        fs.readFile("./views/0.jpg", function(err, data){
            if (err) {
                return console.log(err.message);
            }
            response.end(data);
        });
        // 处理jquery
    } else if (request.url === '/views/jquery.min.js') {
        fs.readFile("./views/jquery.min.js", function(err, data){
            if (err) {
                return console.log(err.message);
            }
            response.end(data);
        });
    }
});
server.listen(3000, "192.168.81.1", function () {
    console.log('服务器开启成功');
});
```

html：

```html
<body>
    <h1>你好，世界！</h1>
    <img src="/views/0.jpg" id="img">
    <input type="button" value="点我隐藏" id="btn">
</body>
<script src="/views/jquery.min.js"></script>
<script>
     $("#btn").click(function(){
         $("#img").hide(1000);
     });
</script>
```

#### （5）在此基础上统一处理静态文件

js文件：

```js
var http = require("http");
var fs = require('fs');
var server = http.createServer();
server.on('request', function (request, response) {
    if (request.url === '/') {
        fs.readFile('./views/index.html', function (err, data) {
            if (err) {
                return console.log(err.message);
            }
            response.end(data);
        });
    }   
    // 统一处理静态资源：
    // 判断请求路径中是否有携带views
    else if (request.url.indexOf("/views") != -1) {
        // 直接将对应的文件读取出来
        // 先将绝对路径转为相对路径
        var url = '.' + request.url;
        fs.readFile(url, function(err, data){
            if(err) {
                return console.log(err.message);
            } 
            response.end(data);
        });
    }
});
server.listen(3000, "192.168.81.1", function () {
    console.log('服务器开启成功');
});
```

html：

```html
<head>
	<link rel="stylesheet" href="/views/index.css">
</head>
<body>
    <h1>你好，世界！</h1>
    <img src="/views/0.jpg" id="img">
    <input type="button" value="点我隐藏" id="btn">
</body>
<script src="/views/jquery.min.js"></script>
<script>
     $("#btn").click(function(){
         $("#img").hide(1000);
     });
</script>
```

#### （6） 完成仿apache的目录浏览功能

> 步骤：
>
> - 服务器
>   - 1、创建一个服务器
>   - 2、如果将来浏览器请求静态页面，我们就将一个静态文件返回到浏览器
>   - 4、服务器接收到浏览器的请求，将当前目录下的所有的路径读取出来，并且返回给浏览器的异步对象
> - 浏览器
>   - 3、通过浏览器发送一个异步请求到服务器，去请求当前服务器的目录数据(getPath)
>   - 5、浏览器接收数据，并且将数据渲染到页面上

js文件：

```js
// 创建一个服务器
// 1、引用http模块
var http = require('http');
var fs = require('fs');

// 2、创建一个服务器对象
var server = http.createServer();

// 3、设置request事件
server.on('request', function (req, res) {
    // 3.1、请求请求参数
    var url = req.url;
    // 3.2、判断是否请求的是首页  /
    if (url === '/') {
        // 将首页的静态文件响应回浏览器
        // 先通过fs模块将内容读取出来
        fs.readFile('./views/index.html', function(err, data){
            if(err) {
                return console.log(err.message);
            } 
            res.end(data);
        });
    }
    // 3.3、判断是否请求的是静态文件
    else if (url.indexOf('/views') != -1) {
        fs.readFile('.' + url, function(err, data){
            if(err) {
                return console.log(err.message);
            } 
            res.end(data);
        });
    }
    // 3.4、判断请求的是否是getPath
    else if (url === '/getPath') {
        //将当前目录下的所有的路径读取出来，并且返回给浏览器的异步对象
        fs.readdir('./', function(err, files){
            if(err) {
                return console.log(err.message);
            }
            // 将files数组转为json格式的字符串
            var str = JSON.stringify(files);
            // console.log(str);
            // 响应回浏览器
            res.end(str);
        });
    }
});
// 4、开启监听
server.listen(3000, '192.168.81.1', function () {
    console.log('开启成功');
});
```

html：

```html
  <style>
    h1 {
      border-bottom: 1px solid #c0c0c0;
      margin-bottom: 10px;
      padding-bottom: 10px;
      white-space: nowrap;
    }
    
    table {
      border-collapse: collapse;
    }
    
    th {
      cursor: pointer;
    }
    
    td.detailsColumn {
      -webkit-padding-start: 2em;
      text-align: end;
      white-space: nowrap;
    }
    
    a.icon {
      -webkit-padding-start: 1.5em;
      text-decoration: none;
    }
    
    a.icon:hover {
      text-decoration: underline;
    }
    
    a.file {
      background: url("data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAIAAACQkWg2AAAABnRSTlMAAAAAAABupgeRAAABHUlEQVR42o2RMW7DIBiF3498iHRJD5JKHurL+CRVBp+i2T16tTynF2gO0KSb5ZrBBl4HHDBuK/WXACH4eO9/CAAAbdvijzLGNE1TVZXfZuHg6XCAQESAZXbOKaXO57eiKG6ft9PrKQIkCQqFoIiQFBGlFIB5nvM8t9aOX2Nd18oDzjnPgCDpn/BH4zh2XZdlWVmWiUK4IgCBoFMUz9eP6zRN75cLgEQhcmTQIbl72O0f9865qLAAsURAAgKBJKEtgLXWvyjLuFsThCSstb8rBCaAQhDYWgIZ7myM+TUBjDHrHlZcbMYYk34cN0YSLcgS+wL0fe9TXDMbY33fR2AYBvyQ8L0Gk8MwREBrTfKe4TpTzwhArXWi8HI84h/1DfwI5mhxJamFAAAAAElFTkSuQmCC ") left top no-repeat;
    }
    
    a.dir {
      background: url("data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAAAGXRFWHRTb2Z0d2FyZQBBZG9iZSBJbWFnZVJlYWR5ccllPAAAAd5JREFUeNqMU79rFUEQ/vbuodFEEkzAImBpkUabFP4ldpaJhZXYm/RiZWsv/hkWFglBUyTIgyAIIfgIRjHv3r39MePM7N3LcbxAFvZ2b2bn22/mm3XMjF+HL3YW7q28YSIw8mBKoBihhhgCsoORot9d3/ywg3YowMXwNde/PzGnk2vn6PitrT+/PGeNaecg4+qNY3D43vy16A5wDDd4Aqg/ngmrjl/GoN0U5V1QquHQG3q+TPDVhVwyBffcmQGJmSVfyZk7R3SngI4JKfwDJ2+05zIg8gbiereTZRHhJ5KCMOwDFLjhoBTn2g0ghagfKeIYJDPFyibJVBtTREwq60SpYvh5++PpwatHsxSm9QRLSQpEVSd7/TYJUb49TX7gztpjjEffnoVw66+Ytovs14Yp7HaKmUXeX9rKUoMoLNW3srqI5fWn8JejrVkK0QcrkFLOgS39yoKUQe292WJ1guUHG8K2o8K00oO1BTvXoW4yasclUTgZYJY9aFNfAThX5CZRmczAV52oAPoupHhWRIUUAOoyUIlYVaAa/VbLbyiZUiyFbjQFNwiZQSGl4IDy9sO5Wrty0QLKhdZPxmgGcDo8ejn+c/6eiK9poz15Kw7Dr/vN/z6W7q++091/AQYA5mZ8GYJ9K0AAAAAASUVORK5CYII= ") left top no-repeat;
    }
    
    a.up {
      background: url("data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAAAGXRFWHRTb2Z0d2FyZQBBZG9iZSBJbWFnZVJlYWR5ccllPAAAAmlJREFUeNpsU0toU0EUPfPysx/tTxuDH9SCWhUDooIbd7oRUUTMouqi2iIoCO6lceHWhegy4EJFinWjrlQUpVm0IIoFpVDEIthm0dpikpf3ZuZ6Z94nrXhhMjM3c8895977BBHB2PznK8WPtDgyWH5q77cPH8PpdXuhpQT4ifR9u5sfJb1bmw6VivahATDrxcRZ2njfoaMv+2j7mLDn93MPiNRMvGbL18L9IpF8h9/TN+EYkMffSiOXJ5+hkD+PdqcLpICWHOHc2CC+LEyA/K+cKQMnlQHJX8wqYG3MAJy88Wa4OLDvEqAEOpJd0LxHIMdHBziowSwVlF8D6QaicK01krw/JynwcKoEwZczewroTvZirlKJs5CqQ5CG8pb57FnJUA0LYCXMX5fibd+p8LWDDemcPZbzQyjvH+Ki1TlIciElA7ghwLKV4kRZstt2sANWRjYTAGzuP2hXZFpJ/GsxgGJ0ox1aoFWsDXyyxqCs26+ydmagFN/rRjymJ1898bzGzmQE0HCZpmk5A0RFIv8Pn0WYPsiu6t/Rsj6PauVTwffTSzGAGZhUG2F06hEc9ibS7OPMNp6ErYFlKavo7MkhmTqCxZ/jwzGA9Hx82H2BZSw1NTN9Gx8ycHkajU/7M+jInsDC7DiaEmo1bNl1AMr9ASFgqVu9MCTIzoGUimXVAnnaN0PdBBDCCYbEtMk6wkpQwIG0sn0PQIUF4GsTwLSIFKNqF6DVrQq+IWVrQDxAYQC/1SsYOI4pOxKZrfifiUSbDUisif7XlpGIPufXd/uvdvZm760M0no1FZcnrzUdjw7au3vu/BVgAFLXeuTxhTXVAAAAAElFTkSuQmCC ") left top no-repeat;
    }
    
    html[dir=rtl] a {
      background-position-x: right;
    }
    
    #listingParsingErrorBox {
      border: 1px solid black;
      background: #fae691;
      padding: 10px;
      display: none;
    }
  </style>
<body>
  <div id="listingParsingErrorBox" i18n-values=".innerHTML:listingParsingErrorBoxText">糟糕！Google Chrome无法解读服务器所发送的数据。请<a href="http://code.google.com/p/chromium/issues/entry">报告错误</a>，并附上<a href="LOCATION">原始列表</a>。</div>
  <span id="parentDirText" style="display:none" i18n-content="parentDirText">[上级目录]</span>
  <h1 id="header" i18n-content="header">C:\dev\ 的索引</h1>
  <table>
    <thead>
      <tr class="header" id="theader">
        <th i18n-content="headerName" onclick="javascript:sortTable(0);">名称</th>
        <th class="detailsColumn" i18n-content="headerSize" onclick="javascript:sortTable(1);">大小</th>
        <th class="detailsColumn" i18n-content="headerDateModified" onclick="javascript:sortTable(2);">修改日期</th>
      </tr>
    </thead>
    <tbody id="tbody">
      <tr>
        <td data-value=".."><a class="icon up" href="#">[上级目录]</a></td>
        <td class="detailsColumn" data-value="0"></td>
        <td class="detailsColumn" data-value="0"></td>
      </tr>
    </tbody>
  </table>
</body>
<script src="/views/jquery.min.js"></script>
<!-- 3、通过浏览器发送一个异步请求到服务器，去请求当前服务器的目录数据 -->
<script>
  $.ajax({
    url: '/getPath',
    type: 'GET',
    dataType: 'json',
    success: function(data){
      // console.log(data);
      // 通过js动态生成html代码
      var str = '';
      for(var i = 0; i < data.length; i ++) {
        str += "<tr>";
        str += '<td data-value="播放器/"><a class="icon dir" href="#">'+ data[i] +'</a></td>';
        str += '<td class="detailsColumn" data-value="0"></td>';
        str += '<td class="detailsColumn" data-value="1489037313">2018/8/11 下午1:28:33</td>';
        str += '</tr>';
      }
      // 将data动态渲染到页面上
      $('#tbody').append(str);
    }
  })
</script>
```

