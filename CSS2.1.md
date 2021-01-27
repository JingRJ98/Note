# 定位
对于浮动元素，包含块定义为最近的块级祖先元素  
对于定位，根元素的包含块由用户代理建立，在HTML中，根元素就是html，可是有些浏览器会使用body作为根元素，在大多数浏览器中，初试包含块是一个视窗大小的矩形  
根元素的包含块就是初试包含块，初试包含块不等于视口  
非根元素，position值为relative或者static，包含块为最近的块级框  
非根元素，position值为absolute，包含块为最近的position不是static的祖先元素  
-如果祖先元素时块级元素，则包含块由内边距边界组成，由该祖先元素的边框界定的区域  
-如果没有祖先，元素的包含块为初始包含块  
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>定位</title>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        .box3{
            border: 10px red solid;
            padding: 10px;
        }
        .box1{
            width: 200px;
            height: 200px;
            background-color: #abf;
            position: relative;
            /* 
                position为relative或者static的非根元素，相对于最近的框元素定位(内边距边框)
             */
             padding: 10px;
        }
        .box2{
            width: 100px;
            height: 100px;
            background-color: #bfa;
            /* 非根元素，position值为absolute，包含块为最近的position不是static的祖先元素,如果祖先元素时块级元素，则包含块由内边距边界组成，由该祖先元素的边框界定的区域  */
        }
    </style>
</head>
<body>
    <div class="box3">
        <div class="box1">
            <div class="box2"></div>
        </div>
    </div>
 
</body>
</html>
```
# 盒模型相关属性默认值
`left`/`top`/`right`/`bottom ` / `width`/` height` 默认值auto 
`margin` /`padding `默认值0 
`border-width `默认值medium
## 盒模型百分比参考
元素的`width` `height`百分比参考于包含块的`width` `height`
元素的`margin` `padding`百分数参考于包含块的`width`
# 浮动
float最初的设计初衷，是为了实现图文混排效果，让文字环绕图片，float脱离文档流但不脱离文本流，也就是文本还会承认元素浮动前所占的区域，围绕它布局；但是其他元素比如div会忽视它的存在进行布局
# 三列布局
要求  
1、两边固定，当中自适应
2、当中内容要完整显示
3、当中优先加载  

定位写三列布局的缺点，定位必须要有包含块开启相对定位，提升层级，不利于写网页布局  
浮动写三列布局，无法实现当中列优先加载  
## 圣杯布局
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>圣杯布局</title>
    <style>
        #header,
        #footer{
            height: 50px;
            line-height: 50px;
            background-color: #abf;
            border: 1px red solid;
            text-align: center
        }
        #body .left,
        #body .right{
            width: 200px;
            background-color: yellow;
            /* 开启浮动后父元素需要解决高度塌陷 */
            float: left;
        }
        /* 解决高度塌陷 */
        .clearfix::before,
        .clearfix::after{
            content: '';
            display: table;
            clear: both;
        }
        #body .middle{
            background-color: red;
            /* 让left和right上来需要开启浮动 */
            float: left;
            /* 浮动的元素宽高只占内容大小 所以指定宽度100%包含块宽度 */
            width: 100%;
        }
        #body .left{
            /* -100%和middle的包含块一样，所以向左边移动一个middle的宽度 */
            margin-left: -100%;
            position: relative;
            left: -200px;
        }
        #body .right{
            /* -200px指right的向左移动自己的宽度 居于middle的右边 */
            margin-left: -200px;
            position: relative;
            right: -200px;
        }
        /* 
            让middle显示出来
            然后给left和right开启相对定位
         */
        #body{
            padding: 0 200px;
            /* 添加一个min-width否则最小窗口布局会乱 */
            min-width: 800px;
        }

    </style>
</head>
<body>
    <!-- 
        要求
        1、两边固定 当中自适应
        2、当中列要完整显示
        3、当中列要优先加载
     -->
    <div id="header">header</div>
    <div id="body" class="clearfix">
        <!-- 中间优先加载 写在最上面 -->
        <div class="middle">middle</div>
        <div class="left">left</div>
        <div class="right">right</div>
    </div>
    <div id="footer">footer</div>
</body>
</html>
```
## 圣杯伪等高布局
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>圣杯布局</title>
    <style>
        #header,
        #footer{
            height: 50px;
            line-height: 50px;
            background-color: #abf;
            border: 1px red solid;
            text-align: center
        }
        #body .left,
        #body .right{
            width: 200px;
            background-color: yellow;
            /* 开启浮动后父元素需要解决高度塌陷 */
            float: left;
        }
        /* 解决高度塌陷 */
        .clearfix::before,
        .clearfix::after{
            content: '';
            display: table;
            clear: both;
        }
        #body .middle{
            background-color: red;
            /* 让left和right上来需要开启浮动 */
            float: left;
            /* 浮动的元素宽高只占内容大小 所以指定宽度100%包含块宽度 */
            width: 100%;
        }
        #body .left{
            /* -100%和middle的包含块一样，所以向左边移动一个middle的宽度 */
            margin-left: -100%;
            position: relative;
            left: -200px;
        }
        #body .right{
            /* -200px指right的向左移动自己的宽度 居于middle的右边 */
            margin-left: -200px;
            position: relative;
            right: -200px;
        }
        /* 
            让middle显示出来
            然后给left和right开启相对定位
         */
        #body{
            padding: 0 200px;
            /* 添加一个min-width否则最小窗口布局会乱 */
            min-width: 800px;
        }
        /* 
            伪等高布局
                将left right 和middle的padding向下延拓
                body的margin回到原来的位置
                裁剪多余空间
         */
        #body .left,
        #body .middle,
        #body .right{
            padding-bottom: 100000px;
            margin-bottom: -100000px;
        }
        #body{
            overflow: hidden;
        }
    </style>
</head>
<body>
    <!-- 
        要求
        1、两边固定 当中自适应
        2、当中列要完整显示
        3、当中列要优先加载
     -->
    <div id="header">header</div>
    <div id="body" class="clearfix">
        <!-- 中间优先加载 写在最上面 -->
        <div class="middle">middle
            <p>我是字</p>
            <p>我是字</p>
            <p>我是字</p>
            <p>我是字</p>
            <p>我是字</p>
            <p>我是字</p>
            <p>我是字</p>
            <p>我是字</p>
            <p>我是字</p>
            <p>我是字</p>
            <p>我是字</p>
            <p>我是字</p>
            <p>我是字</p>
            <p>我是字</p>
        </div>
        <div class="left">left</div>
        <div class="right">right</div>
    </div>
    <div id="footer">footer</div>
</body>
</html>
```
## 双飞翼伪等高布局
双飞翼布局和圣杯布局的不同点  

圣杯布局将body设置padding再将left和right通过相对行为设置到middle的两边

双飞翼布局在middle中再设置一个div 将内容写在div中，对div设置padding


双飞翼布局和圣杯布局的共同点

两种布局都将中间列写在前面优先加载，都将三列浮动然后通过负外边距完成布局
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>双飞翼伪等高布局</title>
    <link rel="stylesheet" href="./reset.css">
    <style>
        body{
            /* 设置最小宽度确保middle有内容显示 */
            /* 最小宽度设置为2*left+right */
            min-width: 600px;
        }
        .header,
        .footer{
            height: 50px;
            background-color: silver;
        }
        /* 设置body */
        /* 设置伪等高 */
        .body{
            overflow: hidden;
        }
        .body .middle,
        .body .left,
        .body .right{
            padding-bottom: 10000px;
            margin-bottom: -10000px;
            float: left;
        }
        .body .left,
        .body .right{
            background-color: #bfa;
            width: 200px;
        }
        .body .middle{
            width: 100%;
            background-color: #abf;
        }
        .body .left{
            margin-left: -100%;
        }
        .body .right{
            margin-left: -200px;
        }
        /* 
            双飞翼布局和圣杯布局的不同点
                圣杯布局将body设置padding再将left和right通过相对行为设置到middle的两边
                双飞翼布局在middle中再设置一个div 将内容写在div中，对div设置padding
        */
        .body .middle .box1{
            padding: 0 200px;
        }
    </style>
</head>
<body>
    <div class="header"></div>
    <div class="body">
        <div class="middle">
            <div class="box1">
                <p>我是字</p>
                <p>我是字</p>
                <p>我是字</p>
                <p>我是字</p>
                <p>我是字</p>
                <p>我是字</p>
            </div>
        </div>
        <div class="left">
            <p>left</p>
        </div>
        <div class="right">
            right
        </div>
    </div>
    <div class="footer"></div>
</body>
</html>
```
# 解决IE6的fixed失效问题（使用绝对定位模拟固定定位）
当html和body其中有一个设置了overflow滚动条设置给文档  
当html和body两个都设置了overflow的滚动条作用给文档，body的滚动条作用给自己  
div的父元素是body，body的父元素是html，html的包含块是视窗大小的初始包含块
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <link rel="stylesheet" href="./reset.css">
    <style>
        html,body{
            /* 子元素撑开的高度 */
            height: 100%;
            /* 禁止系统滚动条 */
            overflow: hidden;
        }
        body{
            /* 
                因为html和body都设置了overflow
                所以此时body的滚动条作用给自己（body）
                此时滚动条滚动的是body而非初始包含块
                因为body里面的开启绝对定位的元素相对于初始包含块定位的，
                初始包含块没有移动
                所以用绝对定位模拟了固定定位
                固定定位是相对于视口定位的，初始包含块一般就是一个视口大小的矩形
            */
            overflow: auto;
            border: 2px red solid;
        }
        .test{
            width: 200px;
            height: 200px;
            background-color: #abf;
            /* 写在第一个div下面看不见，开启绝对定位 */
            position: absolute;
            left: 100px;
            top: 100px;
        }
    </style>
</head>
<body>
    
    <div class="box1" style="height: 2000px;"></div>
    <!-- 此时系统出现滚动条 -->
    <div class="test"></div>
</body>
</html>
```
# stickyfooter 粘连布局
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>Document</title>
    <style>
        /* 
            要求
            1、main的内容足够长时，footer跟着main
            2、main的长度达不到页面高度时，footer保持在页面底部
        */
        *{
            margin: 0;
            padding: 0;
        }
        html,
        body{
            height: 100%;
        }
        .container{
            /* 
                实际上.container容器不能定死高度，否则footer永远位于页面底部
                .container的最小高度为100%（继承自html下的body）
                当.main的内容足够长时，.container的高度被其中的.main撑开
            */
            min-height: 100%;
        }
        /* 设置footer样式 */
        .footer{
            height: 60px;
            line-height: 60px;
            text-align: center;
            background-color: silver;
            /* 负margin将footer移动上来 */
            margin-top: -60px;
        }
        /* 
            此时还有个问题，当main中内容足够多时，底部会和footer重叠
            应该给.main设置padding-bottom
            为什么不给.container加padding
            因为加后会发生.container加高60px，footer挤到下面
        */
        .main{
            padding-bottom: 60px;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="main">
            main<br>
            main<br>
            main<br>
            main<br>
            main<br>         
        </div>
    </div>
    <div class="footer">
        footer
    </div>
</body>
</html>
```
# BFC
## box
box是CSS布局的基本对象和单位,一个页面由许多box组成  
display属性决定了box的类型，不同类型的box，会参与不同的formatting context(一个决定如何绚烂文档的容器)

block-levelbox  
display属性为table/block/list-item的元素，会生成block-level box参与box formatting context（BFC）

inline-level box  
display属性为inline/inline-block/inline-table 的元素，会生成inline-level box ，参与inline formatting context
## 定义
BFC(Block formatting context)直译为“块级格式化上下文”。它是一个独立的渲染区域，只有Block-level box参与，它规定了内部的Block-level box如何布局，并且与这个区域外部毫不相干
## 布局规则
1.内部的Box会在垂直方向，一个接一个放置  
2.BFC的区域不会与float box重叠 （两列布局）   
3.内部的box垂直方向的距离由margin决定，属于同一个BFC的两个相邻box的margin会发生重叠 （兄弟元素margin重叠问题）    
4.计算BFC的高度时，浮动元素也参与计算（清除浮动 haslayout）  
5.BFC就是页面上的一个隔离的独立容器，容器里面的元素不会影响到外面的元素，反之也如此。  
## BFC什么时候出现
1.根元素  
2.float属性不为none  
3.position为absolute或fixed    
4.overflow不为visible    
5.display为inline-block,table-cell,table-caption,flex,inline-flex
## 两列布局
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        body{
            min-width: 600px;
        }
        .left{
            width: 200px;
            height: 200px;
            background-color: #bfa;
            float: left;
        }
        .right{
            height: 200px;
            background-color: #abf;
            overflow: hidden;
        }
    </style>
</head>
<body>
    <div class="left">left</div>
    <div class="right">right</div>
</body>
</html>
```
# 兄弟元素margin重叠问题
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        /* 
            发生，margin重叠的三个条件
                1、属于同一个BFC
                2、两个相邻的box
                3、块级元素
            margin重叠的三个条件只要有一个不满足就不会发生重叠
        */
        .box1,
        .box2,
        .box4,
        .box5,
        .box6,
        .box7{
            width: 200px;
            height: 200px;
            background-color: #abf;
            margin: 100px;
        }
        /* 
            不满足条件1
            box2放到另一个开启BFC的容器中
        */
        .box3{
            overflow: hidden;
        }
        /* 
            不满足条件2
            在box4和box5中间加一个有高度的div
            不建议，因为height发生变化了
        */
        .box{
            height: 1px;
        }
        /* 
            不满足条件3
            将其中一个box(box6)设置为inline-block
            不满足块元素
        */
        .box6{
            display: inline-block;
        }
    </style>
</head>
<body>
    <div class="box1">1</div>
    <div class="box3">
        <div class="box2">2</div>
    </div>

    <div class="box4">4</div>
    <div class="box"></div>
    <div class="box5">5</div>

    <div class="box6">6</div>
    <div class="box7">7</div>
</body>
</html>
```
# 父子元素的margin传递问题
```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        /* 
                BFC什么时候出现
                    1.根元素  
                    2.float属性不为none  
                    3.position为absolute或fixed    
                    4.overflow不为visible    
                    5.display为inline-block,table-cell,table-caption,flex,inline-flex
        */
        .box1 {
            width: 300px;
            height: 300px;
            background-color: #abf;
        }

        .box2 {
            width: 100px;
            height: 100px;
            background-color: #bfa;
            margin: 50px;
        }

        /* 
            发生margin重叠的三个条件
                1、属于同一个BFC
                2、两个相邻的box
                3、块级元素
            margin重叠的三个条件只要有一个不满足就不会发生重叠
        */
        /* 
            解决方法
                1、套一个div
                2、添加border隔开
                3、设置行内块
        */
        /* 1 */
        .box {
            /* 开启BFC第四条 */
            overflow: hidden;
        }
    </style>
</head>

<body>
    <div class="box1">
        <div class="box">
            <div class="box2"></div>
        </div>

    </div>
</body>

</html>
```
