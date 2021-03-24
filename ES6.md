# ES5
2009发布  
## ES5严格模式

在全局或函数的第一条语句定义为"use strict"  
如果浏览器不支持，只解析为一条简单的语句，没有任何副作用  

### 语法和行为的改变

1.必须用var声明变量  
2.禁止自定义的函数中的this指向window  
3.严格模式创建eval作用域   
4.对象不能有重名属性  

## ES5_Object对象方法扩展

### Object.create(object, descriptors)

作用：以指定对象为 原型 创建新的对象，为新的对象指定新的属性，并对属性进行描述

value：指定值

writeable：当前属性值是否可修改，默认为false

configurable：当前属性是否可删除，默认为false

enumerable：当前属性能否用for in枚举，默认为false

```
var obj1 = {
    name: "蔡徐坤",
    age: "20"
}
var obj2 = Object.create(obj1, {
    height: {
        value:180,
        writable:true,
        configurable:true,
        enumerable:true
    }
})
console.log(obj2)
for (var key in obj2) {
    console.log(key)
}
```

### Object.defineProperties(object, descriptors)

Object.defineProperties() 方法直接在一个对象上定义新的属性或修改现有属性，并返回该对象。

get：用来获取当前属性值的回调函数，获取扩展属性值时自动调用

set：修改当前属性值时触发的回调函数，并且实参为修改后的值

存取器属性：setter用来存值，getter用来取值

```
    var obj = {
        firstname: "ABC",
        lastname: "DEF"
    }
    Object.defineProperties(obj, {
        fallname: {
            get:function () {
                console.log("get")
                return this.fallname = this.firstname + this.lastname
            },
            set:function (data) {
                this.firstname = data
                console.log("set" + data)
            }
        }
    })
    console.log(obj.fallname)
    obj.fallname = "123"
    console.log(obj.fallname)

```

### 对象本身的两个方法get set
get propertyName() {}   
set propertyName() {}   

```
var flag = 100
var obj = {
    name:"abc",
    age:18,
    get weight() {
        return flag
    },
    set weight(data) {
        flag = data
        return flag
    }
}
console.log(obj.weight)
obj.weight = 130
console.log(obj.weight)
```

## ES5_Array的扩展

### indexOf()

该方法可以检索一个数组中是否含有指定内容  
如果字符串中含有该内容，则会返回其第一次出现的索引  

### lastIndexOf()

### forEach(function (item, index, arr) {})

遍历数组

### map(function (item, index) {})

遍历数组返回一个加工过的新数组

### filter(function (item, index) {})

遍历返回一个过滤后的子数组，return为true的值

## ES5_call，apply，bind

相同
都能指定函数中的this

不同
apply()数组传参  
call()/apply()立即调用   
bind()不会立即调用，而是将函数返回  

# ES6  
2015发布  

## let

1.作用：  
与var类似，用于声明一个变量   

2.特点：   
    在块级作用域内有效   
    不能重复声明   
    不会预处理，不存在提升   

3.应用：  
循环遍历加监听   
使用let取代var是趋势   

```
var funcs = [];
for (let i = 0; i < 3; i++) {
    funcs[i] = function () {
        console.log(i);
    };
}
funcs[0](); // 0
```
可以理解为

```
(let i = 0) {
    funcs[0] = function() {
        console.log(i)
    };
}

(let i = 1) {
    funcs[1] = function() {
        console.log(i)
    };
}

(let i = 2) {
    funcs[2] = function() {
        console.log(i)
    };
};
```
## const

1.作用：  
定义一个常量  

2.特点：  
    不能修改  
    在块级作用域内有效   
    不能重复声明   
    不会预处理，不存在提升   

3.应用:   
保存不用改变的数据   

## 变量的解构赋值

1.理解：   
从对象或数组中提取数据，并赋值给多个变量   

2.对象的解构赋值  
let {n, a} = {n: "tom", a: 12}   

3.数组的解构赋值   
let [,,a, b,] = [1, 2, 3, 4, 5]  

4.用途：  
给多个形参赋值   

## 模板字符串 

1.作用：   
简化字符串的拼接   

2.格式   
模板字符串必须用``包含  
变化的部分使用${xxx}定义   

```
let obj = {
    name: "abc",
    age: 18
}

let str = `我的名字是${obj.name},我今年${obj.age}岁了`
console.log(str);
```

## 简化的对象写法

简化的对象写法

省略同名的属性与属性值      
省略方法的function   

例如：
```
let x = 1;
let y = 2;
let point = { //同名属性与属性值省略不写
    x,
    y, //省略方法的function
    setX (x) {return this.x = x}
}
```

## 箭头函数详解

1.作用：  
定义匿名函数   

2.基本语法：  
没有参数：() => console.log("aa")  

一个参数： x => i + 2  

大于一个参数：(a, b) => a + b

函数体不用大括号，默认返回结果  
函数体有多个语句，需要用{}包围，若有需要返回的内容，需要手动返回

3.使用场景:  
多用来定义回调函数    

4.箭头函数的特点  
    箭头函数没有自己的this，箭头函数的this不是调用的时候决定的，而是在定义的时候处在的对象就是它的this  
    扩展理解：箭头函数的this看外层是否有函数  
    如果有，外层函数的this就是内部箭头函数的this  
    如果没有，则this是window  
    无法通过call/apply/bind改变this  

## 三点运算符

1.可变参数

用来取代 arguments（伪数组） 比 arguments 灵活，但是只能放在最后收集实参返回数组

```
function fun(a, b, ...value) {
    value.forEach(function (item, index) {
        console.log(item, index)
    })
}
fun(1, 2, 3, 4, 5)
```

2.扩展运算符

```
let arr1 = [3, 4, 5]
let arr2 = [1, 2, ...arr1, 6]
console.log(arr2)
```

## 形参默认值

当不传入参数的时候默认使用形参里的默认值

function Point(x = 1, y = 2) {
    this.x = x
    this.y = y
}

## Promise对象原理详解

Promise对象：代表了未来某个将要发生的事件（通常是一个异步操作）

有了Promise对象，可以将异步操作以同步的流程表达出来

### 创建Promise对象

```
        let promise = new Promise((resolve,reject) =>{
            // 初始化promise状态 pending 初始化
            console.log(1);
            // 执行异步操作 通常是发送ajax请求 开启定时器
            setTimeout(()=>{
                console.log(3);
                // 根据异步任务的返回结果 修改promise的状态
                // 异步任务执行成功
                resolve('hhhhhhh');// 修改promise的状态为成功状态

                // 异步任务执行失败
                // reject('555');// 修改promise的状态为失败状态
            },2000);
        })
        console.log(2);

        promise
        // then里面两个形参传递的是上面resolve()/reject()返回的数据
            .then((a) => {// 成功的调用
                console.log(a,"成功了！！！");
            },(error) =>{// 失败的调用
                console.log(error,"失败了。。。");
            })
```
### 应用

使用promise实现超时处理

使用promise封装处理Ajax请求

## 原始数据类型Symbol

ES5中对象的属性名都是字符串，容易造成重名，污染环境，ES6中添加了一种原始数据类型symbol

### 特点

1.symbol属性对应的值是唯一的，解决命名冲突问题

2.symbol值不能与其他数据进行计算，包括同字符串拼接

3.for in, for of遍历时不会遍历symbol的属性

### 使用

1.调用Symbol函数得到symbol的值

```
let symbol = Symbol();// 不是构造函数 不需要new
console.log(symbol);
let obj = {
    name: "jack",
    age: 18
}
obj[symbol] = "hello";// 属性选择器
console.log(obj);
```

2.传参标识（唯一）

```
let symbol2 = Symbol('aaa2');// 可以给不同的symbol传入唯一标识的参数
let symbol3 = Symbol('aaa3');
console.log(symbol2 == symbol3);// false
```

3.内置Symbol值  
除了定义自己使用的Symbol值以外，ES6还提供了11个内置的Symbol值，指向语言内部的使用方法  

## iterator接口机制

概念：iterator是一种接口机制，为各种不同的数据结构提供统一的访问机制

作用：  
1.为各种数据结构，提供一个统一的，简便的访问接口

2.使得数据结构的成员能够按某种次序排列

3.ES6创造了一种新的遍历命令for of循环，iterator接口主要供for of消费

工作原理：  
    创建一个指针对象（遍历器对象），指向数据结构的起始位置  
     第一次调用next方法，指针自动指向数据结构的下一个成员   
     接下来不断调用next方法，指针会一直往后移动，直到指向最后一个成员  
     每调用next方法返回的是一个包含value和done的对象（value：当前成员的值，done：布尔值）   
     value表示当前成员的值，done对应的布尔值表示当前的数据的结构是否遍历结束   
     当遍历结束的时候返回的value值是undefined，done值为true   

```
        function myIterator(arr){
            let index = 0;// 记录指针的位置
            return {
                // 函数返回值是遍历器对象
                next(){// 简写的对象方法
                    // 判断句
                    // index小于数据长度时继续向后遍历
                    // 一旦到数据末尾，返回str，修改done
                    return index<arr.length?{
                        value: arr[index++],// arr[index++]下标先使用再加加
                        done: false
                    }:{
                        value: '遍历完成！',
                        done: true
                    }
                }
            }
        }
        // 准备一组数据测试
        let arr = [1,2,3,4,5];
        let iteratorObj = myIterator(arr);
        console.log(iteratorObj.next());
        console.log(iteratorObj.next());
        console.log(iteratorObj.next());
        console.log(iteratorObj.next());
        console.log(iteratorObj.next());
        console.log(iteratorObj.next());// 此时返回undefined
        console.log(iteratorObj.next());// 此时返回undefined

```


原生具备iterator接口的数据（可用for of遍历）  
     数组，字符串，arguments，set容器，map容器  
     iterator没有部署在obj上  

```
        let arr = [1, 2, 3, 4]
        for (const item of arr) {
            console.log(item)
        }

        let str = "abcdef";
        for(let i of str){
            console.log(i);
        }
```

## Generator函数

概念：  
可暂停函数，惰性求值函数     
1.ES6提供的解决异步编程的方案之一       
2.Generator函数是一个状态机，内部封装了不同的数据   
3.用来生成遍历器对象    
4.可暂停函数（惰性求值），yield可暂停，next方法可启动，每次返回的是yield后的表达式结果    

特点：   
1.function与函数名之间有一个*号   
2.内部用yield表达式来定义不同的状态    

```
        function* myGenerator(){
            console.log('start');
            let result = yield "hello!";// 暂停

            console.log(result);// 如果next()不传参，输出undefined 否则输出参数
            yield "1";// 每个yield通过.next()方法执行完都会暂停一次

            console.log(12333);
            yield "2";// 暂停

            return 'over'
        }
        // myGenerator();// 函数内部并没有执行

        let MG = myGenerator();
        // MG.next();// 指针对象调用next方法
        console.log(MG.next());// {value: "hello!", done: false}
        console.log(MG.next('12333333'));// {value: "1", done: false}
        console.log(MG.next());// {value: "2", done: false}
        console.log(MG.next());// {value: "return的值", done: true}

```

对象Symbol.iterator 与Generator相结合

```
let obj = {name: "abc", age: 18}
obj[Symbol.iterator] = function* () {
    yield 1
    yield 2
    yield 3
    yield 4
    return 5
}
for (let i of obj) {
    console.log(i)
}
```

## async函数

概念：真正意义上解决异步回调问题，同步流程表达异步操作

本质：Generator的语法糖（语法糖：在原有的语法基础上更加完善）

语法：  
    async function foo () {  
    await 异步操作  
    await 异步操作  
    }  

特点：  
1.不需要像Generator去调用next方法   
2.返回的总是Promise对象，可以用then方法进行下一波操作   
3.async取代Generator函数的*号，await取代Generator的yield   
4.语义上更明确，使用简单   
```
       // async函数

        async function fun(){
            return new Promise (resolve => {// 箭头函数一个参数可以省略括号
                setTimeout(() => {
                    resolve();
                },2000)
            })
        }

        async function fun1(){
            console.log('start',new Date().toTimeString());
            await fun();
            console.log('over',new Date().toTimeString());
        }

        fun1();


        function fun2(){
            return "xxxxx";
        }
        async function fun3(){
            // let result = await Promise.reject(123);
            // console.log(result);
            // 输出报错

            let result1  = await Promise.resolve(123);
            console.log(result1);
            // 输出123 
        }
        fun3();
```

## class

1.通过class定义类/实现类的继承     
2.在类中通过constructor定义构造方法  
3.通过new创建类的实例  
4.通过extends来实现类的继承  
5.通过super调用父类的构造方法   
6.重写从父类中继承的一般方法    

```
        // function Person(name,age){
        //     this.name = name;
        //     this.age = age;
        // }

        // let person = new Person('tom',22);
        // console.log(person);


        class Person {
            // 类的构造方法
            constructor(name, age) {
                this.name = name;
                this.age = age;
            }
            // 类的一般方法
            showName() {
                console.log('父类',this.name);
            }
        }
        let person = new Person('tom', 22);
        console.log(person);
        person.showName();

        // 继承
        class StarPerson extends Person {
            // 当子类继承父类时 必须使用super()声明
            constructor(name, age, salary) {
                super(name, age);// 声明调用父类的构造方法
                this.salary = salary;
            }
            showName() {
                console.log("子类",this.name,this.age);
            }
        }
        let ppp = new StarPerson('jack', 18, 10000);
        console.log(ppp);
        // 如果super()声明不传父类的参数 则输出
        // StarPerson {name: undefined, age: undefined, salary: 10000}
        ppp.showName();//子类 jack 18
        // 子类把父类的方法重写了
        
```
# String扩展

## includes(str)

判断是否包含指定的字符串

```
        let str = 'asdfgjhgkhlk';
        console.log(str.includes('asd'));// true
```

## startsWith(str)

判断是否以指定字符串开头

## endsWith(str)

判断是否以指定字符串结尾

## repeat(count)

指定目标字符串里面出现字母的次数

# Number扩展

## Number.isFinite(i)

判断是否有限大的数

## Number.isNaN(i)

判断是否是NaN

## Number.isInteger(i)

判断是否是整数

## Number.parseInt(str)
不是数字返回NaN  
将字符串转换为队形数值

## Math.trunc(i)

直接去除小数部分

# Array扩展

## Array.from(v)

将伪数组对象或可遍历对象转换为真数组

## Array.of(v1, v2, v3)

将一系列值转换成数组

## find(function(value, index, arr) {return true})

找出第一个满足条件返回true的元素

## findIndex(function(value, index, arr) {return true})

找出第一个满足条件返回true的元素下标

# Object扩展

## Object.is(v1, v2)

判断两个数据是否相等,以字符串判断
```
        console.log(0 == -0);// true
        console.log(Object.is(0,-0));// false
        
        console.log(NaN == NaN);// false
        console.log(Object.is(NaN,NaN));// true
```

## Object.assign(target, sourse1, sourse2...)

将源对象的属性复制到目标身上
```
        let obj = {
            gender: '男'
        }
        let obj1 = {
            name: 'tom',
            age: 19
        }
        Object.assign(obj,obj1);
        console.log(obj);
        // {gender: "男", name: "tom", age: 19}
```

## 直接操作__proto__属性

# 深度克隆

## 浅拷贝（对象/数组）
基本数据类型拷贝后直接生成新数据，修改拷贝后的数据不会影响原数据  

特点：修改拷贝后的数据会影响原数据，使得原数据不安全

## 深拷贝（深度克隆）

特点：拷贝的时候生成新数据，修改拷贝以后的数据不会影响原数据

## 如何实现深拷贝

1.判断数据类型

Object.prototype.toString.call(target).slice(8, -1)  
.call() 指定this 并立即调用

2.遍历对象/数组

for in对象返回属性名，数组返回下标  

```
// 判断数据类型的函数
        function checkType(target){
            return Object.prototype.toString.call(target).slice(8,-1);
        }

        // console.log(checkType(obj3));

        function clone(target) {
            let result;
            let targetType = checkType(target);
            if(targetType === 'Object'){
                result = {};

            }
            else if(targetType === 'Array'){
                result = [];
            }
            else{
                return target;
            }


            // 遍历目标
            for(let i in target){
                let value = target[i];
                // target若为数组，则根据下标赋值给value
                // target若为对象，target[i]代表对象中的i属性对应的属性值，赋值给value

                // 判断目标结构的每一个值是否存在对象/数组（存在嵌套）
                // [1,2,3,[1,2,3,[1,2]]]
                if(checkType(value) === 'Object' || checkType(value) === 'Array'){
                    result[i] = clone(value);
                }
                else{
                    result[i] = value;
                }
            }
            return result;
        }
        let arr000 = [1,2,[11,22,[111.222]]];
        let arr001 = clone(arr000);
        console.log(arr001);
        arr001[2] = {name: 'jack',age: 11};
        console.log(arr000,arr001);
        // [1, 2, Array(3)]
        // [1, 2, {…}]


```

# Set容器

Set容器：无序`不可重复`的多个value的集合体
```
let set =new Set([value])
```

## .add(value)

## .delete(value)

## .has(value)、

## .clear()

## .size

## 应用
数组去重
```
        let arr = [1,2,2,3,3,3,4,5,6];
        let arr1 = arr;
        arr = [];// 清空arr
        let set = new Set(arr1); // 使用set方法去重
        for(let i of set){
            // for of 遍历
            arr.push(i);
        }
        console.log(arr);
```

# Map容器

Map容器：无序的`不重复`的多个key-value集合体
```
        let map = new Map([[key,value]])

        let map = new Map([['name','tom'],['age',18]]);
        console.log(map);
        // Map(2) {"name" => "tom", "age" => 18}
```

## set(key, value)

## get(key)

## delete(key)

## has(key)

## clear()

## size

# ES7
2016发布

## **指数运算符

console.log(3 ** 3);// 27

## Array.prototype.includes(value)
判断数组中是否含有某个元素
```
        let arr111 = [1,2,3,'abc'];
        console.log(arr111.includes('a'));// false
```









