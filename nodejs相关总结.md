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

##### 导入模块`foo.js` 

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

## 三、ECMAScript 6 

一般情况下不建议在window环境下面使用ES6

### 1、 严格模式

```javascript
	'use strict'
```

- 如果开启了严格模式，变量不能直接使用，必须先申明，申明变量时一定要用var / let
- 更多介绍：http://www.ruanyifeng.com/blog/2013/01/javascript_strict_mode.html

### 2、 申明一个变量(let)

- let 申明的变量不存在变量提升 

  ```js
      //console.log(a); // undefined
      //var a = 123;
      //console.log(a); // 123
      //等同于
      var a;
      console.log(a);
      a = 123;
      console.log(a);
      console.log(a);
      let a = 123;
      console.log(a);
  ```

  

- let 申明的变量不允许重复声明

  ```js
      var a = 123;
      var a = 456;
      console.log(a);
      let a = 123;
      let a = 456;
      console.log(a);
  ```

- let 申明的变量存在块级作用域

  - 可以用来解决闭包问题

  ```js
      // 块级作用域：来自于后台
      //  特点：凡是大括号包裹的部分都是一个单独的作用域，我们把这个作用域叫做块级作用域， 块级作用域之间不会相互影响
      if (true) {
          let a = 123;
          console.log(a);
      } 
      // if (true) {
      //     console.log(a);
      // }
      console.log(a);
  ```

  

### 3、 申明一个常量 (const)

- contst申明的常量：一旦设置无法修改

  - 可以改变对象中的属性

- contst申明的常量：一旦设置不可重复声明

  ```js
      // const a = 123;
      // a = 456;
      // console.log(a);
      // 值类型（简单类型）
      //  简单类型的常量一旦设置无法修改
      // 引用类型（复杂类型）
      //  一旦赋值只要不是改变引用还是可以修改的
      const obj = {
          name: "张三"   
      }
      // 修改引用类型的引用地址
      // obj = {};// 如果修改引用地址会报错
      obj.name = "李四";// 修改的是地址中对应对象的属性：
  
      console.log(obj);
  ```

### 4、 字符串的一些扩展方法的使用

- includes() ：返回布尔值，表示是否找到了参数字符串

- startsWith() ：返回布尔值，表示是否找到了参数字符串

- endsWith() ：返回布尔值，表示参数字符串是否在源字符串的尾部

- repeat()：返回一个新字符串，表示将原字符串重复n次

  ```javascript
      var s = "hello world";
      s.startsWith('hello') //true
      s.startsWith('world', 6) //true   ，表示从第6个开始后面的字符是 world
      s.endWith('hello', 5) //true ，表示前5个字符是hello
      'x'.repeat(2)  // “xx”
      'hello'.repeat(2)  // “hellohello”
      'ivan'.repeat(0)  // “”
  ```

### 5、 模板字符串

- 使用“`”来定义模板字符串

- 在模板字符串中可以保持变量的结构，可以识别换行

- 在模板字符串中可以直接使用js代码格式：${ code }

  ```js
      var obj = {
          name: '张三',
          age: 18
      }
      // var a = '<ul><li>' + obj.name + '</li><li>' + obj.age + '</li></ul>';
      // console.log(a);
  
      // 模板字符串：
      //  1.0 拼接字符：输出变量
      // var a = `<ul><li> ${obj.name} </li><li> ${obj.age} </li></ul>`;
      // console.log(a);
      //  2.0 识别换行
      var a = `<ul>
          <li>${obj.name}</li> 
          <li>${obj.age}</li>
      </ul>`;
      console.log(a);
  ```

### 6、 解构赋值

#### （1） 字符串的解构赋值

- var [a,b,c] = 'xyz';

```
    const [a, b, c, d, e] = 'hello';
    a // "h"
    b // "e"
    c // "l"
    d // "l"
    e // "o"
```

#### （2）对象解构

- var {name, age} = {name: 'zs', age: 18}
- 给对象属性设置别名
  - var {name: myName, age} = {name: 'zs', age: 18}
- 属性设置默认值(如果对旬中有这个属性，并且值不为undefined，那么这个属性的值为对象中
  - var {name='ls', age} = {name: 'zs', age: 18}的值，如果不存在或者是值为undefined,那么值为：默认值)

```js
    var obj = {
      name: '张三',
      age: 18
    }
    var {name, age} = obj;
    name // 张三
    age  // 18		
```

- 无顺序问题

#### （3） 数组的解构

- var [x,y,z] = [1,2,3];

```
    var arr = ['a', 'b', 'c']
    var [x, y, z] = arr;
    x // 'a'
    y // 'b'
    z // 'c'
```

- 有顺序问题
- 被赋值的变量和数组中的元素个数可以不相等

#### （4）其它特点

- 可以指定默认值
- 解构出来的元素不一定要与前面的对象一一对应
- 可以给解构出来的元素设置别名

### 7、 箭头函数的推演

- 作用：在nodejs中我们大量使用了回调函数,每次回调函数都用匿名函数来实现,ES6中为了能够让我们书写匿名函数速度加快，就提出了箭头函数，用来简化匿名函数

  ```
      写法1: arr.sort(function(x, y){return x - y ;});
      写法2：arr.sort((x, y) => {return x - y ;});
      写法3：arr.sort((x, y) => x - y);
  ```

- 箭头函数的其它写法

  ```
      如果参数只有一个，可以将()省略    // arr.map(c => c + 1);
      如果没有参数，则一定能要写上()     // ()=> console.log(‘a’)
      如果多于一个参数，每个参数之间用逗号分隔   (x, y) => { ... }
      如果方法体只有一句代码，可以省略{} 和分号，如果有返回可以省略return
      如果方法体多于一句代码，则不能省略{} ,每句代码使用 分号分隔
  ```

- 箭头函数的一些特点

  - 箭头函数没有自己的this，函数体内部写的this，指向的是外层代码块的this

    ```js
        //匿名函数
        var obj = {
            name: '张三',
            age: 18,
            sayHi: function(){
                console.log(`大家好，我叫${this.name},今年${this.age}岁了`);
            }
        }
        obj.sayHi();
        // 箭头函数
        this.name = '李四';
        this.age = 20;
        // window
        var obj = {
            name: '张三',
            age: 18,
            sayHi: () => {// => goes to
                console.log(`大家好，我叫${this.name},今年${this.age}岁了`);
            }
        }
        obj.sayHi();
    ```

  - 箭头函数内部的this是定义时所在的对象，而不是使用时所在的对象并且不会改变

    ```js
        // 匿名函数
        var obj = {
            name: '张三',
            age: 18,
            sayHi: function(){
                console.log(`大家好，我叫${this.name},今年${this.age}岁了`);
            }
        }
        var newObj = {
            name: '李四',
            age: 40
        }
        // 可以通过apply和call动态改变this的指向
        obj.sayHi.apply(newObj);
        // 箭头函数
        this.name = '李四';
        this.age = 30;
        var obj = {
            name: '张三',
            age: 18,
            sayHi: ()=>{
                console.log(`大家好，我叫${this.name},今年${this.age}岁了`);
            }
        }
        var newObj = {
            name: '范冰冰',
            age: 40
        }
        // 函数在定义时this指向的是obj上一层中的this name = '王五'
        // obj.sayHi();
        // 可以通过apply和call动态改变this的指向
        // 调用时使用newObj来调用，并没有改变this的指向
        obj.sayHi.apply(newObj);
    ```

  - 箭头箭头函数不能用作构造函数

    ```js
        // 普通构造函数
        var GirlFirend = function(name, age){
            this.name = name;
            this.age = age;
        }
        var g1 = new GirlFirend('张三', 30);
        console.log(g1.name, g1.age);
    
        var GirlFirend = (name, age) => {
            this.name = name;
            this.age = age;
        }
        var g2 = new GirlFirend('李四', 39);
        console.log(g2.name, g2.age);
    ```

  - 箭头函数内部不存在arguments，箭头函数体中使用的arguments其实指向的是外层函数的arguments

    ```js
        //  什么是arguments：函数在使用时的实参
        // // 普通函数
        // var fn = function () {
        //     // 将所有的传入的实参打印出来
        //     console.log('-----fn-------');
        //     console.log(arguments);
        //     console.log('-----fn-------');
        //     return function () {
        //         console.log('-----fn1-------');
        //         console.log(arguments);
        //         console.log('-----fn1-------');
        //     }
        // }
        // var fn1 = fn(1, 2, 3, 4, 5, 6, 7, 8, 9, 0);
        // fn1(1, 2, 3, 4, 5);
        // // fn 1,2,3,4,5,6,7,8,9,0
        // // fn1 1,2,3,4,5
        // 箭头函数
        var fn = function () {
            // 将所有的传入的实参打印出来
            console.log('-----fn-------');
            console.log(arguments);
            console.log('-----fn-------');
            return  () => {
                console.log('-----fn1-------');
                console.log(arguments);
                console.log('-----fn1-------');
            }
        }
        var fn1 = fn(1,2,3,4,5,6,7,8,9,0);
        fn1(1,2,3,4,5);
    ```

### 8、 对象中属性的简写

```js
    //es5中对象： {add:add, substrict:substrict}
    //es6中对象： {add, substrict}  注意这种写法的属性名称和值变量是同一个名称才可以简写，否则要想es5那样的写法,例如： {addFun:add}
    var name = '李四';
    var age = 20;
    // ES6之前
    var obj = {
        name: name,
        age: age
    }
    //ES6之后
    var obj = {
        name,
        age
    }
    console.log(obj.name, obj.age);
```

### 9、 对象中方法的简写

```js
    //es5中对象： {add:function(){}, substrict:function(){}}
    //es6中对象： {add(){}, substrict(){}}
    //ES6之前
    var obj = {
        name,
        age,
        sayHi: function(){
            console.log(`大家好，我叫${this.name}, 今年${this.age}岁了`);
        }
    }
    // ES6之后
    var obj = {
        name,
        age,
        sayHi(){
            console.log(`大家好，我叫${this.name}, 今年${this.age}岁了`);
        }
    }
    obj.sayHi();
```

### 10、promise

- 含义：承诺（答应去做，但是还没有做）

- 来由：ES6之前是没有promise的，这个玩意是由前端社区提出，在ES6中成为一个标准

- 作用：它是用来简化回调函数的多层嵌套

- 使用：

  ```
    1)要使用promise必须先根据promise构造函数创建一个函数对象
        在promise的构造函数中有两个参数：resolve  reject    这两个参数是两个函数
            这两个参数是与promise中的状态对应：
                pending（进行中）
                fulfilled（已成功）
                rejected（已失败）
            状态的切换有两种方式：
                pending---->fulfilled 操作成功   --->会执行resolve中的方法
                pending---->rejected 操作失败    --->会执行reject中的方法
        在使用promise的时候可以在后面接无数个then方法，then方法可以传递参数
            参数一般分为三种类型：
                1）undefined
                2）普通数据：字符串，数字，boolean,数组，对象
                3）promise对象
    2)使用then方法执行promise
    3)在promise中提供一个统一处理错误的方法：catch
  ```

  - 创建一个promise 对象

    ```
        var p = new Promise(function(resolve, reject){
            if () {
                // 如果成功执行reject
            } else{
                // 如果失败执行resolve
            }
        });
    ```

    - resolve： 成功后执行
    - reject: 失败后执行 

    执行promise的代码：使用p.then()方法执行

    - then(resolve, reject ) 方法可以执行promise的代码
      - 特点：可以无限调用then方法
    - 统一处理捕获异常的方法： catch()

  - then方法返回值：

    - 每个then方法执行完成以后，会将返回值交给下一个then方法，如果没有返回值，其实返回的是undefined
    - 没有返回值
      - 如果没有返回值，返回值为undefined
    - 返回值为：数字，字符串，对象，数组....
      - 下面的then方法可以直接通过resolve方法的参数接收到
    - 返回值为一个新的promise对象：
      - 将来下面紧跟的then方法其实是执行上面返回的promise对象的then方法            

```js
    // 需求：依次将三个文件中的内容读取出来并且输出： 0 ~ 1 ~ 2
    var fs = require('fs');
    // 读取0文件
    fs.readFile('./file/0.txt', function (err0, data0) {
        if (err0) {
            return console.log(err0.message);
        }
        console.log(data0.toString());
        // 读取1文件
        fs.readFile('./file/1.txt', function (err1, data1) {
            if (err1) {
                return console.log(err1.message);
            }
            console.log(data1.toString());
            // 读取2文件
            fs.readFile('./file/2.txt', function (err2, data2) {     
                if (err2) {
                    return console.log(err2.message);
                }
                console.log(data2.toString());
            });
        });
    });
    // 回调地狱
```

使用promise解决回调地狱

```js
    // var p = new Promise(function(reject, resolve){
    //     if () {
    //         // 如果成功执行reject
    //     } else{
    //         // 如果失败执行resolve
    //     }
    // });

    // // 需求：依次将三个文件中的内容读取出来并且输出： 0 ~ 1 ~ 2
    // 创建一个promise对象读取0文件
    var fs = require('fs');
    // 一旦Promise被创建：
    //      promise的状态为： pending 等待
    //      promise执行以后，状态会发生改变
    //          pending -- fulfilled 说明执行成功  执行resolve方法
    //          pending -- rejected 说明执行失败  执行reject
    //          一旦对应的状态确定，就无法改变
    var p0 = new Promise(function (resolve, reject) {
        fs.readFile('./file/0.txt', function (err, data) {
            if (err) {
                reject(err);
            } else {
                resolve(data);
            }
        });
    });
    // 读取1文件
    var p1 = new Promise(function (resolve, reject) {
        fs.readFile('./file/1.txt', function (err, data) {
            if (err) {
                reject(err);
            } else {
                resolve(data);
            }
        });
    });
    // 调用：than
    p0
        .then(data => {
            console.log(data.toString());
            // 不返回值任何内容：返回值 为undefined
        })
        .then((res) => {
            console.log(res); // undeinfed
            console.log('第二个then方法'); 
            // 返回值为非promise对象
            return 'abc';
        })
        .then((str) => {
            console.log(str);// abc
            console.log('第三个then方法');
            // 返回值为promise对象
            return p1;
        })
        .then((data) => {
            console.log(data.toString());
            console.log('第四个then方法');
        });
```

## 四、Express

- 作者：https://github.com/tj
- Github：https://github.com/expressjs/express
- 官网：http://expressjs.com/
- 中文翻译：http://www.expressjs.com.cn/
- awesome-express: https://github.com/wabg/awesome-express

### 1、起步

安装：

```bash
	npm install --save express
```

hello world：

```js
    // 引入express第三方包
    var express = require('express')
    // 创建一个express对象（express用来搭建web服务：相当于创建一了个服务器对象）
    var app = express()

    // 将来浏览器发送get请求，请求网站的根目录，会执行后面的回调函数
    //  回调函数有两个参数：
    //      req:请求对象
    //      res:响应对象
    app.get('/', function (req, res) {
      res.send('Hello World!')
    })

    // 开启监听：监听3000商品，
    // 当开启成功以后会执行后面的回调函数
    app.listen(3000, function () {
      console.log('Example app listening on port 3000!')
    })
```

基本路由：

```js
    app.get('/', function (req, res) {
      res.send('Hello World!')
    })

    app.post('/', function (req, res) {
      res.send('Got a POST request')
    })

    app.put('/user', function (req, res) {
      res.send('Got a PUT request at /user')
    })

    app.delete('/user', function (req, res) {
      res.send('Got a DELETE request at /user')
    })
```

### 2、Express 中外置路由使用

router.js 文件代码如下:

```js
    // 1. 加载外置路由 express 模块
    var express = require('express')

    // 2. 调用 express.Router() 方法，得到一个路由容器实例
    var router = express.Router()

    // 3. 为 router 添加不同的路由
    router.get('/', function (req, res) {
      res.send('hello express')
    })

    router.get('/add', function (req, res) {
      res.send('add')
    })

    // 4. 将 router 路由容器导出（路由对象暴露给外界）
    module.exports = router
```

在 app.js 文件中：

```js
    // 使用express搭建服务
    var express = require('express')

    // 1. 加载路由模块
    var router = require('./router')

    var app = express()

    // 2. 将路由模块导出的路由容器 router 通过 app.use() 方法挂载到 app 实例上
    //    这样的话 app 实例程序就拥有了 router 的路由了
    app.use(router)

    // 把所有的路由添加到一个新的文件中（外置路由）

    // 开启监听
    app.listen(3000, function () {
      console.log('running...')
    })
```

### 3、res.render方法

- 使用：
  - 1.0 下载一个第三方包express-art-template(art-template)
  - 2.0 将这个第三方包注册到express中：
    - app.engine('html', require('express-art-template'));
  - 3.0 可以直接使用render方法了
  - 注意点：
    - 1.0 render方法渲染的静态文件默认会去views文件夹下去找，所以存放静态文件的文件夹，一定要取名叫做views
    - 2.0 默认情况下render渲染的静态文件后缀为art,但是在注册art-template时可以修改为html
- 注意点：
  - res中虽然已经有了render方法但是不能够直接使用，它需要配合一些第三方包来进行使用（art-template的来使用）

index.js

```js
    // res.render方法用来渲染html文件的
    var express = require('express');

    var app = express();
    // 注册 art-template
    app.engine('html', require('express-art-template'));

    // 注册路由
    app.get('/', (req,res) => {
        // 将静态页面响应回浏览器
        // 特点：它在渲染的时候会去一个固定的路径下面去找对应的art文件
        res.render('index.html', {
            name: '张三',
            age: 18
        });
    })

    app.listen(3000, () => {
        console.log('running');
    });
```

index.html

```html
    <body>
        <ul>
            <li>{{name}}</li>
            <li>{{age}}</li>
        </ul>
    </body>
```

### 4、在 Express 中处理静态资源

- 默认情况下express没有帮助我们处理静态文件，如果要处理静态文件，我们需要在express中进行设置
- 设置：
  - 访问是不带路径
    - app.use(express.static('public'))
      - public 是静态文件存放的位置
  - 按照原路径来访问
    - app.use('/imgs', express.static('public'))
    - 在访问时必须带上/imgs才能访问到图片
  - 访问的路径自己来设置
    - app.use('/abc', express.static('public'))

```js
    app.use(express.static('public'))
    app.use(express.static('files'))

    app.use('/public', express.static('public'))
    app.use('/aaa', express.static('public'))

    app.use('/static', express.static(path.join(__dirname, 'public')))
```

index.js

```js
    // 引入express第三方包
    var express = require('express');
    // 创建一个express对象（express用来搭建web服务：相当于创建一了个服务器对象）
    var app = express();

    // 设置静态文件的路径
    // app.use(express.static('imgs')); // 设置完成以后，将来可以访问imgs中的静态文件
    // app.use('/imgs', express.static('imgs'));
    app.use('/abc', express.static('imgs'));


    // 注册模板引擎
    app.engine('html', require('express-art-template'));

    // 渲染静态文件
    app.get('/', function (req, res) {
        res.render('index.html');
    });

    app.listen(3000, function () {
        console.log('running');
    });
```

index.html

```html
    <body>
        <img src="/abc/4.jpg" alt="">
    </body>
```

### 5、express 的中间件

- 什么是中间件：

  - 在express已有的结构上再加入一些自己的代码

- 参数：

  - req:请求报文对象
  - res:响应报文对象
  - next:函数，如果调用这个函数才会继续的执行后续的流程代码

- 应用中间件

  - app.use()
    - app.use(function(){}) 
      - 无论发送任何请求都会执行的中间件
    - app.use('/path', function(){})
      - 只要在请求path路由时才会执行的中间件（无论GET/POST）
  - app.method()
    - app.get()
      - 在get请求时会执行的中间件
    - app.post()
      - 在post请求时会执行的中间件

  ```js
      var express = require('express');
      var app = express();
  
      // 1、app.use 中间件
      //    特点：由于在设置的时候没有加上任何参数，所以在这里任意请求过来都会执行这个中间件
      app.use(function(req, res, next){
          console.log('我是app.use');
          // 调用next执行后续的逻辑代码
          next();
      });
  
      // 2、app.use 的变形
      //     特点：只要在请求/add的时候才会执行的中间件(不管是GET/POST)
      app.use('/add', function(req, res, next){
          console.log('我是app.use /add');
          next();
      });
  
      // 3、app.METHOD  = GET / POST
      //  （1）app.get 在express中其实路由就是一种中间件
      app.get('/add', function(req, res, next){
          console.log('我是中间件app.get /add');
          next();
      })
      //  （2）app.post
      app.post('/add', function(req, res, next){
          console.log('我是中间件app.post /add');
          next();
      });
  
      app.get('/', function(req, res){
          console.log('根目录');
      });
  
      // 设置的路由
      app.get('/add', function(req, res){
          console.log('add');
      });
  
      app.post('/add', function(req, res){
          console.log('add');
      });
  
      app.get('/del', function(req, res){
          console.log('del');
      });
  
      app.listen(3000, function() {
          console.log('running');
      });
  ```

- 路由级中间件

  - 它的用法与应用级中间件完全一样，唯一的区别是
    - 应用级中间件的中间件是挂载在app对象上
    - 路由级中间件的中间件是挂载在router对象上的

  app.js

  ```js
      // 开户服务器
      var express = require('express');
      var router = require('./router');
      var app = express();
  
      //使用外置路由
      app.use(router);
  
      app.listen(3000, () => {
          console.log('running');
      });
  ```

  router.js

  ```js
      var express = require('express');
      var router = express.Router();
  
      router.use(function(req, res, next){
          console.log('router.use');
          next();
      });
      router.use('/add', function(req, res, next){
          console.log('router.use /add');
          next();
      });
      router.get('/add', function(req, res, next){
          console.log('router.get /add');
          next();
      });
  
      router.get('/', function(req, res){
          console.log('根目录');
      });
      router.get('/add', function(req,res){
          console.log('get/add');
      });
  
      // 暴露到外界
      module.exports = router;
  ```

- 错误处理中间件

  - 可以用来处理网站发生的所有错误

  ```js
      var express = require('express');
      var fs = require('fs');
      var app = express();
  
      app.get('/', function(req, res){
          console.log('根目录');
      });
  
      app.get('/add', function(req, res){
          // 会报错
          res.render('add.html');
      });
  
      // 统一错误处理的中间件
      app.use((err, req, res, next) => {
          // console.log("err:" + err.message);
          fs.readFile('./404.html', (err, data) => {
              res.end(data);
          });
      });
  
      app.listen(3000, function() {
          console.log('running');
      });
  ```

- 内置中间件（静态资源处理）

  - express.static(root,option)

## 五、使用nodejs来操作数据库

### 1、连接数据库

```js
    // 使用nodejs来链接mysql
    // 1、引包
    var mySql = require('mysql');
    // 2、设置连接参数
    var connection = mySql.createConnection({
        host: 'localhost',
        user: 'root',
        password: '123456',
        database: 'class_one'
    });
    // 3、开启连接
    connection.connect();
    // 4、执行sql语句
    var strSql = 'SELECT * FROM person';
    connection.query(strSql, (err, result, fields) => {
        if (err) {
           return console.log(err.message);
        }
        console.log(result);
        // [ RowDataPacket { id: 1, name: '张三', age: 18, gender: '男' },
        // RowDataPacket { id: 3, name: '王五', age: 22, gender: '男' } ]
        console.log(fields);
        // 存储的是表中字段的信息
    });


```

### 2、增删改查

```js
    // 引包
    var mysql = require('mysql');
    // 建立连接
    var connection = mysql.createConnection({
        host: 'localhost',
        user: 'root',
        password: '123456',
        database: 'class_one'
    });
    // 开启连接
    connection.connect();
    // 执行sql说到语句
    // 查询
    //      result: 就是数据表中的数据
    //      fields: 数据表中的字段的属性说明
    var strSql = 'SELECT * FROM person';
    // 新增
    //      result: OkPacket对象，这是一个成功对象，说明对数据库的操作成功了
    //          affactedRows: 受影响的行数
    //      fields: undeinfed
    var strSql = 'INSERT INTO person (name, age, gender) VALUES ("赵六", "33", "男")';
    // 修改
    //      result: OkPacket对象，这是一个成功对象，说明对数据库的操作成功了
    //          affactedRows: 受影响的行数
    //      fields: undeinfed
    var strSql = 'UPDATE person SET name="无情", age="80" WHERE id = 1'
    // 删除
    //      result: OkPacket对象，这是一个成功对象，说明对数据库的操作成功了
    //          affactedRows: 受影响的行数
    //      fields: undeinfed
    var strSql = 'DELETE FROM person WHERE id = 5'
    connection.query(strSql, (err, result, fields) => {
        if (err) {
            return console.log(err.message);
        }
        console.log(result);
        console.log(fields);
    });
```



## 六、cookie和session

### 1、cookie

- nodejs 中设置cookie
  - res.wirteHead(200, {'set-cookie', 'uName=admin'});
- 如果要设置硬盘cookie可以使用第三方中间件express: cookie
  - 可以通过这个中间件来操作cookie
    - 设置过期时间
    - 设置起效果的域名
    - 。。。

server.js（服务器）

```js
    var fs = require('fs');
    var express = require('express');
    var bodyParser = require('body-parser')
    var app = express();



    app.use(bodyParser.urlencoded({ extended: false }))
    app.use(bodyParser.json())

    // 设置静态文件
    app.use('/node_modules', express.static('node_modules'));

    // 1.0 设置路由
    // 设置一个首页
    app.get('/', function(req, res){
        // 请求头会带上一个cookie
        // console.log(req.headers.cookie);
        // 验证用户是否登录：只要判断请求头中是否带有cookie
        if (req.headers.cookie === "uName=admin") {
            // 说明登录过：
            res.send('用户已经登录过了，直接访问根上当');
        } else{
            res.send('<script>alert("用户还没有登录");window.location="/login"</script>');
        }
    });

    // 得到登录页面
    app.get('/login', function(req, res){
        fs.readFile('./views/login.html', function(err, data){
            res.end(data);
        });
    });

    // 完成提交数据的逻辑
    app.post('/login', function(req, res){
        // body-parser
        var uName = req.body.uName;
        var pwd = req.body.pwd;
        // 判断
        if (uName === "admin" && pwd === "888") {
            // 要将用户的登录信息保存起来：用cookie来保存
            // 向响应报文头中加入一段内容：cookie
            res.writeHead(200, {
                'set-cookie': 'uName=' + uName
            });
            // 登录成功
            // res.json({
            //     status: 200,
            //     msg: '成功'
            // });
            res.end(JSON.stringify({
                status: 200,
                msg: '成功'
            }));
        } else{
            // 登录失败
            res.json({
                status: 500,
                msg: '不成功'
            });
        }
    });
    app.listen(3000, function() {
        console.log('running');
    });
```

./views/login.html（客户端）

```html
        <style>
            table {
                width: 400px;
                height: 200px;
                border-collapse: collapse;
                margin: 0 auto;
            }

            td {
                border: 1px solid #ccc;
            }
        </style>
	<body>
        <form id="form">
            <table>
                <tr>
                    <td>用户名：</td>
                    <td><input type="text" id="uName" name="uName"></td>
                </tr>
                <tr>
                    <td>密 码：</td>
                    <td><input type="text" id="pwd" name="pwd"></td>
                </tr>
                <tr>
                    <td></td>
                    <td><input type="button" id="login" value="登录"></td>
                </tr>
            </table>
        </form>
    </body>
    <script src="../node_modules/jquery/dist/jquery.min.js"></script>
    <script>
        // 给登录按钮注册事件
        $("#login").on('click', function (e) {
            e.preventDefault();// 阻止默认事件
            // 得到参数
            var params = $("#form").serialize();
            // var data = `uName=${$('#uName').val()}&pwd=${$('pwd').val()}`;
            // 将参数提交到服务器
           var ajax = $.ajax({
                url: '/login',
                type: 'POST',
                data: params,
                dataType: 'JSON'
            });
            // promise
            ajax.then(data => {
                // 判断状态
                if (data.status === 200) {
                    alert(data.msg);
                    // 跳转到首页
                    window.location = '/'
                } else {
                    // 跳转到登录页面
                    alert(data.msg);
                    window.location('/login');
                }
            });
        })
    </script>
```

### 2、session

- nodejs中不能直接使用session，如果要使用必须借助express的第三方中间件：cookie-session

  - 使用步骤：

    - 下载：npm i cookie-session

    - 引用：var cookieSession = require('cookie-session');

    - 注册：

      ```
      app.use(cookieSession({
          name: 'session',
          keys: ['key1', 'key2']
      }))
      ```

    - 使用

      - 设置： req.session.键= 值；
      - 取值： req.session.键

server.js（服务器）

```js
    var fs = require('fs');
    var express = require('express');
    var bodyParser = require('body-parser')
    var cookieSession = require('cookie-session');
    var app = express();

    app.use(bodyParser.urlencoded({ extended: false }))
    app.use(bodyParser.json())

    // 设置静态文件
    app.use('/node_modules', express.static('node_modules'));

    // 注册cookiesession
    app.use(cookieSession({
        name: 'session',
        keys: ['key1', 'key2']
    }))

    // 1、设置路由
    // 设置一个首页
    app.get('/', function(req, res){
       // 得到session
       // console.log(req.session.uName);
       var session = req.session.uName;
       if (session) {
           res.send('用户已经登录过一');
       } else {
           res.send('<script>alert("用户还没有登录");window.location="/login"</script>');
       }
    });

    // 得到登录页面
    app.get('/login', function(req, res){
        fs.readFile('./views/login.html', function(err, data){
            res.end(data);
        });
    });

    // 完成提交数据的逻辑
    app.post('/login', function(req, res){
        // body-parser
        var uName = req.body.uName;
        var pwd = req.body.pwd;
        // 判断
        if (uName === "admin" && pwd === "888") {
            // 要将用户的登录信息保存起来：用session来保存
            req.session.uName = uName;
            res.end(JSON.stringify({
                status: 200,
                msg: '成功'
            }));
        } else{
            // 登录失败
            res.json({
                status: 500,
                msg: '不成功'
            });
        }
    });
    app.listen(3000, function() {
        console.log('running');
    });
```

./views/index.html（客户端）

```html
    <body>
        <form id="form">
            <table>
                <tr>
                    <td>用户名：</td>
                    <td><input type="text" id="uName" name="uName"></td>
                </tr>
                <tr>
                    <td>密 码：</td>
                    <td><input type="text" id="pwd" name="pwd"></td>
                </tr>
                <tr>
                    <td></td>
                    <td><input type="button" id="login" value="登录"></td>
                </tr>
            </table>
        </form>
    </body>
    <script src="../node_modules/jquery/dist/jquery.min.js"></script>
    <script>
        // 给登录按钮注册事件
        $("#login").on('click', function (e) {
            e.preventDefault();// 阻止默认事件
            // 得到参数
            var params = $("#form").serialize();
            // var data = `uName=${$('#uName').val()}&pwd=${$('pwd').val()}`;
            // 将参数提交到服务器
           var ajax = $.ajax({
                url: '/login',
                type: 'POST',
                data: params,
                dataType: 'JSON'
            });
            // promise
            ajax.then(data => {
                // 判断状态
                if (data.status === 200) {
                    alert(data.msg);
                    // 跳转到首页
                    window.location = '/'
                } else {
                    // 跳转到登录页面
                    alert(data.msg);
                    window.location('/login');
                }
            });
        })

    </script>
```