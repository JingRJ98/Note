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


