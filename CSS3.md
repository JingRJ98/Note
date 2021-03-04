# 导学
CSS全称Cascading Style Sheets  
样式表由规则组成，规则由选择器 ＋ 声明块组成（CSS属性+CSS属性值组成的键值对）    
浏览器读取选择器的顺序为从从右往左` div ul li #id{} `  

# CSS的声明优先级
一个选择器的具体特殊性如下确定：   
1.内联声明的特殊性都是 1，0，0，0   
2.ID选择器的特殊性为 0，1，0，0  
3.类，属性和伪类选择器的特殊性为 0 ，0，1，0   
4.元素和伪元素选择器的特殊性为 0，0，0，1   
5.通配符选择器的特殊性 0，0，0，0   
6.结合符`,`对选择器特殊性没有一点贡献   
7.继承没有特殊性，权重连0 0 0 0的通配选择器都不如  

特殊性 1，0，0，0 大于所有以0开头的特殊性（不进位） 选择器的特殊性最终都会授予给其对应的声明 如果多个规则与同一个元素匹配，而且有些声明互相冲突时，特殊性越大的越占优势

### 重要声明
有时某个声明比较重要，超过了所有其他声明，CSS2.1称之为重要声明   
并允许在这些声明的结束分号之前插入` !important `来标志 必须要准确地放置` !important `否则声明无效 `!important `总是放在声明的最后，即分号的前面

### CSS样式来源
CSS样式的来源大致为三种： 1.开发人员 2.用户（Internet选项-辅助功能-用户样式表） 3.用户代理

权重（由高到底）： 用户的重要声明 开发人员的重要声明 开发人员的正常声明 用户的正常声明 用户代理的声明

# 自定义字体&字体图标
@font-face 允许网页开发者为其网页指定字体 字体能从远程服务器或者用户本地安装的字体加载    
如果提供了local()函数，从用户本地查找指定的字体名称，并且找到了一个匹配项, 本地字体就会被使用. 否则, 字体就会使用url()函数下载的资源  
注意：不能在一个CSS选择器中定义@font-face  
font-family 所指定的字体名字将会被用于font或font-family属性  

# 文本新增样式
### opacity
透明度 不是一个可继承属性 0~1
### text-shadow
text-shadow为文字添加阴影。可以为文字与 text-decorations 添加多个阴影，阴影值之间用逗号隔开。  
每个阴影值由元素在X和Y方向的偏移量、模糊半径和颜色值组成。  
默认值：none 不可继承  

color 可选。可以在偏移量之前或之后指定。如果没有指定颜色，则使用UA（用户代理）自行选择的颜色。 Note: 如果想确保跨浏览器的一致性，请明确地指定一种颜色

offset-x offset-y 必选。这些长度值指定阴影相对文字的偏移量。offset-x 指定水平偏移量，若是负值则阴影位于文字左边。 offset-y 指定垂直偏移量，若是负值则阴影位于文字上面。如果两者均为0，则阴影位于文字正后方（如果设置了blur-radius 则会产生模糊效果)。

blur-radius 可选。这是 length 值。如果没有指定，则默认为0。值越大，模糊半径越大，阴影也就越大越淡

语法：
```
/* offset-x | offset-y | blur-radius | color */
text-shadow: 1px 1px 2px black; 

/* color | offset-x | offset-y | blur-radius */
text-shadow: #fc0 1px 0 10px; 

/* 可以指定多层阴影，用逗号隔开 */
text-shadow: black 10px 10px 5px, red 20px 20px 5px; 
```
### 头像-背景模糊
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>模糊背景</title>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        .box{
            width: 100%;
            height: 100px;
            background-color: rgba(0,0,0,0.5);
            position: relative;
        }
        .box .bac{
            position: absolute;
            left: 0;
            right: 0;
            bottom: 0;
            top: 0;
            background-color: red;

            /* 降低层级 否则背景图在头像上面*/
            z-index: -1;
            /* 设置最下面的div背景为图片 */
            background: url(./img/1.JPG) no-repeat;
            /* 背景图按照背景的尺寸100%平铺 不重复 */
            background-size: 100% 100%;

            /* 设置模糊 */
            filter: blur(15px);

        }
        img{
            width: 64px;
            height: 64px;
            margin: 24px 24px;
        }
    </style>
</head>
<body>
    <div class="box">
        <img src="./img/1.JPG" alt="">
        <div class="bac"></div>
    </div>
</body>
</html>
```

### 文字描边
只有webkit才支持：-webkit-text-stroke（准确来说不能算是CSS3的东西，但需要知道）  
-webkit-text-stroke CSS属性为文本字符指定了宽 和 颜色   
它是-webkit-text-stroke-width 和-webkit-text-stroke-color属性的缩写.  
```
        h1{
            font: 46px;
            text-align: center;
            /* 文字描边 */
            -webkit-text-stroke: 1px red;
        }
```
### 文字排版
direction 属性用来设置文本、表列水平溢出的方向。   
rtl 表示从右到左 (类似希伯来语或阿拉伯语)， ltr 表示从左到右 (类似英语等大部分语言).   
从右到左一定要配合unicode-bidi:bidi-override;来使用  
```
        .box{
            width: 200px;
            height: 200px;
            border: 1px red solid;
            margin: 80px auto;
            direction: rtl;
            unicode-bidi:bidi-override;
        }
```
### 溢出显示省略号
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .box {
            /* 盒子如果靠内容撑开，则不会显示省略号 */
            /* display: inline; */
            width: 200px;
            height: 200px;
            border: 1px red solid;
            margin: 80px auto;
            /* 文字不换行 */
            white-space: nowrap;
            /* 裁剪溢出的部分 */
            overflow: hidden;

            /* 文字溢出部分显示省略号 */
            text-overflow: ellipsis;

        }
    </style>
</head>

<body>
    <div class="box">今天天气真不错今天天气真不错今天天气真不错今天天气真不错</div>
</body>

</html>
```

# 盒模型新增样式
## 盒模型阴影
box-shadow  
box-shadow 属性用于在元素的框架上添加阴影效果 ，该属性可设置的值包括，X偏移，Y偏移，阴影模糊半径，阴影扩散半径，和阴影颜色并以多个逗号分隔。  
默认初始值none 适用于几乎任何元素 不可继承 

取值：

inset   
如果没有指定inset，默认阴影在边框外，即阴影向外扩散。   
使用 inset 关键字会使得阴影落在盒子内部 。此时阴影会在边框之内 (即使是透明边框）、背景之上、内容之下。

offset-x offset-y   
这是头两个 length 值，用来设置阴影偏移量。x,y 是按照数学二维坐标系来计算的，只不过y垂直方向向下。 offset-x 设置水平偏移量，正值阴影则位于元素右边，负值阴影则位于元素左边。   
offset-y 设置垂直偏移量，正值阴影则位于元素下方，负值阴影则位于元素上方。可用单位请查看 length。   
如果两者都是0，那么阴影位于元素后面。这时如果设置了blur-radius 或spread-radius 则有模糊效果。需要考虑 inset

blur-radius   
这是第三个 length 值。值越大，模糊面积越大，阴影就越大越淡。 不能为负值。   
默认为0，此时阴影边缘锐利。本规范不包括如何计算模糊半径的精确算法

spread-radius   
这是第四个 length 值。取正值时，阴影扩大；取负值时，阴影收缩。  
默认为0，此时阴影与元素同样大。  
需要考虑 inset

color   
如果没有指定，则由浏览器决定——通常是color的值，不过目前Safari取透明。

语法：
```
/* x偏移量 | y偏移量 | 阴影颜色 */
box-shadow: 60px -16px teal;

/* x偏移量 | y偏移量 | 阴影模糊半径 | 阴影颜色 */
box-shadow: 10px 5px 5px black;

/* x偏移量 | y偏移量 | 阴影模糊半径 | 阴影扩散半径 | 阴影颜色 */
box-shadow: 2px 2px 2px 1px rgba(0, 0, 0, 0.2);

/* 插页(阴影向内) | x偏移量 | y偏移量 | 阴影颜色 */
box-shadow: inset 5em 1em gold;

/* 任意数量的阴影，以逗号分隔 */
box-shadow: 3px 3px red, -1em 0 0.4em olive;

/* 全局关键字 */
box-shadow: inherit;
box-shadow: initial;
box-shadow: unset;
```
## 图片水平居中
原理：  
1、首先将html和body高度设置为100% 占满整个窗口区域  
2、利用body设置水平居中  
3、像body中添加伪元素after(和img形成兄弟元素)  
4、同时为伪元素和img设置vertical-align: middle; img会参考伪元素垂直居中，因为伪元素display设置为行内块  

```
    <style>
        /* 图片水平居中 */
        html,body{
            height: 100%;
        }
        body{
            text-align: center;
        }
        body:after{
            content: "";
            display: inline-block;
            height: 100%;
            vertical-align: middle;
        }
        img{
            width: 200px;
            vertical-align: middle;
        }

    </style>
```
## 倒影
-webkit-box-reflect 只有webkit才支持,准确来说不是CSS3的内容，但需要知道   
默认值none 不可继承  

取值 倒影的方向 第一个值。可选值：above below right left

倒影和原图的距离 第二个值：长度单位

渐变 第三个值 如 linear-gradient()

## resize
resize CSS属性允许你控制一个元素的可调整大小性 注意：一定要配合overflow:auto来使用   
默认值none 不可继承  

取值  
none：元素不能被用户缩放  
both：允许用户在水平和垂直方向上调整元素的大小  
horizontal：允许用户在水平方向上调整元素的大小   
vertical：允许用户在垂直方向上调整元素的大小

## box-sizing
CSS 中的 box-sizing 属性定义了 user agent 应该如何计算一个元素的总宽度和总高度。

在 CSS 盒子模型的默认定义里，对一个元素所设置的 width 与 height 只会应用到这个元素的内容区即content-box。  
如果这个元素有任何的 border 或 padding ，绘制到屏幕上时的盒子宽度和高度会加上设置的边框和内边距值。  
这意味着当你调整一个元素的宽度和高度时需要时刻注意到这个元素的边框和内边距。当我们实现响应式布局时，这个特点尤其烦人。

box-sizing 属性可以被用来调整这些表现:  
content-box 是默认值。如果你设置一个元素的宽为100px，那么这个元素的内容区会有100px 宽，并且任何边框和内边距的宽度都会被增加到最后绘制出来的元素宽度中。  
border-box 告诉浏览器：你想要设置的边框和内边距的值是包含在width内的。也就是说，如果你将一个元素的width设为100px，那么这100px会包含它的border和padding，内容区的实际宽度是width减去(border + padding)的值。大多数情况下，这使得我们更容易地设定一个元素的宽高。  

尺寸计算公式：  
width = border + padding + 内容的宽度  
height = border + padding + 内容的高度  
注意：border-box不包含margin


# 新增UI样式
## 圆角
border-radius  
CSS 属性 border-radius 允许你设置元素的外边框圆角。当使用一个半径时确定一个圆形，当使用两个半径时确定一个椭圆。这个(椭)圆与边框的交集形成圆角效果。  
该属性是一个简写属性，是将这四个属性 border-top-left-radius、border-top-right-radius、border-bottom-right-radius，和 border-bottom-left-radius 简写为一个属性。   
默认值0 不可继承  

取值  
固定的px值定义圆形半径或椭圆的半长轴，半短轴，不能用负值。  
使用百分比定义圆形半径或椭圆的半长轴，半短轴。水平半轴相当于盒模型的宽度，垂直半轴相当于盒模型的高度，不能用负值
```
            /* 椭圆角 */
            border-radius: 50px / 25px;
            /* 简写三个值时 左上 （右上 左下） 右下 */
            border-radius: 20px 40px 100px;
            /* 简写两个值时 （左上 右下） （右上 左下） */
            border-radius: 20px 100px;
```
注意：百分比值在旧版本Chrome和Safari中不支持 在11.50版本以前的Opera中实现有问题 Gecko2.0（Firefox4）版本前实现不标准，水平半轴和垂直半轴都相对于盒子模型的宽度 在旧版本的iOS（iOS5之前）和Android中（webkit 532之前）不支持  
所以尽量使用px值  

转动的风车(没有添加动画版)
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .box{
            width: 400px;
            height: 400px;
            /* border: solid 1px red; */

            /* 居中 */
            position: absolute;
            left: 0;
            right: 0;
            top: 0;
            bottom: 0;
            margin: auto;
            /* 设置动画时间 */
            transition: 20s;
        }
        .box > div{
            margin: 10px;
            width: 180px;
            height: 180px;
            background-color: #bfa;
            /* 浮动提升层级半级 */
            float: left;
            box-sizing: border-box;
        }
        #b1,
        #b4{
            border-radius: 0px 50%;
        }
        #b2,
        #b3{
            border-radius: 50% 0px;
        }
        .box:hover{
            transform: rotate(3600deg);
        }
    </style>
</head>
<body>
    <div class="box">
        <div id="b1">1</div>
        <div id="b2">2</div>
        <div id="b3">3</div>
        <div id="b4">4</div>
    </div>
</body>
</html>
```

## BFC
BFC（block formatting context）块级格式化上下文 是一个独立的渲染区域，只有block-level box参与，它规定了内部的block-level box如何布局，并且与这个外部区域毫不相干  

BFC布局规则：  
1、内部的box在垂直方向，一个接一个放置  
2、BFC区域不会与float box重叠  
3、内部的box垂直距离由margin决定，属于同一个BFC的两个相邻box的margin会发生重叠  
4、计算BFC高度时，浮动元素也参与计算（清除haslayout）  
5、BFC就是页面上一个隔离的独立容器，容器里面的子元素不会影响外部元素

BFC什么时候出现  
根元素  
float属性值不是none  
position 属性值是absolute或者fixed  
overflow 不是visible  
display 为inline-block table-cell flex inline-flex  







