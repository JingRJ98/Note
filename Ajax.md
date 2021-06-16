# 传统网站做的不好的地方
+ 网速慢的情况下，加载缓慢，用户只能等待

+ 表单提交后，如果填写的内容有一项不合格，用户只能重新填写所有的内容

+ 页面跳转，重新加载页面，造成资源浪费，增加用户等待的时间

# Ajax
是浏览器提供的一套方法，可以实现页面`无刷新`更新数据的情况下，向服务端`发送HTTP请求并返回结果`，提高用户浏览网站应用的体验

## 优点
无刷新页面与服务器进行通信


允许根据用户事件部分来更新部分页面内容


## 缺点
没有浏览历史，无法回退

存在跨域问题

SEO不友好
搜索引擎优化 

## 应用场景
+ 页面上拉加载
+ 列表数据无刷新分页
+ 表单项离开焦点数据验证
+ 搜索框下拉文字提示

# 运行环境
需要借助Node开启网站服务器

# XML可扩展的标记语言
被设计用来传输和存储数据

XML中没有预定义的标签，全部是自定义标签

# 例子(GET请求)
点击按钮发送请求
将返回的结果呈现在一个div里面

*配置服务器*
端口号8000`127.0.0.1:8000/server`
```js
// 1、引入express框架
const express = require('express');

// 2、创建应用app
const app = express();

// 3、创建路由规则
app.get('/server',(request,response) => {
    // 设置响应头  设置允许跨域
    response.setHeader('Access-Control-Allow-Origin','*');
    // 设置响应
    response.send(':) 这是我的服务器');

});


// 4、监听端口
app.listen(8000,() =>{
    console.log('服务器启动啦~~');
});
```


*写网页*
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ajax GET 请求</title>
    <style>
        #result{
            width: 200px;
            height: 100px;
            border: solid 1px red;
        }
    </style>
</head>
<body>
    <!-- 
        点按钮发请求
        将响应的内容在#result这个div中呈现
    -->
    <button>点击发送请求</button>
    <div id="result"></div>

    <script>
        // 获取btn
        const btn = document.getElementsByTagName('button')[0];
        // 获取div
        const res = document.getElementById('result');
        // 绑定一个事件
        btn.onclick = function(){
            // 测试交互
            // console.log('test');

            // 1、创建对象
            const xhr = new XMLHttpRequest();
            // 2、初始化，设置请求方法和url
            xhr.open('GET','http://127.0.0.1:8000/server');
            // 3、发送
            xhr.send();
            // 4、事件绑定，处理服务端返回的结果
            // on当什么时候
            // readystate 是xhr对象中的属性 0 1 2 3 4
            xhr.onreadystatechange = function(){
                if(xhr.readyState === 4){
                    // 服务端返回了所有的结果
                    if(xhr.status >= 200 && xhr.status < 300){
                        //返回成功 2xx
                        // 处理结果 行 头 空行 体
                        console.log(xhr.status);// 状态码
                        console.log(xhr.statusText);// 状态字符串
                        console.log(xhr.getAllResponseHeaders());// 所有响应头
                        console.log(xhr.response);// 响应体

                        // 把响应体在div中显示
                        res.innerHTML = xhr.response;
                    }
                }
            }
        }
    </script>
</body>
 </html>
```


实现不刷新页面向服务器发送请求，获取服务器的响应内容





## 设置ajax URL参数
在端口号/server后面加上`?a=100&b=200`

在查询字符串中显示a = 100   b = 200


# POST请求
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>POST</title>
    <style>
        #result {
            width: 200px;
            height: 100px;
            border: solid 1px red;
        }
    </style>
</head>

<body>
    <div id="result"></div>
    <script>
        // 获取元素对象
        const res = document.getElementById('result');
        // 绑定事件
        res.addEventListener('click', function () {
            // 1、创建对象
            const xhr = new XMLHttpRequest();
            // 2、初始化，设置请求类型（POST）与URL
            xhr.open('POST', 'http://127.0.0.1:8000/server?jrj=666');
            // 3、发送(可以设置参数为请求负载)
            xhr.send('a=678&b=200');
            // 4、事件绑定
            xhr.onreadystatechange = function () {
                if(xhr.readyState === 4){
                    // 判断readystate状态，有0 1 2 3 4 五种
                    // 4表示响应已经全部发送过来
                    if(xhr.status >= 200 && xhr.status < 300){
                        // 判断状态码 2xx表示成功
                        res.innerHTML = xhr.response
                    }
                }
            }
        })
    </script>
</body>

</html>
```


# 设置请求头
请求头必须在open之后send之前
`xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded')`

可以自定义请求头
例如`xhr.setRequestHeader('namehahaha','jrj')`
但是浏览器会报错，因为自定义的请求头触发了安全机制
可以在配置服务器中创建路由规则里面添加
`response.setHeader('Access-Control-Allow-Headers','*');`
同时把路由规则的请求改成`all`
app.all()



# 服务端响应json数据
设置响应的时候需要转化为字符串形式
```js
// 3、创建路由规则
app.all('/json-server',(request,response) => {
    // 设置响应头  设置允许跨域
    response.setHeader('Access-Control-Allow-Origin','*');
    // 设置一个数据
    const data = {
        name:'isaac',
        age:22
    }
    // 因为响应必需是一个字符串
    // 所以必须对data进行转换
    let str = JSON.stringify(data);
    // 设置响应
    response.send(str);

});
```

然后在客户端手动对数据进行转化
手动`let data = JSON.parse(xhr.response);`
```js
            // 4、绑定函数处理响应
            xhr.onreadystatechange = function(){
                if(xhr.readyState === 4){
                    // 判断状态4表示响应全部发送完毕
                    if(xhr.status >= 200 && xhr.status < 300){
                        // 判断状态码 2xx表示成功
                        let data = JSON.parse(xhr.response);
                        res.innerHTML = data.name;
                        console.log(data);
                    }
                }
            }
```

也可以使用自动转换格式
`xhr.responseType = 'json'`可以将响应内容直接转换成json格式


# IE缓存
IE浏览器会对Ajax请求的响应结果进行缓存
下一次再次请求的时候，IE浏览器上使用的是本地缓存而非想服务器请求的响应

## 解决
设置请求类型和URL的时候
`xhr.open('GET','http://127.0.0.1:8000/ie?t'+Date.now());`
由于给URL添加了唯一的时间戳
IE浏览器会认为不同的点击发送的不同的请求
从而不断的向服务器发送请求而非使用IE本地缓存



# 请求超时与网络异常处理

在响应中设置一个延时函数
```js
    setTimeout(() => {
        // 设置响应
        response.send(':)这是延时响应');
    }, 3000)
```

客户端可以设置超时
```js
            // 超时设置
            // 两秒钟之内还没有结果就取消请求
            xhr.timeout = 2000;  
```
甚至可以设置一个回调函数来处理超时的结果（联网但是收不到响应的时候）
```js
            // 超时回调,处理超时结果
            xhr.ontimeout = () => {
                alert('你的网络有点异常，请稍后重试TT');
            }
```

甚至还可以设置网络异常的回调(没联网的情况下)
```js
            // 网络异常的回调
            xhr.onerror = () => {
                alert('你没联网~')
            }
```


# 取消请求
对创建的xhr对象使用abort()方法可以取消发送的请求

# 重复发送请求的问题
设置变量表示是否正在发送请求
默认false不发送
从创建对象开始修改为true,表示正在发送请求

当接收状态为4时请求停止

在发送请求的时候判断是否正在发送请求
若是
则使用abort()方法取消请求并发起新的请求


# fetch函数发送ajax请求
fetch接收两个参数
第一个参数是服务器URL
第二个参数是一个对象
对象中包含请求方法、请求头和请求体信息


# 同源
是一种安全策略

同源：协议、域名、端口号必须完全相同

违背同源政策就是跨域

单台服务器的性能是有上限的，所以需要多台服务器协同工作


Ajax发送请求的时候是默认满足同源策略的


# 解决跨域
## jsonp
+ jsonp是什么？
  非官方的跨域方案，只支持get请求
+ jsonp是如何工作的
页面中的一些标签天生具有跨域功能 比如 script img link iframe
例子
当选择使用file协议和http协议打开时app.js
<script src="./js/app.js"></script>
没有问题

<!-- <script src="./js/app.js"></script> -->
<script src="http://127.0.0.1:5500/%E8%B7%A8%E5%9F%9F/jsonp/js/app.js"></script>
将app.js的http协议URL在script标签中用本地file协议打开
`open in browser`
发现自动实现跨域


+ jsonp的使用
  1、动态创建script标签
    `var script = document.createElement('script');`
  2、设置script的src,设置回调函数
  3、将script标签插入到文档中

## CORS
cross origin resource sharing
跨域资源共享
是官方的跨域解决方案
不需要再客户端进行操作。。完全在服务端操作

支持get和post请求

跨域资源共享标准新增了一组HTTP首部字段，允许服务器声明那些源站通过浏览器有权限访问那些资源

+ CORS怎么工作的
  CORS通过设置特定的响应头告诉浏览器，该请求允许跨域，浏览器收到响应之后就会对响应放行
+ 使用
  主要是在服务器端设置响应头
  `response.setHeader("Access-Control-Allow-Origin","*")`
