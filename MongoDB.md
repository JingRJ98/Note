# 数据库分类
数据库主要分为两种
关系型数据库（RDBMS）
MySQL SQL Server……
关系型数据库中全是表


非关系型数据库（Not Only SQL）
MongoDB redis


# MongoDB
为了快速开发web应用而开发设计的数据库系统

设计目标是极简、，灵活、作为web应用栈的一部分

数据模型是面向文档的，所谓文档是一种类似JSON结构，简单理解MongoDB这个数据库中存的是各种各样的JSON（BSON）



# 三个概念
## 数据库（database）
仓库，中可以存放集合
仓库不需要手动创建

## 集合（collection）
集合类似数组，在集合中可以存放文档
集合也不需要手动创建

## 文档（document）
文档是数据库中的最小单位，我们存储和操作的都是文档

## 1、安装MongoDB
## 2、配置环境变量
将MongoDB bin 文件路径添加到计算机
G:\mongodb\bin


## 3、创建文件
打开cmd窗口输入mongod启动mongo 启动mongo服务器
mongod --dbpath 路径 --端口号

再打开一个mongo连接


# 数据库
服务器
    + 保存数据

客户端
    + 操作数据


# 基本指令
show databases
show dbs
展示当前所有的数据库


use 数据库名
进入数据库

db
显示当前在哪一个数据库中

show collections
显示数据库中所有的集合

# CRUD

## 创建
向集合中插入文件
db.集合.insert();
db.集合.insertOne();
db.集合.insertMany();
插入多个文件传入数组


当我们向文件中插入文档时
没有指定_id属性，数据库会自动为文档设置_id
作为文档的唯一标识

## 查询
db.集合.find()
可以传入一个属性作为条件参数
find()可以接收一个对象作为条件参数 返回所有符合条件的文档数组


db.集合.findOne()
查询满足条件的第一个文档对象


db.集合.find({})
查询所有文档


db.集合.find({}).count()
查询所有满足条件参数的文档的数量

MongoDB支持通过内嵌文档的属性进行查询 查询内嵌文档时，此时属性名必须使用引号 
比如 {name:'Tom',age:18,hobbies:{movie:['abc', 'bbc']}} 
db.collection.find({'hobbies.movie':'abc'})

$eq, $gt, $gte, $lt, $lte, $or num大于5000的文档 db.nums.find({num:{$gt:5000}})

num大于500小于600的文档 db.nums.find({num:{$gt:500, $lt:600}})

limit()限制查询上限 查询集合中的前10条文档 db.collection.find().limit(10)

skip()跳过查询 查询集合中的第11~20条文档 db.collection.find().skip(10).limit(10)

查询集合中的num小于10和num大于20的文档 db.collection.find({$or:[{num:{$lt:10}},{num:{$gt:20}}]})

## 修改
db.集合名.update(查询条件,新对象)
注意：update会默认使用新对象替换旧对象
如果需要修改制定的属性，需要使用修改操作符
`$set`
```js
db.stus.update(
    {name:"唐僧"},
    {
        $set:{
            age:50,
            address:"长安"
        }
    }
)
```
`$unset`可以删除指定的属性


db.stus.updateMany()
修改多个文档


db.stus.updateOne()
修改第一个指定要求的文档



## 删除文档
db.stus.remove({})
db.stus.delete({})
db.stus.deleteOne({})
db.stus.deleteMany({})
传入条件参数

#### 删除集合
db.stus.drop();

#### 删库跑路
db.dropDatabase();


# 练习
```js
// 1、进入my_test数据库
use my_test
// 自动创建库和集合

// 2、向数据库的user集合中插入文档
db.users.insert({
    username:'jrj'
})

// 3、查询user集合中的文档
db.users.find();

// 4、统计数据库user集合中的文档数量
db.users.find({}).count();


// 5、查询数据库user集合中username为jrj的文档
db.users.find({
    username:"jrj"
})



// 6、向user集合中username为jrj的文档添加属性为address，属性值为长安的
db.users.updateOne(
    {username:"jrj"},
    {$set:{address:"长安"}}
)



// 7、使用username为TT的属性代替 username为jrj的文档
db.users.replaceOne({username:"jrj"},{username:"TT"})



// 8、删除username为jrj文档的address属性
db.user.update({username:"jrj"},{$unset:{address:1}})



// 9、向nums中插入两万条数据
let ans = [];
for(let i = 0;i < 20000;i++){
    ans.push({num:i})
}
db.nums.insert(ans)
// 尽量少的使用数据库语句


// 10、查询nums中num大于500的文档
db.nums.find({num:{$gt:500}})
// 小于用$lt

// 11、查询nums中num大于500且小于1000的文档
db.nums.find({num:{$gt:500,$lt:1000}})


// 12、查询nums前十条文档
db.nums.find({num:{$lte:10}})
db.nums.find().limit(10)// 表示上限10条文档


// 13、查询11-20条文档
db.nums.find().skip(10).limit(10)
// 表示上限10
// skip表示跳过指定条数文档

```


# MongoDB 文档之间的关系
一对一（one to one）
很少
在MOngoDB中可以通过内嵌文档的形式体现出一对一的关系


一对多（one to many）/多对一（many to one）
最多的
在MongoDB中也可以通过内嵌文档的形式来实现一对多的关系

多对多（many to many）


# 向集合中导入文档
在MongoDB中使用图形化操作，
选中一个集合
点击`ADD DATA`

选择文件，格式`JSON or CSV`




# Mongoose
是一个对象对象文档模型库，它对Node原生的MongoDB模块进行了进一步的优化封装，并提供更多分功能


## 优点
为文档创建一个schema

对模型中的对象/文档进行验证

数据可以通过类型转换为对象

# 使用过程
1、下载安装
npm i mongoose --save

2、引入mongoose
var mongoose = require("mongoose")


3、连接数据库
`mongoose.connect('mongodb://数据库的IP地址：端口号/数据库名',{useMongoClient:true})`
如果端口号是默认的27017，可以不写

监听数据库的链接状态
在Mongoose对象中，有一个属性是connection，该对象表示的就是数据库链接
通过监视该对象的状态，可以用来监听数据库的连接与断开


mongoose.connection.once{"open",function(){}}回调函数是成功连接的事件
mongoose.connection.once{"close",function(){}}连接失败的事件


## 连接
```js
// 引入mongoose
const mongoose = require('mongoose')

// 连接数据库(一般只需连接一次不再断开)
mongoose.connect('mongodb://localhost:27017/test')

// 监听是否连接成功
mongoose.connection.once('open', () => {
    console.log('数据库连接成功')
})
```

## 创建schema对象
```js
// 创建Schema(模式对象)
const Schema = mongoose.Schema
const studentSchema = new Schema({
    name: String,
    number: Number,
    age: Number,
    gender: {
        type: String,
        default: 'male'
    },
    address: String
})
```

## 创建model对象
model代表的是数据库中的集合，通过model才能对数据库进行操作


```js
// 通过Schema创建Model，相当于数据库中的collection
// mongoose.model(modelName, schema)

const StudentsModel = mongoose.model('students', studentSchema)
```

## Model的方法
### c
Model.create(doc(s),[callback])
dos(s)代表一个或者多个文档
然后是操作完成的回调函数


### r
find() find(conditions, [projection], [options], callback) 

findById(id, [projection], [options], callback) 

findOne(conditions, [projection], [options], callback) 

conditions 查询条件 

projection 投影 例：{name: 1, _id: 0}或直接字符串'name -_id' 

options 查询选项(skip, limit) 例：{limit: 10} 

callback 查询结果通过callback返回，find返回数组，findOne,findById返回具体的文档 
注意：通过callback返回的对象就是Document文档对象，文档对象是Model的实例

例如： StudentsModel.find({age: 18}, {name: 1, _id: 0}, {limit: 1}, (err, docs) => { console.log(docs) })


document是model对象的实例，可以使用instanceOf检验


### u
update() 
update(conditions, doc, [options], callback) 默认一个 options为{multi: true}修改多个 

updateOne(conditions, doc, [options], callback) 

updateMany(conditions, doc, [options], callback)

conditions查询条件

doc修改后的对象

options配置参数

例：StudentsModel.update({age: 18}, {$set:{age:20}},err => {if(!err){console.log('修改成功')}})

### d

remove() 

remove(conditions, [callback]) 

deleteOne(conditions, [callback]) 

deleteMany(conditions, [callback])


### 统计文档数量
count() count(conditions, [callback]) callback参数为err,count


## Document对象
document是model的实例

通过model查询到的都是document
