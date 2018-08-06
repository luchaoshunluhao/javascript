## 一、 认识jQuery

### 1、 概述

之前，我们为了方便使用，封装了ajax.js,能够查找指定ID的DOM对象，使用ajax变得非常简单；
而我们做的这些，也早有编程大神做过，并且开放出来提供免费下载使用；

jQuery 就是一款免费且开放源代码的JavaScript代码库；

提供了HTML文档操作，节点查找，事件处理，动画设计，Ajax交互等丰富的功能；
并且兼容各种主流浏览器；

jQuery设计的宗旨就是：**写更少的代码，做更多的事情；**

### 2、 入门使用

**下载代码库：**

官方下载地址：http://jquery.com/download/

**注意：**

jq自2.0版本开始，不在支持IE9一下浏览器；
自3.0版本开始，针对移动端做了优化处理；

**引入并使用：**

```html
<body>
    <input type="button" id="btu" value="点击">
    <div id="re" style="width:200px;height:200px">fds</div>
</body>
<!--引入代码库  -->
<script src="jquery-1.8.3.js"></script>
<script>
    var btu = document.getElementById('btu');
    //绑定点击事件
    btu.onclick = function(){
        //ID选择器，改变CSS样式的背景颜色为红色
        $('#re').css('background', 'red');
    }
</script>
```

## 二、 jQuery中的选择器

什么是选择器？
我们在JS中，我们可以根据不同条件获取DOM：

```js
//根据ID属性值获取
document.getElementById();
//根据clss属性值获取
document.getElementsByClassName()
//根据name属性值获取
document.getElementsByName()
//根据标签名称获取
document.getElementsByTagName()
```

而在上节课，jq代码中获取指定ID的元素，我们使用的是：

`$('#re')`

jq给我们提供了各种各样获取元素的方式，而获取元素的各种方式，
我们统称为 **选择器**

因为选择器众多，我们把各种选择器分为了九个大类：

基本
层级
简单
内容
可见性
属性
表单
表单对象属性

具体用法，见手册 选择器部分；
每类选择器至少演示两个以上的用法；
预留练习记忆时间，重点是能让同学们尽可能的记忆最多的选择器；

## 三、DOM对象与jQ对象

```html
<body>
	<h1>jQuery对象与DOM对象的关系</h1>
	<ul>
		<li>导航1</li>
		<li>导航2</li>
		<li>导航3</li>
		<li>导航4</li>
	</ul>
	<p id="test">test</p>
</body>
<script>
    //没有效果并且报错，充分证明$(选择器)返回值不是一个DOM 对象
    //$('#test').style.background = 'blue';

    //没有效果并报错，证明DOM 对象也不是$()的返回值
    //var test = document.getElementById('test');
    //test.css('background','blue');

    //$()返回的到底是什么？
    //是对象，但不是DOM 对象，而是JQuery对象
    /*
     * jQuery对象与DOM对象是什么关系？
     * jQuery对象按选择器，选中1个或者多个DOM对象，
     * 把这些DOM对象，放在jQuery对象上，
     * 索引从0 开始
     * */
    //console.log($('li'));

    //jQuery对象转化为DOM对象，直接[索引]取值即可
    //$('li')[2].style.background = 'blue';
    //也可以用get(索引)方法
    //$('li').get(3).style.background = 'blue';

    //DOM对象转化为jQuery对象，直接把DOM对象当作值或者参数传给$()
    var test = document.getElementById('test');
    $(test).css('background', 'green');
</script>
```

JQ 对象与JS对象转换的应用：

```js
    $('li').click(function(){
        // this 指向原生js 
        // 想要在事件里使用JQ对象，那么必须将this转为jq对象才能使用
        $(this).css('background', 'red');
        // alert(this.innerHTML);
    });
```

## 四、 jQuery中的属性与CSS

### 1、 基本属性 attr

```html
<body>
    <input type="button" id="btu" value="点击"> <br>
    <img src="91.jpg" id="img">
</body>
<script>
    $('#btu').click(function(){
        //获取被选元素的属性值。 
        var s = $('#img').attr('src');
        alert(s);
        
		//设置被选元素的属性值
        $('#img').attr('src', '92.png')
        
		//设置被选元素的 多个 属性值
        $('#img').attr({'src':'92.png', 'alt':'sdfds'})
		
		//函数返回值为属性值
        $('img').attr('width', function(){
            return 10 * 40;
        });

        //删除元素属性
        $('img').removeAttr('src');
    });
</script>
```

**知识点：**
attr(name) ：根据属性的名称获取元素的属性值
attr(key,value) ：设置元素的属性，key属性，value属性值
attr(properties) ：一次为元素设置多个属性，要求参数是一个json对象
attr(key,fn) ：通过函数的返回值设置元素的属性
removeAttr(name) ：移除元素的属性

### 2、 class属性

```html
<head>
    <meta charset="utf-8">
    <title></title>
    <script type="text/javascript" src="jq183.js"></script>
    <style media="screen">
        td{
            border: 1px solid black;
        }
        table{
            width: 500px; height: 180px;
            border-collapse: collapse;
            background-color: #e0e0e0;
        }
        .l{
            background-color: #fff;
        }
    </style>
</head>
<body>
    <table>
        <tr>
            <td>编号</td><td>姓名</td>
            <td>性别</td><td>年龄</td>
        </tr>
        <tr>
            <td>1</td><td>刘能</td>
            <td>男</td><td>45</td>
        </tr>
    </table>
</body>
<script type="text/javascript">
    $('tr').mouseover(function(){
        //添加class值为l
        $(this).addClass('l');

        //如果有就移除，没有就添加
        // $(this).toggleClass('l');
    })
    $('tr').mouseleave(function(){
        //移除class值为l
        $(this).removeClass('l');

        //如果有就移除，没有就添加
        // $(this).removeClass('l');
    })
</script>
```

**知识点：**
addClass(class) ：为元素添加class属性
removeClass(class) ：移除元素的class属性
toggleClass(class) ：切换元素的class属性，如果有就移除，没有就添加
hasClass(class) ：判断元素是否具有某个class属性

### 3、 css样式设置

```html
<body>
    <div style="width:300px;height:300px;border:1px red solid">
            itcast
    </div>
</body>
<script>
    //获取style属性值
    alert($('div').css('width'));

    //设置style 属性值
    $('div').css('background','yellow');

    //一次性设置多个值
    $('div').css({
        width:200,
        height:200,
        background:'pink'
    });
</script>
```

**知识点**
css(name) ：根据name获取元素的css属性值
css(name,value) ：设置元素的属性值
css(properties) ：一次为元素设置多个属性值，要求参数是一个json对象

### 4、 offset位置

```html
<body>
    <div style="width:300px;height:300px;border:1px red solid">
            itcast
    </div>
</body>
<script>
    // 获取div位置
    var pos = $('div').offset();
    alert('横坐标开始位置' + pos.left);
    alert('纵坐标开始位置' + pos.top);

    //修改坐标位置
    $('div').offset({
        left:50,
        top:30
    });
</script>
```

**知识点**
offset() ：获取元素的横纵坐标，返回一个json对象，拥有left与top属性
offset(coordinates) ：设置元素位置要求是一个json对象，必须包含left与top属性

### 5、 宽高设置

```html
<body>
    <div style="width:300px;height:300px;border:1px red solid">
            itcast
    </div>
</body>
<script>
    //获取宽高值
    alert($('div').width());
    alert($('div').height());

    //设置宽高值
    $('div').width(500);
    $('div').height(500);
</script>
```

**知识点**
width() ：获取元素的宽度
width(value) ：设置元素的宽度
height() ：获取元素的高度
height(value) ：设置元素的高度

### 6、 文本 & 表单值

```html
<body>
    <input type="button" name="" value="文本值" id="i">
    <hr>
    <input type="text" name="" value="" id="u">
    <div id="d"><div><p>icast</p></div></div>
</body>
<script>
    $('#i').click(function(){
        //文本框的内容
        alert($('#u').val());//获取
        $('#u').val(222);//设置

        //文本内容
        $('#d').html('张三'); //设置
        alert($('#d').html()); //获取(包括标签)

        $('#d').text('张三');//设置
        alert($('#d').text());//获取(不包括标签)

        //html()方法和text()方法的区别
        $('#d').html('<strong>张三</strong>'); //内容会被解析
        $('#d').text('<strong>张三</strong>'); //内容原样输出

    });
</script>
```

**知识点**
val() ：获取表单元素的value值
val(val) ：设置表单元素的value值

html() ：获取元素的内容
html(val) ：设置元素的内容

text() ：获取元素的**文本**内容
text(val) ：设置元素的**文本**内容

## 五、 事件编程

### 1、 页面载入事件

05.PHP：

```php
header('Content-type:image/png');
sleep(3);
$img = imagecreatetruecolor(100, 100);
imagepng($img);
```

05-1.html

```html
<body>
<img src="05.php" alt="">
</body>
<script>
    window.onload = function(){
        alert('图片加载完成');
    }
</script>
```

**ready事件**

```html
<body>
<img src="05.php" alt="">
</body>
<script>
    //DOM 及所有资源加载完成后执行
    window.onload = function(){
        alert('图片加载完成');
    }
    //ready 当DOM加载完毕就会被触发运行
    // $().ready(function(){
    //     alert(1);
    // })

    //ready 的简化写法
    $(function(){
        alert('DOM 加载完毕');
    })
</script>
```

### 2、 jq中的事件绑定

**原生js事件绑定语法：**
DOM对象.on事件名称 = 事件的处理程序

**jq事件绑定语法：**
jq对象.事件名称(事件的处理程序);

在JS中，事件绑定一共有三种形式：
行内绑定、动态绑定、事件监听。
问题：jQuery中的事件绑定是哪一种呢？

```html
<body>
    <input type="button" value="点击">
</body>
<script>
    //jq对象 事件绑定
    $('input').click(function(){
        alert(4);
    })
    $('input').click(function(){
        alert(5);
    })
</script>
```

两次事件被先后触发，第一次绑定并没有被替换，因此可知，
jq的事件绑定是**事件监听**

### 3、jq中常用事件

**所有事件都是方法**

blur(fn) ：当失去焦点时触发
change(fn) ：当状态改变时触发
click(fn) ：当单击时触发
dblclick(fn) ：当双击时触发
focus(fn) ：当获得焦点时触发
keydown(fn) ：当键盘按下时触发
keyup(fn) ：当键盘弹起时触发
keypress(fn) ：当键盘按下时触发
load(fn) ：和ready一样都是页面载入事件
unload(fn) ：当页面关闭时触发
mousedown(fn) ：鼠标按下时触发
mouseup(fn) ：鼠标弹起时触发
mousemove(fn) ：鼠标移动时触发
mouseover(fn) ：鼠标悬浮时触发
mouseout(fn) ：鼠标离开时触发
resize(fn) ：当窗口大小改变时触发
scroll(fn) ：当滚动条滚动式触发
select(fn) ：当文本框中的文本选中时触发
submit(fn) ：当表单提交时触发

### 4、 事件切换

#### （1）

问题及效果：
京东天猫等网站首页轮播图，鼠标悬浮之上时，轮播图停止轮播效果，鼠标离开后，轮播效果继续；

知识点：
**hover(fn1,fn2)：**
当鼠标移动到一个匹配的元素上面时，会触发指定的第一个函数。
当鼠标移出这个元素时，会触发指定的第二个函数。

案例代码：

```html
<body>
    <img src="./05-6hover.gif" alt="" id="img">
</body>
<script>
    $('#img').hover(function(){//鼠标悬浮选中元素之上
        $(this).attr('src', '05-6hover.png');
    },function(){//鼠标离开选中元素
        $(this).attr('src', '05-6hover.gif');
    })
</script>
```

#### （2）

问题及效果：
点击折叠再点击展开效果，类似‘我的电脑’侧边目录；

知识点：
**toggle(fn1,fn2,fn3...，fnN)：**
点击切换事件，第一次点击执行fn1,第二次点击执行fn2,第三次点击执行fn3，
当所有函数执行完后再点击，则再次从第一个开始执行；

案例代码：

```html
<head>
    <title></title>
    <script src="./jq183.js"></script>
    <style>
        div,h2{margin: 0;padding: 10px}
        #box{width: 300px;}
        #box h2{background-color: #369;}
        #box div{border: 1px solid red; height: 200px}
    </style>
</head>
<body>
    <div id="box">
        <h2>折叠效果</h2>
        <div id="box2">
            管理员管理
        </div>
    </div>
</body>
<script>
    $('#box').toggle(function(){
        $('#box2').hide();
    },function(){
        $('#box2').show();
    })
</script>

```

### 5、 事件处理

问题及效果：
某不可描述之网站有不可描述的资源；
但点击下载时，弹出广告页面，再回去点击下载后，下载生效；

知识点：
**one('事件1 事件2 事件N',fun) ：**
 为选中元素绑定 一次性 事件(多个事件用空格隔开)；

**bind('事件1 事件2 事件N',fun) :**
为选中元素绑定一个或多个事件(多个事件用空格隔开)；
  注：jQuery 3.0中已弃用此方法，请用 on()代替。

**unbind('事件1 事件2 事件N') :**
bind 的反向操作，为选中元素 删除 一个或多个事件(多个事件用空格隔开)；
jQuery 3.0中已弃用此方法，请用 off()代替。

案例代码：

```html
<body>
    <input type="button" id="btu" value="下载">
</body>
<script>
    $('#btu').one('click', function(){ //为按钮绑定一次性点击事件
        //在新标签页打开广告
       window.open('http://www.baidu.com');
       //为元素绑定多个事件
       $(this).bind('click mouseleave', function(){
           alert('下载成功');
           //删除绑定过的事件
           $(this).unbind('mouseleave');
       })
    })
</script>
```

### 6、事件对象

#### （1） 阻止事件冒泡

问题及效果：
什么是事件冒泡？？

本意是：
div被点击时才会触发事件，但是，因为事件冒泡特性，未被点击的div也触发了事件的执行；
因此，我们需要阻止事件的冒泡行为；

事件冒泡问题代码展示：

```html
<head>
    <title></title>
    <meta charset="UTF-8">
      <script src="jq183.js"></script>
     <style>
        div{padding: 50px}
        #div3{width: 300px;height: 300px;background-color: red}
        #div2{width: 200px;height: 200px;background-color: yellow}
        #div1{width: 100px;height: 100px;background-color: blue}
     </style>
</head>
<body>
    <div id="div3">
        <div id="div2">
            <div id="div1"></div>
        </div>
    </div>
</body>
<script>
    $('#div3').click(function(){
        alert(3);
    })
    $('#div2').click(function(event){
        alert(2);
    })
    $('#div1').click(function(){
        alert(1);
    })
</script>
```

修改以上代码中 JS 部分，阻止事件冒泡；

```html
<script>
    $('#div3').click(function(ev){
        alert(3);
        ev.stopPropagation();
    })
    $('#div2').click(function(ev){
        alert(2);
        ev.stopPropagation();
    })
    $('#div1').click(function(ev){
        alert(1);
        ev.stopPropagation();
    })
</script>
```

知识点：
**event.stopPropagation()**
防止事件冒泡到DOM树上，也就是不触发的任何前辈元素上的事件处理函数。

#### （2） 阻止默认行为

问题及效果：
什么是默认行为？
如：a 标签的点击跳转、submit按钮的点击提交、选中文本的拖拽搜索等等……

有时我只是需要a标签的样式并不希望有点击跳转的效果；
用户填写完表单时，表单内容也会在前台JS中进行验证，内容不合法，数据也不能提交；

因此，在某些时候，我们需要阻止标签元素的默认行为；

案例代码：

```html
<body>
    <a href="http://www.qq.com" id="tx">腾讯链接</a> <br>
    <hr>
    <form action="05-8-2.php" method="get">
        用户名：<input type="text" name="names" value="" id="names"><br>
        <input type="submit" value="提交" id="sub">
    </form>
</body>
<script>
    $('#tx').click(function(){
        alert(1);
    })

    $('#sub').click(function(){
        if($('#names').val() == ''){
            alert('用户名不能为空');
        }
    })
</script>
```

修改上述代码的JS部分，阻止元素默认行为

```html
<script>
    $('#tx').click(function(ev){
        alert(1);
        ev.preventDefault();
    })

    $('#sub').click(function(ev){
        if($('#names').val() == ''){
            alert('用户名不能为空');
            ev.preventDefault();
        }
    })
</script>
```

知识点：
**event.preventDefault()**
阻止默认事件行为的触发。

## 六、 jQuery 中的效果

### 1、 基本效果

问题及效果：
05-6-2toggle 案例中的折叠效果并不理想，修改使其在展开或者折叠中都有过程，成动画播放效果；

案例代码：
直接修改修改 05-6-2toggle 代码，添加动画效果；

```html
<head>
    <title></title>
    <meta charset="UTF-8">
    <script src="./jq183.js"></script>
    <style>
        div,h2{margin: 0;padding: 10px}
        #box{width: 300px;}
        #box h2{background-color: #369;}
        #box div{border: 1px solid red; height: 200px}
    </style>
</head>
<body>
    <div id="box">
        <h2>折叠效果</h2>
        <div id="box2">
            管理员管理
        </div>
    </div>
</body>
<script>
    $('#box').toggle(function(){
        $('#box2').hide(
            3000,
            'swing',
            function(){
                alert(1)
            }
        );
    },function(){
        $('#box2').show(3000, 'linear', function(){});
    })
</script>
```

知识点：
**hide([speed,[fn]])** 隐藏显示的元素
speed : 三种预定速度之一的字符串("slow","normal", or "fast")或
表示动画时长的毫秒数值(如：1000);
fn:在动画完成时执行的函数。

**show([speed,[fn]])** 显示隐藏的匹配元素
speed : 三种预定速度之一的字符串("slow","normal", or "fast")或
表示动画时长的毫秒数值(如：1000);
fn:在动画完成时执行的函数。

### 2、 滑动效果

问题及效果：
图片的滑动收起与隐藏

案例代码：

```html
<body>
    <input type="button" id="down" value="slideDown">
    <input type="button" id="up" value="slideUp">
    <input type="button" id="toggle" value="slideToggle">
    <br>
    <hr>
    <img src="./06-2silde.png" id="re" >
</body>
<script>
    $('#down').click(function(){
        //滑动效果展示
        $('#re').slideDown(3000, function(){
            alert('总有刁民想害朕');
        });
    })
    $('#up').click(function(){
        //滑动效果隐藏
        $('#re').slideUp(3000, function(){
            alert('我还会回来的');
        });
    })
    $('#toggle').click(function(){
        //若隐藏则展示，若展示则隐藏
        $('#re').slideToggle(3000, function(){
            alert('你还敢点吗？');
        });
    })
</script>
```

知识点：
**slideDown([speed],[fn])** 显示
通过高度变化（向下增大）来动态地显示所有匹配的元素，在显示完成后可选地触发一个回调函数。

**slideUp([speed,[fn]])** 隐藏
通过高度变化（向上减小）来动态地隐藏所有匹配的元素，在隐藏完成后可选地触发一个回调函数。

**slideToggle([speed],[fn])** 切换
通过高度变化来**切换**所有匹配元素的可见性，并在切换完成后可选地触发一个回调函数

### 3、 淡入淡出效果

问题及效果：
图片淡入淡出效果

案例代码：

```html
<body>
    <input type="button" id="in" value="fadeIn">
    <input type="button" id="out" value="fadeOut">
    <br>
    <hr>
    <img src="./06-3fade.jpg" id="re" >
</body>
<script>
    $('#in').click(function(){
        //淡入效果展示
        $('#re').fadeIn(3000, function(){
            alert('总有刁民想害朕');
        });
    })
    $('#out').click(function(){
        //淡出效果隐藏
        $('#re').fadeOut(3000, function(){
            alert('我还会回来的');
        });
    })
</script>
```

知识点：
**fadeIn([speed],[fn])** 淡入
通过不透明度的变化来实现所有匹配元素的淡入效果，并在动画完成后可选地触发一个回调函数。

**fadeOut([speed],[fn])** 淡出
通过不透明度的变化来实现所有匹配元素的淡出效果，并在动画完成后可选地触发一个回调函数。

### 4、 自定义动画

问题及效果：
JQ中的动画效果很多，但是总有些我想要但是没有的动画；

知识点：
**animate(params,[speed],[easing],[fn])**

params:一组包含作为动画属性和终值的样式属性和及其值的集合
speed:三种预定速度之一的字符串("slow","normal", or "fast")或表示动画时长的毫秒数值(如：1000)
easing:要使用的擦除效果的名称(需要插件支持).默认jQuery提供"linear" 和 "swing".
fn:在动画完成时执行的函数，每个元素执行一次。

案例代码：

```html
<body>
    <input type="button" id="ai" value="animate">
    <br>
    <hr>
    <img src="./06-4animate.jpg" id="re" style="position:absolute">
</body>
<script>
    $('#ai').click(function(){
        //淡入效果展示
        $('#re').animate(
            {left:"900", top:"-500"},//动画属性
            3000,  //执行时长
            function(){ //执行后的回调函数
                alert('成全你');
            }
        );
    })
</script>
```

## 七、 jQuery 中的文档处理

### 1、 插入操作

#### （1） 内部插入

知识点：

**append(content)**
向匹配的元素内部追加内容。

**appendTo(content)**
把匹配的元素追加到另一个指定的元素集合中

**prepend(content)**
内容前置到匹配的元素内部；

**prependTo(content)**
把匹配的元素前置到另一个、指定的 元素 集合中。

案例代码：

```html
<body>
    <input type="button"  value="dina" id="btu">
    <div id="re">
        我是DIV
    </div>
    <p id="p">P标签</p>
</body>
<script>
    $('#btu').click(function(){
        //向匹配的元素内部追加内容。
        $('#re').append('尾部');

        //把匹配的元素追加到另一个指定的元素集合中
        $('#re').appendTo('#p');

        //内容前置到匹配的元素内部；
        $('#re').prepend('头部');

        //把匹配的元素前置到另一个、指定的 元素 集合中。
        $('#re').prependTo('#p');

    })
</script>
```

#### （2） 外部插入

知识点：
**after(content)**
在匹配的元素之后插入内容。

**before(content)**
在匹配的元素之前插入内容。

**insertAfter(content)**
把匹配的元素插入到另一个、指定的元素集合的后面。

**insertBefore(content)**
把匹配的元素插入到另一个、指定的元素集合的前面。

案例代码：
上节代码修改JS部分

```html
<script>
    $('#btu').click(function(){
        //在匹配的元素之后插入内容。
        $('#re').after('标签后');

        //在匹配的元素之前插入内容。
        $('#re').before('标签前');

        //把匹配的元素插入到另一个、指定的元素集合的后面。
        $('#re').insertAfter('#p');

        //把匹配的元素插入到另一个、指定的元素元素集合的前面。
        $('#p').insertBefore('#re');
    })
</script>
```

**注意：**
内部插入与外部插入的区别

### 2、删除

知识点：
**empty()**
删除匹配的元素集合中所有的子节点。

**remove([expr])**
从DOM中删除所有匹配的元素。

案例代码:

```html
<body>
    <input type="button" value="删除内容" id="empty">
    <input type="button" value="删除节点1" id="remove">
    <input type="button" value="删除节点2" id="re">
    <hr>
    <ul id="chi">
        <li id="lzj">辣子鸡</li>
        <li>香酥鸭</li>
        <li>糖醋鱼</li>
        <li>红烧肉</li>
    </ul>
</body>
<script>
    //删除选中节点的内容
    $('#empty').click(function(){
        $('#chi').empty();
    })

    //在DOM树中删除选中节点
    $('#remove').click(function(){
        $('#chi').remove();
    })

    //在选中节点中删除指定节点
    $('#re').click(function(){
        $('li').remove('#lzj');
    })
</script>
```

### 3、 复制(克隆)

知识点：
**clone([Even])**
克隆匹配的DOM元素
Even：一个布尔值（true 或者 false）指示事件处理函数是否会被复制。

案例代码：
修改上节代码

```html
<body>
    <input type="button" value="克隆" id="clone">
    <hr>
    <ul id="chi">
        <li id="lzj">辣子鸡</li>
        <li>香酥鸭</li>
        <li>糖醋鱼</li>
        <li>红烧肉</li>
    </ul>
</body>
<script>
    $('#lzj').click(function(){
        alert(1);
    })
    $('#clone').click(function(){
        //仅克隆内容
        $('#lzj').clone().appendTo('#chi');
        //克隆内容与事件
        $('#lzj').clone(true).appendTo('#chi');
    })

</script>
```

### 4、 替换

知识点：
**replaceWith(content)**
将所有匹配的元素替换成指定的HTML或DOM元素。

**html([val])**
val 有值，则用于设定HTML内容的值，没有则获取内容值；

案例代码：

```html
<body>
    <input type="button" value="替换DOM" id="replace">
    <input type="button" value="替换内容" id="html">
    <hr>
    <ul id="chi">
        <li id="lzj">辣子鸡</li>
        <li>香酥鸭</li>
        <li>糖醋鱼</li>
        <li>红烧肉</li>
    </ul>
</body>
<script>
    $('#replace').click(function(){
        var t = '<li>西湖牛肉羹</li>'
        //替换选中节点的DOM
       $('#lzj').replaceWith(t);
    })

    $('#html').click(function(){
        //替换选中节点的内容
       $('#lzj').html('蒜蓉西兰花');
    })
</script>
```

### 5、包裹

知识点：
**wrap(html|ele|fn)**
把所有匹配的元素用其他元素的结构化标记包裹起来。

**unwrap()**
移出选中元素的父元素

**wrapAll(html|ele)**
将所有匹配的元素用单个元素包裹起来

**wrapInner(html|ele|fn)**
将每一个匹配的元素的子内容(包括文本节点)用一个HTML结构包裹起来

案例代码：

```html
<body>
    <input type="button" value="wrap" id="wrap">
    <input type="button" value="wrapAll" id="wrapAll">
    <input type="button" value="unwrap" id="unwrap">
    <input type="button" value="wrapInner" id="wrapInner">
    <hr>
    <div>海贼王</div>
    <div>火影忍者</div>
    <div>龙猫</div>
    <div><p>千与千寻</p></div>
</body>
<script>
    $('#wrap').click(function(){
        $('div').wrap('<strong></strong>');
    })
    $('#wrapAll').click(function(){
        $('div').wrapAll('<strong></strong>');
    })
    $('#unwrap').click(function(){
        $('p').unwrap();
    })
     $('#wrapInner').click(function(){
        $('div').wrapInner('<i></i>');
    })
</script>
```

### 6、查找

问题及效果：
将选择器以 jq方法调用 形式实现；

知识点：
eq(index) ：根据元素的index索引来查找元素
filter(expr) ：筛选操作，$(‘div’).filter(‘.cls1’);
not(expr) ：匹配除指定选择器以外的其他元素
children([expr]) ：获取当前元素下的所有子元素
find(expr) ：获取当前元素下的所有后代元素
next([expr]) ：获取当前元素下紧邻的下一个元素
prev([expr]) ：获取当前元素上紧邻的上一个元素
parent([expr]) ：获取当前元素的父元素
siblings([expre]) ：获取当前元素的所有同级兄弟元素

案例代码：

```html
<body>
    <input type="button" value="eq" id="eq">
    <div>div111</div>
</body>
<script>
    $('#eq').click(function(){
        $('div').eq(0).html('div');
    })
</script>
```

### 7、 综合案例-任务清单

问题及效果：

类似奇妙清单、todolist等任务应用；

案例代码：

```html
    <head>
        <title></title>
        <meta charset="UTF-8">
            <script src="jq183.js"></script>   
         <style>
            #box{
                width: 400px;
                margin: 0 auto;
            }
            #show{
                font-size: 12px;
            }
            span{
                font-size: 12px;
                background-color: 	#F0FFF0;
            }
            s{
                font-size: 12px;
                color: 	#7B7B7B;
                background-color: #F0F0F0;
            }

         </style>
    </head>
    <body>
        <div id="box">
            <!--添加任务  -->
            <input type="text" value="" style="width:300px" id="list_value">
            <input type="button" value="添加任务" id="add">
            <!--任务列表  -->
            <div class="lists">
                 <div>
                    <input type="checkbox"><span>明天去吃麻辣小龙虾</span>
                </div>
            </div>
            <hr>
            <!--显示与隐藏  -->
            <div>
                <p id="show" >显示已完成任务</p>
            </div>
            <!--已完成任务的列表  -->
            <div id="hide" style="display:none">
                 <div>
                    <s>撸串，撸666串</s>  
                </div>
            </div>

        </div>
    </body>
    <script>
        //添加新任务
        $('#add').click(function(){
            //获取表单内容
            var val = $('#list_value').val();
            //表单内容不能为空
            if(val != ''){
                //创建任务
                var lists = '<div><input type="checkbox" id="t2"><span>' + val + '</span></div>';
                //添加任务
                $('.lists').prepend(lists);
                //为任务绑定事件
                $('#t2').on('click', function(){
                    //取值
                    var v = $(this).next().html();
                    //创建已完成任务
                    var o = '<div><s>' + v + '</s></div>';
                    //添加到已完成任务列表
                    $('#hide').prepend(o);
                    //找到父级元素并删除
                    $(this).parent().remove();
                });

                //清空表单
                $('#list_value').val('');
            }else{
                alert('不能空');
            }
        })

        //已完成 任务的显示和隐藏
        $('#show').toggle(function(){
            //显示已完成任务
            $('#hide').show(500);
            //修改按钮标识
            $(this).html('隐藏已完成任务');            
        },function(){
            $('#hide').hide(500);
            $(this).html('显示已完成任务')
        })
    </script>
```

## 八、 插件

**问题及效果:**
想实现商城购物车中全选与反选功能，发现jq中并没有提供相应功能；
类似这种jq中没有的功能，我们都可以通过插件的形式自己实现，并在jq中使用；

### 1、 为元素扩展新方法

基本语法:

`$.fn.extend(ob)或者 $、jQuery.fn.extend(ob)`

ob： JS对象，例：

```js
$.fn.extend({
	ex1.function(){},
	ex2.function(){},
});
```

**案例代码：**

```html
<body>
    <div id="box">JQ插件</div>
</body>
<script>
    $.fn.extend({
        ex1:function(color){
            this.css('background', color);
        }
    });
    //使用
    $('#box').ex1('yellow');
</script>
```

### 2、扩展jq对象本身

**知识点：**
**jQuery.extend(ob) 或者 $.extend(ob)**
ob： JS对象，

例：

```html
$.extend({
	ex1.function(){},
	ex2.function(){},
});

```

案例代码：

```html
<script>
    $.extend({
        min: function(a, b) { return a < b ? a : b; },
        max: function(a, b) { return a > b ? a : b; }
    });
    //使用
    alert($.min(1,3));
</script>
```

### 3、 综合案例

```html
    <body>
        <input type="button" value="全选" id="all"> 
        <input type="button" value="全不选" id="unall"> 
        <input type="button" value="反选" id="un"> 
        <hr>
        <input type="checkbox" value=""> HTML  <br>
        <input type="checkbox" value=""> Javascript <br> 
        <input type="checkbox" value=""> PHP <br> 
        <input type="checkbox" value=""> Python <br> 
        <input type="checkbox" value=""> Java <br> 
        <input type="checkbox" value=""> C/C++ <br> 
    </body>
    <script>
        $.fn.extend({
            all:function(){
                this.attr('checked', true);
            },
            unall:function(){
                this.attr('checked', false);
            },
            un:function(){
                for(var i = 0; i < this.length; i++){
                    if(this[i].checked == true){
                        this[i].checked = false;
                    }else{
                        this[i].checked = true;
                    }
                }
            }
        });
        //使用
        $('#all').click(function(){
            $(':checkbox').all();
        });
        $('#unall').click(function(){
            $(':checkbox').unall();
        });
        $('#un').click(function(){
            $(':checkbox').un();
        });
    </script>
```

### 4、 each 方法

问题及效果:
在上一节插件中有个反选的功能，本质上就是对选中的每个对象进行遍历操作；
jq原生有没有类似的功能呢？

知识点：
**each(callback)**
以每一个匹配的元素作为上下文来执行一个函数。

案例代码：

拿到上节课代码进行修改

```html
<script>
    $('#un').click(function(){
        $(':checkbox').each(function(){
            //判断并取反
            if(this.checked == true){
                this.checked = false;
            }else{
                this.checked = true;
            }
            //直接将值取反
            // this.checked = !this.checked;
        });
    });
</script>
```

## 九、 jQ中的Ajax

### 1、 认识jQ中ajax的封装

jQ 对于ajax的封装有两层实现；
$.ajax 为底层封装实现；
基于 `$.ajax` ，分别实现了`$.get` 与`$.post` 的高层封装实现；

### 2、 ajax 的底层实现

基本语法：
**$.ajax(obj)**

对象的参数设置及含义：

**async：** 	     	布尔类型，代表是否异步，true代表异步，false同步，默认为true
**cache：**      	是否缓存，布尔类型，true代表缓存，false代表不缓存，默认为true
**complete：**    	当Ajax状态码（readyState）为4的时候所触发的回调函数
**contentType：** 	发送信息至服务器时内容编码类型；(默认: "application/x-www-form-urlencoded") 
**data：** 			要求是一个字符串格式，Ajax发送时所传递的数据
**dataType：** 		期待的返回值类型，可以是text，xml，json，默认为text类型
**success：** 		当Ajax状态码为4且响应状态码为200时所触发的回调函数
**type：** 			Ajax发送网络请求的方式，(默认: "GET")；
**url：** 			请求的url地址

案例代码：

**GET 请求**

```html
<body>
    <input type="button" value="点击" id="btu">
</body>
<script>
    $('#btu').click(function(){
        //get请求
        $.ajax({
            url:'9-2.php?id=11',
            success:function(data){
                alert(data);
            }
        });
    });
</script>
```

**POST 请求**

```html
//POST请求及同步异步
$.ajax({
    url:'9-2.php',
    type:'post',
    data:'id=1111',
    success:function(data){
        alert(data);
    },
    // async:false,
});
// alert(22); //检验同步异步
```

**设置返回值类型**

```html
//设置返回值类型
$.ajax({
    url:'9-2.php?id=11',
    success:function(data){
        alert(data.a);
    },
    //jq接到后台的json字符串，转成对象后呈现给用户
    dataType:'json',
});
```

**PHP后台代码**

```php
// sleep(3);
if($_GET['id'] == 11)
{  //get
 //if($_POST['id'] == 11)
 //{   post
 //    echo 'jq_ajax';
    echo json_encode(['a' => '2222']); //json 返回
}else
{
    echo 'hhh';
}
```

### 3、 ajax 的高层实现

#### （1） GET 应用

基本语法：
**$.get(url, [data], [callback], [type])**

url:待载入页面的URL地址
data:待发送 Key/value 参数。
callback:载入成功时回调函数。
type:返回内容格式，xml, html, script, json, text, _default。

案例代码：

```html
<script>
    $('#btu').click(function(){
        $.get('9-2.php', function(data){
            alert(data.a);
        }, 'json');
    });
</script>
```

但是注意：IE浏览器存在缓存问题；
**解决缓存问题** 修改：

```
<script>
    $('#btu').click(function(){
        var da = {_:new Date().getTime()};
        $.get('9-2.php', da, function(data){
            alert(data.a);
        }, 'json');
    });
</script>
```

#### （2） POST 应用

**$.post(url, [data], [callback], [type])**
url:发送请求地址。
data:待发送 Key/value 参数。
callback:发送成功时回调函数。
type:返回内容格式，xml, html, script, json, text, _default。

案例代码：

```html
<script>
    $('#btu').click(function(){
        $.post('9-2.php',
        {id:'11'},
        function(data){
            alert(data.a);
        }, 'json');
    });
</script>
```

## 十、 jQ中的跨域问题

Ajax技术受到浏览器同源策略的限制，禁止从一个域上向另外一个域发送请求。
也就是说，受到请求的 URL 的域必须与当前 Web 页面的域相同。这意味着浏览器隔离来自不同源的内容，以防止它们之间的操作。

后台不同域下的PHP代码

```php
$arr = ['a' => 1, 'b' => 'san', 'c' => 'wu', 'd' => 4];
$str = json_encode($arr);
echo $_GET['fn'] . "($str)";
```

前端jq跨域的三种用法

```html
<script>
    $('#btu').click(function(){
        //$.ajax 方法的jsonp跨域
        $.ajax({
            url:'http://bbs.com/1.php?fn=?',
            dataType:'jsonp',
            success:function(data){
                alert(data.b);
            }
        });

        //$.get 方法的jsonp跨域
        $.get('http://bbs.com/1.php?fn=?', function(data){
            alert(data.b);
        }, 'jsonp');
        
        //  $.getJSON 方法的jsonp跨域
        $.getJSON(
            'http://bbs.com/1.php?fn=?',
            function(data){
                alert(data.b);
            },
        );
    });
</script>
```

## 十一、 第三方插件

### 1、 分页插件

找到适合自己的插件下载，解压后将无关文件删除；
本质上来说，只要引入js文件就可以使用了，但有时也需要样式表等文件，具体看需求；

http://www.jq22.com/jquery-info13734

打开示例代码，查看插件的使用方式；

```js
var options = {
    "id": "page",	//显示页码的元素
    "data": datas,	//显示数据
    "maxshowpageitem": 2,	//最多显示的页码个数
    "pagelistcount": 2,		//每页显示数据的个数
    "callBack": function(result){
        var cHtml = "";
        for(var i = 0; i < result.length; i++){
            cHtml += "<li>" + result[i].name + "</li>";	//处理数据
        }
        $("#demoContent").html(cHtml);//将数据增加到页面中
    }
};
page.init(datas.length. 1. options);
```

根据示例代码实现分页:
page.php

```php
mysql_connect('localhost', 'root', '123456');
mysql_query('use test');
mysql_query('set names utf8');

//SQL 语句
$sql = "select * from test ";
$res = mysql_query($sql);
$data = [];
while($row = mysql_fetch_assoc($res))
{
    $data[] = $row;
}

echo json_encode($data);
```

page.html

```html
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link href="page.css" type="text/css" rel="stylesheet"/>
    <script src="http://www.jq22.com/jquery/jquery-1.10.2.js"></script>
    <script type="text/javascript" src="page.js"></script>
</head>
<body>
 <ul id="demoContent"></ul>
 <ul class="page" id="page"></ul>
</body>
</html>
<script type="text/javascript">
$.get('page.php', function(data){
    datas = data;
    console.log(datas);
    options = {
	"id": "page",//显示页码的元素
	"data": datas,//显示数据
    "maxshowpageitem": 3,//最多显示的页码个数
    "pagelistcount": 2,//每页显示数据个数
    "callBack": function(result){
            var cHtml="";
            for(var i = 0; i < result.length; i++){
                cHtml += "<li>" + result[i].name + "</li>";//处理数据
            }
            $("#demoContent").html(cHtml);//将数据增加到页面中
        }
    };
    page.init(datas.length, 1, options);
}, 'json')

</script>
```

### 2、 旋转插件

http://www.jqueryrotate.com/

基本使用：

```html
<body>
    <img src="ie.png" id="img">
</body>
<script src="../jq183.js"></script> 
<script src="jQueryRotate.js"></script>
<script>
    $("#img").rotate({
        bind:{
            //绑定鼠标悬浮旋转事件
            mouseover : function() {
				//从当前角度旋转至180度
				$(this).rotate({animateTo:180});
            },
            //绑定鼠标离开旋转事件
            mouseout : function() {
				//从当前角度旋转至0度
                $(this).rotate({animateTo:0});
            }
        }
    });
</script>
```

抽奖案例：

```html
<head>
    <title></title>
    <meta charset="UTF-8">
      <script src="../jq183.js"></script> 
      <script src="jQueryRotate.js"></script> 
      <style>
        .rotate-bg{
            width: 509px;
            height: 509px;
            background: url(ly-plate.png);
            position: absolute;
            top: 0;
            left: 0;
        }
        .lottery-star{
            width:214px;
            height:214px;
            position:absolute;
            top:150px;
            left:147px;
        }
      </style>
</head>
<body>
    <div class="rotate-bg"></div>
    <div class="lottery-star">
        <img src="rotate-static.png" id="lotteryBtn">
    </div>
</body>
<script>
    $('#lotteryBtn').rotate({
        bind:{
            click:function(){
                var d = Math.random()*360;
                if(0 < d && d <= 45){
                    var text = '再接再励';
                }else if(45 < d && d <= 90){
                    var text = '恭喜获得2等奖';
                }else if(90 < d && d <= 180){
                    var text = '再接再励';
                }else if(180 < d && d <= 225){
                    var text = '恭喜获得3等奖';
                }else if(225 < d && d <= 315){
                    var text = '再接再励';
                }else if(315 < d && d < 360){
                    var text = '恭喜获得yi等奖';
                }
                var zhuan = d + 1080 + 180;
                    $("#lotteryBtn").rotate({
                        angle:0, 
                        duration: 5000,
                        animateTo: zhuan, //angle是图片上各奖项对应的角度，1440是我要让指针旋转4圈。所以最后的结束的角度就是这样子^^
                        callback:function(){
                            alert(text)
                        }
                }); 
            }},
    });
</script>
```

### 3、 百度Echarts图表工具库

**介绍：**
ECharts，一个纯 Javascript 的图表库，可以流畅的运行在 PC 和移动设备上，
兼容当前绝大部分浏览器（IE8/9/10/11，Chrome，Firefox，Safari等），
底层依赖轻量级的 Canvas 类库 ZRender，提供直观，生动，可交互，可高度个性化定制的数据可视化图表。
ECharts3 中更是加入了更多丰富的交互功能以及更多的可视化效果，并且对移动端做了深度的优化。

**使用：**

官网： http://echarts.baidu.com/

根据教程，首先下载相应代码包：

引入 ECharts

```html
<head>
    <meta charset="utf-8">
    <!-- 引入 ECharts 文件 -->
    <script src="echarts.min.js"></script>
</head>

```

**绘制一个简单的图表**

在绘图前我们需要为 ECharts 准备一个具备高宽的 DOM 容器。

```html
<body>
    <!-- 为 ECharts 准备一个具备大小（宽高）的 DOM -->
    <div id="main" style="width: 600px;height:400px;"></div>
</body>
```

然后就可以通过 echarts.init 方法初始化一个 echarts 实例并通过 setOption 方法生成一个简单的柱状图

```html
<script type="text/javascript">
    // 基于准备好的dom，初始化echarts实例
    var myChart = echarts.init(document.getElementById('main'));

    // 指定图表的配置项和数据
    var option = {
        title: {
            text: 'ECharts 入门示例'
        },
        tooltip: {},
        legend: {
            data:['销量']
        },
        xAxis: {
            data: ["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
        },
        yAxis: {},
        series: [{
            name: '销量',
            type: 'bar',
            data: [5, 20, 36, 10, 10, 20]
        }]
    };

    // 使用刚指定的配置项和数据显示图表。
    myChart.setOption(option);
</script>
```

注意： 代码中的 option 变量值 为 图标配置项，具体含义可查看手册 **配置项**

**向后台动态获取数据，形成图标**
复制上节代码，修改JS部分

```html
<script>
    var myChart = echarts.init(document.getElementById('main'));
     // 指定图表的配置项和数据
    myChart.setOption({
        title: {
            text: '姓名及年龄分布',
        },
        tooltip: {show:true},
        legend: {
            data:['姓名及年龄'],
        },
        xAxis: {
            splitNumber:'20',
            data: []
        },
        yAxis: {},
        series: [{
            name: '姓名及年龄',
            type: 'bar',
            data: []
        }]
    });
    $.get('d2.php',function(das){
            // 使用刚指定的配置项和数据显示图表。
            myChart.setOption({
                xAxis: {
                    data: das.name
                },
                series: [{
                    data: das.age
                }]
            });
        },'json'
    )
</script>
```

**后台PHP代码**

```php
mysql_connect('localhost', 'root', '123456');
mysql_query('use test');
mysql_query('set names utf8');

//SQL 语句
$sql = "select * from test where id<14";
$res = mysql_query($sql);
$data = [];
while($row = mysql_fetch_assoc($res))
{
    $data[] = $row;
}
//组合制作 echarts 所需要的数据结构
$d = [];
foreach($data as $v)
{
    $d['name'][] = $v['name'];
    $d['age'][] = $v['age'];
}

echo json_encode($d);
```

## 十二、CDN加速

假设我们的服务器在北京，广州的用户来访问我们的网站，
我们的代码需要跨越2000+公里下载到用户的浏览器；

如果将我们的代码放在各大城市，根据用户所在地去距离用户最近的地方下载，那么我们网站的打开速度将会大大提升；

这就是所谓的CDN加速的基本原理；

而像 jQ 这样的公用代码库，也有各大公司提供的相应CDN节点，而且是免费的；

http://www.bootcdn.cn
http://cdn.code.baidu.com

