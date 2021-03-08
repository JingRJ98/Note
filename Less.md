# 注释
以` // `开头的注释是不会被编译到CSS文件中去的

以` /* */ `包裹的注释会被编译到CSS文件中去

# 变量

用@来申明一个变量：  
@变量名: 变量值;  
@red: red;  
@m: margin;  
@selector: #wrap;  
1.作为普通属性值来使用：直接使用@red  
2.作为选择器和属性名： @{selector} { @{m}: 10px;}  
3.作为URL：@{url}  
4.变量的延迟加载 一个{}为一个作用域，{}全部加载完才确定变量的值，也就是说后设的变量值会覆盖先设的变量值  

注意变量在Less中属于块级作用域

# Less中的嵌套规则
1.基本的嵌套规则（父子级关系）  
2.&的使用（代表外层父元素）   
 
# Less的混合(mixin)  
混合就是将同一系列的属性从一个规则集引入到另一个规则集的方式  
## 1.普通混合  
```
.juzhong {
    //不加()的话.juzhong{}会被编译到CSS中
    position:absolute;
    top:0;
    bottom:0;
    left:0;
    right:0;
    margin:auto;
    width:100px;
    height:100px;
    border:1px solid;
}

#div1 {
    .juzhong;
}

#div2 {
    .juzhong;
}


```

## 2.不带输出的混合

```
.juzhong() {
    //加()不会被编译到CSS中去
    position:absolute;
    top:0;
    bottom:0;
    left:0;
    right:0;
    margin:auto;
    width:100px;
    height:100px;
    border:1px solid;
}

#div1 {
    .juzhong();
}

#div2 {
    .juzhong();
}


```

## 3.带参数的混合

```
.juzhong(@w, @h) {
    position:absolute;
    top:0;
    bottom:0;
    left:0;
    right:0;
    margin:auto;
    width:@w;
    height:@h;
    border:1px solid;
}

#div1 {
    //实参和形参不对应会报错
    .juzhong(100px, 100px);
}

#div2 {
    .juzhong(200px, 200px);
}


```

## 4.带参数且有默认值的混合

```
.juzhong(@w:10px, @h:10px) {
    position:absolute;
    top:0;
    bottom:0;
    left:0;
    right:0;
    margin:auto;
    width:@w;
    height:@h;
    border:1px solid;
}

#div1 {
    //实数可传可不传，但实参顺序要和形参一样
    .juzhong(100px);
}

#div2 {
    .juzhong(200px, 200px);
}


```

## 5.命名参数

```
.juzhong(@w:10px, @h:10px) {
    position:absolute;
    top:0;
    bottom:0;
    left:0;
    right:0;
    margin:auto;
    width:@w;
    height:@h;
    border:1px solid;
}

#div1 {
    //实数可传可不传，可指定传参数，不考虑参数顺序
    .juzhong(@h:100px);
}

#div2 {
    .juzhong(@h:200px, @w:100px);
}


```

## 6.匹配模式
```
@import "./sanjiaoxing.less"

#wrap {
    .sanjiaoxing(匹配符,参数，参数)
}
```

```
.sanjiaoxing(@_) {
    相同样式
}

.sanjiaoxing(匹配符, @w, @h) {
    不同样式
}
.sanjiaoxing(匹配符, @w, @h) {
    不同样式
}
.sanjiaoxing(匹配符, @w, @h) {
    不同样式
}
```
## 7.arguments变量

```
.border(@a, @b, @c) {
    border: @arguments;
}

#wrap {
    .border(1px, red, solid)
}

```
# Less的运算
Less里面计算，计算双方只需要一方带单位就行
# Less的继承
继承性能上比混合高    
灵活性没有混合好（不可设参）
```
.p1{
    height: 200px;
    width: 200px;
}
.p2:extend(.p1){
    background-color: #bfa;
}


// 等同于
.p1,
.p2 {
  height: 200px;
  width: 200px;
}
.p2 {
  background-color: #bfa;
}
```
```
.p3{
    .p1();// 直接引用，相当于把p1的样式直接复制过来
    background-color: #bfa;
}

// 等同于
.p3 {
  height: 200px;
  width: 200px;
  background-color: #bfa;
}
```
第二种不建议使用，复制两遍效率不如第一种高 
# Less避免编译
~"不会被编译的内容"

`padding: ~"calc(100px + 100)";`
# 导入其他less
` @import "01.less"; `在本less文件中引入其他less文件
