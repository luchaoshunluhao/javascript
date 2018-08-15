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
//下一行listen方法中第二个参数可以指定自己的IP，也可以不写，不写时在浏览器访问localhost:3000即可
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

> 但是此方法在打开网页后会出现小bug，即文件和目录分不清，图标都会显示文件夹的样子；文件大小和修改时间显示不正确，若要修复bug这需要后面的知识。

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

#### （7）使用fs核心模块来判断路径是否为文件&文件夹

```js
var fs = require('fs');
var str = './01.js';
// 可以使用fs核心模块中的方法来进行判断
// fs.stat用来判断路径的状态
//  path:要判断的路径
//  callback:判断之后的回调函数
//      err:异常信息
//      stats:状态对象（obj）
//          size:大小
//              如果是文件有大小
//              如果是目录，没有大小
//          mtime:内容被修改的时间
fs.stat(str, function(err, stats){
    if(err) {
        return console.log(err.message);
    }
    // console.log(stats);
    if(stats.isFile()) {
        console.log(str + '是文件');
        console.log(stats.size);
    } else {
        console.log(str + '是目录');
    }
});
```

#### （8）仿apach的目录浏览功能-服务器渲染

```js
var http = require('http');
var fs = require('fs');
//下载使用npm下载art-template 第三方包，用来渲染数据到html结构中
var template = require('art-template');
// 创建一个服务器
var server = http.createServer();
// 设置请求事件
server.on('request', function (req, res) {
    // 如果读取根目录，并数据 + html结构响应回去
    var url = req.url;
    // 判断
    if (url === '/') {
        // 得到html结构
        //  readFile读取出来 的内容是十六进制的buffer数组
        fs.readFile('./views/index.html', function (err, data) {
            if (err) {
                return console.log(err.message);
            }
            // res.end(data);
            // 得到数据
            fs.readdir('./', function (err1, files) {
                if (err1) {
                    return console.log(err1.message);
                }
                // 区分文件和文件夹
                var fileArr = [];
                var dirArr = [];
                var count = 0;
                for (var i = 0; i < files.length; i++) {
                    (function (i) {
                        fs.stat(files[i], function (err2, stat) {
                            count ++;
                            if (err2) {
                                return console.log(err2.message);
                            }
                            if (stat.isFile()) {
                                fileArr.push({
                                    name: files[i],
                                    type: 'file',
                                    size: stat.size,
                                    time: stat.mtime
                                });
                            } else {
                                dirArr.push({
                                    name: files[i],
                                    type: 'dir',
                                    size: stat.size,
                                    time: stat.mtime
                                });
                            }
                            if (count === files.length) {
                                var newArr = dirArr.concat(fileArr);
                                // newArr 就是我们要的数据对象
                                // 将数据与结构结合
                                // 数据: newArr [{name: ,type:'',size:'',time:''}]
                                // 结构：data
                                // 问题：如何装饰数据与结构结合：
                                //    找第三方包：art-template可以用来帮助我们完成这个操作
                                var htmlStr = template.render(data.toString(), {
                                    newArr: newArr
                                });
                                res.end(htmlStr);
                            }
                        });
                    })(i);
                }
            })
        });
    }
})
// 开启服务器
server.listen(3000, function () {
    console.log('running');
});
```

### 3、 Node中的模块系统

#### （1）什么是模块?

- 随着项目的推进、逻辑的复杂,不可能把所有js代码都写在一个文件中
- **一个js文件就是一个具有独立功能的模块**
- Node中按照模块去划分功能,有一套模块加载机制:
  - module.exports导出模块成员
  - require()导入模块成员

#### （2）导入模块(require方法)

- **作用**：加载并执行模块中的代码!!!!

- **使用**：`require()` 方法的()中可以写:

  ```js
  // 1. node自带的模块,如fs、http
  require('fs');
  // 2. 通过路径引入的自己的js文件
  require('./foo.js');
  ```
  > 注意事项

  ① `require()` 加载模块是**同步**加载!!

  ② 引入自己的js文件时,路径中的./或者../**不能省略**

  ③ 如果省略,`require()` 会把它当成是一个node自带的模块

  报错信息不要害怕!!!一定要去看!!!

  ④ 模块后缀`.js` **可以省略不写**

#### （3）导出模块

模块中定义的变量是**局部**的, 

那如何在A模块使用B模块中定义好的变量呢?

这个问题, 就涉及到了模块加载机制

##### 导出模块中的变量

- 每个模块中都有一个 `module` 对象
- `module `对象中有一个` exports `对象
- 在CommonJS 中规定：一个模块返回数据可以通过module.exports和rexports两个关键字来返回
- 模块最终返回的仅仅只是 modules.exports
- exports 仅仅只是 modules.exports的一个引用
- 我们可以把需要导出的成员都挂载到` module.exports ` 对象上

```
验证module.exports与exports的关系：
	1）console.log(module.exports === exports);
	2）exports.a = 123;
	3）exports = fucntion() {}
	4）exports = modules.exports =  fucntion() {}
```

**导入模块`foo.js` **

```js
var a = 10;
var b = 20;
function add(){};

module.exports.a = a;
module.exports.b = b;
module.exports.add = add;

// 可以理解为在模块的末尾有这样一句代码: return module.exports;
// return module.exports;
```

##### 导入模块`main.js` 

```js
// 1 导入模块
var foo = require('./foo.js');
// 2 使用模块中的成员                  
console.log(foo.add);
console.log(foo.a);
```

#### （4）模块加载机制

- require关键字：

  - 可以帮助一个模块加载另一个模块

- 优先从缓存中加载

  - Node 加载模块时，如果这个模块已经被加载过了，则会直接缓存起来，将来再次引用时不会再次加加载这个模块（即：如果一个模块被加载两次，则模块中的代码只会被执行一次）
  - 加载模块本质上是加载模块中的modules.exports值

- 核心模块

  - 先去缓存中看下是否存在，如果有，直接拿来使用
  - 如果没有，则加载

- 自定义模块

  - 以 './' 或者 '../' 或者 'c:/xxx' 类似于这样的标识路径作为加载名

- 第三方模块：包

  - 先在当前文件的模块所属目录去找 node_modules目录
  - 如果找到，则去该目录中找 moment 目录
  - 如果找到 moment 目录， 则找该目录中的 package.json文件
  - 如果找到 package.json 文件，则找该文件中的 main属性
  - 如果找到main 属性，则拿到该属性对应的文件
  - 如果找到 moment 目录之后，
    - 没有package.json
    - 或者有 package.json 没有 main 属性
    - 或者有 main 属性，但是指向的路径不存在 
    - 则 node 会默认去看一下 moment 目录中有没有 index.js ,index.node, index.json 文件
  - 如果找不到index 或者 找不到 moment 或者找不到 node_modules 
  - 则进入上一级目录找 node_moudles 查找（规则同上）
  - 如果上一级还找不到，继续向上，一直到当前文件所属磁盘的根目录
  - 如果到磁盘概目录还没有找到，直接报错

  ```
  核心模块：
  	由 Node 本身提供，通过唯一的模块标识名进行加载
  	核心模块本质上也是文件模块，它已经被编译到可执行文件中了
  第三方模块
  用户自定义模块
  ```

- 模块的兼容处理
  - 有些模块即能在浏览器端使用，又能在服务器端使用，是因为它们作了兼容处理（如：moment）

#### （5）模块分类及第三方模块(包)的使用

- 核心模块
  - 由 `Node` 本身提供，例如` fs` 、`http` 等
- 自定义(用户)模块
  - 自己写的.js文件，按照路径来加载，注意 `./` 或者 `../` 不能省略
- 第三方模块
  1. 在[npm网站](https://www.npmjs.com/)找包(模块) 
  2. 打开cmd, 使用命令 `npm install 包名` 安装包
  3. 在需要使用的位置, 通过`require('第三方包名') ` 加载包
  4. 看文档调用 API

### 4、art-template 第三方包

#### （1）使用art-template

```js
// 1、遍历对象
// var template = require('art-template');
// // 有html结构
// var str = '<ul><li><%=name%></li><li>{{age}}</li></ul>';
// // 也有数据
// var obj = {
//     name: '张三',
//     age: 18
// };
// // 结合
// //  render可以结合html结构和数据
// //      str:结构
// //      obj：数据
// var htmlStr = template.render(str, obj);
// console.log(htmlStr);

// 2、遍历数组
var template = require('art-template');
// 准备结构
var str = '<ul>{{each arr}}<li>{{$index}}----{{$value.name}}----{{$value.age}}</li>{{/each}}</ul>';
// 数据
var arr = [
    {name: '张三', age: 18},
    {name: '李四', age: 30}
]
// 结合
var htmlStr = template.render(str, {
    arr: arr
});
console.log(htmlStr);

//需要结合
//  art-template的使用步骤：
//  1、下载
//  2、在html结构中书写art-template的语法
//      输出：
//          {{name}}
//      条件：
//          {{if 条件}} ... {{else if 条件}}... {{else}}
//      循环
//          {{each 数据}} {{$index}} {{$value}}  {{/each}}
//  3、通过nodejs代码将结构与数据结合起来
```

#### （2）使用url核心模块来将参数转为对象

```js
// url核心模块可以帮助我们将路径后面的参数得到
//  url: http://192.168.11.1:8080/abc/index.html?name=abc&age=18

// 引用
var url = require('url');
// pase路径
var strUrl = 'http://192.168.11.1:8080/abc/index.html?name=abc&age=18';
var urlObj = url.parse(strUrl, true);
console.log(urlObj);
```

### 5、npm包管理器

#### （1） [npm](https://www.npmjs.com/) 是什么

- npm 全称  `Node Package Manager`，它的诞生是为了解决 Node 中第三方包共享的问题。 和浏览器一样，由于都是 JavaScript，所以前端开发也使用 npm 作为第三方包管理工具。 例如大名鼎鼎的 jQuery、Bootstrap 等都可以通过 npm 来安装。 所以官方把 npm 定义为  `JavaScript Package Manager`。

- > yarn也是包管理器

#### （2）npm 命令行工具

- 只要你安装了 node 就已经安装了 npm,可以在cmd中进行npm的指令操作

  ```bash
  // 检验npm是否安装成功
  npm --version
  ```

- 常用命令

  ```cmd
  // 在项目中初始化一个 package.json 文件,凡是使用 npm 来管理的项目都会有这么一个文件
  // 只敲一次就可以!
  npm init   
  
  // 跳过向导，快速生成 package.json 文件,简写是npm init -y
  npm init --yes
  
  // 一次性安装 dependencies 中所有的依赖项,简写是 npm i
  npm install
  
  // 安装指定的包，可以简写为 npm i 包名
  // npm 5 以前只下载，不保存依赖信息，如果需要保存，则需要加上 --save 选项
  // npm 5 以后就可以省略 --save 选项了
  npm install 包名
  
  // 一次性安装多个指定包
  npm install 包名 包名 包名 ...
  
  // 安装指定版本的包!!!
  npm install jquery@版本号
  // 如果不指定版本号,默认安装最新稳定版本
  
  // 卸载指定的包
  npm uninstall 包名
  
  // 查看使用帮助
  npm help
  
  // 查看某个命令的使用帮助
  // 例如我忘记了 uninstall 命令的简写了，这个时候，可以输入 npm uninstall --help 来查看使用帮助
  npm 命令 --help
  ```

#### （3）package.json

- 我们的项目会放到云端的仓库中，例如 github ，第三方包没有上传的意义，我们只需要把我们的源码放到云端仓库，`node_modules` 目录中存储的就是第三方包（不用担心丢失问题），如果没有 `package.json` 文件则你就找不回来了。

- 建议每一个项目都要有一个  `package.json`  文件（包描述文件，就像产品的说明书一样），给人踏实的感觉最重要的就是保存这个项目的第三方依赖信息（因为我们不需要提交第三方包到我们的云端仓库，只需要提交我们自己的代码），有了这个文件中的依赖信息结合  `npm install`  命令我们就可以放心了。

- 这个文件可以通过 `npm init` 的方式来自动初始化出来。

  ```cmd
  npm init
  ```

- 对于咱们目前来讲，最有用的是那个 `dependencies` 选项，可以用来帮我们保存第三方包的依赖信息。

- 如果你的 `node_modules` 删除了也不用担心，我们只需要：`npm install` 就会自动把 `package.json` 中的 `dependencies` 中所有的依赖项都下载回来。

- 建议每个项目的根目录下都有一个 `package.json` 文件

  - 不同的项目有不同依赖，各自保存各自的

- 执行 npm install 包名的的时候可以加上--save

  ```
  --save
  ```

  这个选项，目的是用来保存依赖项信息

  - npm 5 以前不会自动保存依赖信息到 package.json 文件中，必须手动加 `--save` 选项才可以
  - npm 5 以后不需要加 `--save` 选项了，因为它会自动保存依赖项

#### （4） package-lock.json

- npm 5 以前是不会有 `package-lock.json` 这个文件的。
- 当你安装包的时候，npm 都会生成或者更新 `package-lock.json` 这个文件。
- npm 5 以后的版本安装包不需要加 `--save` 参数，它会自动保存依赖信息
- 当你安装包的时候，会自动创建或者是更新 `package-lock.json` 这个文件
- `package-lock.json`  这个文件会保存  `node_modules`  中所有包的信息（版本、下载地址）
  - 这样的话重新 `npm install` 的时候速度就可以提升

