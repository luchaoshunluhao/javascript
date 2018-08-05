## 一、概述

Bootstrap 是由 Twitter 公司(全球最大的微博)的两名技术工程师研发的一个基于HTML、CSS、JavaScript 的开源框架。该框架代码简洁、视觉优美，可用于快速、简单地构建基于 PC 及移动端设备的 Web 页面需求。
Bootstrap 最为重要的部分就是它的响应式布局，通过这种布局可以兼容 PC 端、PAD以及手机移动端的页面访问。
Bootstrap2中，对某些关键部分增加了对移动设备友好的样式,Bootstrap3是移动设备优先的;

Bootstrap 下载及演示：
国内文档翻译官网：[http://www.bootcss.com](http://www.bootcss.com "http://www.bootcss.com")

#### 特点

1.跨设备、跨浏览器
2.响应式布局
3.提供的全面的组件（导航栏，标签，按钮等）
4.内置 jQuery 插件
5.支持 HTML5、CSS3

## 二、写个小例子

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link rel="stylesheet" href="bootstrap.min.css">
</head>
<body>
<input type="button" class="btn btn-info" value="提交">
<input type="button" class="" value="提交">
</body>
</html>
```

## 三、排版样式

Bootstrap 全局 CSS 样式中的排版样式，包括了标题、页面
主体、对齐、列表等常规内容。
Bootstrap 将全局 font-size 设置为 14px，line-height 行高设置为 1.428(即20px)；
\<p>段落元素被设置等于 1/2 行高(即 10px)；

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <!--引入与不引入bootstrap,查看页面效果，-->
    <link rel="stylesheet" href="bootstrap.min.css">
</head>
<body>
<input type="button" class="btn btn-info" value="提交">
<input type="button" class="" value="提交">
<!--页面主体-->
<p>穆罕默德 伊斯兰教创始人，政治领袖</p>
<p class="lead">牛顿 发现日光十七色混合的人</p>
<p>耶稣基督 基督教创始人</p>
<p>释迦牟尼 佛教创始人</p>
<p>孔丘 儒教创始人</p>

<!--标题-->
<h1>保罗 基督教最伟大的使徒</h1>
<h2>蔡伦 纸的发明人</h2>
<h3>古登堡 活字印刷及活字印刷法的创始人</h3>
<h4>Bootstrap 框架</h4>
<h5>Bootstrap 框架</h5>
<h6>Bootstrap 框架</h6>

<!--内联文本元素-->
<del>我是del</del>
<s></s>
<ins>Bootstrap 框架</ins>
<small>Bootstrap 框架</small>
<strong>Bootstrap 框架</strong>
<em>Bootstrap 框架</em>

<!--对齐-->
<p class="text-left"> 居左</p>
<p class="text-center">居中</p>
<p class="text-right">居右</p>
<p class="text-justify">两端对齐,支持度不佳</p>
<p class="text-nowrap">不换行</p>
</body>
</html>
```

## 四、表格

Bootstrap 提供了一些丰富的表格样式供开发者使用。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link rel="stylesheet" href="bootstrap.min.css">
</head>

<!--
响应式表格
表格父元素设置响应式,小于 768px 出现边框
<body class="table-responsive">
-->

<body class="table-responsive">

<!--实现基本的表格样式-->
<!--<table class="table">-->

<!--条纹状表格-->
<!--<table class="table table-striped">-->

<!--带边框的表格-->
<!--<table class="table table-bordered">-->

<!--悬停鼠标-->
<table class="table table-hover">

    <thead>
    <!--
    状态类
    active 鼠标悬停在行或单元格上
    success 标识成功或积极的动作
    info   标识普通的提示信息或动作
    warning 标识警告或需要用户注意
    danger 表示危险或潜在的带来负面影响的动作
    -->
    <tr class="success">
        <th>编号</th>
        <th>姓名</th>
        <th>性别</th>
        <th>年龄</th>
    </tr>
    </thead>
    <tbody>

    <!--隐藏某一行-->
    <tr class="sr-only">
        <td>1</td>
        <td>张三</td>
        <td>男</td>
        <td>50</td>
    </tr>
    <tr>
        <td>2</td>
        <td>李四</td>
        <td>女</td>
        <td>48</td>
    </tr>
    <tr>
        <td>3</td>
        <td>王五</td>
        <td>男</td>
        <td>52</td>
    </tr>
    </tbody>
</table>

<!--可作为按钮使用的标签或元素-->
<!--转化成普通按钮-->
<a href="###" class="btn btn-default">Link</a>
<input type="button" class="btn btn-default" value="Input">
<button class="btn btn-default">Button</button>


<!--预定义样式-->
<!--一般信息-->
<!--
btn-default 默认样式btn-default 默认样式
btn-success 成功样式
btn-info    一般信息样式
btn-warning 警告样式
btn-danger  危险样式
btn-primary 首选项样式
btn-link    链接样式
-->
<button class="btn btn-success">Button</button>


<!--从大到小的尺寸-->
<button class="btn btn-info btn-lg">Button</button>
<button class="btn btn-info">Button</button>
<button class="btn btn-info btn-sm">Button</button>
<button class="btn btn-info btn-xs">Button</button>

<!--激活状态-->
<button class="btn btn-info btn-block active">Button</button>

<!--禁用状态-->
<button class="btn btn-info btn-block disabled">Button</button>
</body>
</html>
```

## 五、表单和图片

**基本格式**

```html
<form class="form-horizontal">
    <div class="form-group">
        <label class="col-sm-2 control-label">电子邮件</label>
        <div class="col-sm-10">
            <input type="email" class="form-control" placeholder="请输入您的电子邮件">
        </div>
    </div>
    <div class="form-group">
        <label class="col-sm-2 control-label">密码</label>
        <div class="col-sm-10">
            <input type="password" class="form-control" placeholder="请输入您的密码">
        </div>
    </div>
</form>
```

注:只有正确设置了输入框的 type类型,才能被赋予正确的样式。支持的输入框控件包括:text、password、datetime、datetime-local、date、month、time、week、number、email、url、search、tel 和 color。

**内联表单**
让表单左对齐浮动,并表现为 inline-block 内联块结构

```html 
 <form class="form-inline"> 
```

注:当小于768px,会恢复独占样式

**表单合组**
前后增加片段

```html
<div class="input-group">
    <div class="input-group-addon">¥</div>
    <input type="text" class="form-control">
    <div class="input-group-addon">.00</div>
</div>
```

**复选框和单选框**
设置复选框,在一行

```html
<div class="checkbox">
    <input type="checkbox">体育
</div>
<div class="checkbox">
    <input type="checkbox">音乐
</div>
```

**设置禁用的复选框**

```html
<div class="checkbox disabled">
    <input type="checkbox" disabled>音乐
</div>
```



**下拉列表**

```html
<select class="form-control">
    <option>1</option>
    <option>2</option>
    <option>3</option>
    <option>4</option>
</select>
```

**图片形状 三种**

```html
<img src="img/pic.png" alt="图片" class="img-rounded">
<img src="img/pic.png" alt="图片" class="img-circle">
<img src="img/pic.png" alt="图片" class="img-thumbnail">
```

**响应式图片**

```html
 <img src="img/pic.png" alt="图片" class="img-responsive"> 
```

## 六、栅格系统

移动设备优先

```html
<meta name="viewport" content="width=device-width, initial-scale=1,maximum-scale=1, user-scalable=no">
触屏设备 添加 meta 属性user-scalable=no 可以禁用其缩放功能。视情况而定
```

栅格系统用于通过一系列的行（row）与列（column）的组合来创建页面布局，随着屏幕尺寸的增加，系统会自动分为最多12列。
行（row）必须包含在 .container中，内容应当放置于列（column）内，并且，只有列（column）可以作为行（row）的直接子元素。
栅格系统中的列是通过指定1到12的值来表示其跨越的范围。例如，三个等宽的列可以使用三个 .col-xs-4 来创建。

```html
<div class="container-fluid">
    <div class="row">
        <div class="col-md-8">.col-md-8</div>
        <div class="col-md-4">.col-md-4</div>
    </div>
    
    <div class="row">
        <div class="col-sm-4">.col-md-4</div>
        <div class="col-sm-4">.col-md-4</div>
        <div class="col-sm-4">.col-md-4</div>
    </div>
</div>
```

## 七、辅组类和响应式工具

辅助类
1.情景文本颜色

```html
各种色调的字体
<p class="text-muted">柔和灰</p>
<p class="text-primary">主要蓝</p>
<p class="text-success">成功绿</p>
<p class="text-info">信息蓝</p>
<p class="text-warning">警告黄</p>
<p class="text-danger">危险红</p>

各种色调的背景
<p class="bg-primary">主要蓝</p>
<p class="bg-success">成功绿</p>
<p class="bg-info">信息蓝</p>
<p class="bg-warning">警告黄</p>
<p class="bg-danger">危险红</p>
```

3.关闭按钮

```html
<button type="button" class="close">&times;</button>
```

三角符号(将字体文件夹，放入项目中，才能显示其他图标)

```html
<span class="caret"></span>
```

屏幕尺寸大小的激活和隐藏

```html
<div class="visible-xs-block">超小屏幕激活显示</div>

<div class="hidden-xs">超小屏幕激活隐藏</div>
```

## 八、导航组件

```html
基本导航标签页
<ul class="nav nav-tabs">
胶囊式导航
<ul class="nav nav-pills">
垂直胶囊式导航
<ul class="nav nav-pills nav-stacked">
导航两端对齐
<ul class="nav nav-tabs nav-justified">
    <li class="active"><a href="#">首页</a></li>
    <li><a href="#">资讯</a></li>
    <li><a href="#">产品</a></a></li>
    <li><a href="#">关于</a></li>
</ul>
```

## 九、路径、分页和徽章组件

路径组件也叫做面包屑导航。

```html
路径组件做面包屑导航。
面包屑导航
<ol class="breadcrumb">
    <li><a href="#">首页</a></li>
    <li><a href="#">产品列表</a></li>
    <li class="active">韩版 2015 年羊绒毛衣</li>
</ol>

分页组件
默认分页
<ul class="pagination">
    <li><a href="#">&laquo;</a></li>
    <li><a href="#">1</a></li>
    <li><a href="#">2</a></li>
    <li><a href="#">3</a></li>
    <li><a href="#">4</a></li>
    <li><a href="#">5</a></li>
    <li><a href="#">&raquo;</a></li>
</ul>
首选项和禁用
<li class="active"><a href="#">1</a></li>
<li class="disabled"><a href="#">2</a></li>
翻页效果
<ul class="pager">
    <li><a href="#">上一页</a></li>
    <li><a href="#">下一页</a></li>
</ul>
对齐翻页链接
<ul class="pager">
    <li class="previous"><a href="#">上一页</a></li>
    <li class="next"><a href="#">下一页</a></li>
</ul>
//翻页项禁用
<li class="previous disabled"><a href="#">上一页</a></li>


徽章
未读信息数量徽章
<a href="#">信息 <span class="badge">10</span></a>
按钮中使用徽章
<button class="btn btn-success">
    提交 <span class="badge">3</span>
</button>

激活状态自动适配色调
<ul class="nav nav-pills">
    <li class="active">
        <a href="#">首页 <span class="badge">2</span></a>
    </li>
    <li><a href="#">资讯</a></li>
</ul>
```

## 十、巨幕、页头、缩略图、警告框等组件

```html
巨幕组件主要是展示网站的关键性区域。

<div class="jumbotron">
    <div class="container">
        <h2>网站标题</h2>
        <p>这是一个学习性的网站!</p>
        <p><a href="#" class="btn btn-default">更多内容</a></p>
    </div>
</div>

<div class="container">
    <div class="jumbotron">
        <h2>网站标题</h2>
        <p>这是一个学习性的网站!</p>
        <p><a href="#" class="btn btn-default">更多内容</a></p>
    </div>
</div>

页头组件
增加一些空间
<div class="page-header">
    <h1>大标题 <small>小标题</small></h1>
</div>

缩略图组件
缩略图配合响应式
<div class="container"><div class="row">
    <div class="col-xs-6 col-md-3 col-sm-4">
        <div class="thumbnail">
            <img src="pic.jpg" alt="">
        </div>
    </div>
    <div class="col-xs-6 col-md-3 col-sm-4">
        <div class="thumbnail">
            <img src="pic.jpg" alt="">
        </div>
    </div>
    <div class="col-xs-6 col-md-3 col-sm-4">
        <div class="thumbnail">
            <img src="pic.jpg" alt="">
        </div>
    </div>
    <div class="col-xs-6 col-md-3 col-sm-4">
        <div class="thumbnail">
            <img src="pic.jpg" alt="">
        </div>
    </div>

警告框组件是一组预定义消息。
//基本警告框
<div class="alert alert-success">Bootstrap</div>
<div class="alert alert-info">Bootstrap</div>
<div class="alert alert-warning">Bootstrap</div>
<div class="alert alert-danger">Bootstrap</div>
//带关闭的警告框
<div class="alert alert-success">
    Bootstrap
    <button type="button" class="close" data-dismiss="alert">
        <span>&times;</span>
    </button>
</div>
```

## 十一、Well和进度条 组件

```html
Well 组件
这个组件可以实现简单的嵌入效果。
嵌入效果
<div class="well">
    Bootstrap
</div>
有 lg 和 sm 两种可选值
<div class="well well-sm">
    Bootstrap
</div>

进度条组件
进度条组件为当前工作流程或动作提供时时反馈。
//基本进度条
<div class="progress">
    <div class="progress-bar" style="width: 60%;">60%</div>
</div>
//最低值进度条
<div class="progress">
    <div class="progress-bar" style="min-width:20px">0%</div>
</div>
//结合情景的进度条
<div class="progress">
    <div class="progress-bar progress-bar-success" style="min-width:20px;width:60%">60%</div>
</div>
//条纹状,IE10+支持
<div class="progress">
    <div class="progress-bar progress-bar-success progress-bar-striped" 
    style="min-width:20px;width:60%">60%</div>
</div>
//动画效果
<div class="progress">
    <div class="progress-bar progress-bar-success progress-bar-striped
active" style="min-width:20px;width:60%">60%</div>
</div>

//堆叠效果
<div class="progress">
    <div class="progress-bar progress-bar-success"
         style="min-width:20px;width:35%">35%</div>
    <div class="progress-bar progress-bar-warning"
         style="min-width:20px;width:20%">20%</div>
    <div class="progress-bar progress-bar-danger"
         style="min-width:20px;width:10%">10%</div>
</div>

```

## 十二、列表组、面板

```html
列表组组件用于显示一组列表的组件。
基本实例
<ul class="list-group">
    <li class="list-group-item">1.这是起始</li>
    <li class="list-group-item">1.这是起始</li>
    <li class="list-group-item">1.这是起始</li>
    <li class="list-group-item">1.这是起始</li>
</ul>
列表项带勋章
<li class="list-group-item">
    1.这是起始<span class="badge">10</span>
</li>
链接和首选
<div class="list-group">
    <a href="#" class="list-group-item active">
        1.这是起始<span class="badge">10</span>
    </a>
    <a href="#" class="list-group-item">2.这是第二条数据</a>
    <a href="#" class="list-group-item">3.这是第三排信息</a>
    <a href="#" class="list-group-item">4.这是末尾</a>
</div>
按钮式列表
<div class="list-group">
    <button class="list-group-item active">
        1.这是起始 <span class="badge">10</span>
    </button>
    <button class="list-group-item">2.这是第二条数据</button>
    <button class="list-group-item">3.这是第三排信息</button>
    <button class="list-group-item">4.这是末尾</button>
</div>


面板组件就是一个存放内容的容器组件。
基本实例
<div class="panel panel-default">
    <div class="panel-body">
        这里是详细内容区!
    </div>
</div>
带标题容器的面板
情景效果:default、success、info、warning、danger、primary
<div class="panel panel-default">
    <div class="panel-heading">
        面板标题
    </div>
    <div class="panel-body">
        这里是详细内容区!
    </div>
</div>
带注脚的面板
<div class="panel-footer">
    这里是底部
</div>
表格类面板
<div class="panel panel-default">
    <div class="panel-heading">
        表格标题
    </div>
    <div class="panel-body">
        <p>这里是表格标题的详细内容!</p>
    </div>
    <table class="table">
        <tr>
            <th>1</th>
            <th>2</th>
            <th>3</th>
        </tr>
        <tr>
            <td>1</td>
            <td>2</td>
            <td>3</td>
        </tr>
    </table>
</div>
列表类面板
<div class="panel panel-default">
    <div class="panel-heading">
        表格标题
    </div>
    <div class="panel-body">
        <p>这里是表格标题的详细内容!</p>
    </div>
    <ul class="list-group">
        <li class="list-group-item">1.这里是首页</li>
        <li class="list-group-item">1.这里是首页</li>
        <li class="list-group-item">1.这里是首页</li>
        <li class="list-group-item">1.这里是首页</li>
    </ul>
</div>
```