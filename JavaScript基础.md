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

## 16.1Math对象
math数学对象 不是一个构造函数，不需要new调用，可以直接使用里面的属性和方法  
```
        console.log(Math.PI);  //3.141592653589793
        console.log(Math.max(1,99,3));
        console.log(Math.max(1,-1));
        console.log(Math.max(1,'hhh'));// NaN
        console.log(Math.max());// -Infinity
```
例
```
 var myMath = {
            PI:3.121592653589,
            max:function(){
                var max = arguments[0];
                for(var i = 1;i<arguments.length;i++){
                    if(arguments[i]>max){
                        max = arguments[i];
                    }
                }
                return max;
            }
        }

        console.log(myMath.PI);
        console.log(myMath.max(1,2,3,4,1));

```
### 16.1.1 绝对值方法
Math.abs();
输入为字符型，会自动隐式转换，若不能转换成数字则输出NaN  

### 16.1.2 三个取整方法
#### 1、Math.floor()
向下取整
```
        console.log(Math.floor(0.9));//0
        console.log(Math.floor(1.1));//1
```
#### 2. Math.ceil()
向上取整
#### 3.Math.round()
四舍五入取整  
.5在负数时，也是向大取（取绝对值更小的数字）
```
        console.log(Math.round(-1.8));//-2
        console.log(Math.round(-1.5));//-1
        console.log(Math.round(-1.1));//-1
```

### 16.1.3随机数方法
可以用来生成一个0-1 `[0,1)` 之间的随机数 `console.log(Math.random());`

生成一个0-x之间的随机数`console.log(Math.random()*x)`  

生成一个x~y之间的随机数 `console.log(Math.random()*(y-x)+x)`  

生成两个数之间的整数（包含这两个数）
```
        // 生成两个数之间的整数（包含这两个数）
        function getRandom(min,max){
            return Math.floor(Math.random()*(max-min+1))+min;

        }
        console.log(getRandom(1,3));
```
随机点名
```
        // 生成两个数之间的整数（包含这两个数）
        function getRandom(min,max){
            return Math.floor(Math.random()*(max-min+1))+min;

        }
        //随机点名
        var arr = ['a','b','c']; //输入人名
        console.log(arr[getRandom(0,arr.length-1)]);//arr.length是数组中的元素个数，但是数组索引号是从0~arr.length-1
```
猜数字
```
        // 猜数字
            // 生成两个数之间的整数（包含这两个数）
            function getRandom(min, max) {
                return Math.floor(Math.random() * (max - min + 1)) + min;
            }
        var num = getRandom(1, 10);// 系统生成一个数
        while (true) {
            var getnumber = prompt('请输入1~10之间的数：');
            if (num < getnumber) {
                alert('大了');
            }
            else if (num > getnumber) {
                alert('小了');

            }
            else {
                alert('你猜对了！！！');
                break;// 退出整个循环
            }
        }
```

## 16.2 Date对象
日期对象是一个构造函数，必须使用new关键字来调用创建日期对象
```
        var date = new Date();
        console.log(date);
        // 不带任何参数输出当前时间

        // 字符串型 输出指定的时间
        var date1 = new Date('2010-10-1 8:8:8');
        console.log(date1);
```
### 16.2.1 Date的方法
##### getFullYear() 年
获取本地时间当年的年份
##### getMonth() 月
获取本地时间当前的月份（0-11）第0个月表示1月，所以输出结果比实际月份少1
##### getDate() 日
获取当前时间的日期
##### getDay() 星期几
获取当前日期对象是周几 会返回一个0-6的值  
0 表示周日 1-6表示周一到周六   
##### getHours() 时
获取当前时间的小时数
##### getMinutes() 分
获取当前时间的分钟数
##### getSeconds() 秒
获取当前时间的秒数
##### 获得毫秒数
获得距离1970年1月1号0时0分过去了多少毫秒  
1秒 = 1000毫秒  
```
        var date = new Date();
	console.log(date.getTime());
	// 或者
	console.log(date.valueOf());
	
	// 简单写法（最常用的用法）
        var date1 = +new Date;
        console.log(date1);
	
	//H5新增的更更简单的写法
	console.log(Date.now());
```
### 16.2.2 倒计时
```
 // 倒计时
        function countDown(time){
            var nowTime = +new Date();//当前时间
            var inputTime = +new Date(time);// 用户输入的时间
            var times = (inputTime - nowTime)/1000;// 距离目标时间还有多少秒
            var s = parseInt(times % 60);//秒
            s = s < 10 ? '0'+s : s;
            var m = parseInt(times/60%60);//分
            m = m < 10 ? '0'+m : m;
            var h = parseInt(times/3600%24);//时
            h = h < 10 ? '0'+h : h;
            var d = parseInt(times/3600/24);//天
            d = d < 10 ? '0'+d : d;
            return d + '天' + h + '时' + m + '分' + s + '秒';

        }
        console.log(countDown('2021-2-18 8:00:00'));// 时间需要写成字符串格式

```
## 16.3 数组对象
判断是否是数组
```
        var arr = [];
        var obj = {};
        console.log(arr instanceof Array);
        // 返回true
        console.log(obj instanceof Array);
        // 返回false

        console.log(Array.isArray(arr));
```
### 添加/删除数组元素
push(参数1……)  
末尾添加一个或多个元素，修改原数组，返回新数组的长度  

pop()  
删除数组最后一个元素，把数组长度减1，无参数，修改原数组  
返回它删除的元素的值  

unshift()   
向数组的开头添加一个或多个元素，修改原数组  
返回新数组的长度  

shift()  
删除数组的第一个元素，数组长度减一，无参数，修改原数组  
返回第一个元素的值

### 筛选数组
```
        // 将数组中大于某个值的元素删除，并将剩下的元素存入新数组里面
        var arr = [1500,1200,4000,3000,1000,1800];
        var newArr = []; // 新建数组存放保留的数据
        for(var i = 0;i < arr.length;i++){
            if(arr[i] < 2000){
                // newArr[newArr.length] = arr[i];
                newArr.push(arr[i]);
                // 把符合要求的arr元素向新空数组的末尾添加
            }
        }
        console.log(newArr);
```
### 数组排序
reverse()  
颠倒数组中的元素的顺序，无参数  
该方法会改变原数组，返回新数组  
```
    var arr = [1,2,3,4,5,6];
    console.log(arr.reverse());
```

sort()  
对数组的顺序进行排序  
改变原数组，返回新数组  
```
        var arr1 = [1,3,2,5,2];
        arr1.sort();
        console.log(arr1);
```
注意：sort()只能处理个位数的排序，因为只对首位数字比较，两位数的排序
```
        var arr2 = [1,22,13,4,77,5];
        arr2.sort(function(a,b){
            return a - b;
        });
        console.log(arr2);
        // 输出 [1, 4, 5, 13, 22, 77]
```
` a-b `从小到大  
` b-a `从大到小  

### 数组索引
indexOf()  
数组中查找给定元素的第一个索引位置  
如果存在返回第一个出现的指定元素的索引号，如果没有就返回-1  

lastIndexOf()  
在数组中查找指定元素的最后一个索引位置，没有返回-1  
```
        var arr = [1,2,3,3,3,4,4,45,5,5,56,6,6,7,6,6,6,6,6,6,6,6,6,6,33,4,2,6,];
        console.log(arr.length);//28
        console.log(arr.indexOf(6));// 返回第一个6的索引号11
        console.log(arr.indexOf(100)); // -1
        console.log(arr.lastIndexOf(6)); // 27
```
### 数组去重（重点案例）
```
        var arr = [1,2,'-1','-1',3,3,3,4,4,45,5,5,56,6,6,7,6,6,6,6,6,6,6,6,6,6,33,4,2,6,];
        // console.log(arr.length);//28
        var arr1 = [];
        for(var i = 0;i<arr.length;i++){
            if(arr1.indexOf(arr[i]) == -1){
                // 在新数组中查找旧数组元素的第一个索引
                // 等于-1说明新数组中没有旧数组的这个元素
                // 则将旧数组中的这个元素放到新数组中
                // 实现去重
                arr1[arr1.length] = arr[i];
            }
        }
        console.log(arr1);
        //  [1, 2, 3, 4, 45, 5, 56, 6, 7, 33]
```
### 数组转换成字符串
toString()  
将数组转换成字符串，逗号隔开，返回一个字符串  

join('自定义的分隔符')  
用于将数组中所有元素转换为一个字符串，返回一个字符串  
```
        var arr = [1,2,'-1','-1',3,3,3,4,4,45,5,5,56,6,6,7,6,6,6,6,6,6,6,6,6,6,33,4,2,6,];
        console.log(arr.toString());
        // 1,2,-1,-1,3,3,3,4,4,45,5,5,56,6,6,7,6,6,6,6,6,6,6,6,6,6,33,4,2,6
        console.log(arr.join('|'));
        // 1|2|-1|-1|3|3|3|4|4|45|5|5|56|6|6|7|6|6|6|6|6|6|6|6|6|6|33|4|2|6
```
## 16.4 字符串对象
### 16.4.1 包装
对象才有属性和方法，复杂数据类型才有属性和方法  
但是简单数据类型也可以有属性 

基本包装类型就是把简单数据类型包装成复杂数据类,这样简单数据类型就有了属性和方法 
在JS中为我们提供了三个包装类，通过这三个包装类可以将基本数据类型的数据转换为对象

new String() 可以将基本数据类型字符串转换为String对象  

new Number() 可以将基本数据类型的数字转换为Number对象

new Boolean() 可以将基本数据类型的布尔值转换为Boolean对象

注意：我们在实际应用中不会使用基本数据类型的对象，如果使用基本数据类型的对象，在做一些比较时可能会带来一些不可预期的结果  
方法和属性只能添加给对象，不能添加给基本数据类型 当我们对一些基本数据类型的值去调用属性和方法时，浏览器会临时使用包装类将其转换为对象，然后在调用对象的属性和方法 调用完以后，在将其转换为基本数据类型
```
        var str = 'andy';
        console.log(str.length); // 4

        // 包装过程
        // (1) 把简单数据类型转换成复杂数据类型
        var temp = new String('andy');
        // (2) 把临时变量的值给str
        str = temp;
        // (3) 销毁临时变量
        temp = null;

```
### 16.4.2 字符串不可变
指的是字符串的值内容不可变，只是地址变了，内存中新开辟一个空间存放新的字符串内容  
所以不要大量拼接字符串  
字符串所有的方法都不会修改字符串本身，都是新开辟空间存放新的字符串（字符串的不可变性）  
### 根据字符返回位置
indexOf('查找的字符')  
要查找的字符起始位置  
查不到返回-1  

indexOf('要查找的字符',[起始的索引号位置])  
从索引号位置往后查  
查不到返回-1  
```
        var str = 'abcdefgccccedf';
        console.log(str.indexOf('c'));// 2
        console.log(str.indexOf('c',[2]));// 2
        console.log(str.indexOf('c',[3]));// 7
```
lastIndexOf()  
从后往前找，只找第一个匹配的位置  

例子
```
        // 查找字符串中所有o的位置以及出现的次数
        var str = 'oooabcdefoxyozzopp';
        var index = str.indexOf('o');// 6
        var num = 0;
        while(index !== -1){
            console.log(index);
            num++;
            index = str.indexOf('o',[index+1]);
        }
        console.log('o出现了'+ num +'次');
```
### 根据位置返回字符（重要）
charAt(index)  
返回指定位置的字符（index字符串的索引号）  
str.charAt(0)
```
        var str = 'abcde';
        console.log(str.charAt(3));// d
        // 遍历所有的字符
        for(var i = 0;i<str.length;i++){
            console.log(str.charAt(i));
        }
```

charCodeAt(index)  
获取指定位置字符的ASCII码  
str.charCodeAt(0)  
用以判断用户按了哪一个键  
```
        var str = 'abcde';
        // 遍历所有的字符
        for(var i = 0;i<str.length;i++){
            console.log(str.charCodeAt(i));
            // 97 98 99 100 101
        }
```

str[index]  
获取指定位置处字符  
H5新增,IE8支持 和charAt()等效  
```
        var str = 'abcde';
        console.log(str[3]);// d
        // 遍历所有的字符
        for(var i = 0;i<str.length;i++){
            console.log(str[i]);
            // a b c d e
        }

```

例
```
        // 查找字符串里面出现最多次的字符以及出现的次数
        var str ='aamjkbcdefooedfoogk';
        var obj = {};// 新建对象保存所有出现过的字符和次数
        for(var i = 0;i<str.length;i++){
            var character = str.charAt(i);
            if(obj[character]){
                // 对象里面已有的属性值加一
                obj[character]++;

            } 
            else{
                // 对象里面原先没有的属性赋值为1
                obj[character] = 1;
            }
        }
        console.log(obj);
        var max = 0;
        var ch = '';
        for(var k in obj){
            // k得到的是属性名
            // obj[k]得到属性值
            if(obj[k] > max){
                max = obj[k];
                ch = k;// 因为k属于局部变量，在for循环外无意义
            }

        }

        console.log('出现次数最多的字母是 '+ ch + ' 出现了'+ max + '次');
        // 出现次数最多的字母是 o 出现了4次
```
### 字符串操作方法
concat(str1,st2……)  
用于连接多个字符串。等价于+，但是+更常用  
```
        var str = 'jrj';
        console.log(str.concat('SB','JRJ','kkkkk'));
        // jrjSBJRJkkkkk
```

substr(start,length)  
从start开始，length是取的个数  
```
        var str1 = 'kkkkkjrjkkkkk';
        console.log(str1.substr(5,3));
        // 从索引号5开始取，取三个字符 jrj
```
### 替换字符
replace()  
只会替换第一个字符  
```
        var str = 'kjrjkkjrj';
        console.log(str.replace('j','t'));
        // ktrjkkjrj
```
替换所有
```
        var str = 'jrjrjrjrjrj';
        while(str.indexOf('j') !== -1){
            str = str.replace('j','*')

        }
        console.log(str);
```
### 字符转换成数组
split('分隔符')  
```
        var str = 'a|b|c|b|d';
        console.log(str.split('|'));
        // 根据字符串的分隔符区分数组里面的分隔符
        //  ["a", "b", "c", "b", "d"]
```

-------------------------
# 17简单数据类型和复杂数据类型
简单数据类型又叫基本数据类型或者值类型，复杂数据类型又叫引用类型  
值类型，在变量中存储的是值本身  
string number Boolean undefined null  
注意：typeof null 会输出object，是一个空的对象  

复杂数据类型：在存储变量中存储的仅仅是地址（引用），因此叫做引用数据类型  
通过new关键字创建的对象（系统对象，自定义对象）如object array date等  

## 17.1堆和栈
栈 存放简单数据类型 直接存放的是值  
堆 存放复杂数据类型，首先在栈里面存放十六进制的地址指向堆，一般由程序员分配释放，若程序员不释放，由垃圾回收机制回收    

## 17.2传参
### 简单类型传参
函数的形参也可以看作变量，把值类型变量作为参数传递给形参时，其实是把变量在栈空间里面的值复制一份给形参，当局部对形参做任何修改，都不会改变外部变量的值  

### 复杂类型传参
函数的形参可以看做变量，当把引用类型的变量传给形参时，其实是把变量在栈空间里保存的堆地址复制给了形参，形参和实参保存的是同一个堆地址，指向同一个堆数据，所以操作的是同一个对象  

-----------
# web apis
api application programming interface(应用程序编程接口)预定义的函数，提供应用程序与开发人员基于软件或硬件得以访问的能力，不需要访问源码或者内部机制 `接口`  

web api是操作浏览器功能和页面元素的API（DOM和BOM）  
web api很多都是方法（函数）  
# DOM
DOM document object model 文档对象模型 处理可扩展标记语言的标准编程`接口`  
通过接口可以改变网页的内容样式等  
## 获取元素
### 1、根据ID获取
getElementById(),返回的是对象
```
	<body>
	    <!-- <div class="box1"></div> -->
	    <div id = "time">2021-2-20</div>
	    <script>
		// 因为文档页面从上到下，所以script写在标签的下面
		var timer = document.getElementById('time');// 参数是ID
		console.log(timer);
		// 返回的是对象，如果找不到返回null
		console.dir(timer);// dir打印返回的元素对象，更好的查看属性和方法

	    </script>
	</body>
```
### 2、根据标签名获取
getElementByTagName() 返回的对象的集合以伪数组的形式存储  
我们想要依次打印元素对象可以采取遍历的形式  
返回的元素是动态的  
页面只有一个，返回的还是以伪数组的形式  
没有元素，返回的是空的伪数组  

可以通过父元素获取内部子元素 必须指明是哪一个父元素  
### 3、通过类名获取
getElementByClassName()  
不兼容IE8及以下浏览器

### 4、querySelector()
返回指定选择器的第一个元素对象  
```
    <div class="box">1</div>
    <div class="box">2</div>

    <script>
        var firstBox = document.querySelector('.box');
        console.log(firstBox);
        // 返回第一个box
        // 参数必须带符号，类，ID等
    </script>
```
### 5、querySelectorAll()
返回指定选择器的所有元素对象集合  

## 获取特殊元素
### 获取body元素
```
    <script>
        var bbb = document.body;
        console.log(bbb);
    </script>
```
### 获取html元素
```
    <script>
        var hhh = document.documentElement;
        console.log(hhh);
    </script>
```

---------
## 事件
事件由三部分组成，事件源，事件类型，事件处理程序

事件源：事件被触发的对象 如创建的按钮

事件类型：如何触发如鼠标点击，鼠标经过，键盘按下

事件处理程序：通过一个函数赋值的方式完成
```
	<body>
		// 创建事件源
	    <button id="btn">点我 就现在</button>

	    <script>
		// 获取按钮节点
		var btn = document.getElementById('btn');
		// 事件处理程序
		btn.onclick = function(){
		    alert('点我干嘛？？？');
		}
	    </script>
	</body>
```
### 事件基础
执行事件的步骤  
1、获取事件源  
2、注册事件（绑定事件）  
3、添加事件处理程序  

## 操作元素
element.innerText  
从起始位置到终止位置的内容，但它去除html标签，同时空格和换行也会去掉  

element.innerHTML  
起始位置到终止位置的全部内容，包括html标签，同时保留空格和换行  
```
    <button>显示当前系统时间</button>
    <div>某个时间</div>
    <script>
        // 点击按钮，div里面的文字发生变化
        // 1、获取元素
        var btn = document.querySelector('button');
        var div = document.querySelector('div');
        // 2、注册事件
        btn.onclick = function(){
            div.innerText = getD();// 若果这行代码不在函数里面，相当于不注册事件直接运行
        }
        function getD(){
            var date = new Date();
            var year = date.getFullYear();
            var month = date.getMonth()+1;
            var date111 = date.getDate();// 千万要注意！！！这里的变量不能和一开始的date冲突，否则显示下一行的getDay is not a function
            var day = date.getDay();
            var arr = ['星期日','星期一','星期二','星期三','星期四','星期五','星期六'];

            return'今天是'+year+'年'+month+'月'+date111+'日'+arr[day];

        }
        console.log(getD() );
    </script>
```

.innerText和.innerHTML区别 ：前者不识别HTML标签
```
 	var div = document.querySelector('div');
        div.innerHTML = '今天天气<strong>真不错</strong>';// 识别标签
        // div.innerText = '今天天气<strong>真不错</strong>'; // 不识别，直接当文本输出
```
## 修改元素属性
```
    <button id="ldh">刘德华</button>    
    <button id="lcw">梁朝伟</button>    
    <br><br>
    <img src="./img/01.jpg" alt="" title="刘德华">
    <script>
        // 1、获取元素
        var ldh = document.getElementById('ldh');
        var lcw = document.getElementById('lcw');
        var img = document.querySelector('img');

        // 2、注册事件
        ldh.onclick = function(){
            img.src = "./img/01.jpg";
            img.tile = "刘德华";
        }
        lcw.onclick = function(){
            img.src = "./img/02.jpg";
            img.title = "梁朝伟";
        }
    </script>
```
## 操作表单元素
```
    <button>按钮</button>
    <input type="text" value="输入内容">
    <script>
        // 1、获取元素
        var btn = document.querySelector('button');
        var inp = document.querySelector('input');

        // 2、注册事件
        btn.onclick = function(){
            // input.innerHTML = '点击了';
            // innerHTML是修改普通盒子比如div标签内的内容
            
            // 表单内容是通过value修改
            inp.value = '点击了';
	    
	    // 如果按钮点击一次后不能再被点击，使用disabled
            this.disabled = true;// this指向的是事件函数的调用者
        }
    </script>
```

##### 京东登录
```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .box {
            width: 400px;
            border-bottom: 2px solid #aaa;
            /* 上边距100px 居中 */
            margin: 200px auto;
            position: relative;
        }

        .box input {
            width: 370px;
            height: 30px;
            border: 0px;
            /* 去除外边框 */
            outline: none;
        }

        .box img {
            width: 24px;
            position: absolute;
            top: 5px;
            right: 0px;

        }
    </style>
</head>

<body>
    <div class="box">
        <label for="">
            <img src="./img/闭眼.png" alt="" id="eye">
        </label>
        <input type="password" name="" id="password">
    </div>
    <script>
        // 1、获取元素
        var eye = document.getElementById('eye');
        var password = document.getElementById('password');

        // 2、注册事件
        // 设置一个flag来表示密码框的状态，通过01变换实现切换
        var flag = 0;
        eye.onclick = function () {
            if (flag == 0) {
                // 密码框改为文本框 显示密码
                password.type = "text";
                eye.src = "./img/睁眼.png";
                flag = 1;
            }
            else{
                // 密码框改为密码框 不显示密码
                password.type = "password";
                eye.src = "./img/闭眼.png";
                flag = 0;
            }

        }



    </script>
</body>

</html>
```
## 操作样式属性
通过JS修改元素的大小颜色位置等样式  
Js里面的样式采取驼峰命名法 fontSize，backgroundColor  
Js修改style样式操作，产生的是行内样式，比CSS样式的权重更高  
##### 淘宝关闭二维码样式
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>淘宝二维码</title>
    <style>
        .box{
            width: 74px;
            height: 88px;
            border: 1px solid #ccc;
            margin: 100px auto;
            font-size: 12px;
            text-align: center;
            color: #f40;
            position: relative;
        }
        .box img{
            height: 50px;
            margin-top: 5px;
        }
        .box .close-btn{
            position: absolute;
            top: -1px;
            left: -16px;
            width: 14px;
            height: 14px;
            border: 1px solid #ccc;
            font-family:Arial, Helvetica, sans-serif;
            cursor: pointer;
        }
    </style>

</head>
<div class="box">
        <body>
        淘宝二维码
        <img src="./img/02.jpg" alt="">
        <i class="close-btn">×</i>
    </div>
    <script>
        // 1、获取元素
        var btn = document.querySelector('.close-btn');
        var box = document.querySelector('.box');
        // 2、注册事件 程序处理
        btn.onclick = function(){
            box.style.display = 'none';
        }
    </script>
</body>
</html>
```
### 焦点
onfocus 得到焦点   
onblur 失去焦点  
##### 京东文本框
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>京东文本框</title>
    <style>
        input{
            color: #ccc;
            margin: 200px 200px;
        }
    </style>
</head>
<body>
    <input type="text" value="手机">
    <script>
        // 1、获取元素
        var text = document.querySelector('input');
        // 2、注册事件 获得焦点事件
        text.onfocus = function(){
            if(this.value == '手机'){
                text.value = "";
            }
            // 获得焦点使文本框字色变深
            this.style.color = '#333';
        }
        // 3、失去焦点事件
        text.onblur = function(){
            if(this.value == ''){
                text.value = '手机';
            }
            // 失去焦点文本框颜色变浅
            this.style.color = '#ccc';
        }
    </script>
</body>
</html>
```
## 通过className修改样式
如果使用element.style.修改元素样式，一次只能改一种  
可以在CSS中写好类包含所有样式改变  
然后通过给当前元素添加类名  
this.className = '类名';
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        div{
            width: 200px;
            height: 200px;
            background-color: #bfa;
        }
        .change{
            background-color: #aab;
            color: #f60;
            font-size: 25px;
            margin: 200px auto;
        }
    </style>
</head>
<body>
    <div>嗷嗷嗷啊</div>
    <script>
        // 1、获取元素
        var div = document.querySelector('div');
        // 2、注册事件 程序处理
        div.onclick = function(){
            // 修改当前元素的类名
            // 类名已经写在style里面
            this.className = 'change';
        }
    </script>
</body>
</html>
```
注意：className会直接覆盖掉原先的类名！  
如果需要保留原先的类名  
this.className = '原先的类名 修改的类名';  

--------------
## 排他思想（算法）
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
    <button>按钮1</button>
    <button>按钮2</button>
    <button>按钮3</button>
    <button>按钮4</button>
    <button>按钮5</button>
    <script>
        // 1、获取元素
        var btns = document.getElementsByTagName('button');
        // 2、注册事件 程序处理
        for(var i = 0;i<btns.length;i++){
            btns[i].onclick = function(){
                /*
                    1、先把所有按钮的背景颜色去掉
                    2、再把选中的按钮颜色变色
                */
               for(var j=0;j<btns.length;j++){
                   btns[j].style.backgroundColor = '';
               }
                this.style.backgroundColor = '#abf';
            }
        }
    </script>
</body>
</html>
```
### 鼠标经过
onmouseover 鼠标经过  
onmouseout 鼠标离开  


## 自定义属性操作
#### 获取属性值
element.属性 获取属性值 获取内置属性   
element.getAttribute('属性') getAttribute获取的是自己设置的属性  

#### 修改属性值
element.属性 = '值'  
element.getAttribute('属性','值')  

#### 移除属性值
.removeAttribute('属性')  

# 节点
获取元素常用的两种形式  
1、利用DOM方法获取  
逻辑性不强，繁琐

2、节点操作  
利用父子兄弟关系获取  

页面中所有的内容都是节点 DOM中使用node表示节点  
一般来说，节点至少拥有节点类型（nodetype） 节点名称（nodeName） 节点值（nodevalue）三个基本属性  
元素节点的节点类型是1  
属性节点的节点类型是2  
文本节点的节点类型是3（包括文字 空格 换行）  
实际开发中，主要操作的是元素节点  

## 节点层级
### 父节点
.parentNode 离元素最近的父节点  
找不到父节点返回null  
### 子节点
通过具体的元素节点调用

1.childNodes  
表示当前节点的所有子节点（换行也算文本节点）注意：IE8及以下，不会将空白换行作为节点  
可以使用nodeType判断，去除换行  
文本节点类型是3，元素节点类型是1    
也可以使用children（非标准）  

2.firstChild   
表示当前节点的第一个子节点  
可能包含其他节点  
firstElementChild IE9

3.lastChild  
表示当前节点的最后一个子节点  
可能包含其他节点  
lastElementChild IE9  

实际开发中可能使用.children[0]表示第一个节点  
.children[ul.children.lengtth - 1]表示最后一个节点  
### 兄弟节点
1.previousSibling  
属性，表示当前节点的前一个兄弟节点  
包含元素或文本节点（换行）  

2.extSibling  
属性，表示当前节点的后一个兄弟节点  
包含元素或文本节点（换行）  
nextElementSilbling 下一个兄弟元素节点不包括文本（换行）  

兼容性问题：自己封装一个函数  

## 创建节点
.createElement  
可以用于创建一个元素节点对象 它需要一个标签名作为参数，将会根据该标签名创建元素节点对象 并将创建好的对象作为返回值返回   
例如： 创建一个li标签 ` var li1 = document.createElement("li"); `

appendChild()  
向一个父节点末尾添加一个新的子节点 用法: 父节点.appendChild(子节点);

insertBefore()  
可以在指定的子节点前插入新的子节点 语法： 父节点.insertBefore(新节点(前),旧节点(后));  

## 删除节点
removeChild()  
```
        // 1、获取元素
        var ul = document.querySelector('ul');
        // 2、删除元素
        ul.removeChild(ul.children[0]);// 删除第一个子节点
```
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <button>删除</button>
    <ul>
        <li>A</li>
        <li>B</li>
        <li>C</li>
        <li>D</li>
    </ul>
    <script>
        // // 1、获取元素
        var ul = document.querySelector('ul');
        // // 2、删除元素
        // ul.removeChild(ul.children[0]);// 删除第一个子节点

        // 点击按钮依次删除元素
        var btn = document.querySelector('button');
        btn.onclick = function(){
            
            if(ul.children.length == 0){
                // 禁用删除按钮
                this.disabled = true;
            }
            else{
                ul.removeChild(ul.children[0]);
            }
        }
    </script>
</body>
</html>
```
## 复制节点
```
        // 1、获取元素
        var ul = document.querySelector('ul');
        // 2、复制节点
        var lili = ul.children[0].cloneNode(true);

        ul.appendChild(lili);
```
如果.cloneNode()括号里面参数为空，或者是false，称为浅拷贝，只复制节点本身，不复制节点内容  

括号里为true称为深拷贝，复制标签和内容  
 
##### 动态生成表格
```
<!DOCTYPE html>
<html lang="zh">

<head>
    <meta charset="UTF-8">
    <title>表格</title>
    <style>
        table {
            width: 500px;
            margin: 100px auto;
            border-collapse: collapse;
            text-align: center;
        }

        td,
        th {
            border: solid 1px #333;
        }

        thead tr {
            /* 设置表头 行 */
            height: 40px;
            background-color: #abf;
        }
    </style>
</head>

<body>
    <table>
        <thead>
            <tr>
                <th>名字</th>
                <th>科目</th>
                <th>成绩</th>
                <th>操作</th>
            </tr>
        </thead>

        <tbody>

        </tbody>
    </table>

    <script>
        // 1、学生数据
        var dates = [
            {
                name: '孙悟空',
                subject: '语文',
                score: 100
            },
            {
                name: '唐僧',
                subject: '语文',
                score: 95
            },
            {
                name: '猪八戒',
                subject: '语文',
                score: 70
            },
            {
                name: '沙和尚',
                subject: '语文',
                score: 90
            }
        ];
        // 2、创建表格的行数（数组元素个数）
        var tbody = document.querySelector('tbody');
        for (var i = 0; i < dates.length; i++) {
            var tr = document.createElement('tr');
            tbody.appendChild(tr);
            // td是数组里面对象的属性个数 dates[i]
            // 遍历对象
            // j 得到属性名
            //  obj[j] 得到属性值
            for (var j in dates[i]) {
                // 创建单元格
                var td = document.createElement('td');
                // 把每个单元格添加元素到行里面
                tr.appendChild(td);
                // dates是数组 dates[i]是数组里面第i个元素（对象） dates[i][j]是数组里面对象的属性值
                // console.log(dates[i][j]);
                // 向单元格中添加元素
                td.innerHTML = dates[i][j];
            }

            // 创建操作里面的 删除单元格
            // 3、创建单元格，数字取决于数组每个元素 对象里面的属性个数
            var td = document.createElement('td');
            tr.appendChild(td);
            // 在最后一个单元格添加内容(删除的链接)
            td.innerHTML = '<a href="#">删除</a>'

        }

        // 4、创建删除操作 获取所有的a 创建事件 删除a所在的行
        var aaa = document.querySelectorAll('a');
        for(var i = 0;i<aaa.length;i++){
            aaa[i].onclick = function(){
                // 点击链接删除a所在的行
                tbody.removeChild(this.parentNode.parentNode);
            }
        }



    </script>
</body>

</html>
```
## 三种动态创建元素的区别
document.write() （很少使用）     
直接将内容写入页面的内容流，但是文档流执行完毕，会导致页面全部重绘  
```
<body>
    <button>
        按钮
    </button>
    <script>
        var btn = document.querySelector('button');
        btn.onclick = function(){
            document.write('<div>123</div>');
        }

    </script>
</body>
```

innerHTML创建元素  
```
<body>
    <div class="inn"></div>
    <script>
        var inn = document.querySelector('.inn');
        inn.innerHTML = '<a href="#">百度</a>';
    </script>
</body>
```

createElement()  
```
<body>
    <div class="cre"></div>
    <script>
        var cre = document.querySelector('.cre');
        var a = document.createElement('a');
        cre.appendChild(a);
    </script>
</body>
```
使用innerHTML()创建大量元素时，效率更高  
但是前提是不要使用拼接字符串的形式，而要使用数组的形式  
结构稍微复杂  

## DOM重点核心
为了能够让js操作HTML，js有一套自己的dom接口  
学习dom主要是针对元素的操作,增，删，改，查，属性操作，事件操作

增加：  
document.write()  
innerHTML  
creatElement()  

删除：  
removeChild

改：  
1、修改dom元素属性 src href title等  
2、修改普通元素内容 innerHTML innerText  
3、修改表单元素 value type disabled  
4、修改元素样式style className  

查：  
1、DOM提供的API getElementById getElementByTagName (不推荐)  
2、H5新方法 querySelector querySelectorAll (推荐)  
3、利用节点获取元素 父子兄弟节点  

属性操作：  
setAttribute 设置dom属性值  
getAttribute 得到属性值  
removeAttribute 删除属性  

事件操作：  
鼠标点击 经过 离开 焦点等  

--------------------

# 事件高级

## 注册事件
注册事件有两种方式：传统方式和监听注册事件  
### 传统
on开头的例如onclick鼠标点击    
特点 注册事件的唯一性，只运行靠后的处理函数  
### 方法监听注册事件  
addEventListener() 推荐使用  

同一个元素同一个事件可以添加多个监听器 不会出现唯一性问题  
该方法三个参数   
type 事件类型字符串带引号 比如click mouseover 不带on   
listener 事件处理函数 事件发生时 会调用该函数  
useCapture 可选参数 是一个布尔值默认false   

addEventListener()中的this是绑定事件的对象 不支持IE8及以下

attachEvent() 在IE8中及以前可以使用attachEvent()来绑定事件  
参数：   
1.事件的字符串，要on  
2.回调函数 这个方法也可以同时为一个事件绑定多个处理函数   
不同的是它是后绑定先执行，执行顺序和addEventListener()相反  

注册事件兼容性问题解决
```
        function addEventListener(element ,eventName,fn){
            // 判断当前浏览器是否支持addEventLisener方法
            if(element.addEventListener){
                element.addEventListener(eventName,fn);// 第三个参数默认false

            }
            else if(element.attachEvent){
                element.attachEvent('on'+eventName,fn);

            }
            else{
                element['on'+ eventName] = fn;
            }
        }
```
## 删除事件
### 传统
.onclick = null;  
### 方法监听注册方式
.removeEventListener(type,listener,useCapture)  

例
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        div{
            width: 100px;
            height: 100px;
            background-color: #bfa;
        }
    </style>
</head>
<body>
    <div class="a">1</div>
    <div class="b">2</div>
    <div class="c">3</div>
    <script>
        var divs = document.querySelectorAll('div');

        // 传统绑定事件
        divs[0].onclick = function(){
            alert(111);
            // 传统删除事件
            divs[0].onclick = null;
        }

        // 方法监听注册事件
        // 三个参数，type字符串要加引号不要on
        divs[1].addEventListener('click',fn);
        // 因为要删除函数 所以函数不能使用匿名的
        function fn(){
            alert(222);
            // 方法监听删除
            divs[1].removeEventListener('click',fn);
        }

    </script>
</body>
</html>
```
## DOM事件流
事件发生时会在元素节点之间按照特定的顺序传播，这个传播过程就是DOM事件流  
事件流分为三个阶段  

1.捕获阶段 在捕获阶段时从最外层的祖先元素，向目标元素进行事件的捕获，但是默认此时不会触发事件

2.当前目标阶段 事件捕获到目标元素，捕获结束开始在目标元素上触发事件

3.冒泡阶段 事件从目标元素向它的祖先元素传递，依次触发祖先元素上的事件 addEventListener 第三个参数是false或省略 处于冒泡阶段  

如果希望在捕获阶段就触发事件，可以将addEventListener()的第三个参数设置为true，一般情况下我们不会希望在捕获阶段触发事件，所以这个参数默认都是false   

IE8以下的浏览器没有捕获阶段  

## 事件对象
```
            // event就是事件对象 写到侦听函数的小括号里 可以当成形参看待
            // 事件对象只有事件存在才会存在 是系统自动创建的 不需要传递实参
            // 事件对象是事件一系列相关数据的集合 比如鼠标点击包含鼠标的相关信息 例如鼠标坐标
            // 键盘事件包含键盘按键信息
            // 事件对象可以自己命名 event evt e
            // 事件对象也有兼容性问题 通过window.event 解决
            // e = e || window.event 
```
### 事件对象常见的属性和方法
e.target 返回触发事件的方法 标准  
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        div{
            width: 150px;
            height: 150px;
            background-color: #abf;
        }
    </style>
</head>
<body>
    <div>1234</div>
    <ul>
        <li>a</li>
        <li>b</li>
        <li>c</li>
        <li>d</li>
    </ul>
    <script>
        var div = document.querySelector('div');
        div.addEventListener('click',function(e){
            console.log(e.target);// 返回触发事件的对象div1234
            console.log(this);// 返回绑定事件的对象div 1234
        })


        var ul = document.querySelector('ul');
        ul.addEventListener('click',function(e){
            console.log(this);// 给ul绑定事件 this指向ul 返回ul
            console.log(e.target);// 返回点击的li
        })
    </script>
</body>
</html>
```


e.srcElement 返回触发事件的对象 非标准 ie6-8使用

e.type 返回事件的类型 比如click 不带on  

e.returnValue 该属性阻止默认事件（默认行为）非标准 ie6-8使用 比如不让链接跳转  

e.preventDefault() 该方法阻止默认事件 标准 比如不让链接使用

## 阻止冒泡
所谓的事件的冒泡指的是事件的向上传导，当后代元素上的事件被触发时，其祖先元素的相同事件也会被触发 在开发中大部分情况冒泡都是有用的，如果不希望发生事件冒泡，可以通过事件对象来取消冒泡

e.stopPropagation()阻止冒泡 标准  

e.cancelBubble = true 该属性阻止冒泡 非标准 ie6-8使用  

## 事件委派
原理：不给每个子节点单独设置事件监听器 而是事件监听器设置在父节点上 然后利用冒泡原理影响设置每个子节点  
在父节点上设置事件 然后利用target找到点击li 然后事件冒泡到ul上  
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
    <ul>
        <li>a</li>
        <li>b</li>
        <li>c</li>
        <li>d</li>
    </ul>
    <script>


        var ul = document.querySelector('ul');
        ul.addEventListener('click',function(e){
            // alert('aaaaaaa');
            //  点击某个li时，事件会冒泡到Ul上 弹出


            // e.target可以得到当前点击的对象
            e.target.style.backgroundColor = '#b66';
        })
            
    </script>
</body>
</html>
```
## 常用的鼠标事件
