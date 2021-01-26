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
