# 1. JS语法
1、严格区分大小写  
2、每一条语句以分好结尾，如果不写分号浏览器会自动添加分号，但是会消耗性能，有时会写错  
3、JS中会忽略多个空格和换行，所以可以利用空格和换行对代码进行格式化
# 2.字面量和变量
字面量=常量：不可变的量 1 2 3 4 ……字面量可以直接使用，但是不建议使用  
变量可以用来保存字面量 变量更加方便使用，开发中都是通过变量保存数据  
```
   <script>
        // 在js中使用var声明变量
        var a;
        // 为变量赋值
        a=123;
        a=456;
        // 声明和赋值同时
        var b = 7777;
    </script>
```
# 3.标识符
js中可以自主命名的都是标识符，例如变量名，函数名，属性名  
命名规则：  
1、标识符中可以含有字母/数字/下划线/$  
2、标识符不能以数字开头  
3、标识符不能是ES中的关键字或保留字  
4、标识符一般采用驼峰命名法，首字母小写，每个单词的字母大写，其余字母小写 xxxYyyZzz  
js底层代码保存时实际上采用unicode编码，理论上所有的UTF-8含有的内容都可以作为标识符
# 4.数据类型
数据类型指的就是字面量的类型，在js中有六种数据类型  
object属于引用数据类型 其余五个是基本数据类型
## 4.1. String

String字符串
    在JS中字符串需要使用引号
    使用双引号或单引号都可以，但不能混着用
    引号不能嵌套，双引号里不能放双引号，单引号里不能放单引号

在字符串中我们可以使用 \ 作为转义字符，当表示一些特殊符号时可以使用\进行转义  
同一个标识符只需要声明一次，下面修改会自动覆盖

```
    \" 表示 "
    \' 表示 '
    \n 表示换行
    \t 制表符
    \\ 表示\
```

## 4.2. Number

在JS中所有的数值都是Number类型，包括整数和浮点数

可以使用typeof检查变量类型
```
   <script>
        
        var a = "123";
        var b = 123;
        console.log(a);
        console.log(b);
        //typeof检查数据类型
        console.log(typeof a);
        console.log(typeof b);
    </script>
```

JS中可以表示的数字的最大值
Number.MAX_VALUE  
1.7976931348623157e+308

JS中可以表示的大于0的最小值
Number.MIN_VALUE  
5e-324

如果使用Number表示的数字超过了最大值，则会返回
    Infinity 正无穷
    -Infinity 负无穷
    使用typeof检查Infinity也会返回number

NaN是一个特殊的数字，表示Not A Number
    使用typeof检查一个NaN也会返回number

注意：如果使用JS进行浮点运算，可能得到一个不精确的结果 如：0.1+0.2
所以千万不要使用JS进行对精确度要求比较高的运算

## 4.3. Boolean

Boolean布尔值
布尔值只有两个，主要用来做逻辑判断
true：表示真
false：表示假
使用typeof检查一个布尔值时，会返回boolean

## 4.4. Null

Null（空值）类型的值只有一个，就是null
null这个值专门用来表示一个为空的对象

注意:使用typeof检查一个null值时，会返回object

## 4.5. Undefined

Undefined（未定义）类型的值只有一个，就undefind
当声明一个变量，但是并不给变量赋值时，它的值就是undefined  
使用typeof检测undefined，返回undefined

## 4.6. object
# 5.强制类型转换
主要指将其他数据类型转换成string number boolean  
## 5.1 转换成string
方式一  
调用被转换数据类型的tostring()方法,不改变原变量
```
    <script>
        var a = 123;
        var b = a.toString();
        console.log(typeof a);
        console.log(typeof b);
        console.log(b);
    </script>
```
注意：null和undefined这两个值没有toString()方法，如果调用会报错
方式二  
调用String()函数，并将被转换的数据作为参数传递给函数
```
    <script>
        var a = null;
        a = String(a);
        console.log(a);
        console.log(typeof a);
    </script>
```
对于Number和Boolean实际上就是调用toString()方法 但是对于null和undefined，不会调用toString()方法 它会将null直接转换为"null" 将number直接转换为"number"

方式三  
隐式的类型转换，浏览器自动完成，实际上也调用String()函数
```
c = c + '';
```
## 5.2 转换成number
方式一  
使用Number()函数
```
    <script>
        var a = "1234";
        a = Number(a);
        console.log(a);
        console.log(typeof a);
    </script>
```
字符串转数值  
1、纯数字字符串 直接转换为对应数字  
2、如果字符串中有非数字，转换成NaN  
3、空字符串，转换成数字0
布尔值转数值 true转成1 false转成0    

null转数值，结果为0  

undefined转数值 结果为NaN  

方式二
parseInt函数转换成整数  
parseFloat函数转换成浮点数
```
    <script>
        var a = "123.111px123";
        a = parseFloat(a);
        console.log(a);
        console.log(typeof a);
    </script>
```
注意 首个字符必须是数字，否则输出NaN  
对非string使用parseInt或者parseFloat 会先转换成string再操作

##### 其他进制
```
    <script>
        // 十六进制 0x
        // 八进制 0
        // 二进制 0b(但时不时所有的浏览器都支持)
        var a = 0xC;
        console.log(a);
        var b = 0111;
        console.log(b);
        var c = 0b1111;
        console.log(c);
    </script>
```
 使用parse函数可以指定第二个参数表示进制parseInt(b,10);
 ## 5.3 转换成Boolean
 方式一  
 
 使用Boolean()函数  
 除了null和NaN，其余都输出true    
 字符串除了空，都输出true  
 null和undefined都转换成false  
 对象也会转成true
 ```
    <script>
        var a = 123;
        a = Boolean(a);
        console.log(a);
        console.log(typeof a);
    </script>
 ```
 方式二
 
 隐式类型转换  
 为任意数据类型做两次非运算，即可将其转换成布尔值（Boolean）
 # 6.运算符
 运算符也叫操作符，通过运算符可以对一个或多个值进行运算，并获取运算结果    
 比如typeof就是运算符，可以获得一个值的类型  
 返回值是字符串  
 ## 6.1 算数运算符 + - * / %  
 当对非数字类型的值运算时，先转换成数字再计算   
 任何数和NaN运算都是NaN  
 两个字符串运算会进行拼串操作  
 任何值和字符串运算，会先转换成字符串再拼接
 ```
     <script>
        var a = 123;
        var result = typeof a;
        console.log(result);
        console.log(typeof result);
        // typeof的返回值是个字符串
        var b = 123;
        b = undefined + "456";
        console.log(b);
        console.log(typeof b);//undefined456  string
    </script>
 ```
任何值做- * /时，都会转换成number计算
## 6.2 一元运算符
一元运算符，只需要一个操作数  
`+` `-` 正号负号，对于非number值，可以先转换成number 再计算
一元运算符优先于算数运算符  
### 自增自减
自增可以使变量在自身的基础上加1，原变量的值立即增加1  
自增分为两种后++/前++ 无论是a++还是++a，都会立即使原变量的值立即自增1  
不同的是，a++和++a的值不同  
a++的值等于原变量的值  
先赋值后运算

++a的值等于自增后的值  
先运算后赋值

自减同理

例1：
```
    <script>
        var d = 20;
        var a = d++ + ++d +d;
        console.log("a = "+a);
        //a = 20 + 22 +22 = 64
        var b = 20;
        b = b++;
        console.log("b = "+b);
        //b=10
    </script>
```
例2：
```
        var n1 = 10,n2 = 20;
        var n = n1++;
        console.log("n = "+n);//10
        console.log("n1 = "+n1);//11
        n = ++n1;
        console.log("n = "+n);//12
        console.log("n1 = "+n1);//12
        n = n2--;
        console.log("n = "+n);//20
        console.log("n2 = "+n2);//19
        n=--n2;
        console.log("n = "+n);//18
        console.log("n2 = "+n2);//18
```
## 6.3逻辑运算符
三种逻辑运算符 对于非布尔值进行与或运算时，先转换成布尔值再运算     
! 非  
!可以用来对一个值进行非运算 所谓非运算就是值对一个布尔值进行取反操作，true变false，false变true 如果对一个值进行两次取反，它不会变化 如果对非布尔值进行元素，则会将其转换为布尔值，然后再取反 所以我们可以利用该特点，来将一个其他的数据类型转换为布尔值 可以为一个任意数据类型取两次反，来将其转换为布尔值，原理和Boolean()函数一样

&& 与  
两个值都为true时才输出true，若果第一个值是false，则不会看第二个值，两个数中有false，返回靠前的false，第一个值时true，返回第二个值  

|| 或  
两个值都为false时才输出false，若果第一个值是true，则不会看第二个值 ，两个值都是true，返回靠前的true，第一个值是false，返回第二个值

## 6.4 赋值运算符
将符号右侧的值赋值给左侧的变量  
```
a += 5;
a = a + 5;
两者等价
```
## 6.5关系运算符
通过关系运算符可以比较两个值之间的大小关系，如果关系成立它会返回true，如果关系不成立则返回false  
非数值比较的情况，会将其转换成数字再比较  
任何值和NaN做任何比较都是false  
两个字符串比较，不会将其转换成数字比较，而会分别比较字符串中Unicode编码，只比第一位（和按照文件名排序有关）两位一样则比较下一位  
如果比较的是字符串型的数字可能会出现不可预期的结果注意一定要转型  


相等运算符 ==
用来比较两个值是否相等，相等返回true，不等返回false  
如果值的类型不同，则会自动进行类型转换，将其转换为相同的类型然后再比较  
NaN不和任何值相等  
判断b是否是NaN  
isNaN()判断是否是NaN，若是，返回true

!= 不相等运算符  

=== 判断两个值是否全等，不会对数值进行类型转换，如果类型不一样，直接返回false  
!== 判断两个数值是否不全等，不会自动类型转换，两个值类型不同，直接返回true  


## 6.6Unicode编码
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <script>
        // 使用转义字符和编码显示Unicode
        // \u+四位十六进制编码
        console.log("\u2620");
    </script>
</head>
<body>
    <!-- 
        在网页中使用Unicode编码
        &#+【十进制】编码
     -->
    <h1 style="font-size: 100px;">&#9760;</h1>
</body>
</html>
```
## 6.7 条件运算符
条件表达式?语句1:语句2;  
条件运算符在执行时，首先对条件表达式进行求职，如果该值为true 执行语句1，并返回执行结果，如果该值为false，执行语句2，并返回结果  
例：
```
    <script>
        // 获取a b c中最大值
        var a=20,b=60,c=40;
        var d = a>b?a:b;
        var max = c>d?c:d;
        console.log("max = "+max);
    </script>
```
如果条件表达式的结果是非布尔值，会将其转换成布尔值，再运算  
## 6.8 运算符的优先级
`,`运算符，可以同时指定多个变量并赋值  
和数学中一样，运算符存在优先级  
# 7.语句
语句是按照自上向下的顺序一条一条执行的，可以用`{}`为语句进行分组  
同一个`{}`中的语句称为一组语句，要么都执行，要么都不执行，他们称为代码块  
代码块的结尾不需要分号，js中的代码块只具有分组的作用，没有其他功能，代码块中的内容外部完全可见  
## 7.1流程控制语句
流程控制语句使程序可以根据一定的条件选择执行  
1、条件判断语句  
2、条件分支语句  
3、循环语句  

1、条件判断可以在执行代码之前进行判断，条件成立才会执行语句，条件不成立就不执行  
if语句后的`{}`不是必须的，但是尽量写
语法1
```
        var a = 3;
        if (a > 5){
            alert("hhhhh");
            alert("wwwwww");
        }
``` 
语法2
```
        var a = 3;
        if (a > 5){
            alert("hhhhh");
            alert("wwwwww");
        }
        else{
            alert("cuocuocu");
        }
```
语法3
```
        var a = 10;
        if (a < 5){
            alert("小于5");
        }
        else if(a < 8){
            alert("小于8");
        }
        else if(a < 15){
            alert("小于15");
        }
        else{
            alert("不对不对不对")
        }
```
只会有一个代码块执行，一旦有一个代码块执行了，整个语句结束了  

练习1
```
		<script type="text/javascript">
			/*
			 * 	从键盘输入小明的期末成绩:
			 *	当成绩为100时，'奖励一辆BMW'
			 *	当成绩为[80-99]时，'奖励一台iphone15s'
			 *	当成绩为[60-80]时，'奖励一本参考书'
			 *	其他时，什么奖励也没有
			 */
			var grade = prompt("请输入小明的期末成绩：");
			if(grade>100 || grade<0 || isNaN(grade)){
				alert("错误！");
			}
			else if(grade==100){
				alert("给你一辆BMA");
			}
			else if(grade<100 && grade>=80){
				alert("给你一个iPhone13");
			}
			else if(grade<80 && grade>=60){
				alert("给你一本书");
			}
			else{
				alert("给你一个大嘴巴子！！！");
			}

		</script>
```
练习2
```
	<script type="text/javascript">
		/*
		 * 	大家都知道，男大当婚，女大当嫁。那么女方家长要嫁女儿，当然要提出一定的条件： 
		 *	高：180cm以上; 富:1000万以上; 帅:500以上;
		 *	如果这三个条件同时满足，则:'我一定要嫁给他'
		 *	如果三个条件有为真的情况，则:'嫁吧，比上不足，比下有余。' 
		 *	如果三个条件都不满足，则:'不嫁！' 
		 */
		var a1 = prompt("请输入你的身高（cm）：");
		var a2 = prompt("请输入你的财富（万）：");
		var a3 = prompt("请输入你的颜值：");
		if (isNaN(a1) || isNaN(a2) || isNaN(a3)) {
			alert("请输入数字");
		}
		else {
			if(a1 >= 180 && a2 >= 1000 && a3 >= 500){
			alert("非你不可！！！");
			}
			else if(a1 < 180 && a2 < 1000 && a3 < 500) {
				alert("不嫁");
			}
			else {
				alert("凑活吧");
			}
		}
	</script>
```
## 7.2 switch 条件分支语句
