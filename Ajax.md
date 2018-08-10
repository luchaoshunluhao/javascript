## 一、 认识Ajax

### 1、 初识 ajax

我们平常上网，不管是注册账号，还是浏览网页，其本质就是通过客户端向服务器发送请求，服务器接到请求后返回处理后的数据给客户端；
在我们之前学习代码中，向服务器提交数据典型的应用是就是 form 表单，其中的 action 就是我们提交数据的服务器端地址；

完成一个 form 表单；
当我们点击提交按钮时，页面就会跳转到服务器页面；

但是，我本不想让页面跳转，数据也能被发送到服务器端，同时，还可以接受服务器返回的数据；

当我注册一个网站的账号时，填写完用户名并没有点击提交，但是，用户名如果有重复，文本框的傍边便会提示我更换用户名；

类似的功能还有 验证短信的发送、百度搜索的关键字推举、无刷新的分页等等……

想要完成这些类似的功能实现，我们今天所要学习的ajax技术，就是核心技术；

ajax 也是技术名词的缩写：
Asynchronous `[ə'sɪŋkrənəs; eɪ-]` ：异步的；
JavaScript ：JavaScript语言
And ：和、与
XML ：数据传输格式

1998年微软公司（Microsoft）的Outlook Web Access第一次使用了ajax技术，允许客户端脚本发送HTTP请求，并随后集成在IE4.0中应用（XMLHTTP），到2005年，谷歌（Google）把Ajax成功应用于自家的多款Web系统中（Gmail邮箱、Google Map、Google 搜索建议），

从此Ajax被越来越多的人所接受…

**客户端通过HTTP向服务器发送请求**

### 2、 快速入门

```html
<body>
    <form action="1-1-1.php" method="get">
        <input type="text" name="names" value=""><br>
        <input type="button" value="提交">
    </form>
</body>
<script>
    //获取DOM对象
    var inp = document.getElementsByTagName('input');
    //绑定点击事件
    inp[1].onclick = function(){
        //获取文本值
        var v = inp[0].value;
        //获取ajax对象
        var xhr = new XMLHttpRequest();
        //监听状态变化
        xhr.onreadystatechange = function(){
            //判断状态值
            if(xhr.readyState == 4){
                //获取服务器返回信息
                alert(xhr.responseText);
            }
        }
        //打开链接
        xhr.open('get', '1-1-2.php');
        //发送连接
        xhr.send();
    }
</script>
```

1-1-2.php

```php
echo 123;
```

## 二、 Ajax对象

### 1、 获取对象

通过上一节我们发现，想要使用 ajax 的一系列功能，我们就必须先得到 ajax 对象

基于 W3C标准 浏览器：

```js 
var xhr = new XMLHttpRequest();
```

基于IE内核的浏览器:

```js 
var xhr = new ActiveXObject('Microsoft.XMLHTTP');
```

```html
<script>
    var btu = document.getElementById('btu');
    btu.onclick = function(){
        //基于 W3C标准 浏览器
        var xhr = new XMLHttpRequest();
        alert(xhr);

        //基于IE内核的浏览器， W3C标准浏览器中报错
        var xhr = new ActiveXObject('Microsoft.XMLHTTP');
        alert(xhr);
    }
</script>
```

浏览器标准不一样，得到的对象也不一样，我们也不知道客户使用什么样的浏览器，因此，我们需要解决兼容性问题；

修改上述代码并测试，**具有兼容性**：

```html
<script>
var btu = document.getElementById('btu');
btu.onclick = function(){
	try{
		var xhr =  new XMLHttpRequest()
	}catch(e){};

	try{
		var xhr = new ActiveXObject('Microsoft.XMLHTTP')
	}catch(e){};

	alert(xhr);
}
</script>
```

再次对代码进行修改 **兼容代码封装进函数调用**

```html
<script>
    var btu = document.getElementById('btu');
    btu.onclick = function(){
        //封装进函数供其他程序调用
        function cXHR(){
            try{return new XMLHttpRequest()}catch(e){};
            try{return new ActiveXObject('Microsoft.XMLHTTP')}catch(e){};
        }
        alert(cXHR());
    }
</script>
```

将函数写入单独的文件，共其他地方引入调用

**创建createXHR.js** 
将函数复制到文件 createXHR.js 内并保存，代码如下：

```js
function cXHR(){
    try {return new XMLHttpRequest()}catch(e){};
    try {return new ActiceXObject('Microsoft.XMLHTTP')}catch(e){};
}
```

**使用：**

```html
//文件引入
<script src="createXHR.js"></script>
<script>
    var btu = document.getElementById('btu');
    btu.onclick = function(){
		//函数调用
        alert(cXHR());
    }
</script>
```

顺便封装一个方法：
使用id属性获取DOM对象，方便后面使用

```js
function gid(id){
    return document.getElementById(id);
}
```

### 2、 ajax对象的属性、方法 *

火狐开发者文档：
https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest 

#### （1） 属性

- **readyState： Ajax状态码 * **
  0：表示对象已建立，但未初始化，只是 new 成功获取了对象，但是未调用open方法
  1：表示对象已初始化，但未发送，调用了open方法，但是未调用send方法
  2：已调用send方法进行请求
  3：正在接收数据（接收到一部分），客户端已经接收到了一部分返回的数据
  **4：接收完成，客户端已经接收到了所有数据 * **
- status ：http响应状态码
  200代表成功获取服务器端数据
  404未找到页面等等……
- statusText ：http响应状态文本
- **reponseText：如果服务器端返回字符串，使用responseText进行接收**
- responseXML ：如果服务器端返回XML数据，使用responseXML进行接收
- **onreadystatechange：当 readyState 状态码发生改变时所触发的回调函数**

#### （2）方法

- **open(method,url,async)：初始化Ajax对象 (打开)**
  method:http请求方式，get/post
  url:请求的服务器地址
  async:布尔值，ture代表异步请求，false代表同步请求；

- **setRequestHeader(header,value)：设置请求头信息**
  header ：请求头名称
  value ：请求头的值

- xhr.getAllResponseHeaders() 获取全部响应头信息
- xhr.getResponseHeader('key') 获取指定头信息

- **send(content) ：发送Ajax请求**
  content ：	如果是get请求时，此参数为null;如果是post请求时，此参数就是要传递的数据

  **注意: 所有相关的事件绑定必须在调用send()方法之前进行.**

#### （3） 同步与异步

例如，小明去餐馆排队点餐，前台服务员将小明的菜单告诉厨师进行制作，此时小明后面排队的人就一直等着，
直到厨师制作完成，把饭菜送到小明手里后离开，后面的人才能继续点餐；这就是同步处理

但是，如果前台服务员将小明的菜单告诉厨师后，服务员发给小明一个好牌去旁边等待，后面的人继续点餐，
厨师将小明的饭菜做好后，随时呼唤小明就餐；这就是异步处理

服务器的不同做法，就代表着 Ajax 的同步或异步处理；
小明就是客户端；
厨师就是后台服务器；

PHP后台代码：

```php
sleep(2);
$data = 't1';
echo $data;
```

前台代码：

```html
<script src="createXHR.js"></script>
    <script>
        function t1(){
            var xhr = cXHR();
            xhr.onreadystatechange = function(){
                if(this.readyState == 4){
                    alert(this.responseText);
                }
            }
            //false同步
            //true 异步
            xhr.open('get', '02.php', false); 
            xhr.send(null);
        }
        function t2(){
            alert('t2');
        }
        t1();
        t2();
    </script>
```

## 三、 判断用户名是否可用--案例

 前台代码

```html
<body>
    <input type="text" value="" id="names"> 
    <span id="tip"></span>
</body>
<script src="createXHR.js"></script>
<script>
    var inp = gid('names');
    inp.onblur = function(){
        var xhr = cXHR();
        xhr.onreadystatechange = function(){
            if(xhr.readyState == 4){
                // alert(xhr.responseText);
                if(xhr.responseText == 1){
                    var h = '<font color="red">用户名已经被占用</font>';
                    gid('tip').innerHTML = h;
                }else{
                    var h = '<font color="green">用户名可用</font>';
                    gid('tip').innerHTML = h;
                }
            }
        }
        xhr.open('get','03-1.php?names=' + inp.value);
        xhr.send();
    }
</script>
```

后台PHP代码

```php
$v = $_GET['names'];
//链接数据，查询是否存在用户名 //此步骤省略

if($v == 'admin')
{
    echo 1;
}else
{
    echo 0;
}
```

## 四、 缓存问题

### 1、 缓存的产生

以上一节的案例为模板，使用IE浏览器测试；

```php
$v = $_GET['names'];
//连接数据，查询是否存在用户名
//此步省略
sleep(2);
if($v == 'admin') 	//在浏览器输入'zhangsan'，和这里存的'admin'不一致，所以显示用户可用
{
    echo 1;
}else
{
    echo 0;
}
```

```php
$v = $_GET['names'];
//连接数据，查询是否存在用户名
//此步省略
sleep(2);
if($v == 'zhangsan')	//'zhangsan'这个用户名应该是被占用的，但是在IE浏览器里却是用户可用
{
    echo 1;
}else
{
    echo 0;
}
```

原因：
在Ajax的get请求中，如果运行在IE内核的浏览器下，
其如果**向同一个url发送多次请求**时，就会产生所谓的缓存问题。
缓存问题最早设计初衷是为了加快应用程序的访问速度，
但是其会影响Ajax实时的获取服务器端的数据。

### 2、 客户端解决缓存问题

产生缓存的问题就是 我们的客户端向同一个 url 发送了多次请求；
如果我们每次请求的url不同，那么，缓存问题就不会存在了；

我们可以在请求地址的后面加上一个无意义的参数，参数值使用随机数即可，
那么每次请求都会产生随机数，URL就会不同，缓存问题就被解决了；

**Math.random()**：返回 0--1 之间的随机数，包括 0 但不包括 1；

修改代码如下：

```js
var url = '03-1.php?names=' + inp.value + '&_=' + Math.random();
xhr.open('get', url);
```

但是，随机数虽然解决了问题，但是，我们不能保证每次生成的随机数都不一样；
也就是说，使用随机数存在一定的隐患；

**new Date().getTime()** ： 获取当前时间的毫秒时间戳
修改代码如下：

```js
var url = '03-1.php?names=' + inp.value + '&_=' + new Date().getTime();
xhr.open('get', url);
```

### 3、 设置响应头禁用客户端缓存

服务器端在相应客户端请求时，可以设置相应头详细，如：
header(‘Content-type:text/html; charset=utf-8’) ：告诉客户端浏览器，使用utf-8的编码格式解析页面信息。

在php代码中添加一下代码：

```php
//告诉客户端浏览器不要缓存数据
header("Cache-Control: no-cache");
```

## 五、 Ajax发送POST请求

### 1、 post请求

将之前写过的 get 请求修改为 post 请求；

```js
//请求地址
var url = '03-1.php';
//open参数为post
xhr.open('post', url);
//设置请求头
xhr.setRequestHeader('Content-type', 'application/x-www-form-urlencoded');
//设置post请求参数值
xhr.send('names=' + inp.value);
```

ajax中get请求与post请求的区别是：
 1：传参方式：
	get请求在url尾部传递参数；
	post 请求在send()方法中传递参数

 2：请求头：
	post 请求需要生命请求头 xhr.setRequestHeader('Content-type','application/x-www-form-urlencoded');
	get 不需要设置；

 3：参数值类型：
	get 传参值只能是数字、字符串
	post 可以传递数字、字符串意外，还可以传递二进制数据；

### 2、Ajax 实现无刷新上传文件

普通文件上传，需要form表单，点击上传按钮后，页面会跳转：

HTML 代码：

```html
<form action="05.php" method="post" enctype="multipart/form-data">
    <input type="file" name="pic" > <br>
    <input type="submit" value="上传" >
</form>
```

PHP后台移动文件代码：

```php
//移动文件到新位置
move_uploaded_file($_FILES['pic']['tmp_name'], './' . $_FILES['pic']['name']);
```

上传完成后，我们在浏览器中打开调试工具可以看到结果。

**文件上传原理：**

由此我们可以推断，文件上传的原理就是，浏览器客户端将文件载入并解析为二进制数据，
然后通过HTTP协议将数据发送到服务器端，文件上传就已经成功了；
但是对于服务器来说，接收到的文件会放到系统缓存中，
我们需要使用PHP的move_uploaded_file函数将文件移至我们设置好的目录下，并对缓存文件重新命名；
完成移动操作后，我们就可以在服务器端看见上传后的文件了；

想要使用Ajax完成文件上传，首先我们要学会，Ajax作为客户端如何将文件读入并解析为二进制数据；
HTML5为我们提供了 **FormData 对象**：
通过FormData对象可以组装一组用 XMLHttpRequest发送请求的键/值对。它可以更灵活方便的发送表单数据，因为可以独立于表单使用。
如果你把表单的编码类型设置为multipart/form-data，则通过FormData传输的数据格式和表单通过submit() 方法传输的数据格式相同;

FormData 手册
https://developer.mozilla.org/zh-CN/docs/Web/API/FormData/Using_FormData_Objects

```html
<body>
    <form id="fm"  enctype="multipart/form-data" action="05.php" method="post">
        <input type="file" name="pic" > <br>
        <input type="submit" value="上传" id="su">
    </form>
</body>
<script src="createXHR.js"></script>
<script>
    var fm = gid('fm');
    fm.onsubmit = function(){
        var xhr = cXHR();
        xhr.onreadystatechange = function(){
            if(xhr.readyState == 4){
                if(xhr.responseText == 1){
                    alert('上传成功');
                }else{
                    alert('上传失败');
                }
            }
        }
        var url = '05.php';
        xhr.open('post', url);
        //FormData 会把表单的数据(包括文件流)，整体打包
        var fmdata = new FormData(this); 
        //发送整个FormData对象
        xhr.send(fmdata);
        //阻止提交跳转
        return false;
    }
</script>
```

## 六、 Ajax与XML

Ajax请求后台返回数据时，都是简单的字符串或数字；

如果后台有大量数据要返回，我们应该怎么办？

目前有两种技术方案：

1：将数据打包成  **XML** 的格式进行传输

2：将数据打包成  **json** 的格式进行传输

### 1、 XML基本语法规则

XML 的语法规则很简单，但很严格。

**XML 文档必须有根元素**
根元素是所有其他元素的父元素；

```xml
<root>
  <child>
    <subchild>.....</subchild>
  </child>
</root>
```

如上代码，root就是根元素；

**XML 声明**

`<?xml version="1.0" encoding="utf-8"?>`
声明文件是可选部分,如果存在需要放在文档的第一行；
version ：版本号，代表XML使用的版本号
encoding ：编码格式，默认UTF-8

所谓的文档声明就是告诉解析器当前文档格式、版本号以及编码格式。

**所有的 XML 元素都必须是成对闭合标签**

非闭合标签是非法的，解析器将报错，不无正常解析；

```xml
<user>
    <name>刘能</name>
    <!-- 错误的,无结束标签 -->
    <age>46
	<!-- 错误的,无开始标签 -->
    男</sex>
</user>
```

**XML 标签对大小写敏感**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<user>
    <name>刘能</name>
    <!-- 错误，标签大小写不一致 -->
    <Age>46</age>
    <sex>男</sex>
</user>
```

**XML标签不允许有交叉嵌套**
**XML标签名不建议使用特殊字符，尽量只用数字字母下划线**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<user>
    <name>刘能</name>
    <age>46</age>
    <!-- 不建议使用 -->
    <s-ex>男</s-ex>
    <s.ex>男</s.ex>
</user>
```

### 2、 PHP 解析XML

XML是一种数据传输格式，当PHP接收到的数据就是一段XML的时候，我们的PHP应该怎么处理XML数据呢？

在PHP5版本以后，其提供了一个非常非常强大的类库，SimpleXML类库，专门用于实现对XML文档的解析操作。

#### 解析原理

XML在解析时一共要经历三个步骤：

① 读取XML文档到内存； 

② 形成DOM树结构； 

③ 生成SimpleXML对象。

#### SimpleXML类库

**user.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<user>
    <man>
        <name>刘能</name>
        <age>46</age>
        <sex>男</sex>
    </man>
    <man sex="男">
        <name>广坤</name>
        <age>48</age>
    </man>
</user>
```

有user.xml 文件，内容如上，如何使用PHP解析呢？
SimpleXML类库提供了：

simplexml_load_file('xml_file_path')方法：
**将XML文件解释成一个对象**

simplexml_load_string('xml_url_path')

**将XML字符串解释成一个对象**

```php 
$xml = simplexml_load_file('user.xml');
var_dump($xml);
```

注意：
如果当前读取的节点是对象就通过->来进行访问。
如果当前读取的节点是数组就通过[]来进行访问。

获取XML数据中的所有name值

**foreach循环遍历：**

```php
$xml = simplexml_load_file('user.xml');
foreach ($xml -> man as $v)
{
    echo '姓名:' . $v -> name . '；年龄：' . $v -> age . '<hr>';
}
```

**for循环遍历：**

```php
$xml = simplexml_load_file('./01.xml');
$length = count($xml);
for($i = 0; $i < $length; $i++)
{
    echo $xml -> man[$i] -> name;
}
```

### 3、 PHP 解析XML 案例

准备一个有表单提交功能的HTML页面，
输入想要查询的城市后，点击提交按钮，将这个城市的天气打印出来：

html代码：

```html
<form action="03.5.php" method="get">
    <input type="text" name="city"><br>
    <input type="submit" value="提交">
</form>
```

后台PHP处理文件代码：

```php
//接受前台提交的数据
$city = $_GET['city'];

//组装请求地址
$url = 'http://v.juhe.cn/weather/index?cityname=' . $city . '&dtype=xml&format=&key=810c3b2c488bc37d5f521196d8799a72';

//发送请求并接受返回的数据
$s = file_get_contents($url);
// echo $s; //打印返回的XML数据

//使用 simplexml_load_string 函数读入并解析XML数据
$xml = simplexml_load_string($s);

//找到并打印我们想要的数据
echo '城市：' . $xml -> result -> today -> city . '<hr>';
echo '气温：' . $xml -> result -> today -> temperature . '<hr>';
echo '天气：' . $xml -> result -> today -> weather . '<hr>';
echo '着装建议：' . $xml -> result -> today -> dressing_advice . '<hr>';
```

### 4、PHP 生成XML

根据XML语法规则，使用PHP写字符串即可；

PHP 代码：

```php
mysql_connect('localhost', 'root', '123456');
mysql_query('use test');
mysql_query('set names utf8');

//SQL 语句
$sql = "select * from test";
$res = mysql_query($sql);
//生成XML格式数据
$xml = '<users>';
while($row = mysql_fetch_assoc($res))
{
    $xml .= '<admin>';
    $xml .= '<id>' . $row['id'] . '</id>';
    $xml .= '<name>' . $row['name'] . '</name>';
    $xml .= '</admin>';
}
$xml . ='</users>';
//响应头声明文件类型
header('Content-type:text/xml');
echo $xml;
```

### 5、 Ajax获取XML数据

```html
<body>
    <input type="button" value="获取XML" id="su">
</body>
<script src="createXHR.js"></script>
<script>
    var fm = gid('su');
    fm.onclick = function(){
        var xhr = cXHR();
        xhr.onreadystatechange = function(){
            if(xhr.readyState == 4){
                //弹出获取到的数据
                alert(xhr.responseText);
            }
        }
        var url = '06.php';
        xhr.open('post', url);
        //设置请求头
        xhr.setRequestHeader('Content-type', 'application/x-www-form-urlencoded');
        xhr.send();
    }
</script>
```

此时，我们已经能够获取到后台返回的数据了，但是，如果我想将 用户名 全部取出并且展示到浏览器的界面中；
数据虽然接受到了，但是，JS并没有办法解析使用这些数据；

前面在介绍Ajax属性时，有一个属性是专门接受XML数据的：

responseXML ：如果服务器端返回XML数据，使用responseXML进行接收

修改代码，使用responseXML接受数据；

```js 
xhr.onreadystatechange = function(){
    if(xhr.readyState == 4){
        //弹出获取到的数据(接受XML数据)
        alert(xhr.responseXML);
    }
}
```

运行代码发现，我们得到的是一个XML的DOM对象；

### 6、JS解析XML

**非标准模型中，键与值被解析为一个节点；**
**标准模型中，键与值被解析为上下级两个节点；**

**标准模型在获取到相应的节点值还需要进一步获取其子节点，然后才能获取到其值。**

修改上述代码，完成功能，将所有 用户名 展示到浏览器界面

```js
xhr.onreadystatechange = function(){
	if(xhr.readyState == 4){
	    //接受XML数据
	    var x = xhr.responseXML;
	    var admin = x.getElementsByTagName('admin');
	    for(var i = 0; i < admin.length; i++){
	        //标准DOM解析查找方式
	        var user = admin[i].
	        getElementsByTagName('name')[0].
	        childNodes[0].
	        nodeValue;
	        //将数据放入id为d的div标签中
	        gid('d').innerHTML += user + '<br>';
	    }
	}
}
```

小技巧：仔细思考发现，不管DOM树是否标准，都是DOM树

```js
xhr.onreadystatechange = function(){
    if(xhr.readyState == 4){
        //接受XML数据
        var x = xhr.responseXML;
        var admin = x.getElementsByTagName('admin');
        for(var i = 0; i < admin.length; i++){
            var user = admin[i].
            getElementsByTagName('name')[0].innerHTML;//不管DOM树是否标准，都是DOM
            gid('d').innerHTML += user + '<br>';
        }
    }
}
```

JS如何操作HTML的DOM，就如何操作XML的DOM；

## 七、 Ajax与json

XML之所以应用广泛，就因为XML数据结构化明确，适合大数据传输；
但是，在PHP中生成XML数据时，需要我们填写很多成对标签，然后声明响应头为XML；
而在JS解析时，也要进行DOM节点的遍历查找；

而字符串，没有结构化，容易造成混乱，无法完成大量数据的传输；
难道，我们就不能创造一种具有结构明确的字符串格式吗？

生成和解析简单，易读且结构化明确，适合大数据传输的字符串结构：JSON

```json
{"name":"刘能", "age":"45", "height":172}
```

```json
[
	{"name":"刘能", "age":"45", "height":172},
	{"name":"大脚", "age":"43", "height":168},
	{"name":"赵四", "age":47, "height":175}
]
```

### 1、 什么是JSON

JSON 指的是 JavaScript 对象表示法（JavaScript Object Notation）
JSON 是轻量级的文本数据交换格式
JSON 独立于语言 *
JSON 具有自我描述性，更易理解

**注意：**
JSON 使用 Javascript语法来描述数据对象，但是 JSON 仍然独立于语言和平台。
JSON 解析器和 JSON 库支持许多不同的编程语言。

JSON 其实就是长的和JS对象几乎一样的 **字符串** ，

### 2、 PHP生成JSON & JS解析json

之前的案例中，后台PHP从数据库获取到数据后，生成XML格式返回给前端，
修改第6章案例中PHP代码，使PHP生成json字符串：

```php
mysql_connect('localhost', 'root', '123456');
mysql_query('use test');
mysql_query('set names utf8');

//SQL 语句
$sql = "select * from test";
$res = mysql_query($sql);
$data = [];
while($row = mysql_fetch_assoc($res))
{
    $data[] = $row;
}
//json_encode 转为json字符串
echo json_encode($d);
```

修改之前的案例中前端代码，使JS解析json字符串为数组对象：

```html
<script src="createXHR.js"></script>
<script>
    var fm = gid('su');
    fm.onclick = function(){
        var xhr = cXHR();
        xhr.onreadystatechange = function(){
            if(xhr.readyState == 4){
                var d = xhr.responseText;
                //将json字符串解析为JS数组对象
                var f = JSON.parse(d);
                //循环数组
                for(var i = 0; i < f.length; i++){
                    //获取对象值
                    var u = f[i].name;
                    gid('d').innerHTML += u +'<br>';
                }
            }
        }
        var url = '08-2.php';
        xhr.open('post', url);
        //设置请求头
        xhr.setRequestHeader('Content-type', 'application/x-www-form-urlencoded');
        xhr.send();
    }
</script>
```

### 3、 无刷新录入系统--案例

前台代码

```html
<body>
   姓名：<input type="text" value=""> <br>
   年龄：<input type="text" value=""> <br>
   性别：<input type="text" value=""> <br>
   <input type="button" value="提交" id="btu">
</body>
<script src="createXHR.js"></script>
<script>
    var btu = gid('btu');
    btu.onclick = function(){
        var inp = document.getElementsByTagName('input');
        //将数据存入JS对象；
        var ar = {"name":inp[0].value, "age":inp[1].value, "sex":inp[2].value};
        // console.log(ar);//打印并查看数据类型

        var jn = JSON.stringify(ar);//将JS对象转为JSON字符串
        // console.log(jn);//打印并查看数据类型

        //Ajax 发送数据
        var xhr = cXHR();
        xhr.onreadystatechange = function(){
            if(xhr.readyState == 4){
                if(xhr.responseText == 1){
                    inp[0].value = '';
                    inp[1].value = '';
                    inp[2].value = '';
                    alert('录入成功');
                }else{
                    alert('录入失败');
                }
            }
        }
        xhr.open('get', '08-3.php?data=' + jn);
        xhr.send();
    }
</script>
```

后台PHP代码

```php
mysql_connect('localhost', 'root', '123456');
mysql_query('use test');
mysql_query('set names utf8');

//获取前台传参
$json = $_GET['data'];
// echo $json;

//将JSON字符串解析为PHP对象
// $d = json_decode($json);
// $sql = 'insert into test(name, age, sex) values ("' . $d -> name . '",' . $d -> age . ',"' . $d -> sex . '")';

//将JSON字符串解析为PHP数组
$d = json_decode($json, true);
$sql = 'insert into test(name,age,sex) values ("' . $d['name'] . '",' . $d['age'] . ',"' . $d['sex'] . '")';
$res = mysql_query($sql);
if(mysql_insert_id() > 0)
{
    echo 1;
}else
{
    echo 0;
}
```

### 4、 知识点总结

#### （1） JS操作JSON

```js
//JS数组转JSON字符串
var arr = ['路飞', '索隆', '娜美', '乔巴', '罗宾'];
var s = JSON.stringify(arr);
//结果为 数组形式的 JSON 字符串 
console.log(s);
```

结果： ["路飞","索隆","娜美","乔巴","罗宾"]

------

```js
//JS对象转JSON字符串
var arr = {'name':"路飞", 'age':17, 'money':5, 'nature':'橡胶'};
var s = JSON.stringify(arr);
//结果为 对象形式的 JSON 字符串 
console.log(s);
```

结果：{"name":"路飞","age":17,"money":5,"nature":"橡胶"}

------

```js
//对象形式的JSON字符串转JS 
var arr = '{"name":"路飞", "age":17, "money":5, "nature":"橡胶"}';
var s = JSON.parse(arr);
//结果为 JS对象
console.log(s);
```

------

```js
//数组形式的JSON字符串转JS
var arr = '["路飞", "索隆", "娜美", "乔巴", "罗宾"]';
var s = JSON.parse(arr);
//结果为 JS 数组
console.log(s);
```

------

#### （2） PHP操作JSON

```php
//数组格式的JSON字符串转PHP
$d = '["路飞", "索隆", "娜美", "乔巴", "罗宾"]';
$s = json_decode($d);
//结果为 PHP 数组
var_dump($s);
```

结果：
`array(5) { [0]=> string(6) "路飞" [1]=> string(6) "索隆" [2]=> string(6) "娜美" [3]=> string(6) "乔巴" [4]=> string(6) "罗宾" }`

------

```php
//对象格式的JSON字符串转PHP
$d = '{"name":"路飞", "age":17, "money":5, "nature":"橡胶"}';
//结果为 PHP 对象
$s = json_decode($d);

//结果为 PHP 关联数组
$s = json_decode($d, true);

var_dump($s);
```

结果：
`object(stdClass)#1 (4) { ["name"]=> string(6) "路飞" ["age"]=> int(17) ["money"]=> int(5) ["nature"]=> string(6) "橡胶" }`

`array(4) { ["name"]=> string(6) "路飞" ["age"]=> int(17) ["money"]=> int(5) ["nature"]=> string(6) "橡胶" }`

------

```php
//PHP索引数组生成JSON
$arr = ["路飞", "索隆", "娜美", "乔巴", "罗宾"];
$jn = json_encode($arr);
//结果为 数组形式的 JSON 字符串
var_dump($jn);
```

结果：["路飞","索隆","娜美","乔巴","罗宾"]

```php
//PHP关联数字
$arrs = ['name' => '路飞', 'age' => 17, 'money' => 5, 'nature' => '橡胶'];

//PHP对象
class Hz{}
$arr = new Hz();
$arr -> name = '路飞';
$arr -> age = 17;
$arr -> money = 5;
$arr -> nature = '橡胶';

//PHP中关联数组和对象，生成的JSON字符串均为对象形式JSON
echo json_encode($arrs);
echo json_encode($arr);
```

#### （3） 总结

**生成JSON：**
JS 数组转JSON为 数组形式JSON
JS 对象转JSON为 对象形式JSON

PHP 索引数组转JSON为 数组形式JSON
PHP 关联数组转JSON为 对象形式JSON
PHP 对象转JSON为 对象形式JSON

**解析JSON：**

数组形式JSON转 JS数组
对象形式JSON转 JS对象

数组形式JSON转 PHP索引数组
对象形式JSON转 PHP对象
对象形式JSON转 PHP关联数组(参数true)

**函数及方法：**

json_encode()： PHP转JSON；
json_decode(data，[true]):JSON 转PHP对象或关联数组；

JSON.parse():JSON字符串转JS
JSON.stringify():JS转JSON

**注意：**
JSON就是字符串，各种编程语言都可以解析或生成的 **字符串**

## 八、 Ajax框架的封装

如果一个页面中有十几个地方用到Ajax，那么我们需要写十几次open()、十几次send()、十几次获取xhr对象；
代码重复相当多，而凡是有代码重复的地方，就有封装的可能；

创建新文件： ajax.js 

### 1、 餐前甜点

之前我们为了方便使用，封装过使用指定 id 获取DOM对象及获取xhr对象；
我们对之前的代码进行一次修改，使其更加优雅；

**定义一个自调用匿名函数**

```js
(function(){
	//code……
})();
```

为什么 定义一个自调用匿名函数？
在实际项目开发中，如果一个项目同时引入了多个javascript框架，可能会产生命名的冲突问题，
如果使用自调用匿名函数来封装javascript框架，所有变量处于封闭状态，就可以避免这个问题。

**封装一个$函数，用于获取指定id的dom对象**

```js
(function(){
	//封装$函数，获取指定 id 的DOM对象并返回给调用者
    var $ = function(id){
        return document.getElementById(id);
    }
})();
```

我们在前台代码中引入并使用ajax.js 

```html
<body>
   <div id="d">div</div>
</body>
<script src="ajax.js"></script>
<script>
    alert($('d'));
</script>
```

出现了报错，报错原因： 函数 $ 为局部变量；

**让 $ 局部变量全局化**

```js
(function(){
    //封装$函数，获取指定 id 的DOM对象并返回给调用者
    var $ = function(id){
        return document.getElementById(id);
    }
    //将局部变量 $ 复制给顶层window对象，使其成为全局变量
    window.$ = $;
})();
```

### 2、 封装get方法

ajax代码我们都会写，问题是：
如何把代码放进匿名函数中并且外部可以调用？

```js
(function(){
    //封装$函数，获取指定 id 的DOM对象并返回给调用者
    var $ = function(id){
        return document.getElementById(id);
    }
    //将局部变量 $ 复制给顶层window对象，使其成为全局变量
    window.$ = $;

    //声明gets方法
    var gets = function(url){
        var xhr = new XMLHttpRequest();
        xhr.onreadystatechange = function(){
            if(xhr.readyState == 4){
                alert(xhr.responseText);
            }
        }
        xhr.open('get', url);
        xhr.send();
    }
    //将局部变量 gets 复制给顶层window对象，使其成为全局变量
    window.ajax_get = gets;
})();
```

这样写并没有语法错误，也可以正常调用，但是，随着功能的不断增加，
我们的window对象也会被赋予各种各样的值，最终还是会导致混乱；

**在JavaScript中一切都是对象**

\$ 也可以被当作对象，我们就可以将ajax函数赋值给 $；

```js
(function(){
    //封装$函数，获取指定 id 的DOM对象并返回给调用者
    var $ = function(id){
        return document.getElementById(id);
    }

    //声明ajax函数，并复制给$;
    $.get = function(url){
        var xhr = new XMLHttpRequest();
        xhr.onreadystatechange = function(){
            if(xhr.readyState == 4){
                alert(xhr.responseText);
            }
        }
        xhr.open('get', url);
        xhr.send();
    }
    window.$ = $;
})();
```

前台调用

```html
<script>
    $.get('09-1.php');
</script>
```

### 3、解决获取Ajax对象的兼容性

修改上节代码：

```js
//获取Ajax对象
$.init = function(){
    try{return new XMLHttpRequest()}catch(e){};
    try{return new ActiveXObject('Microsoft.XMLHTTP')}catch(e){};
}

//声明ajax函数，并复制给$;
$.get = function(url){
    var xhr = $.init(); //调用init,获取ajax对象
    xhr.onreadystatechange = function(){
        if(xhr.readyState == 4){
            alert(xhr.responseText);
        }
    }
    xhr.open('get', url);
    xhr.send();
}
```

### 4、 获取Ajax的返回值

前台调用：

```html
<script>
    var cb = function(msg){
        $('d').innerHTML = msg;
    }
    $.get('09-1.php', cb);
</script>
```

修改 ajax.js

```js
$.get = function(url, callback){
    var xhr = $.init(); //调用init,获取ajax对象
    xhr.onreadystatechange = function(){
        if(xhr.readyState == 4){
            callback(xhr.responseText);
        }
    }
    xhr.open('get', url);
    xhr.send();
}
```

前台调用修改：

```html
<script>
    // var cb = function(msg){
    //     $('d').innerHTML = msg;
    // }
    $.get('09-1.php', function(msg){
        $('d').innerHTML = msg;
    });
</script>
```

### 5、 配合后台获取不同的返回值类型

修改 ajax.js

```js
//声明ajax函数，并复制给$;
$.get = function(url, callback, type=null){
    var xhr = $.init(); //调用init,获取ajax对象
    xhr.onreadystatechange = function(){
        if(xhr.readyState == 4){
            if(type == null){
                callback(xhr.responseText);
            }
            if(type == 'xml'){
                callback(xhr.responseXML);
            }
            if(type == 'json'){
                var t = JSON.parse(xhr.responseText);
                callback(t);
            }
        }
    }
    xhr.open('get', url);
    xhr.send();
}
```

前台调用，代码修改：

```html
<script>
    $.get('09-1.php', function(msg){
        console.log(msg);
    }, 'json');
</script>
```

### 6、 仿百度搜索推举--案例

后台PHP模糊查找获取数据：

```php
$v = $_GET['v'];
mysql_connect('localhost', 'root', '123456');
mysql_query('use test');
mysql_query('set names utf8');
//SQL 语句
$sql = "select * from test where name like '" . $v . "%'";
$res = mysql_query($sql);
$data = [];
while($row = mysql_fetch_assoc($res))
{
    $data[] = $row;
}
echo json_encode($data);
```

前台请求遍历数据：

```html
<body>
    <input type="text" id="key"><br>
    <div id="result"></div>
</body>
<script src="ajax.js"></script>
<script>
    //oninput 元素的值发生改变时触发。
    //该事件仅支持<input>、<textarea> 元素
    $('key').oninput = function(){
        var v = this.value;
        $.get('09-6.php?v=' + v, function(msg){
            // console.log(msg);
            $('result').innerHTML = '';
            for(var i = 0; i < msg.length; i++){
                $('result').innerHTML += '<div>' + msg[i].name + '</div>';
            }
        }, 'json');
    }
</script>
```

### 7、 无刷新分页

整体思路：
用户点击上一页、下一页，点击触发事件，根据当前页码，拼接ajax请求参数，发送请求；
后台接受请求及参数，链接数据库获取数据，处理数据后返回前台；
前台接到数据后，删除旧数据，遍历添加新数据；

前台代码：

```html
<body>
    <a href="#" onclick="s()">上一页</a>
    <a href="#" onclick="x()">下一页</a>
    <div class="">
        <table id="tb">
        </table>
    </div>
    <!--存储当前页码数据 隐藏 -->
    <input type="hidden" name="" value="1" id="h">
</body>
<script type="text/javascript" src="ajax.js"></script>
<script type="text/javascript">
    function pub(p){
        $.get('09-7page.php?page=' + p, function(msg){
            // console.log(msg);
            $("h").value = msg.p;//更改当前页码数
            delete msg.p;//删除旧数据
            //制作表格头
            $("tb").innerHTML = '<tr><td>编号</td><td>内容</td></tr>';
            //遍历数据并展示
            for(var i = 0; i < 3; i++){
                var h = '<tr>';
                h += '<td>' + msg[i].id + '</td>';
                h += '<td>' + msg[i].name + '</td>';
                h += '</tr>';
                $("tb").innerHTML += h;
            }
        }, 'json');
    }
    //页面加载完成，调用函数发送ajax 
    window.onload = function(){
        pub(0);
    }
    //上一页
    function s(){
        pub(parseInt($('h').value) - 1); //当前页减一
    }
    //下一页
    function x(){
        pub(parseInt($('h').value) + 1);//当前页加一
    }
</script>
```

后台PHP代码：

```php
mysql_connect('localhost', 'root', '123456');
mysql_query('use test');
mysql_query('set names utf8');
//查询SQL
//获取数据总条数
$sql = "select count(*) as num from test";
$res = mysql_query($sql);
$row = mysql_fetch_assoc($res);
$count= $row['num'];//获取数据总条数

$psize = 3; //设置每页条数
//ceil 向上取整
$pcount = ceil($count / $psize);//最大页码数

//获取get传参，第几页数据
$page = isset($_GET['page']) ? $_GET['page'] : 0;
if($page < 1)
{ //页码小于1，则取1
    $page = 1;
}
if($page > $pcount)
{//页码大于最大数，则去最大数
    $page = $pcount;
}

$offset = ($page - 1) * $psize; //计算查询区间
$sql = "select * from test limit $offset, $psize";
$res = mysql_query($sql);
$data = [];
while ($row = mysql_fetch_assoc($res)) 
{
    $data[] = $row;
}
//返回当前页码数
$data['p'] = $page;
echo json_encode($data);
```

## 九、 跨域问题及解决方案

### 1、 认识jsonp

```html
<script src="ajax.js"> </script>
<script>
    $.get('http://bbs.com/1.php', function(){});
</script>
```

ajax 请求的URL地址，不在当前域名下，就会出现：同源策略进制读取位于xxx的远程资源。

**同源策略，也叫跨域禁止策略；**
阻止从一个域上加载的脚本，获取或操作另一个域上的资源；

但是，公司内部系统的数据交互就无法进行：
公司OA系统 ：http://oa.itcast.cn 
公司ERP系统 ：http://erp.itcast.cn 
公司ESM系统 ：http://esm.itcast.cn 

而Web页面上调用js文件时则不受是否跨域的影响
（不仅如此，我们还发现凡是拥有"src"这个属性的标签都拥有跨域的能力，比如script、img、iframe）；
src 的能力就是把远程的数据资源加载到本地(图片、JS代码等);

前台代码：

```html
<script src="ajax.js"> </script>
<script>
    //提前写好函数，调用函数需要传参
    function cb(msg){
        console.log(msg);
    }
</script>
<!--src加载进来的代码就是一个JS的函数调用,cb函数调用  -->
<script src="http://bbs.com/1.php"></script>
```

后台PHP代码：

```php
$arr = ['a' => 1, 'b' => 'san', 'c' => 'wu', 'd' => 4];
$str = json_encode($arr);
//返回字符串，JS代码的函数调用
//要返回的数据作为函数传参传递
echo "cb(" . $str . ")";
```

**修改前后台代码，增加灵活性；**

前台代码：

```html
<script src="ajax.js"> </script>
<script>
    //提前写好函数，调用函数需要传参
    function callback(msg){
        console.log(msg);
    }
</script>
<!--src加载进来的代码就是一个JS的函数调用,cb函数调用  -->
<!--地址get传参，告知后台函数调用名称 -->
<script src="http://bbs.com/1.php?cb=callback"></script>
```

后台PHP代码：

```php
$arr = ['a' => 1, 'b' => 'san', 'c' => 'wu', 'd' => 4];
$str = json_encode($arr);
//返回字符串，JS代码的函数调用
//要返回的数据作为函数传参传递
//接受参数拼接，作为函数调用名称
echo $_GET['cb'] . "($str)";
```

### 2、 如何使用JSONP

```html
<body>
   <input type="button" id="btu" value="点击">
</body>
<script src="ajax.js"> </script>
<script>
    //提前写好函数，调用函数需要传参
    function callback(msg){
        console.log(msg);
    }
    //动态添加script标签及src属性
    $('btu').onclick = function(){
        var sc = document.createElement('script');
        sc.src = "http://bbs.com/2.php?cb=callback";
        document.getElementsByTagName('head')[0].appendChild(sc);
    }
</script>
```

就是在远程服务器上设法动态的把数据装进js格式的文本代码段中，供客户端调用和进一步处理；
在前台通过动态添加script标签及src属性，表面看上去与ajax极为相似，但是，这和ajax并没有任何关系；
为了便于使用及交流，逐渐形成了一种 **非正式传输协议**，人们把它称作 **JSONP** ；

该协议的一个要点就是允许用户传递一个callback参数给服务端，
然后服务端返回数据时会将这个callback参数作为函数名来包裹住JSON数据，
这样客户端就可以随意定制自己的函数来自动处理返回数据了。

### 3、 跨域资源共享（ CORS）机制

https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Access_control_CORS

php代码中添加一下header头声明:

 Access-Control-Allow-Origin:* //域名，* 允许所有 

php:(服务端代码) 

```php
<?php
header('Access-Control-Allow-Origin:http://localhost'); 
echo 1;
```