# 一、CSS入门

## 1、css选择器

选择器的作用是“用于确定（选定）要进行样式设定的标签（元素）”。 

有若干种形式的选择器。每种形式代表某种含义，以选定某种特征的元素。

比如：标签选择器： p{ ... }           h1{...}           div{ ... } 

## 2、css常用的几个属性

> color:             文字颜色（前景色）
>
> font-size:        文字大小
>
> font-family:    字体，比如：微软雅黑， 黑体，宋体，仿宋体，”Times  New  Roman”
>
> font-style:       就是设置字形是”正体”还是“斜体”(italic）
>
> font-weight:    设置是否粗体
>
> background:    背景色
>
> border:           设置边框
>
> text-decoration:      设置“装饰线”（下划线，中划线，上划线）
>
> text-align:       对齐
>
> width:            宽
>
> height:           高

# 二、选择器

## 1、选择器综述

### （1）选择器分类

基础选择器

关系选择器

属性选择器

伪类选择器

伪元素选择器

### （2）选择器语法的符号含义 

> E：        代表“Element”，即元素；
>
> S：         代表“Seletor”，即选择器；
>
> attr：      代表“attribute”，即属性；

## 2、基础选择器

### （1）标签选择器：E

标签选择器的形式上是一个标签名（一个单词）。

比如：

P{ .... }	div{ .... }	  img{ .... }

### （2）类选择器：.calss

类选择器的形式上是一个英文点（.）后面紧跟一个类名（className）。

类名是在标签上通过class属性而设定。我们可以自己设定类名。

> **注意**：
>
> 1， 一个类可以供多个标签使用！
>
> 2，一个标签可以同时设定多个类，用空格隔开。
>
> 这样设定后，多个类所设定的属性都可以作用在该标签上。

### （3）id选择器：#id

id选择器的形式上是一个英文井号（#）后面紧跟一个id名。id名是在标签上通过id属性而设定。我们可以自己设定id名。

> **特别注意**：
>
> 一个网页中的id不能“重名”（但class名可以重复）。

### （4）通配符选择器： * 

通配符选择器非常简单，就一个星号(*)，表示“所有标签”，同得不多。

*{ .....声明......}

表示所有标签都应用该css样式的设定。

## 3、关系选择器

关系选择器是通过元素之间的“位置关系的特征”来确定所选元素。

### （1）子代选择器：S1>S2  

匹配S1中的下一级S2。下一级就是“子级”，或子代。

其中S1，S2都可以是独立使用的选择器（比如id选择器，class选择器，标签选择器等）。

比如S1为div， S2为p，即形式为“div > p”，就表示找出div中的所有子级p标签。

又比如：

- \#p1>a{ ... }    ：表示找出id为p1的标签中的所有子代a标签。
- .cc>p{ ... }     ：表示找出class为cc的标签中的所有子代p标签。
- \#p2>.cc2>img{ ... } ：表示找出id为p2中的子代的class为cc2中的所有子代img标签。

### （2）后代选择器：S1  S2 

匹配S1内部的所有后代S2。

此时就不仅仅局限于子代标签了，还包括孙代，曾孙代，等等。

简单说，就是找出放在S1所选中的标签中的所有S2所选中的标签。

- div  p{ ... }   ：匹配div中的所有后代p标签，即凡是放在div中的p标签都会找出来。 
- \#p1  a{ ... }  ：匹配id为p1的标签中的所有a标签，即只要a标签在#p1中就可以。 
- .cc  p{ ... }    ：匹配class为cc的标签中的所有p标签，即只要p标签在.cc中就可以。
- \p2  .cc2  img{ ... } ：匹配id为p2中的class为cc2中的所有img标签。

### （3）相邻选择器：S1+S2 

匹配S1后面紧挨着的同级（兄弟）元素S2。

### （4）兄弟选择器：S1~S2 

匹配S1后面的所有同级（兄弟）元素S2。

## 4、属性选择器

属性选择器是通过元素的属性的特征信息来确定所选元素。

### （1）[attr]

匹配具有所给定属性名称的标签。

其中attr是一个“示意性符号”，表示“属性名”。

- [color] { background: yellow; }            //能选中具有color属性的所有标签。
- [width] { border: 1px solid  red; }       //能选中具有width属性的所有标签。

### （2）[attr="val"]

匹配具有某个属性且属性值为给定值的标签。

- [color=”red”] { background: yellow; }         //能选中具有color属性且值为”red”的所有标签。
- [width=”100”] { border: 1px solid  red; }    //能选中具有width属性且值为”100”的所有标签。
- \<hr  color=”red” />
- \<table  width=”100”  >....\</table>

### （3）[attr~="val"]

匹配具有某个属性且属性值包含所给定**单词**的标签。

注意：

​	必须是一个“单词”形式，比如属性值为”a  dog”，则使用”dog”可以匹配，而使用”do”不能匹配。

​	对于中文，除非有明确的空格，否则一句连续的句子（含中文标点符号）也只能算一个单词。

- \<p  title=”a  dog”>...\</p>

- [title~=”dog”]{ .... }             //可以选中上面那个p标签
- [title~=”do”]{ ..... }              //选不上。

### （4）[attr*="val"]

匹配具有某个属性且属性值包含给定的字符的标签。

- \<p  title=”a  dog”>...\</p> 
- [title*=”dog”]{ .... }             //可以选中上面那个p标签 
- [title*=”do”]{ ..... }              //也可以选上

### （5）[attr^="val"]

匹配具有某个属性且属性值以给定的字符开头的标签。

- \<p  title=”a  dog”>...\</p> 
- [title^=”dog”]{ .... }             //选不上
- [title^=”a”]{ .... }                 //能选上 
- [title^=”a  d”]{ ..... }           //也可以选上

### （6）[attr$="val"]

匹配具有某个属性且属性值以给定的字符结尾的标签。

## 5、伪类选择器

伪类选择器是通过单冒号（：）和**特定的具有某种含义的单词**来确定所选元素。

所谓伪类选择器，是相对于“类选择器”来说的，对比如下：

类选择器：

说明：类的名称是由我们程序员来设定的，符合命名规范就行。

形式：**.**类名称{ ... }

伪类选择器：

说明：伪类的名称是css标准中所预先设定的，我们不能自己设定。可用的伪类名不多。

形式：**:**伪类名称{ ... }

### （1）:link, :visited, :hover, :active, 

这4个伪类主要用于表示一个链接（也就是a标签）的4种不同状态。

它们可以设定一个链接在不同状态下的外观表现（样式表现）。

- :link        ——表示一个链接初始时候的状态。 
- :visited    ——表示一个链接在访问（点击）过之后的状态。 
- :hover     ——表示一个链接在“鼠标移上去”（鼠标悬停）的时候的状态。
- :active     ——表示一个链接在“活动状态”的时候的状态，通常就是点击的瞬间（按住不放能看到）。

> 注意：
>
> ​	:hover可以用于其它标签，并且经常用！
>
> ​	对于a链接的这4个状态，他们有顺序问题，必须按上述顺序才有合理效果。

### （2）E:focus

表示一个元素在成为可输入状态（获得焦点）的时候，主要用于表单元素。

其中“E”表示某个元素（或某个选择器所选中的元素）。

这样连着写，即表示该元素在获得焦点的时候，其样式表现如何。后面的“E”也都是这个意思。

也可以不用前面写“E”，而是直接用“:focus”，但实际应用中，一般会在前面有这个限定。

比如：

- input:focus{ .... }                 //表示input元素在获得焦点的时候 
- :focus{ .... }                         //也可以不用input ，但此时其实所选择的范围扩大了（不仅仅针对input元素）。 

### （3）E:first-child, E:last-child, E:only-child, E:nth-child(n) 

这几个伪类用于表示（或选中）“具有某种特征的子元素E”。

- E:first-child    ——匹配作为父元素的第一个子元素E。
- E:last-child     ——匹配作为父元素的最后一个子元素E。
- E:only-child   ——匹配作为父元素的唯一一个子元素E。
- E:nth-child(n) ——匹配作为父元素的第n个子元素E。括号中的n是一个具体数字 ，还可以这样用：nth-child(2n+1）表示奇数项， nth-child(2n+2)表示偶数项 。

> 注意：
>
> 上述也可以单用（不要冒号前面的部分），但一般较少这样用。

### （4）E:empty，E:checked，E:enabled，E:disabled

- E:empty

		匹配元素内部为空（没有内容）的元素。其中“内容”指的是一个标签内是否有其他html代码或文字。显然，单标签内是不可能有内容的。

- E:checked

		匹配被选中的元素（用于input且type为radio或checkbox的时候） 

- E:enabled

  匹配“可用的/有效的元素”（用于表单元素）。

- E:disabled

  匹配“不可用的/有效的元素”（用于表单元素）。

### 颜色表示法（额外）

颜色有如下表示法 ：

​	***英文单词**：    red,  blue, green,  yellow,  pink,  purple 

​	***RGB表示法**：

​		将一个颜色，使用红（R，red）， 绿（G，green）， 蓝（B，blue）来表示。

​		这3个叫做“基本颜色”，都按0-255分为256个层级。

​		所有颜色，都可以使用这3个颜色的不同层级（配比）来调配而成。

​		形式：rgb(红的配比， 绿的配比，蓝的配比）；

​		举例：

​			color: rgb(255, 0, 0)              //这是红色 

​			color: rgb(0,255, 0);              //这是绿色 

​			color:rgb(0, 0, 255);              //蓝色

​			color:rgb(255, 255, 0);          //黄色 

​	***RGBA表示法**：

​		A代表“透明度”，值从0到1的小数。0表示全透明。1表示不透明，此时就是RGB颜色 

​		形式：rgba(红的配比， 绿的配比，蓝的配比，透明度）；

​		color: rgba(100, 30, 70, 0.5),  

​		color: rgba(255, 0, 0, 0.66)           //这是红色

​	***16进制表示法**：

​		形式：#6个16进制数字！

​		前两个数字表示“红的配比”，中间两数字表示绿的配比，后两个数字表示蓝的配比。

## 6、伪元素选择器

伪元素选择器是通过双冒号（：：）和特定的具有某种含义的单词来确定所选元素。

伪元素选择器通常是“本没有这个元素（标签）”，但会创建出一个隐性元素并对其进行样式设定。

伪元素选择器又称为“伪对象选择器”。

### （1）E::before

表示在元素E的内部的最前面创建一个元素（伪元素）。

其中必须写上一个属性：content:”内容”;         //当然，内容可以为空。

### （2）E::after

表示在元素E的内部的最后面创建一个元素（伪元素）。

其中必须写上一个属性：content:”内容”;         //当然，内容可以为空。

### （3）E::selection

表示将元素E中“选中的文字”单独作为一个元素（伪元素）。

### （4）E::first-letter 

表示元素E中的“第一个字符”可以单独作为一个元素（伪元素）。

### （5）E::first-line 

表示元素E中的“第一行”可以单独作为一个元素（伪元素）。

## 7、常见选择器的组合

选择器的组合是将多个不同形式的选择器组合起来以确定所选元素。

### （1）E.className

举例：

- div.c1{ .... }
- p.cc2{ .... }

> 注意：他们是“紧挨在一起的”！ 否则就成为了后代选择器了。 

### （2）E#id

- div#id1{ ... } 
- p#id2{ ... }

### （3）E[属性选择器]

- [src]        //找所有有src属性的标签
- img[src]  //找img标签并且有src属性
- img[src*=”dog”]  找img标签并且有src属性并且属性中包含“dog”这个字符！

### （4）并集选择器：S1, S2

两个选择器，可以使用一个英文逗号（,）连接起来。

表示这两个选择器，都使用同样一个样式设定（属性设定）。

比如：

- p, div{ ... } 
- \#price, .addr{ ... }
- p.cc,  .cc,  div  .cc2{ ... } 。

### （5）更复杂的选择器组合举例

- \#main  .container  div { .... } ; 
- \#main  .box>p[align=”center”] { .... } 
- table#m2  div  .box2  p:nth-child(2) { .... } 
- div#m1  .box1  div  input[type=’text’]:focus { .... }

## 8、css样式的特性

### （1）层叠性

所谓层叠性，是指对同一元素同一属性的设定，后设定的某个样式（属性），会覆盖之前设定的样式。

比如：

- .cc1{ color: red;} 
- .cc1{color: blue;} 
- \<div  class=”cc1”>文字内容\</div> 

则class为cc1的元素中的文字颜色就是blue，即后者覆盖了前者的设定。

分两种情况：

- 两个相同的选择器，设置了同样的属性，后者覆盖前者——层叠性体现之一 。
- 两个不同但同级优先性的选择器，设置了同样的属性，也是后者覆盖前者——体现之二 。

### （2）继承性

所谓继承性，是指对某个元素所设定的样式，不但影响该元素本身，还可能影响该元素的后代元素。

> 注意：
>
> 实际上继承性不是普遍情况，而只是少数一些属性才具有继承性（即能够影响后代元素）。
>
> 应用中继承性通常用在有关文字的属性上。

### （3）优先性

所谓优先级，就是指一个标签的显示效果（样式表现），可能受若干个因素的影响，但哪一个因素的影响大，则最终效果就按该因素的设定，也就是“更优先”的意思。

伪元素选择器 > !important  > 行内样式 > **id选择器** >**类选择器（或伪类选择器）** > **元素选择器** >  **\***  > 继承样式 > 浏览器默认样式

其中，伪元素选择器又有： ::first-letter  >  ::selection  >  ::first-line

上述加粗的部分实际应用最常见。

> **什么是“!important”？**
>
> 就是在一个属性的设定中，在属性值后面加“!important”标识，然后在加分号（;），例如：
>
> ​	.c1{ color: red!important; }
>
> ​	\#d1{ color: yellow; }
>
> 此时，如果上述两个选择器都能选中某一个元素，则其中的文字就是红色（!important优先了）

> **选择器的优先级怎么计算？** 
>
> ​	对于复合选择器（比如div.c1， 或 #id1>.c2， 或#id2>.c3  p  span，等等），又该怎么确定他们的优先级呢？
>
> ​	首先，根据上述的基本优先级原则，遵循“官大一级压死人”的规则。
>
> ​		比如：
>
> ​			选择器1： #id1{.....}
>
> ​			选择器2： .c1>.c2>p{....}
>
> ​			则选择器1优先；
>
> ​	其次，如果具有同级的优先级，则比谁的数量多。
>
> ​		比如：
>
> ​			选择器1： .cc1  .cc3 {.....}，
>
> ​			选择器2： .cc1  .cc2  .cc3 {....} 
>
> ​			则选择器2优先；
>
> ​	最后，综合上述两条规则就可以判断出哪个是优先的。

# 三、有关文字的属性

## 1、字体属性

字体属性是用来设定“文字字形”的外观表现，主要包括： 

- color：颜色
- font-family：字体名称
- font-size：大小
- font-style：是否斜体

font综合属性的语法：`font：[ <' [font-style] '> || <' [font-weight] '> ]? <' [font-size] '> [ / <' [line-height] '> ]? <' [font-family] '> ];`

## 2、文本属性

文本属性通常指的是作为文字内容的整体性特性（而不是具体文字的表现特性）。 

| **属性名称**    | **含义**                               | **举例**                                   | **其他说明**                                                 |
| --------------- | -------------------------------------- | ------------------------------------------ | ------------------------------------------------------------ |
| text-align      | 一段文字的对齐方式                     | text-align: center;                        | 可用值：left， center， right                                |
| text-decoration | 一段文字的”修饰线”                     | text-decoration：underline                 | 可用值：underline（下划线），overline（上划线），line-through（中划线） |
| text-indent     | 设置一段文本的“首行缩进”的宽度（距离） | text-indent:   24px;                       | px是长度单位，表示“像素”                                     |
| line-height     | 设定文字的“行高”                       | line-height:   30px;   line-height:   2em; | em是长度单位，表示“字高”                                     |
| letter-spacing  | 设定文字的“字符间距”                   | letter-spacing:   3px;                     | 注意：中文的每个字都算一个字符                               |
| word-spacing    | 设定文字的“单词间距”                   | word-spacing:   15px;                      | 注意：单词通常是以“空格”隔开的。因此，连续的中文即使很长也只能算一个单词。 |

# 四、有关盒子的属性

盒子就是一个元素（标签）的所辖范围，简单来说，基本就是一个“矩形区域”。 

## 1、盒子的概述

所谓盒子，就是将html网页中的标签在网页版面中所占据的平面范围，抽象出来的一个“视觉形状”。

一个最简单的理解就是：**几乎所有标签，都可以看做是一个“矩形盒子”，具有一定的宽高（区域）**。

总体上来说，一个盒子，是由若干个部分构成的，从内到外依次包括：

​	盒子内容区，内边距区，边框，外边距区

![BubbleSort_01](https://raw.githubusercontent.com/luchaoshunluhao/images/master/box.png)

> content：内容
>
> padding：内边距，又称为内补白，是一片空白区域
>
> border：边框
>
> margin：外边距，又称为外补白，也是一片空白区域
>
> top，right，bottom，left：上，右，下，左

> 特别注意：
>
> 1，一般情况下，一个盒子中放置内容或其他元素（元素也是盒子），实际是放在内容区的。
>
> 2，平常我们看不到内边距，边框和外边距，是因为他们默认都是0（宽度，或厚度）。

## 2、盒子的宽高属性width和height

设置盒子的宽高属性，实际上设置的是盒子内容区的宽高。

而盒子实际占据的区域的宽高，可以这样来计算： 

​	盒子所占宽：

​		margin-left + border-left + padding-left + **width** + padding-right + border-right + margin-right 

​	盒子所占高 :

​		margin-top + border-top + padding-top + **height** + padding-bottom + border-bottom + margin-bottom 

除了这两个基本宽高属性，还有以下4个范围限定性宽高属性，有时候也会用一用：

min-width：   设定最小宽度

max-width：  设定最大宽度

min-height：  设定最小高度

max-height：  设定最大高度

## 3、边框属性border

边框属性就是设置一个盒子的边框线的具体特性。

边框线的特性有3个：

- border-style： 线型，属性值通常有：solid(实线)， dashed(虚线)， dotted(点线) 
- border-width： 线的粗细，长度单位，比如1px
- border-color： 线的颜色，颜色值，比如red， rgb(255, 0, 0)， #FF3366 

又由于一个盒子的边框有4个方位(top, right, bottom, left)，则总体上就至少有12个边框属性，形式为： 

​	border-方位-特性，比如：border-top-style， border-top-width，border-top-color， border-right-width， border-left-color，等等。

​	示例：

​	border-top-style: solid; 

​	border-right-color: #FF0000;  

​	border-left-width: 2px;

实际上，还有若干个“单边综合属性”，比如：

​	border-top：一次性设置上边框线的特性； 

​	border-left：一次性设置左边框线的特性；

应用中，最常用的其实是“border”这一个最大的综合属性，它一次性设置4个边的3个特性，比如： 

​	border： 1px  solid  red;          //表示4变的边框线都是宽度为1px的红色实线。 

## 4、内边距属性padding

含义：内边距是指在盒子结构中，盒子的边框线和内容之间的一段空白区域（内容放不进去）。 

> 我们能设置的就是这个空白区域的大小（宽度）。同样分4个方向，分别可以单独设置： 
>
> padding-top：1px；             //上内边距 
>
> padding-right：2px；           //右内边距 
>
> padding-bottom：4px；       //下内边距
>
> padding-left：8px；             //左内边距 
>
> 还有一个综合属性： 
>
> padding：宽度1【宽度2】【宽度3】【宽度4】；   //这个用的最多，推荐使用。 
>
> 这个综合属性可以设置1-4个值，不同个数的值，其含义不同，如下所示：
>
> - 1个值：        表示4个方向都是这个值。 
> - 2个值：        第1个表示上下边距的值，第2个表示左右边距的值 。
> - 3个值：        第1个表示上边距的值，第2个表示左右边距的值，第3个表示下边距的值。 
> - 4个值：        依次代表top， right， bottom， right这4个方向的内边距的值。 

## 5、外边距属性

含义：外边距是指在盒子结构中，盒子的边框线，跟盒子的外部其他元素之间的一段空白区域。 

> 我们能设置的就是这个空白区域的大小（宽度）。 
>
> 它的属性设置和含义，跟内边距（padding）非常类似：
>
> margin-top：1px；              //上外边距
>
> margin-right：2px；            //右外边距 
>
> margin-bottom：4px；       //下外边距 
>
> margin-left：8px；              //左外边距 
>
> margin：宽度1  【宽度2】【宽度3】 【宽度4】；    //同时设置4个方向，用的最多，推荐使用。

**外边距的“重叠性”：**

​	当两个垂直方向的外边距（即margin-top和margin-bottom）挨在一起的时候（就是垂直方向上相邻），则这两个外边会“重叠在一起”，表现为只有更大的那个外边距的高度(本来“按理”是两个相加的高度)。 

## 6、背景属性background

含义：背景是指在盒子结构中，衬托在边框线范围以内的背景颜色或背景图。

主要的背景属性设置有：

**设置背景颜色：** background-color：yellow;

**设置背景图：** background-image：url(图片路径);     //注意，图片路径是相对于当前网页或css文件(对外部样式来说) 

**设置背景图的位置**（有背景图的前提下有效）：**background-position**：水平位置 [，垂直位置]； 

> 说明：
>
> ​	如果不设置该属性，默认值为“0,0”，即在盒子的左上角。 
>
> ​	可以设置1个值或2个值；设置1个值的时候，第二个默认为center（居中）。 
>
> ​	水平位置：可以设置为长度值，或百分比，或以下固定值：left/center/right。
>
> ​	垂直位置：可以设置为长度值，或百分比，或以下固定值：/top/center/bottom 

**设置背景图是否重复**（有背景图的前提下有效）：**background-repeat**：属性值1 [,属性值2]；

> 有以下几个值可用：
>
> repeat：         重复，默认值；
>
> no-repeat：    不重复； 
>
> repeat-x：      只在x方向重复；
>
> repeat-y：      只在y方向重复；

**背景综合属性background**：

​	可以同时设置上述几个有关背景的属性，相互之间用空格隔开，比如： 

​	background：yellow；                只设置背景颜色； 

​	background：yellow  url(./images/bg.jpg)  no-repeat；

​	background：yellow  url(./images/bg.jpg)  repeat-y  lelft  top；

​	background：yellow  url(‘/images.bg.jpg)  repeat  no-repeat  5px  10px；

## 7、轮廓属性outline

含义：轮廓指的是盒子边框线外面再套一层“修饰性”线条，该线条只有视觉效果，不占版面空间。

实际上，如果有外边距（margin），轮廓线是可以跟margin有重叠的。

轮廓属性主要有：

outline-width：      轮廓线宽度

outline-style：       轮廓线线型

outline-color：      轮廓线颜色

outline-offset：      轮廓线距离边框线的距离（间隙）

# 五、有关布局的属性

## 1、布局属性

### （1）盒子的显示效果属性

含义：指设置一个盒子（元素，标签）在网页中的基本显示特性，最常见的就是显示为块元素特性还是行内元素特性。

> 通过这个属性，则所有表现型元素，都可以任意将其作为块元素或者行内元素来使用！ 

> 常用的属性值有：
>
> block：          显示为块状元素
>
> inline：          显示为行内元素
>
> block-inline：显示为行内块元素
>
> ​	含义：整体表现为块元素(不会自动折行)，但可以跟其他行内元素并行在一行(表现为行内元素)。
>
> ​	说明：一个img就是典型的行内块元素（它本身不会折行，但一行可以放置多个）。
>
> none：           不显示（隐藏元素）

> 关于元素按显示特性分类：
>
> 块状元素：
>
> 元素独占“一行”。
>
> 典型标签：div,  p,  h1~h6,  pre,  hr,  ul,  ol,  li,  dl, dt, dd,  table。
>
> 行内元素：
>
> 元素在一行内从左到右“流式显示”，直到碰到行尾，再自动换行下一行显示。
>
> 典型元素：span, a, b, strong, i, font, em, 
>
> 行内块元素：
>
> 元素本身不换行（不折断），但只要能显示得下，则一行可以显示多个（跟行内元素一样）。
>
> 典型元素：
>
> img,  input, select,  textarea,  button,  video,  audio

> 特别注意：
>
> - 行内元素不能设置宽高值。行内元素的宽高值由其中的内容多少、文字大小和行高决定。
> - 行内元素不能设置上下外边距和上下内边距（实际可以设置，但无效，不占空间）。
> - 行内元素可以设置边框，但上下边框不占空间（左右边框会占空间）。
> - 行内块和块元素都具有盒子的所有属性，唯一区别是行内块可以多个出现在一行中。

### （2）浮动属性float

① 浮动的含义与作用：

浮动就是让一个元素往左或右边“尽量挤靠”，以使其周边文字（行内元素）可以围绕该浮动元素显示。

其典型的表现就是一张图片向左对齐（align=”left”）的时候，图片标签前后的文字都能够绕着图片展示。

让图片浮动，就能够使其本身优先靠在一边（左边或右边），而使“其他行内元素”围绕其展示。 

> 浮动属性float的值包括：
>
> left（向左浮动）， right（向右浮动）， none（不浮动）。
>
> 语法：
>
> ​	float：left；       或           float：right；

② 浮动的特性：

- 对行内元素来说：浮动元素会先于同一行中的行内元素而占据其所设定方向的水平空间；
- 对块状元素来说：浮动元素相当于“浮起来了”，块状元素会被浮动元素“遮挡”；
- 多个浮动元素会依次往设定的方向“挤靠”，直到放不下，再往“下一行”，继续“挤靠”； 
- 浮动元素往下一行挤靠时，如碰到“突出物”，则会被“卡住”，但仍然按挤靠规则进行显示； 
- 浮动盒子失去“垂直支撑力”，表现为不占它外层盒子高度，但仍然有宽度；

③ 浮动的清除

当一个盒子内部出现浮动元素，则该盒子不会被该浮动元素“撑高”，也就是说，父盒子失去了理应包住子盒子的高度。（当然，如果父盒子中有其他非浮动元素撑着，也就具有该其他非浮动元素所应该撑出的高度）

这通常都不符合正常的文档布局的需要——正常的需要就是外层盒子需要包住内层盒子。 

这就需要清除浮动了。

使用属性clear，有常见的3个值：

clear: left:表示该元素左边不要出现浮动元素；

clear: right：表示该元素右边不要出现浮动元素；

clear:both：表示该元素**两边都不要**出现浮动元素；——这是最常见的需求（场景）。

所谓清除浮动，其实就是让父盒子中的浮动特性“终止”（结束）。这样父盒子就具有了正常的高度，可以正常包住其内部的浮动盒子。

做法1：设置父盒子的overflow属性为hidden；

```html+css
/*css*/
.box1{
	...
	overflow:hidden;
}
<!--html-->
<div class='box1'>
	<div class='inner'>文字</div>
</div>
```



做法2：在父盒子内部的末尾添加一个“清除浮动”的空盒子。

```html+css
/*css*/
.box1{...}
.clear{
    clear:both;
}
.box1 .inner{...}
<!--html-->
<div class='box1'>
	<div class='inner'>文字</div>
	<div class='clear'></div>    <!--空盒子，用于清除浮动-->
</div>
```



做法3：给父盒子的末尾添加一个“清除浮动”的伪元素（::after）。

```css+html
/*css*/
.box1{...}
.box1::after{
    content:"";
    display:block;
    clear:both;
}
<!--html-->
<div class='box1'></div
```

### （3）溢出属性overflow

当一个盒子里面有浮动元素，则：

- 如果该盒子不设置高度，就应该清除浮动。 
- 如果该盒子设置了高度，此时就应该考虑溢出时的处理效果！
- 如果该盒子设置了高度，则里面盒子的浮动，清不清除都无关紧要。

含义：就是设置一个盒子内部的内容，超出了该盒子的设定大小的时候，怎么显示该内容的问题。

> overflow常用值有：
>
> auto：     自动，按浏览器的默认设置自动处理，可能各浏览器会有所不同。 
>
> scroll：   滚动，就是超出范围的时候，盒子出现滚动条（像浏览器的滚动条那样）。 
>
> hidden： 隐藏，就是将超出部分隐藏起来（视觉上不可见）。
>
> visible： 显示，就是虽然，超出去了，但仍然显示出来，这是这个属性的默认值，无需设置。 
>
> 此时，虽然可能超出外层盒子，但不会影响外层盒子后续的位置（布局）。

### （4）可见性属性visibility

含义：设置元素的可见性。主要有两个值： 设置元素的可见性。主要有两个值：visible：可见；hidden： 隐藏 。

> 特别注意：
>
> 设置visibility为hidden，虽然元素不可见了，但元素原本所占的空间仍然存在（效果是一片空白）
>
> 对比：设置display为none，也是隐藏，但此时该元素不但不可见，而且不占版面空间。

## 2、布局思想

### （1）布局思想

> 表格布局思想：
>
> ​	使用表格，将页面分割为若干区域：
>
> ​	纵向：就用表格的tr。
>
> ​	横向：就用表格的td实现。
>
> ​	层层分割：每个区块只考虑是“横向”还是“纵向”。
>
> ​	表格布局思想，被抛弃的原因是：网页展示速度慢！非常慢！
>
> div+浮动布局思想：
>
> ​	纵向：使用div，自然上下排列出来。
>
> ​	横向：使用浮动div，并做好清除浮动工作（使浮动元素不影响后续元素）。
>
> ​	层层分割：每个区块只考虑是“横向”还是“纵向”。

### （2）定位属性

定位就是通过有关定位的属性来明确设定一个盒子的在以下两个方面的位置：

​	1，在（x,y）平面上所处位置。

​	2，在高度（z轴）方向的位置（层次）。

这是相对于一个盒子的“自然位置”和“浮动位置”而言的。

​	自然位置就是所谓的正常的文档流所确定的位置。

​	浮动位置就是由于浮动的特性而确定的位置。

#### ①  定位方式属性position

position用于设定一个元素的位置按什么方式来确定。

通俗说就是设定元素“放在哪个位置”（可由4个定位属性确定：top，left, right, bottom）。

> 有如下4个值可用：
>
> static：   静态定位（其实就是没有定位）
>
> 是一个元素的默认定位方式，也就是一个文档中元素的**正常文档流**所确定的定位。
>
> 对其给定定位位置（top，left, right, bottom）的值无效。
>
> relative：相对定位
>
> 相对于其本来应该所处的位置而设定一个相对性定位。
>
> 需给定位置（top，left, right, bottom）
>
> absolute：绝对定位
>
> 相对于其上层最近的一个非static定位元素而设定的一个绝对性定位。
>
> 需给定位置（top，left, right, bottom）；
>
> **而如果其所有上级都没有非static****定位元素，就相对于窗口来定位**——手册上说的相对于body，是不准确的！
>
> fixed：   固定定位
>
> 相对于当前网页窗口而设定的一个绝对性定位。
>
> 需给定位置（top，left, right, bottom）。

> **注意：**
>
> - relative定位虽然会改变元素的位置，但不影响上级盒子和相邻盒子该有的正常宽高和位置。
>
> - absolute定位和fixed定位的元素脱离了文档流，也就是上级盒子中不会计算其宽高（像没有一样）

#### ② 定位位置属性：top，left，right，bottom

就是对于3种定位方式（relative， absolute， fixed），所给定的具体位置值。

可以是使用距离“上”，“左”，“下”，“右”各多少来定。

比如：

```css
.cc1{
	position: absolute;
	left: 5px;  top: 10px;
}
```

> 注意：top和bottom不能同时用；left和right不能同时用！

#### ③ 层叠属性z-index

含义：

​	就是将一个元素（盒子）默认情况下所展示在的那个平面（就是屏幕所在面）的垂直线当做z轴方向（就是眼睛盯屏幕时的那个“视线”方向），朝眼睛方向为z轴的正方向。则z-index可以设定一个元素（盒子）在z轴方向的“叠放层次”的高低，用整数表示。越大值表示越高，也就是离眼睛越近，自然就会覆盖住比它低的其他盒子。

# 六、列表与表格样式

列表样式指的是ul（无序列表）和ol（有序列表）的表现特性；

表格样式指的是table的表现特性。

## 1、列表样式 

列表样式主要是设置ul或ol前面的那个“列表符”的特性，包括：

- list-style-type：用于设置列表样式的类型，比如原点(disc)，圆圈(circle)，阿拉伯数字(decimal)，罗马数字，英文字母。有了这个属性，对ul和ol来说，就没有差别了！

- list-style-image：用于设置列列表前面的小图标（图像），也就是说，用一个图片来代替上面的列表符。

  如果设置了这项，则list-style-type就失效。

- list-style-position：用于设置列表项目符的位置，只有两个值：outside(外面，默认），inside（里面）。指的是列表符，是放在li盒子的里面，还是放在li盒子的外面。 

- list-style：上述3个属性的综合属性。 

> 说明：**实际应用中，通常使用背景图像来代替“list-style-type”和“list-style-image”**。 

## 2、表格样式

表格样式主要是从整体上设置一个表格的外观表现，而不涉及到具体的每一个单元格。

表格样式的属性主要包括：

- border-collapse：设置表格的单元格边线是否合并；有两个值可用：separate（分离），collapse（合并） 
- border-spacin：设置表格单元格之间的间隙，长度单位。注意：只有在border-collapse的值为separate时才有效。 
- caption-side：设置表格标题（caption标签）的放置位置，可用值有：top，bottom。（还有left和right）。

# 七、CSS3高级特性

## 1、盒子新特性

### （1）盒子阴影box-shadow

属性：box-shadow 

作用 ：用于设定一个盒子的阴影效果 。

形式： box-shadow：水平偏移值  垂直偏移值  【模糊值】【外延值】【颜色】【inset】； 

说明：

- 至少设置两个长度值，分别表示阴影的水平偏移量和垂直偏移量，可以为负；
- 模糊值是设定阴影的模糊效果的宽度，可以不设置，则默认为0；
- 外延值是设定阴影再“扩大”的宽度，可以不设置，则默认为0； 
- inset表示设置“内阴影”，可以不设置，则默认为外阴影。

> 举例：
>
> .box1{ box-shadow: 2px 2px red; } 
>
> .box2{ box-shadow: 2px 5px 2px #00FFFF; }
>
> .box3{ box-shadow: 2px 5px 2px 3px rgba(33, 33, 33, 0.5); } 
>
> .box4{ box-shadow: 2px 5px rgba(66,66,66,0.5) inset; } 

###（2）圆角边框border-radius

属性：border-radius

作用：用于设定一个盒子的圆角特性。

形式：border-radius: 水平圆角半径 [/ 垂直圆角半径]； 

说明：

- 垂直半径可以省略，则其同水平半径的值。

- 半径设置可以提供1~4个值，具体如下。

  - 提供1个：4个角都为该值； 

  - 提供2个：第1个表示上左和下右，第2个表示上右和下左；
  - 提供3个：第1个表示上左，第2个表示上右和下左；第3个表示下右； 
  - 第供4个：分别代表4个角上的半径（依次上左，上右，下右，下左）。

> 举例：
>
> border-radius: 5px;               //4个角半径均为5px； 
>
> border-radius: 5px/15px;       //4个角水平半径为5px，垂直半径为15px；
>
> border-radius: 5px 6px 7px 8px;    //四个角半径分别是5px，6px，7px，8px；
>
> border-radius: 5px 6px 7px 8px/15px 16px 17px 18px; 

### （3）图像边框border-image 

① 原理说明：

图像边框是指使用一张图片来作为一个盒子的边框。其实就是将图片作为背景图铺上到“边框区域”上去。但这个铺设到边框的图片，并非像常规背景图那样简单直接地铺设上去，而是有其特定的规则。

其铺设原理是：

将要作为背景的图片，分割为9个部分（如上图所示），然后4个角4个边分别铺设对应部分，中间区域就铺设背景图片的中间部分。其中4个边和中间区域，可以类似常规背景一样进行“平铺(repeat)”,或进行拉伸(缩放)。从而达到整个盒子的完美背景呈现。

② 主要属性 

边框背景的主要属性有：

- **border-image-source**：设置作为边框背景的图片源；

- **border-image-slice** ：设置要将边框背景图片进行“切割”的分割方式。

  - 形式为：border-image-slice: 数值 [fill];   //**特别注意：这里的数值不带单位！** 其中“数值”可以是1-4个值，分别代表上右下左4个方向的“切割厚度”。

  - fill代表“填充”，用于中间区域填充到盒子内容区。

- **border-image-width**：设置图片边框的宽度，也可以设定1-4个值。

  - 通常设定为auto（自动），此时就会使用border-image-slice所设定的切割厚度 。

- **border-image-repeat**：设置边框背景的填充方式，可以设定1-2个值，表示横向和纵向的填充方式。

  - 可用值如下：

  - stretch： 指定用拉伸方式来填充边框背景图，**这是默认值，也最常用，推荐使用**。
  - repeat： 指定用重复平铺方式来填充边框背景图。类似背景图的repeat，**背景图不改变大小** 。
  - round： 指定用平铺方式来填充边框背景图。图片会根据边框的尺寸动态 **调整图片的大小**直至正好可以铺满整个边框。
  - space： 指定用平铺方式来填充边框背景图。图片会根据边框的尺寸动态**调整图片的之间的间距**直至正好可以铺满整个边框。 

> 注：有的浏览其中应用边框图属性需同时设定border属性。

### （4）背景图高级特性

有关盒子的背景设置，在CSS3中，又增加了几个属性，如下所示：

- **background-attachment**： 设置背景图像的滚动特性，可用值有：

  - scroll：          相对于当前盒子固定（盒子滚动，则背景图也会滚动），这是默认值。 

  - local：           相对于当前盒子的内容固定（内容滚动，则背景图也会滚动）。 
  - fixed：          相对于当前浏览器窗体固定（类似固定定位，即它会始终在窗口的某个位置）。

- **background-origin**：设置背景图像的参考原点（位置），实际就是背景出现的范围。可用值有： 

  - border-box：  在boder区域范围内（含border）。 

  - padding-box：在padding区域范围内（含padding），这是默认值。
  - content-box： 在内容区域范围内。 
  - 此属性主要是跟background-position的位置计算有关。

- **background-clip** ：设置背景图像向外裁剪的区域，裁剪范围以外就被裁剪了(不显示)。可用值有： 

  - border-box： 从border区域外沿（即不含border）开始向外裁剪背景，这是默认值。

  - padding-box：从padding区域外沿（即不含padding）开始向外裁剪背景。  
  - content-box： 从content区域外沿开始向外裁剪背景。

- **background-size**： 值1 [, 值2] 。设置背景图像的大小，可设置2个值，分别表示横向和纵向的大小。可用值有：

  - 长度： 用长度值指定背景图像大小。不允许负值。

  - 百分比： 用百分比指定背景图像的缩放大小。不允许负值。
  - auto： 背景图像的真实大小。
  - cover： 将背景图像等比缩放到完全覆盖容器，背景图像有可能超出容器。
  - contain： 将背景图像等比缩放到宽度或高度与容器的宽度或高度相等，背景图像不超出容器。

- 背景重复性的值在C3中多两个可用的值：round，space 

### （5）渐变背景gradient

渐变背景其实是设置background-image属性的值，设置的不是一个单一颜色，而是多个颜色，并按给定方式进行渐变 。

#### ① 线性渐变linear-gradient 

- 含义：线性渐变是让背景颜色按照某个方向（角度）的方式来进行过渡变化。

- 语法：background-image：linear-gradient([角度，]  颜色1，颜色2 [，颜色n...] ); 

- 说明：

  - 角度以从下到上（12点整的方向）为0度，顺时针为正角度，默认为180度。

  - 角度还可以使用to left，to right，to top， to bottom这几个关键字；
  - 至少设置2个颜色（这样才能实现渐变）；可设置多个颜色，都能自动实现渐变；
  - 每个颜色还可以设置“截止位置”，表示该颜色在渐变中的“关键点”（位置），形式为：颜色  位置，比如：red  30px;  或  #00ff00  20%; 

- 举例：

  - background-image：linear-gradient(red, blue);    //从上到下由红色转蓝色

  - background-image：linear-gradient(90deg, red, blue); //从左到右由红色转蓝色
  - background-image：linear-gradient(90deg, red, blue, green);     //从左到右由红色转蓝色再转绿色 
  - background-image：linear-gradient(45deg, red, blue 30%, green );    //从左下角到右上角，由红色转蓝色到30%位置，然后再渐变为绿色终止 

#### ② 径向渐变radial-gradient

- 含义：径向渐变是让背景颜色从某个中心点以圆或椭圆向外扩散的方式来进行过渡变化。 

- **语法**：background-image：radial-gradient( [形状][大小]  [at 位置，] 颜色1，颜色2 [，颜色n...]) 

- **说明**：

  - **形状**可以是circle（圆）或ellipse（椭圆），默认是跟随盒子（可能是圆，也可能是椭圆）； 

  - **大小**是指渐变从圆心开始向外进行过渡变化的距离（半径），圆用一个值，椭圆用2个值（空格隔开）；

    - 大小还可以使用如下4个关键字： 

    - farthest-corner：    最远角，表示从圆心开始，渐变到最远的角的位置。下面也类似； 
    - farthest-side：       最远边；
    - closest-corner：     最近角；
    - closest-side：         最近边；

  - **位置**可以是一个值（表示横坐标，纵坐标默认居中），或2个值（横纵坐标，空格隔开）；位置还可以使用top， right， bottom，left，center这5个关键字；

  - **颜色**至少包含2个，每个颜色还可以设定“截止位置”；

    - background-image: radial-gradient(red, green, white); //默认为适应盒子，并在中心 
    - background-image: radial-gradient(circle,red, green, white);       //设定为圆形 
    - background-image: radial-gradient(circle at 60px 30px, red, green, white); //圆心位置为（60,30）
    - background-image: radial-gradient(farthest-side at 60px 30px, red, green, blue); //渐变到最远角 
    - background-image: radial-gradient(circle closest-side,  red, green, blue);//圆形，渐变到最近的边 
    - background-image: radial-gradient(100px, red, green, blue);//大小为100px(圆形)，默认在中心位置 
    - background-image: radial-gradient(100px 50px, red, green, blue);//大小为100px和50px(椭圆形) 

## 2、多栏布局column

### （1）基本概念

所谓多栏布局，就是一个盒子设置栏宽属性或栏数量属性，就构成多栏布局，则其中的内容，会先在第一栏展示，第一栏展示满后，再展示到第二栏，以此类推。

多栏布局最常见的就是杂志或报纸上常见的“分栏版面”。比如杂志最常用的是分为两栏。

多栏布局通常用于盒子内部主要以文字（行内元素）为主的情形。

给一个盒子设定栏宽属性或栏数量属性（二选一），就可以实现多栏布局效果。

### （2）主要属性

- 栏宽度属性column-width
  - 设定分栏布局中一个栏的宽度值；实际宽度会根据外层盒子的宽度有所调整（可能变大）。 
- 栏数量属性column-count 
  - 设定分栏布局中的总栏数。
- columns属性：
  - 上述column-width和column-count的综合属性；
  - **使用形式：columns:** **栏宽值**  **栏目数；** 
  - 实际表现上，当总宽度大于等于“栏宽x栏目数”时，栏目数固定，栏宽可能会有所调整（变大）。 
  - 当总宽度小于“栏宽x栏目数”时，栏目数会减少（保证栏宽不小于设定的栏宽）。 
- 栏间隙属性column-gap 
  - 设定栏与栏之间的宽度值，默认是font-size大小（比如14px）
- 栏分割线属性column-rule 
  - 栏分割线属性，就是两栏之间的线，如果不设定默认就是“空的”，就没有分割线，只有间隙（gap）。 
  - 栏分割线属性类似边框线（但只是一条线），可以设定：线宽，线型，线色。
  - 有如下几个属性：
    - column-rule-width：设定线宽，比如1px，5px； 
    - column-rule-style：设定线型，比如solid，dashed，dotted；
    - column-rule-color：设定线色，比如red， #ff9966， rgb(200,100,0)
    - column-rule：上述3个属性的综合属性。

## 3、弹性布局flex 

### （1）基本概念

弹性布局是指，可以设定一个容器盒子中的若干个（数量可变的）子盒子，在父盒子中的横向或纵向有序整齐排列。其典型应用就是页面中的导航布局的实现 。

弹性布局的实现，主要是在父盒子（容器盒子）上定义相应的属性，则其内部的子盒子就能够按照所定义的样式进行显示。

### （2）主要属性

弹性布局的主要属性设置包括如下几个：

- display: flex; 

  - 说明：设置盒子的显示模式为弹性盒模型，即该盒子成为了弹性盒模式的容器盒子。 

- flex-direction: 

  - 说明：设置弹性盒模式的子盒子的排列方式，有如下4个方式（4个属性值）：
    - row：横向排列 
    - row-reverse：横向排列，但顺序反向 
    - column：纵向排列 
    - column-reverse：纵向排列，但顺序反响

- flex-wrap：

  - 说明：设置弹性盒模式的子盒子超出时的换行特性，常用属性值有：
    - nowrap：不换行，尽量在一行显示，这是默认值。此时有可能会超出父盒子（当子盒子有最小宽度设置时）。
    - wrap：自动换行 
    - wrap-reverse：换行，但反向显示（即其实显示到上一行去了）

- justify-content：

  > 说明：设置子盒子的主轴方向的一行中的排布方式。 
  >
  > 所谓主轴就是由flex-direction所决定的方向为主轴，对应另一个方向为辅轴。
  >
  > 假如flex-direction为column或column-reverse，则纵向为主轴，横向为辅轴。 

  - 常用属性值有： 
    - flex-start：子盒子从所设定的起始位置开始排列出来，空隙留后面； 
    - flex-end：子盒子从所设定的终止位置开始排列出来，空隙留前面；
    - center：子盒子完全从居中的位置开始排列出来，空隙留两边；
    - space-between：子盒子两边紧靠父盒子，空隙留在相互的中间且均等；
    - space-around：子盒子均衡布置，分布给每个盒子的空隙都一样。

> **两个重要概念：主轴，辅轴** 
>
> 主轴方向：平面直角坐标系中X轴的方向。
>
> 辅轴方向：平面直角坐标系中Y轴的方向。
>
> flex-direction: row-reverse;
>
> flex-wrap:wrap-reverse;

- align-content：

  > 说明：设置子盒子在辅轴方向的排布方式，大于一行且辅轴有多余空间时时才有效。 

  - 常用的属性值有：
    - flex-start：子盒子从所设定的起始位置开始排列出来，空隙留后面； 
    - flex-end：子盒子从所设定的终止位置开始排列出来，空隙留前面； 
    - center：子盒子完全从居中的位置开始排列出来，空隙留两边； 
    - space-between：子盒子两边仅靠父盒子，空隙留在相互的中间； 
    - space-around：子盒子均衡布置，空隙均衡出现；

- align-items：

  > 说明：设置子盒子在当前行中辅轴方向的对齐方式。 

  - flex-start：子盒子定位于所设定的起始位置，空隙留后面；
  - flex-end：子盒子定位于设定的终止位置，空隙留前面；
  - center：子盒子定位于居中的位置，空隙留两边；
  - baseline：子盒子定位于基准位置；
  - stretch：子盒子进行拉伸（充满纵轴）；

## 4、2D变换transform（2D）

### （1）基本概念

2D变换的基本含义是：将浏览器页面（电脑屏幕所在面）当做一个二维平面，然后，通过CSS的设置，使网页元素能够在这个平面上进行“形状变换”。 

简单说就是，在一个元素的“本来”外观表现上，可以对其实行：位移，旋转，缩放，斜拉变形等。

### （2）主要属性

- transform：

  这是最主要的变换属性；其实所有变换都是通过这个属性，使用不同的值来实现的。

  而所用不同的值，主要就是指定不同的**变换函数**（一个单词），以及所需要变换的数值；

  常用的2D变换形式如下：

  - transform: translatex(值)：           将元素水平移动给定的值；
  - transform: translatey(值)：           将元素垂直移动给定的值；
  - transform: translate(x值，y值)： 同时进行水平和垂直移动；
  - transform: rotate(角度值)：         将元素旋转给定的角度； 
    - 旋转的方向是：正值为顺时针方向，负值为逆时针方向；
  - transform: scalex(比例值)：         x方向进行缩放；
  - transform: scaley(比例值)：         y方向进行缩放；
  - transform: scale(x比值, y比值):  同时进行水平和垂直方向的缩放；
  - transform: skewx(角度值)：        将元素从x方向拉伸给定的角度；
  - transform: skewy(角度值)：        将元素从y方向拉伸给定的角度；
  - transform: skew(x角度,y角度):   将元素从x和y方向拉伸给定的角度；

  > 特别注意：
  >
  > 对一个元素可以同时进行多项变换。 
  >
  > 进行多项变换时，多个变换属性值要一并写在一起，相互之间用空格隔开，类似这样： 
  >
  > ​        transform: translatex(5px)  translatey(10px)  rotate(20deg)  scale(1.5, 2); 
  >
  > 对于进行了变换的元素，虽然形状或位置都可能变了，但并不影响其他元素(即不影响布局效果)。 

- transform-origin： 

  - 指定变换时的“原点”（基点）；默认是该变换元素的“中心点”（center, center）；形式：

    transform-origin：水平坐标  垂直坐标；

    其中：    水平坐标可以用一个长度值，或百分比，或left，center，right； 

    ​		垂直坐标可以用一个长度值，或百分比，或top，center，bottom；

## 5、3D变换transform（3D）

### （1）基本概念

3D变换是在2D变换的基础上，再加上一个维度（z轴），构成了三维空间。

新加上的这个z轴，是跟网页页面（电脑屏幕）垂直的那个方向，也就是眼睛到屏幕的“垂直线”。

相当于将网页元素（一个矩形的平面）置于3D空间中，并对其实行某种变换。

### （2）主要属性

3D变换仍然还使用2D变换的2个属性（transform和transform-origin），不过在transform的属性值中，又增加了若干变换函数，以达到在3D空间中将盒子进行某种变换操作的目的。

另外，对于3D变换，还会多出来几个属性，分别用于设定3D变换场景下所需要的一些特征信息。 

3D变换的主要属性有：

- transform-style：

  用于设定元素变换的方式（2D还是3D），默认是flat（平面，也就是2D）；

  设置为preserve-3d，就可以实现3D变换。

  注意：该属性应该设置在变换元素的父级元素上。

- perspective：

  透视距离，用于设定观察3D视图时眼睛离屏幕（也就是z=0）的距离，即观察点的远近。

  默认透视距离是“无穷大”，即最远处。 

  注意：该属性应该设置在变换元素的上级元素上。 

- perspective-origin： 

  透视点，即观察3D视图时眼睛的位置，也就是眼睛直对屏幕的那个点在（x，y）坐标系上的坐标值。

  默认为（center，center），也就是父元素的中心点。

  注意：该属性应该设置在变换元素的上级素上。

- transform-orgin ：

  含义跟2D变换一样，用于指定元素变换时的“原点”（基点）；

- transform：

  含义跟2D变换一样，只是多了一些有关3D变换的变换函数，主要有： 

  - translateX(x), translateY(y), translateZ(z), translate3d(x, y, z)：
  - rotateX(x角度), rotateY(y角度), rotateZ(z角度), rotate3d(x, y, z, deg)：旋转变换；其旋转规则为： 
    - 左手“抓住”某轴，大拇指指向该轴正方向，则正值会沿其余手指的方向旋转，否则相反；
    - rotate3d中，x，y，z是数值，是相对大小，deg才是角度。 
  - scaleX(x), scaleY(y), scaleZ(z), scale3d(x, y, z)：缩放变换 。

### （3）案例

```html+css
<style>
		.box{
			border:solid 1px red;
			width: 800px;
			height:500px;
			margin:10px auto ;
			padding-top:50px;
		}
		.box>.pic{
			border:solid 2px blue;
			width:200px;
			height:300px;
			position:relative;
			margin:0 auto;
			perspective: 1000px;
			perspective-origin:center -100px;
			transform-style:preserve-3d;
		}
		.box>.pic>img{
			width:200px;
			height:300px;
			position:absolute;
			left:0;
		}
		.box>.pic>img:nth-child(1){
			transform:rotatey(0deg) translatez(300px);
		}
		.box>.pic>img:nth-child(2){
			transform:rotatey(40deg) translatez(300px);
		}
		.box>.pic>img:nth-child(3){
			transform:rotatey(80deg) translatez(300px);
		}
		.box>.pic>img:nth-child(4){
			transform:rotatey(120deg) translatez(300px);
		}
		.box>.pic>img:nth-child(5){
			transform:rotatey(160deg) translatez(300px);
		}
		.box>.pic>img:nth-child(6){
			transform:rotatey(200deg) translatez(300px);
		}
		.box>.pic>img:nth-child(7){
			transform:rotatey(240deg) translatez(300px);
		}
		.box>.pic>img:nth-child(8){
			transform:rotatey(280deg) translatez(300px);
		}
		.box>.pic>img:nth-child(9){
			transform:rotatey(320deg) translatez(300px);
		}

	</style>
</head>
<body>
	<div class="box">
		<div class="pic">
			<img src="images/girl1.jpg" alt="">
			<img src="images/girl2.jpg" alt="">
			<img src="images/girl3.jpg" alt="">
			<img src="images/girl4.jpg" alt="">
			<img src="images/girl5.jpg" alt="">
			<img src="images/girl6.jpg" alt="">
			<img src="images/girl7.jpg" alt="">
			<img src="images/girl8.jpg" alt="">
			<img src="images/girl9.jpg" alt="">
		</div>
	</div>
```

## 6、过渡效果transition

### （1）基本概念

过渡（transition）是指，能够让一个元素的属性，从某个值，变换到另一个值的时候，不是表现为“立即实现”（突然变化），而是表现为“逐步变化”，则视觉效果看起来就是“动画效果”了 。

过渡效果在应用中通常结合鼠标的动作而展现出来，最常见的就是使用“:hover”伪类。

过渡效果的设置主要设置如下几项：

​	参与过渡的属性名，过渡的时长，过渡的方式，以及过渡发生前的延迟时间。

### （2）主要属性

- transition-property：要用于实现过渡的属性名；
- transition-duration：过渡时长；比如：2s；
- transition-timing-function：过渡方式；常用的过渡方式如下所示：
  - linear：线性过渡。
  - ease：平滑过渡，这是默认值 
  - ease-in：由慢到快。 
  - ease-out：由快到慢 。
  - ease-in-out：由慢到快再到慢。
- transition-delay：过渡效果发生前的延迟时长，比如：1s 。
- transition：以上4属性的综合属性，并可以设定多属性过渡（比如位置和颜色同时变化)，形式如下： 
  - transition：第1个过渡 【，第2个过渡】【，第3个过渡】 【......】；
  - 每个过渡的形式为：过渡属性名  过渡时长  【过渡方式】【延迟时长】；

代码示例：

```css
/*示例1*/
transition-property: width;
transition-duration: 2s;
transition-timing-function: ease-in-out;
trasitiion-delay: 3s;
/*示例2*/
transition: width  2s  ease-in-out  3s;
/*示例3*/
transition-property: width,  height,  background ;
transition-duration: 2s  3s  3s;
transition-timing-function: ease  ease-in-out  linear;
trasitiion-delay: 3s  2s  0s;
/*示例4*/
transition: width 2s  ease , height 2s 2s  linear, background 2s  4s ;
```

**transition-timing-function的效果研究：** 

```html+css
<style>
	/**
	 * transition-timing-function：过渡方式；常用的过渡方式如下所示：
	 * linear：线性过渡。
	 * ease：平滑过渡，这是默认值
	 * ease-in：由慢到快。
	 * ease-out：由快到慢。
	 * ease-in-out：由慢到快再到慢。
	 */
		.box{
			width:1000px;
			border:solid 1px red;
		}
		.box>div{
			width:100px;
			height:50px;
			border:solid 1px blue;
			margin:5px;
		}
		.box:hover>div{margin-left:850px;}

		.box>.box1{transition: margin-left  10s linear;}
		.box>.box2{transition: margin-left  10s ease;}
		.box>.box3{transition: margin-left  10s ease-in;}
		.box>.box4{transition: margin-left  10s ease-out;}
		.box>.box5{transition: margin-left  10s ease-in-out;}

	</style>
</head>
<body>
	<div class="box">
		<div class="box1">linear</div>
		<div class="box2">ease</div>
		<div class="box3">ease-in</div>
		<div class="box4">ease-out</div>
		<div class="box5">ease-in-out</div>
	</div>
</body>
```

## 7、动画效果animation

### （1）基本概念和语法

动画效果其实可以看着过渡效果的升华版：

​	过渡效果是实现元素在某个（或某些）属性的两个不同值之间的状态变化效果；

​	动画效果是预先定义好某个（或某些）属性的多个不同值之间的状态变化效果，并对之命名，而后可多次应用在不同的元素上。

简单说就是：

​	过渡效果是“实现某元素的某种状态变化效果”，

​	动画效果是“定义某种状态变化效果，并可拿来用”。

动画效果的基本语法如下：

```css
<style>
@keyframes  动画名{
    0% {属性设置。。。}		/*表示动画的起始处/*
    ...... {属性设置。。。}	/*这表示还可以设置中间的若干状态*/
    100% {属性设置。。。}		/*表示动画的结束处/*
}
选择器{
	animation：动画名 动画播放设置；		/*动画播放设置有若干项控制项*/
}
</style>
```

> 说明：
>
> - 可以设置（定义）若干个动画(取不同名称)，后续都可以用在不同的元素上（选择器所决定）； 
> - 每个动画可以定义若干个关键状态（百分比决定），通常至少需要0%和100%；
> - 每个状态可以定义若干个属性值，表示动画播放到该时刻时的元素外观表现；
> - 属性的设置跟通常css的属性设置一样，比如：color:red; width:200px; transform:rotate(90deg);  
> - 动画播放设置中可以设置若干项，比如：持续时间，播放方式，延迟时间，是否循环，等等； 

### （2）主要属性

- animation-name：动画名；
- animation-duration：动画持续时间；
- animation-timing-function：动画播放播放方式（效果），也有如下几个常用的效果名：
  - linear：线性过渡，就是匀速进行
  - ease：平滑过渡，这是默认值 
  - ease-in：由慢到快。 
  - ease-out：由快到慢 。
  - ease-in-out：由慢到快再到慢。
- animation-delay：动画播放前的延迟时间； 
- animation-iteration-count：动画播放循环次数，使用数字或infinite（无限）；
- animation-direction：动画播放方向（正向还是反向），可用的值有：
  - normal：常规（就是从前往后播放）
  - reverse：反向（就是从后往前播放） 
  - alternate：交替（就是先从前往后，再从后往前），播放次数大于1次才有意义 
  - alternate-reverse：反向交替（就是先从后往前，再从前往后），播放次数大于1次才有意义 
- animation-fill-mode：动画停止（播放结束）时元素停留的状态，可用的值有：
  - forwards：     停留在前面（动画播放的结尾处）； 
  - backwards：   停留在后面（动画播放的开时处）； 
  - both：           两边都可停（动画停在哪边就哪边）； 
- animation-play-state：设置动画启动或暂停，有两个可用的值：
  - running：       运行状态（默认值），也就是运行动画效果； 
  - paused：        暂停状态，也就是动画效果运行中停下来（此时如果需要还可以继续运行）；
- animation：上述属性的综合属性，并依次按该顺序列出（不需要的项直接省略）。

### （3）案例

```css
@keyframes  ani1{ 
    0%{		background:red; 	transform:rotate(0deg);}
    100%{	background:blue; 	transform:rotate(360deg);}
}
.c1{
    animation-name: ani1;
    animation-duration: 3s;
    animation-timing-function: ease-in-out;
    animation-iteration-count:infinite;
}
```

```css
$keyframes  ani1{ 
    0%{		background:red; 	transform:rotate(0deg);}
    100%{	background:blue; 	transform:rotate(360deg);}
}
.c1{
	animation: ani1  3s  ease-in-out  infinite;
}
```

演示**animation-direction，和animation-fill-mode：** 

```css+html
	<style>
		@keyframes moveLeft2Right{
			0%{
				left:0px;
			}
			100%{
				left:800px;
			}
		}
		div{
			border:solid 1px red;
			width: 100px;
			height:50px;
			margin:5px;
			position:relative;
			left:0px;
			animation-name:moveLeft2Right;
			animation-timing-function:linear;
			animation-duration: 5s;
			animation-iteration-count:3;

		}
		.box1{
			animation-direction: normal;
			animation-fill-mode: forwards;
		}
		.box1:hover{
			animation-play-state:paused;
		}
		.box2{
			animation-direction: reverse;
			animation-fill-mode: backwards;
		}
		.box3{
			animation-direction: alternate;
			animation-fill-mode: both;
		}
		.box4{
			animation-direction: alternate-reverse;
			animation-fill-mode: both;
		}
	</style>
</head>
<body>
	<div class="box1">normal, forwards</div>
	<div class="box2">reverse, backwards</div>
	<div class="box3">alternate, both</div>
	<div class="box4">alternate-reverse, both</div>
</body>
```

连续播放效果：

```html
	<style>
		@keyframes xuanzhuan{
			0%{
				transform:rotatex(-15deg) rotatey(0deg);
			}
			100%{
				transform:rotatex(-15deg) rotatey(360deg);
			}
		}
		.box{
			border:solid 0px red;
			width:960px;
			margin:50px auto 10px;
			perspective: 1200px;
			perspective-origin: center center;

		}
		.box>.container{
			border:solid 0px blue;
			width:200px;
			height:300px;
			position: relative;
			left:50%;
			margin-left:-100px;
			transform-style:preserve-3d;

			transform:rotatex(-15deg);

			animation-name: xuanzhuan;
			animation-duration: 6s;
			animation-timing-function: linear;
			animation-iteration-count: infinite;
		}
		.box>.container:hover{
			animation-play-state: paused;
		}
		.box>.container>img{
			width:200px;
			height:300px;
			position: absolute;
			left:0;
			top:0;
			transform-origin: center center;
		}
		.box>.container>img:nth-child(1){transform: rotatey(0deg) translatez(300px)}
		.box>.container>img:nth-child(2){transform: rotatey(40deg) translatez(300px)}
		.box>.container>img:nth-child(3){transform: rotatey(80deg) translatez(300px)}
		.box>.container>img:nth-child(4){transform: rotatey(120deg) translatez(300px)}
		.box>.container>img:nth-child(5){transform: rotatey(160deg) translatez(300px)}
		.box>.container>img:nth-child(6){transform: rotatey(200deg) translatez(300px)}
		.box>.container>img:nth-child(7){transform: rotatey(240deg) translatez(300px)}
		.box>.container>img:nth-child(8){transform: rotatey(280deg) translatez(300px)}
		.box>.container>img:nth-child(9){transform: rotatey(320deg) translatez(300px)}
	</style>
</head>
<body>
	<div class="box" title="场景，舞台">
		<div class="container" title="容器">
			<img src="images/girl1.jpg" alt="">
			<img src="images/girl2.jpg" alt="">
			<img src="images/girl3.jpg" alt="">
			<img src="images/girl4.jpg" alt="">
			<img src="images/girl5.jpg" alt="">
			<img src="images/girl6.jpg" alt="">
			<img src="images/girl7.jpg" alt="">
			<img src="images/girl8.jpg" alt="">
			<img src="images/girl9.jpg" alt="">
		</div>
	</div>
</body>
```

**一走一停播放效果的关键代码：**

```html
		@keyframes xuanzhuan{
			0%{transform:rotatex(-15deg) rotatey(0deg);}
			/*表示从0%时间到2%时间，旋转从0到40deg，下同*/
			2%{transform:rotatex(-15deg) rotatey(40deg);}
			/*表示从2%时间到11%时间，旋转不变，即不旋转，下同*/
			11%{transform:rotatex(-15deg) rotatey(40deg);}

			13%{transform:rotatex(-15deg) rotatey(80deg);}
			22%{transform:rotatex(-15deg) rotatey(80deg);}
			
			24%{transform:rotatex(-15deg) rotatey(120deg);}
			33%{transform:rotatex(-15deg) rotatey(120deg);}

			35%{transform:rotatex(-15deg) rotatey(160deg);}
			44%{transform:rotatex(-15deg) rotatey(160deg);}

			46%{transform:rotatex(-15deg) rotatey(200deg);}
			55%{transform:rotatex(-15deg) rotatey(200deg);}

			57%{transform:rotatex(-15deg) rotatey(240deg);}
			66%{transform:rotatex(-15deg) rotatey(240deg);}

			68%{transform:rotatex(-15deg) rotatey(280deg);}
			77%{transform:rotatex(-15deg) rotatey(280deg);}

			79%{transform:rotatex(-15deg) rotatey(320deg);}
			88%{transform:rotatex(-15deg) rotatey(320deg);}

			90%{transform:rotatex(-15deg) rotatey(360deg);}
			99%{transform:rotatex(-15deg) rotatey(360deg);}
		}
```

滑动门效果：

```html
	<style>
		.nav{
			display:flex;
		}
		.nav>a{
			display: inline-block;
			height:35px;
			padding-left:7px;
			background: url(images/bg_r1_c1.png) left top no-repeat;
		}
		.nav>a:hover{
			background-image: url(images/blue_r1_c1.png);
		}
		.nav>a>span{
			display: inline-block;
			height:35px;
			line-height: 35px;
			padding-right:25px;
			background: url(images/bg_r1_c2.png) right top no-repeat;
		}
		.nav>a:hover>span{
			background-image: url(images/blue_r1_c2.png);
		}
	</style>
</head>
<body>
	<div class="nav">
		<a href=""><span>首页</span></a>
		<a href=""><span>三个字</span></a>
		<a href=""><span>四字标题</span></a>
		<a href=""><span>五个字标题</span></a>
	</div>
```

手风琴效果：

```html
	<style>
		.box{
			display: flex;
			border:solid 1px red;
			width:600px;
			margin:0 auto;
		}
		.box>div{
			/*下一行表示，如果容器盒子放下子盒子的设置宽度还有剩余，就去按该比例“分配”
			这里，因为所有div都是1，所以就是均分剩余空隙*/
			flex:1;
			height:240px;
			width:100px;
			margin:1px;
			border:solid 1px blue;
			transition:flex 1s, background 1s;
		}
		.box>div:hover{
			flex:1.5;
			background: yellow;
		}

	</style>
</head>
<body>
	<div class="box">
		<div>内容1内容1内容1内容1内容1内容1内容1内容1内容1内容1内容1内容1内容1内容1内容1内容1内容1</div>
		<div>内容2内容2内容2内容2内容2内容2内容2内容2内容2内容2</div>
		<div>内容3内容3内容3内容3内容3内容3内容3内容3内容3内容3内容3内容3内容3内容3内容3内容3内容3内容3内容3内容3内容3</div>
		<div>内容4内容4内容4内容4内容4内容4</div>
		<div>内容5内容5内容5内容5内容5内容5内容5内容5内容5内容5内容5内容5内容5内容5内容5内容5内容5内容5内容5内容5内容5内容5</div>
	</div>
</body>
```

# 八、额外

## 1、光标形状设置cursor

含义：

​	设置鼠标在某个盒子上的时候的光标形状。

形式： 

​	cursor：光标形状名；

常用的光标形状名有：

​	default（默认）,  pointer（手形）,  text（文本编辑形）,  help（帮助）,  wait（等待）。

在实际网页中，我们常常并不使用a标签，但也同样做出有a标签的效果（链接，手的形状）。

## 2、盒子缩放zoom 

- 含义：

​	用于设置某个盒子在其本来的大小基础上进行一定的大小缩放。

- 形式 ：

​	zoom: 缩放比例；              //缩放比例可以是数字或百分比。

> 说明：
>
> ​	它是对整个盒子进行整体缩放，无法做到横向纵向单独控制的缩放。
>
> ​		对比：transform:scale()可以实现横向纵向单独控制的缩放。 
>
> ​	zoom缩放的盒子是“实质上”改变了大小，因而也会影响其后续元素的位置。
>
> ​		对比：transfor:scale()m实现的缩放不会影响后续元素的位置，只是视觉上的改变。

## 3、文字阴影text-shadow

- 形式： 

  box-shadow：水平偏移值  垂直偏移值 【模糊值】【颜色】 ； 

- 说明：

  偏移值可以为负 。

  模糊值不能为负。

  颜色如不设置，则默认随字体颜色。一般设置为灰色（gray）比较逼真。 

  可以设置多个阴影，每个阴影的设置相互用逗号（，）隔开就可以。

- 举例：

  .box1{ text-shadow: 2px 2px red; } 

  .box2{ text-shadow: 2px 5px 2px #00FFFF; } 

  .boxe{ text-shadow: 2px 5px 0 red, -2px -2px 0 #f0f0f0;

- 演示案例： 

  ```html
  	<style>
  		.box1{
  			font-size:40px;
  			text-shadow: 2px 2px 0px  red;
  		}
  		.box2{
  			font-size:40px;
  			text-shadow: 2px 2px 0px  red, -2px -2px 0px  red;
  		}
  		.box3{
  			font-size:100px;
  			background: gray;
  			color:gray;
  			text-shadow:-2px -2px 0 white, 2px 2px 0 black;
  		}
  		.box4{
  			font-size:100px;
  			background: gray;
  			color:gray;
  			text-shadow:-2px -2px 0 black, 2px 2px 0 white;
  		}
  	</style>
  </head>
  <body>
  	<div class="box1">一些文字，some texts</div>
  	<div class="box2">一些文字，some texts</div>
  	<hr>
  	<h3>凹凸文字效果</h3>
  	<div class="box3">一些文字，some texts</div>
  	<div class="box4">一些文字，some texts</div>
  </body>
  ```

  彩色文字：

  本质：    就是用“图”作为文字“笔画线”的背景！

  这里的图，我们用这个：background-image: linear-gradient（）；

  再 结合这个属性：background-clip：text；            /\*背景从文字笔画线以外裁切掉\*/

  以及结合这个属性：text-fill-color: transparent;        //设置文字笔画线为透明色。

  举例：

  ```html
  	<style>
          .box{
              display: inline-block;
              font-size: 30px;
              background-image:linear-gradient(90deg, red, orange, yellow, green, aqua, blue, purple, red);
              background-size: 100px; 100px;
              /*各浏览器的兼容代码要卸载前面！*/
              -webkit-background-clip: text;
              background-clip:text;	/*背景从文字比划线以外裁切掉*/
              -webkit-text-fill-color: transparent;
              -moz-text-fill-color: transparent;
              text-fill-color:transparent;	/*文字为透明色*/
          }
  	</style>
  <body>
      <div>
          <div class="box">
              一些文字。一些文字。一些文字。一些文字。一些文字。一些文字。
          </div>
      </div>
  </body>
  ```

## 4、文字溢出text-overflow

设置一行文字在一行显示不下但又不允许换行时的表现形式，有两个可用值：

​	text-overflow: clip | ellipsis

​		clip：直接切掉（不显示）；

​		ellipsis: 切掉后续部分并添加英文省略号（...）

注意：

使用该属性要求容器盒子设置overflow为非visible，width为非auto，且white-space为不允许换行（nowrap）。

white-space：用于设定文字在行尾碰到空格的时候，是否换行下来。 

​	常用值：wrap（可换行，默认值）；  no-wrap（不可换行）

## 5、盒子模型box-sizing

含义：

​	所谓盒子模型，是指css中，设置一个盒子的宽高（width，height）值，是按盒子的“内容区”设置，还是按盒子的“边框区”设置的问题。

​	传统上，设置盒子的宽高指的是设置盒子内容区的宽高。

​	这个属性就是可以改变这个特性，可以将盒子的宽高属性，指定为是盒子的边框区域的宽高值。

可用值：

box-sizing: content-box;        //内容模式，也就是传统的模式

box-sizing: border-box;         //边框模式，设置宽高值（width，height）包括了border在内的范围。

**内容模式**的盒子实际占据宽度为：

​	margin-left + border-left + padding-left + **width** + padding-right + border-right + margin-right；

**边框模式**的盒子实际占据宽度为：

​	margin-left + **width** + margin-right；

​	此模式有时候称为“减模式”，就是实际内容区的宽度，是从设置的宽度（width）减去border和padding 

高度方向同理。

案例：

```html
	<style>
	/**
	 * 假设：
	 * 1，整体宽度为300x280.
	 * 2， 主体灰色边框线为1px
	 * 3，公开课上面的红色边框线为2px。
	 * 4，头部区域高度（含边框线）为40px。
	 */
	.tab{
		box-sizing:border-box;
		width:300px;
		border:1px solid gray;
		border-top:none;
	}
	ul{
		list-style: none;
	}
	ul>li{
		text-indent: 25px;
		background:url(images/tubiao.png) no-repeat 0px 0px;
	}
	.top{
		overflow: hidden;/*清除浮动*/
	}
	.top>.left{
		float:left;
		box-sizing: border-box;
		height:40px;
		border-top: solid 2px red;
		width:50%;
		line-height: 38px;
		text-align: center;
		font-size:18px;
		color:red;
	}
	.top>.right{
		float:right;
		box-sizing: border-box;
		height:40px;
		border: solid 1px gray;
		border-right:none;
		width:50%;
		padding-right:15px;
		line-height: 38px;
		text-align: right;
		background:#e0e0e0
	}
	</style>
```

## 6、居中大全

### （1）文字居中：

左右居中：

​	text-align:center;

垂直居中：

​	一行文字可以做到：

​	line-height: 盒子高度；

### （2）不同大小图片在固定盒子中居中

方法1：

​	左右居中：

​		父盒子：text-align: center；

​	上下居中：

​		父盒子中： line-height: 父盒子高度

​		图片本身：  verticle-align:middle;

方法2：

​	图片：positon: relative

​	左右居中：

​		left: 50% ；          50%是父盒子的水平方向中间位置

​		margin-left :-图宽/2 

​	上下居中：

​		top: 50%；            50%是父盒子的垂直方向中间位置

​		margin-top:  - 图高/2

**方法3：——兼容性好！**

​	父盒子：

​		display: table-cell;         //将盒子转换为单元格，此时其跟一个单元格一样表现。

​	左右居中：

​		父盒子上：text-align: center;

​	上下居中：

​		父盒子上：verticle-align: middle;

**方法4：——兼容性好！**

​	左右上下居中：

​		图片上： postion: relative;

​		left:50%;

​		top:50%

​		transform: translate(-50%, -50%);