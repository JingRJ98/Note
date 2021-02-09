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
通过.length可以查看字符串的长度
`console.log(str.length);`

字符串+其他类型，结果都是字符串
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
拼接字符串方法（最常用）  
隐式的类型转换，浏览器自动完成，实际上也调用String()函数
```
c = c + '';
```
## 5.2 转换成number
字符串转数值  
1、纯数字字符串 直接转换为对应数字  
2、如果字符串中有非数字，转换成NaN  
3、空字符串，转换成数字0  
4、布尔值转数值 true转成1 false转成0    
5、null转数值，结果为0    
6、undefined转数值 结果为NaN  

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

方式二（重要）
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

方式三
隐式转换 算术运算中，自动转换成数字型
```
'12' - 0
```

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
 
 一言以蔽之，代表空，否定的值都会被转换成false
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
练习3
```
		<script type="text/javascript">
			/*
			 * 	编写程序，由键盘输入三个整数分别存入变量num1、num2、num3，
			 * 	对他们进行排序，并且从小到大输出。
			 */
			var num1 = +prompt("请输入第一个数：");
			var num2 = +prompt("请输入第二个数：");
			var num3 = +prompt("请输入第三个数：");
			var max_num,middle_num,min_num;
			if(num1>=num2){
				if(num1>=num3){
					max_num = num1;
					if(num2>=num3){
						middle_num = num2;
						min_num = num3;
					}
					else{
						middle_num = num3;
						min_num = num2;
					}
				}
				else{
					middle_num = num1;
					min_num = num2;
					max_num = num3;
				}
			}
			else{
				if(num2>=num3){
					max_num = num2;
					if(num1>=num3){
					middle_num = num1;
					min_num = num3;
					max_num = num2;
					}
					else{
					middle_num = num3;
					min_num = num1;
					max_num = num2;
					}
				}
				else{
					middle_num = num2;
					max_num = num3;
					min_num = num1;
				}
			}
			alert(min_num +"，"+middle_num+"，"+max_num);

		</script>
```
## 7.2 条件分支语句
条件分支语句也叫switch语句  
语法：`switch(条件表达式){语句}`  
执行时会将case后的值和switch后面的条件表达式的值进行全等比较，如果结果为true，则从当前case处开始执行，如果结果为false，则继续比较，使用break退出switch语句  
所有结果都是false，则转到default内容  
switch和if语句有重合部分，根据实际使用 
```
        var num = 2;
        switch(num){
            case 1:console.log("一");
            break;
            case 2:console.log("二");
            break;
            case 3:console.log("三");
            break;
	    default:
	    break;
        }
```
##### 练习1
```
		<script type="text/javascript">
			/*
			 * 对于成绩大于60分的，输出'合格'。低于60分的，输出'不合格'
			 */
			var grade = +prompt("请输入成绩：");
			switch(parseInt(grade/10)){
				case 6:
				case 7:
				case 8:
				case 9:
				case 10:
				console.log("成绩合格");
				break;
				default:
					console.log("成绩不合格！");
					break;
			}
		</script>
```
## 7.3 while循环
反复执行一段代码多次  
创建一个循环1、初始化变量 2、在循环中设置条件表达式 3、定义一个更新表达式，每次更新初始化变量  
```
    <script>
        var i = 1;
        // while循环
        while(i<1){
            document.write(i++ +"<br/>");
        }
        // do循环
        do{
            document.write(i++ +"<br/>");
        }while(i<1)
    </script>
```
do循环先执行再判断保证循环体至少执行一次，while先判断再执行  
while练习：假设投资的年利率为5%，求1000块增长到5000块需要多少年？
```
    <script>
        var money=1000,i = 0;
        while(money<5000){
            money *= 1.05;
            i++;
        }
        console.log("money=:"+money);
        console.log("年=:"+i);
    </script>
```
## 7.4 for循环
 ```
 for(初始化表达式; 条件表达式; 更新表达式) {
    语句...;
}
1、执行初始化表达式
2、执行条件表达式，结果为true执行语句，false终止循环
3、执行更新表达式
4、重复第二步

for循环的三个部分都可以省略，也可写在外部，全部省略为死循环
 ```
 #### 练习
 练习1
 ```
     <script>
        // 求1到100所有奇数的和
        var sum=0; //定义sum初始为0
        for(i=0;i<100;++i){
            i++;
            sum += i;
        }
        document.write(sum+"<br/>");       
    </script>
 ```
 练习2
 ```
     <script>
        // 打印1-100之间所有7的倍数的个数及总和
        var sum = 0;
        for(i=1;i<=40;i++){
            if((i%7) == 0){
                document.write(i+"<br/>");
                sum += i;
            }

        }
        document.write("所有7的倍数总和=："+sum);
    </script>
 ```
 练习3
 ```
     <script>
        // 水仙花数
        // 水仙花数是一个三位数。它每个位上的数字的三次幂之和等于它本身
        // 例如153=1^3+5^3+3^3
        var s=0;
        for(a=1;a<10;a++){
            for(b=0;b<10;b++){
                for(c=0;c<10;c++){
                    if((a*a*a+b*b*b+c*c*c) == a*100+b*10+c){
                        s=a*100+b*10+c;
                        document.write(s+"<br/>")
                    }
                }
            }
        }
    </script>
 ```
 练习4  
 第一版
 ```
     <script>
        // 判断质数
        var  s = +prompt("请输入一个大于1的整数：");
        var count =0;
        for(i=1;i<parseInt(s/2);i++){
            if(s % i == 0){
                count++; 
            }
            if(count > 1){
                console.log("不是质数");
            }

        }
        // 可以判断不是质数的情况，若是质数，则无输出
    </script>
 ```
 练习4  
 第二版 在第一版的基础上添加了一个标志
 ```
     <script>
        // 判断质数
        var  s = +prompt("请输入一个大于1的整数：");
        var count =0;

        var flag = true;//设置一个标志，代表默认输入数是质数
        for(i=2;i<s;i++){
            if(s % i == 0){
                count++; 
            }
            if(count == 1){
                console.log("不是质数");
                flag = false;
            }

        }
        if(flag){
            console.log("是质数");
        }


    </script>
 ```
 练习5
 ```
     <script>
        /*
            在页面中输出如下图形
            *
            **
            ***
            ****
            *****
            ******
            ……
        */
       var s=8;
       for(i=1;i<=s;i++){
            for(j=1;j<=i;j++){
                document.write("*");
            }
            document.write("<br/>");//换行
       }
    </script>
 ```
 练习6
 ```
     <script>
        /*
            在页面中输出如下图形
            *****
            ****
            ***
            **
            *
            ……
        */
       var s=8;
       for(i=1;i<=s;i++){
            for(j=s;j>=i;j--){
                document.write("*");
            }
            document.write("<br/>");//换行
       }
    </script>
 ```
 练习7
 ```
         // 打印九九乘法表
        for(i=1;i<=9;i++){
            for(j=1;j<=i;j++){
                document.write(j+"*"+i+"="+(i*j)+"&nbsp;&nbsp;&nbsp;&nbsp;");
            }
            document.write("<br/>")
        }
 ```
 练习8
 ```
     <script>
        // 输出100以内的质数
        for(i=2;i<100;i++){
            var flag = true;
            for(j=2;j<i;j++){
                if(i%j == 0){
                flag = false;
                }
            }
            if(flag){
                document.write(i+"<br/>");
            }
        }

    </script>
 ```
 ## 7.5 break和continue
 break关键字可以用来退出switch语句或循环语句 不能用于if语句，会立即终止离他最近的循环  
 可以为循环语句创建标签标记循环，使用break时，可以在break后面跟着标签，这样可以终止指定标签的循环，而不是最近的循环  
 
 continue关键字可以用来跳过当次循环，只会对最近的循环起作用，可以设置标签对指定循环进行作用
 
 # 8.对象
 js中数据类型：`string字符串` `number数值` `boolean布尔值` `null空值` `undefined未定义` 除了这五种基本数据类型，别的都是对象  
 基本数据类型都是单一的数值，之间没有关系，不能成为一个整体  
 对象属于一种复合的数据类型
 ## 8.1对象分类
 1、内建对象：由ES标准中定义的对象，在任何ES的实现中都可以使用，比如math string number boolean function object
 （详解见16.内置对象）
 
 2、宿主对象由js的运行环境提供的对象，目前来讲主要是浏览器提供的对象 比如BOM DOM
 
 3、自定义对象，由开发人员自己创建的对象
 ## 8.2创建对象
 #### 1.用字面量创建对象
 ```
           // 字面量创建对象
           var obj = {
           name: '孙悟空',
           age: 18,
           gender: '男',
           sayHi: function(){
               console.log('hi');
             } 
           };
 ```
 多个属性或者方法用`,`隔开  
 调用对象的属性  
1、对象["属性名"] = 属性值;    
2、对象.属性    
使用[]这种形式操作属性，更加灵活  
在[]中可以直接传递一个变量，这样变量值是多少就会读取那个属性  
js对象的属性值可以使任意类型，甚至也可以是另一个对象  
 #### 2.用new Object创建对象
 ```
        // new创建
        // 用等号赋值的方法添加属性和对象的方法
        var obj = new Object();
        obj.name = '孙悟空';
        obj.age = 18;
        obj.gender = '男';
        obj.sayHi = function(){
            console.log('hi~~~');
        };
 ```
 属性结束需要用分号结束  
 
#### 3.用构造函数创建对象
用构造函数创建对象是因为前两种创建对象的方式一次只能创建一个对象  
这个函数封装的是对象，把对象的相同的属性和方法抽象出来封装  
```
        // 构造函数
        function People(name,age,gender){ //构造函数函数名首字母必须大写
            this.name = name;
            this.age = age;
            this.gender = gender;
            // 构造函数不需要return
        }
        var ldh = new People('刘德华',18,'男');
        var zxy = new People('张学友',20,'男');
        console.log(typeof ldh);
        console.log(zxy.age);
```
调用函数返回的类型时object  即ldh是一个对象  
调用构造函数必须使用new  
构造函数不需要return  
我们只要new了调用函数就是创建了一个对象  

事例
```
        // 构造函数首字母必须大写
        function People(name,type,blood){
            this.name = name;
            this.type = type;
            this.blood = blood;
            this.attack = function(attack_){
                console.log(attack_);
            };
        }
        var lp = new People('廉颇','力量',500);
        var hy = new People('后羿','射手',100);
        console.log(lp.type);
        console.log(hy['name']);
        hy.attack('远程');
```
--------------------
构造函数是创建的一类 类class  
对象特指一个具体的事物，用构造函数创建对象的过程也叫对象的实例化

# 8.3 引用数据类型保存地址
JS中的变量都是保存在栈内存中，基本数据类型的值直接在栈内存中存储，值与值之间独立存在，修改一个变量不会影响另一个变量  
对象是保存在堆内存中，每创建一个新的对象，就会在堆内存中开辟一个新的空间，变量保存的是对象的内存地址，可以进行引用  

当比较两个基本数据类型的值时，就是比较值  
当比较两个引用数据类型时，需要先看是不是同一个地址  
# 8.4对象字面量
`var obj = {};`使用对象字面量创建对象  
使用对象字面量可以在创建对象时直接指定对象中的属性
```
        var obj = {
            name:"孙悟空",
            age:28,
            gneder = "男"
        }
```
属性名和属性值是一组一组的对应结构，名和值之间用`:`连接，属性和属性之间用 `,`隔开，最后一个属性后不需要`,`  

# 9.函数
函数也是一个对象，函数中可以封装一些功能（代码），在需要时可以调用  
创建一个函数对象
```
    var fun = new Function();
```
使用typrof检查fun时会返回function  
可以将要封装的代码以字符串的形式传递给构造函数，封装到函数中的代码不会立即执行，函数中的代码会在函数调用的时候执行  
调用函数：
```
        var fun = new Function("console.log('hello world!');");
        // console.log(typeof fun);
        // console.log('hello world!');
        fun(); //调用
        fun();
        fun();
```
在实际开发中很少采用构建函数来创建  

更多使用函数声明创建函数：
```
        function fun2(){
            console.log("这还是我的函数！！！")
            alert("hahhahahahah");
            document.write("┭┮﹏┭┮");
        }
        fun2();
```
## 9.1函数的参数
可以在函数的（）指定一个或多个形参，多个形参使用`,`隔开，声明形参就相当于在函数内部声明了对象，但是并不赋值  
在调用函数时可以在（）中指定实参，实参会赋值给函数中对应的实参  
调用函数时解析器不会检查实参的类型，可能会收到非法参量  
也不会检查实参的数量，多余的实参不会赋值（忽略），如果实参数量少于形参数量，未注明的形参是undefined  
实参可以是任意数据类型  
## 9.2函数返回值
可以使用return设置函数的返回值，return会作为函数的执行结果返回，可以定义一个变量接受该结果
```
        function sum(a,b,c){
            // console.log(a+b);
            var d = a+b+c;
            return d;
        }
        var result = sum(5,1,6);
        console.log("resukt="+result);
```
return 后可以跟任何值或者不写，相当于返回undefined，可以是对象、函数……  
使用return可以结束整个函数  
return只能返回后面接近的结果，若要返回多个结果，应当在return后面用`[` `]` 将结果包括进去  

```
        function fun(){
            alert("函数要执行了~~~");
            for(i=0;i<10;i++){
                if(i == 5){
                    // break;退出当前循环
                    // continue; 退出当次循环
                    return;
                    // return直接退出整个函数
                }
                console.log(i);
           
            }
            alert("完了~~~");
        }
        fun();
```
练习
```
        // 函数比较两个数中的最大值
        function fun(num1,num2){
            var max;
            if(num1 > num2){
                max = num1;
            }
            else{
                max = num2;
            }
            return max;
        }
        console.log('最大的数是：'+fun(4,Infinity));
	
	 // 改进版(返回值不同)
        function fun(num1, num2) {
            var max;
            if (num1 > num2) {
                return num1;
            }
            else {
                return num2;
            }
        }
        console.log('最大的数是：'+fun(4,Infinity));
	
	
	// 改进版plus
        function fun(num1, num2) {
            return num1 > num2 ? num1 : num2;
        }
        console.log('最大的数是：'+fun(4,Infinity));
```
练习二
```
        // 求数组中最大的元素
        // 我的思路：冒泡，取最后一个
        function getMaxArr(arr){
            for(var i = 0;i<arr.length;i++){
                for(var j = 0;j<arr.length-i;j++){
                    if(arr[j]>arr[j+1]){
                    var a = arr[j];
                    arr[j] = arr[j+1];
                    arr[j+1] = a;
                    }
          
                }
            }
            return arr[arr.length-1]
        }
        var result = getMaxArr([1,3,7,12,6,6,2,4]);
        console.log(result);
```
break结束当前循环体，如for,while   
continue 跳出本次过程，继续下一次循环  
return 结束整个函数中间的代码  
## 9.4立即执行函数
(声明函数)();立即执行函数  
```
        // 立即执行
        // 创建匿名函数
        (function(){
            alert("我是一个匿名函数~~~");
        })();
	
	
        (function(a,b){
            alert("我是一个匿名函数~~~");
	    console.log(a+b);
        })(1,2);
```

## 9.5
对象的属性值也可以是函数。  
如果一个函数作为对象的属性值，那么这个函数叫做对象的方法（method），调用函数叫做调用对象的方法  
只有名称的区别，本质一样
```
        // 创建一个对象
        var obj1 = new Object();
        // 向对象中添加属性
        obj1.name ="孙悟空";
        // 设置对象的属性值是函数
        // 函数功能为打印name属性值
        obj1.fun = function(){
            console.log(obj1.name);
        }
        // 调用这个函数
        // 例 document.write();
```
## 9.6遍历对象中的属性(也能遍历方法)
for (变量 in 对象){} 可以遍历对象  
```
        // 创建一个对象，有多个属性
        var obj = {
            name:"jrj",
            age:18,
            gender:"男",
            address:"花果山"
        };
        // 枚举对象中的属性
        for(var n in obj){
            console.log(n); //n是变量 输出属性名
            console.log(obj[n]); // 输出属性值 (注意[]里面是变量，不需要'')
        }
```

## 9.7构造函数plus（原版见8.2/3）
构造函数和普通函数的区别就是调用方式的不同，普通函数是直接调用，构造函数需要new关键字调用  

new关键字在构造函数过程中的作用：    
1、在内存中创建一个空的对象    
2、将新建的对象设置为函数中的this，在构造函数中可以用this来引用新的对象      
3、执行函数中的代码给空对象添加属性或方法     
4、将新建的对象作为返回值返回（所以构造函数里面不需要return）    

使用同一个构造函数创建的对象，称为一类对象，也将一个构造函数称为类，通过一个构造函数创建的对象，叫做实例

使用instanceof可以检查一个对象是否是一个类的实例，如果是返回true，否则返回false，所有对象都是object的实例。
```
        function Person(name,age,gender){
            this.name = name;
            this.age = age;
            this.gender = gender;
            this.sayName = function(){
                alert(this.name);
            };
        }
        var per = new Person("孙悟空",18,"男");
        var per2 = new Person("玉兔精",20,"女");
        console.log(per2);
```
## 9.8构造函数的缺陷
方法被反复创建新的，浪费资源  
可以将sayName方法在全局作用域中定义，实现共享  

改造前：
```
        // 方法是在构造函数的内部创建的
        // 每执行一次都会创建一个新的sayName 所有实例的sayName都是唯一的
        // 构造函数执行一次就会创建一个新的方法，但是方法都是一样的，这是没有必要，可以使所有的对象共享同一个方法
        
        function Person(name,age,gender){
            this.name = name;
            this.age = age;
            this.gender = gender;
            // 向对象中添加一个方法
            this.sayName = function(){
                alert("大家好~~~我是"+this.name);
            };
        }
        //创建person的实例
        var per = new Person("孙悟空",18,"男");
        var per2 = new Person("白骨精",18,"女");
        var per3 = new Person("沙和尚",48,"男");
        per3.sayName();
```
改造后：
```
        // 创建一个sayName共用方法
        function fun(){
            alert("大家好~~~我是"+this.name);
        };
        function Person(name,age,gender){
            this.name = name;
            this.age = age;
            this.gender = gender;
            // 向对象中添加一个方法
            this.sayName = fun;
            };
        
        //创建person的实例
        var per = new Person("孙悟空",18,"男");
        var per2 = new Person("白骨精",18,"女");
        var per3 = new Person("沙和尚",48,"男");
        per3.sayName();
```
缺点：将函数定义在全局定义域中，污染了全局作用域的命名空间，而且定义在全局作用域中也很不安全
# 10.作用域
作用域指一个变量作用的范围，js中一共两种作用域

1、全局作用域  
直接编写在script标签中的js代码，都在全局作用域  
全局作用域在页面打开时创建，关闭时销毁  
在全局作用域中，有一个全局对象window，可以直接使用  
在全局作用域中创建的变量都会作为window的属性保存，创建的函数都会作为window的方法保存  
全局作用域中的所有变量都是全局变量，在页面的任意部分都可以访问到

2、函数作用域    
调用函数时创建函数作用域，函数执行完毕，函数作用域销毁，每调用一次函数就会创建一次新的函数作用域  
函数作用域中可以访问到全局变量  
全局作用域中无法访问函数作用域的变量  
当在作用域中操作变量，就近原则，函数中的先找函数作用域中的变量，然后再找上一级。全局中先找全局的  
如果在函数中要使用全局变量，可以指定window.变量   
在函数中不使用var声明的变量都会成为全局变量  
定义形参相当于在函数作用域中声明变量

## 作用域链
内部函数访问外部函数的变量，采取链式查找的方法，决定取哪个值  
（就近原则）

# 11.预解析
浏览器运行js代码分为两步 1、预解析2、代码执行  
var关键字会在所有代码执行之前声明，但是不会赋值  
如果声明变量时不使用var，则声明不会提前。

使用函数的声明形式创建的函数（function 函数名(){}），他会在所有的代码执行之前就被创建，所以我们可以在函数声明前调用  
使用函数表达式创建的函数表达式（var 函数名 = function（）{}）不会被声明提前，所以不能再声明之前调用

预解析实例
一
```
        var num = 10;
        fun();
        function fun() {
            console.log(num);
            num = 20;
        }
        // 结果为10
        // 解释
        /*
            var num;
    
            function fun(){
                console.log(num);
                num = 20;
            }
            num = 10;
            fun();
        */
```
二
```
        var num = 10;
        fun();
        function fun() {
            console.log(num);
            var num = 20;
        }
        // 结果为wndefined
        // 解释
        /*
            var num;
    
            function fun(){
                var num;
                console.log(num);
                num = 20;
            }
            num = 10;
            fun();
            函数局部作用域，var声明提升到当前作用域的最前面，并没有赋值，就近原则，结果为undefined
        */
```
三
```
        var num = 10;
        function fun(){
            console.log(num);
            var num = 20;
            console.log(num);
        }
        fun();
        // undefined和20
        // 解释：var声明提到局部作用域的前面，第一个未赋值，第二个赋值了
```
四
```
        // 经典
        fun();
        console.log(c);
        console.log(b);
        console.log(a);
        function fun(){
            var a=b=c=9;
            console.log(a);
            console.log(b);
            console.log(c);
        }
        // 结果9 9 9 9 9 报错
        // 解释：var a=b=c=9;
        // 相当于
        // var a = 9;
        // b = 9;
        // c = 9;
        // bc未使用var声明，看做全局变量，a作为局部变量
```

# 12.this
解析器在调用函数时每次都会向函数内部传递一个隐含参数，这个隐函参数就是this，this指向的是一个对象，这个对象称为函数执行的上下文对象，根据函数调用方式的不同，this会指向不听的对象  
1、以函数的形式调用，this永远都是window（实际上函数调用就相当于window.fun(); 本质上还是方法的对象）

2、方法的形式调用，this就是调用方法的对象
```
        function fun(){
            console.log(this);
        }
        fun();
        // 输出window
	
        // 创建一个对象
        var obj = {
            name:"景仁杰",
            sayName:fun
        };
        console.log(obj.sayName == fun);
        // //输出true

        obj.sayName();//调用的是局部
        fun();//调用的window
```

3.
```
        var name = "全局";

        // 创建一个函数
        function fun(){
            console.log(this.name);//如果不加this.使用obj.sayName()输出都是全局
        }

        // 创建两个对象
        var obj ={
            name:"孙悟空",
            sayName:fun
        };
        var obj2 ={
            name:"猪八戒",
            sayName:fun
        };
        fun();
        // 希望调用obj.sayName时输出对象的名字
        obj.sayName();
        obj2.sayName();
```
4.以构造函数调用，this就是新创建的对象

# 13.使用工厂创建对象
通过该方法可以大量创建对象
```
        function creatPerson(name,age,gender){
            // 创建一个对象
            var obj = new Object();
            // 向对象中添加属性
            obj.name = name;
            obj.age = age;
            obj.gender = gender;
            obj.sayName = function(){
                alert(this.name);
            };
            return obj;
        }
        var obj2 = creatPerson("孙悟空",18,"男");
        var obj3 = creatPerson("猪八戒",28,"男");
        var obj4 = creatPerson("沙和尚",38,"男");
        obj4.sayName();
```
# 14.原型
prototype 创建的每一个函数都会向函数中添加一个属性prototype（唯一的）这个属性对应的对象，这个对象就是原型对象

# 15. 数组
数组就是一组数据的集合，将一组数据存在单个变量名下，数组中可以存储任意类型的元素  

## 数组创建
方式一
```
        //  new关键字 创建一个空数组
        var arr = new Array();
```
方式二(常用)
```
        // 数组字面量创建数组
        var arr = [];
```
数组里面的数据用`,`隔开  
声明数组并赋值称为数组初始化  
## 获取数组元素
数组名[ 索引号 ] 索引号从0开始
```
        console.log(arr[3]);
```
没有索引号的元素输出undefined  
可以通过给指定索引号的数组元素赋值，会替换掉原来的元素  
不要直接给整个数组赋值！！  
## 遍历数组
数组索引号从0开始，i从0开始，i<元素个数
```
        // 遍历
        var arr1 = ['N','M','S','L'];
        for(var i = 0;i<4;i++){
            console.log(arr1[i]);
        }
```
数组的长度  
```
	console.log(arr.length);
```
数组的长度是元素个数，不要和索引号混淆  
使用长度可以arr.length动态监控数组的长度  

## 练习
练习一
```
        // 求数组元素的和，并求平均
        var arr = [2,6,1,7,4,10];
        var sum = 0;
            var average;
        for(var i = 0;i<arr.length;i++){
            sum+=arr[i];
        }
        average = sum/arr.length;
        console.log('和为：'+sum);
        console.log('平均数为：'+average);
```
练习二
```

        // 求数组最大值
        var arr = [1,6,1,77,52,25,7,99,90];
        var max = arr[0];
        for(var i = 1;i<arr.length;i++){
            if(arr[i] > max){
                max = arr[i];
            }
        }
        console.log('数组最大值是：' + max);
```
练习三
```
        // 分割数组变成字符串
        var arr = ['N','M','S','L'];
        var str = '';
        for(var i = 0;i<arr.length;i++){
            str += '|'+arr[i];
        }
        console.log(str+'|');
```
练习四
```
	// 在数组中依次放入0-100
        var arr = [];
        for(var i = 0;i<100;i++){
            arr[i] = i+1;
        }
        console.log(arr);
```
练习五
```
        // 将数组中大于10的元素筛选出来存入新数组
        var arr = [1,23,44,5,66,7,9,10];
        var arr1 = [];
        var j = 0;
        for(var i = 0;i<arr.length;i++){
            if(arr[i] > 10){
                arr1[j] = arr[i];
                j++;
            }
        }
        console.log(arr1);
```
练习五补充：可以直接使用arr1[arr1.length]来自动设置新数组的长度，不需要j  

练习六
```
       // 将数组中的0删掉，形成新数组
        var arr = [0,30,0,6,6,6,6,0,0,1,0];
        var arr1 = [];
        for(var i = 0;i<arr.length;i++){
            if(arr[i] !== 0){
                arr1[arr1.length] = arr[i];
            }
        }
        console.log(arr1);
```
练习七
```
        // 将数组的内容左右翻转
        var arr = ['N','M','hhh','S','L','c'];
        var arr1 = [];
        for(var i = arr.length-1;i>=0;i--){
            arr1[arr1.length] = arr[i];
        }
        console.log(arr1);
```

## 冒泡排序
冒泡排序是一种算法，可以把一系列数据按照一定的顺序进行排列（从小到大或者从大到小）  
原理：
```
        // 冒泡排序
        var arr = [4,3,5,2,1];
        // 外层循环确定总趟数
        for(var i = 0;i<arr.length;i++){
            // 内循环确定一趟里面的交换次数
            for(var j = 0;j<arr.length-i;j++){
                // 内部交换两个元素
                if(arr[j]>arr[j+1]){
                    var a = arr[j];
                    arr[j] = arr[j+1];
                    arr[j+1] = a;

                }
            }
        }
        console.log(arr);
```
## arguments
当形参不确定的时候，可以使用arguments指代，arguments会传递所有的实参  
arguments实际上是伪数组  
1、具有数组的length属性  
2、按照索引的方式进行存储  
3、没有真正数组的方法，如push，pop  

可以用数组的方式对arguments进行遍历，只有函数具有arguments，且每个函数都内置了arguments

----------------------------------------------------------------

# 16.内置对象
js中对象分为三种：自定义对象，内置对象，浏览器对象  
内置对象是js语言自带的对象，供开发者使用，并提供一些最基本或必要的功能/属性/方法  

### Math对象



