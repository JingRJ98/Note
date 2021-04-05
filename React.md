# React
原生js直接操作DOM，效率低  
浏览器进行大量的重绘重拍   
原生js没有组件化的编码方案 代码复用率低   

# React的特点

1.声明式编码   
2.组件化编码   
3.支持客户端，服务端渲染   
4.高效   
    原因：  
    1.不直接操作DOM，虚拟DOM  
    2.DOM diff算法 最小化页面重绘   
5.单向数据流   

# React JSX
```
<body>
	<!-- 准备好一个“容器” -->
	<div id="test"></div>

	<!-- 引入react核心库 -->
	<script type="text/javascript" src="../js/react.development.js"></script>
	<!-- 引入react-dom，用于支持react操作DOM -->
	<script type="text/javascript" src="../js/react-dom.development.js"></script>
	<!-- 引入babel，用于将jsx转为js -->
	<script type="text/javascript" src="../js/babel.min.js"></script>

	<script type="text/babel" > /* 此处一定要写babel 不写babel 默认写的jsx */
		//1.创建虚拟DOM
		const VDOM = <h1>Hello,React</h1> /* 此处一定不要写引号，因为不是字符串 */
		//2.渲染虚拟DOM到页面
		// render渲染的意思
		// 
		ReactDOM.render(VDOM,document.getElementById('test'))
	</script>
</body>
```

## 虚拟DOM
两种创建方式   
1、
```
		//1.创建虚拟DOM
		// (标签名，标签属性，标签内容)
    // 每一个标签要想使用必须使用React.creatElement(1,2,3)创建
		const VDOM = React.createElement('h1',{id: 'title'},React.createElement('span',{},'hello'))
		//2.渲染虚拟DOM到页面
		ReactDOM.render(VDOM,document.getElementById('test'))
``` 
2、
```
		//1.创建虚拟DOM
		const VDOM = (  /* 此处一定不要写引号，因为不是字符串 */
			<h1 id="title">
				<span>Hello,React</span>
			</h1>
		)
		//2.渲染虚拟DOM到页面
		ReactDOM.render(VDOM,document.getElementById('test'))
```
React提供了一些API来创建一种“特别”的一般js对象   
`const vDOM = React.createElement('h1', {id:'myTitle'}, 'hello world')`   
关于虚拟DOM：  
					1.本质是Object类型的对象（一般对象）  
					2.虚拟DOM比较“轻”，真实DOM比较“重”，因为虚拟DOM是React内部在用，无需真实DOM上那么多的属性。  
					3.虚拟DOM最终会被React转化为真实DOM，呈现在页面上。  

```
	<script type="text/babel" > /* 此处一定要写babel */
		//1.创建虚拟DOM
		const VDOM = (  /* 此处一定不要写引号，因为不是字符串 */
			<h1 id="title">
				<span>Hello,React</span>
			</h1>
		)
		//2.渲染虚拟DOM到页面
		ReactDOM.render(VDOM,document.getElementById('test'))

		const TDOM = document.getElementById('demo')
		console.log('虚拟DOM',VDOM);// Object
		console.log('真实DOM',TDOM);
		// debugger;
		// console.log(typeof VDOM);
		// console.log(VDOM instanceof Object);判断是不是对象
		/* 
				关于虚拟DOM：
					1.本质是Object类型的对象（一般对象）
					2.虚拟DOM比较“轻”，真实DOM比较“重”，因为虚拟DOM是React内部在用，无需真实DOM上那么多的属性。
					3.虚拟DOM最终会被React转化为真实DOM，呈现在页面上。
		 */
	</script>
```

# JSX
```

	<script type="text/babel" >
		const myId = 'aTgUiGu'
		const myData = 'HeLlo,rEaCt'

		//1.创建虚拟DOM
		const VDOM = (
			<div>
				<h2 className="title" id={myId.toLowerCase()}>
					<span style={{color:'white',fontSize:'29px'}}>{myData.toLowerCase()}</span>
				</h2>
				<h2 className="title" id={myId.toUpperCase()}>
					<span style={{color:'white',fontSize:'29px'}}>{myData.toLowerCase()}</span>
				</h2>
				<input type="text"/>
				<good>123333</good>
			</div>
		)
		//2.渲染虚拟DOM到页面
		ReactDOM.render(VDOM,document.getElementById('test'))

		/* 
				jsx语法规则：
						1.定义虚拟DOM时，不要写引号。
						2.标签中混入JS表达式时要用{}。
						3.样式的类名指定不要用class，要用className。
						4.内联样式，要用style={{key:value}}的形式去写。
							第一个引号表示js表达，里面的{}表示对象，写键值对
						5.只有一个根标签
						6.标签必须闭合（或者加<……/>自闭合）
						7.标签首字母
								(1).若小写字母开头，则将该标签转为html中同名元素，若html中无该标签对应的同名元素，则报错。
								(2).若大写字母开头，react就去渲染对应的组件，若组件没有定义，则报错。

		 */
	</script>
```
1.全称 JavaScript XML   
2..React定义的一种类似于XML的JS扩展语法：XML + JS   
3.作用：用来创建React虚拟DOM对象   
`const vDOM = <h1>hello world</h1>`  
    注意：不是字符串也并不是HTML/XML标签  
    它最终产生的就是一个JS对象   
4.标签名任意   
5.标签属性任意   
6.基本语法规则    
    遇到 < 开头的代码，以标签语法解析：HTML同名标签转换为HTML同名元素，其他标签需要特别解析   
    遇到 { 开头代码，以JS语法解析：标签中的JS代码必须用{}包含   
7.babel.js作用   
    浏览器不能直接解析JSX代码，需要babel转译为纯JS代码   
    只要用了JSX，都要加上type='text/babel'，声明需要babel来处理  
    
## 表达式和代码
一个表达式可以产生一个值，可以放在需要的地方  
```
						(1). a
						(2). a+b
						(3). demo(1)
						(4). arr.map() 数组方法
						(5). function test () {}
```
语句（代码）
```
						(1).if(){}
						(2).for(){}
						(3).switch(){case:xxxx}
```
### jsx练习
```
<script type="text/babel" >
	// 模拟数据
	// obj不允许作为react的节点
	var data = ['j','r','j'];
	// 创建虚拟DOM 

		const VDOM = (
			<div>
				<h1>前端js框架</h1>	
				<ul>
   // 动态读取数据，js表达式要写在{}中
	 // 同时使用变量需要放在{}中
					{
						data.map((item,index) =>{
							return <li key = {index}>{item}</li>
						})
					}
				</ul>
			</div>
		)

	// 渲染虚拟DOM
			ReactDOM.render(VDOM,document.getElementById('test'))
	</script>
```

# React面向组件编程
## 什么是模块
一般一个js文件就是一个模块  
作用：复用js 简化js  

## 什么是组件

用来实现特定局部功能效果的代码集合（HTML/CSS/JS/video……）

## 组件的定义与使用
### 函数式组件    
			执行了ReactDOM.render(<MyComponent/>.......之后，发生了什么？  
					1.React解析组件标签（标签首字母大写），找到了MyComponent组件。  
					2.发现组件是使用函数定义的，随后调用该函数，将返回的虚拟DOM转为真实DOM，随后呈现在页面中。   

babel开启严格模式后 禁止自定义函数指向window
```
	<script type="text/babel">
		//1.创建函数式组件
		// 因为标签的首字母小写时会寻找同名的标签 大写时则渲染响应的组件
		// 所以必须大写
		function MyComponent(){
			console.log(this); //此处的this是undefined，因为babel编译后开启了严格模式
			return <h2>我是用函数定义的组件(适用于【简单组件】的定义)</h2>
		}
		//2.渲染组件到页面
		ReactDOM.render(<MyComponent/>,document.getElementById('test'))
	</script>
```
### 类式组件  

```
	<script type="text/babel">
		//1.创建类式组件
		// React.Component是React内置类
		class MyComponent extends React.Component {
			render(){
				//render是放在哪里的？—— MyComponent的原型对象上，供实例使用。
				//render中的this是谁？—— MyComponent的实例对象 <=> MyComponent组件实例对象。
				console.log('render中的this:',this);
				return <h2>我是用类定义的组件(适用于【复杂组件】的定义)</h2>
			}
		}
		//2.渲染组件到页面
		// 组件标签需要闭合
		ReactDOM.render(<MyComponent/>,document.getElementById('test'))  
		/* 
			执行了ReactDOM.render(<MyComponent/>.......之后，发生了什么？
					1.React解析组件标签，找到了MyComponent组件。
					2.发现组件是使用类定义的，随后new出来该类的实例，并通过该实例调用到原型上的render方法。
					3.将render返回的虚拟DOM转为真实DOM，随后呈现在页面中。
		*/
	</script>
```

----------------------------------

# 类的复习
			总结：  
				1.类中的构造器不是必须要写的，要对实例进行一些初始化的操作，如添加指定属性时才写。   
				2.如果A类继承了B类，且A类中写了构造器，那么A类构造器中的super是必须要调用的。   
				3.类中所定义的方法，都放在了类的原型对象上，供实例去使用。    
```
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>1_类的基本知识</title>
</head>
<body>
	<script type="text/javascript" >
		//创建一个Person类
		class Person {
			//构造器方法
			constructor(name,age){
				//构造器中的this是谁？—— 类的实例对象
				this.name = name
				this.age = age
			}
			//一般方法
			speak(){
				//speak方法放在了哪里？——类的原型对象上，供实例使用
				//通过Person实例调用speak时，speak中的this就是Person实例
				console.log(`我叫${this.name}，我年龄是${this.age}`);
			}
		}

		// 创建一个Student类，继承于Person类
		// 继承 extends
		class Student extends Person {
			constructor(name,age,grade){
				// 必须先使用super()调用父类中已经定义的构造器属性
				super(name,age)
				this.grade = grade
				this.school = '尚硅谷'
			}
			// 重写从父类继承过来的方法
			speak(){
				console.log(`我叫${this.name}，我年龄是${this.age},我读的是${this.grade}年级`);
				this.study()
			}
			study(){
				//study方法放在了哪里？——类的原型对象上，供实例使用
				//通过Student实例调用study时，study中的this就是Student实例
				console.log('我很努力的学习');
			}
		}
		
		class Car {
			constructor(name,price){
				this.name = name
				this.price = price
				// this.wheel = 4
			}
			//类中可以直接写赋值语句,如下代码的含义是：给Car的实例对象添加一个属性，名为a，值为1
			a = 1
			wheel = 4
			static demo = 100
		}
		const c1 = new Car('奔驰c63',199)
		console.log(c1);
		console.log(Car.demo);
	</script>
</body>
</html>
```

----------------------------

## 注意
 
1.组件名必须首字母大写    
2.虚拟DOM元素只能有一个根元素    
3.虚拟DOM元素必须有结束标签  

## render()渲染组件标签的基本流程

1.React解析组件标签，找到了MyComponent组件。   
2.发现组件是使用类定义的，随后new出来该类的实例，并通过该实例调用到原型上的render方法。  
3.将render返回的虚拟DOM转为真实DOM，随后呈现在页面中。  

---------------------------------------

# 原生js事件绑定的复习
三种绑定方式  

第一种  
DOM2级  
Element.addEventListener(('click', () => {}, false))  

参数：

1.事件的字符串，不要加on

2.回调函数，当事件触发时该函数会被调用

3.是否在捕获阶段触发事件，需要一个布尔值，默认都传false

优点：可以为一个元素的一个事件绑定多个回调函数，多个回调函数按绑定顺序执行

缺点：兼容性不好，不支持IE8及以下

解绑：removeEventListener，三个参数必须全部一致才能解绑  


第二种  
DOM0级

Element.onclick = () => {}

优点：兼容性好

缺点：只能为一个元素的一个事件绑定一个监听函数，如果绑定多个，则后绑会覆盖先绑

解绑：赋值null
```
		<button id="btn1">按钮1</button>
		<button id="btn2">按钮2</button>
		<button onclick="demo()">按钮3</button>

		<script type="text/javascript" >
			const btn1 = document.getElementById('btn1')
			btn1.addEventListener('click',()=>{
				alert('按钮1被点击了')
			})

			const btn2 = document.getElementById('btn2')
			btn2.onclick = ()=>{
				alert('按钮2被点击了')
			}

			function demo(){
				alert('按钮3被点击了')
			}

		</script>
```

---------------------------------------

# 类的this复习
方法也是特殊的属性  
先找到属性，赋值给变量的时候，是沿着原型链找到的类的方法，并不是通过实例调用的，而是相当于直接调用函数（方法）   
非严格模式下指向window    
严格模式下禁止指向window，所以是undefined   
```
			class Person {
				// 构造器
				constructor(name,age){
					this.name = name
					this.age = age
				}
				// 方法
				study(){
					//study方法放在了哪里？——类的原型对象上，供实例使用
					//通过Person实例调用study时，study中的this就是Person实例
					console.log(this);
				}
			}

			const p1 = new Person('tom',18)
			p1.study() //通过实例调用study方法
			const x = p1.study
			x()
			// 这里是先赋值，直接调用，非严格模式下指向window，严格模式下就是undefined
			// 类里面默认已经开启严格模式了
			// 所以undefined
```

## 组件实例对象的三大属性

### state（状态）

state是组件对象最重要的属性，值是对象（可以包含多个数据）

组件被称为状态机，通过更新组件的state来更新对应的页面显示（重新渲染组件）

```
	<script type="text/babel">
		//1.创建组件
		class Weather extends React.Component{
			
			//构造器调用几次？ ———— 1次
			constructor(props){
				console.log('constructor');
				// 继承里面必须调用super()方法
				super(props)
				//初始化状态
				this.state = {isHot:false,wind:'微风'}
				//解决changeWeather中this指向问题（原来是undefined）

				// ↓这个changeWeather指的是render返回里面点击事件绑定的
				this.changeWeather = this.changeWeather.bind(this)
				//                      ↑这个changeWether是原来类里面定义的方法
				// 						通过原型链查找到，通过bind修改this，返回新函数
			}

			//render调用几次？ ———— 1+n次 1是初始化的那次 n是状态更新的次数
			render(){
				console.log('render');
				//读取状态
				const {isHot,wind} = this.state
				// react绑定点击事件时使用的是onClick，C大写！！
				// onClick = {}使用原生js表达，并且不能加()表示立即执行函数并赋值
				return <h1 onClick={this.changeWeather}>今天天气很{isHot ? '炎热' : '凉爽'}，{wind}</h1>
			}

			//changeWeather调用几次？ ———— 点几次调几次
			changeWeather(){
				//changeWeather放在哪里？ ———— Weather的原型对象上，供实例使用
				//由于changeWeather是作为onClick的回调，所以不是通过实例调用的，是直接调用
				//类中的方法默认开启了局部的严格模式，所以changeWeather中的this为undefined
				
				console.log('changeWeather');
				//获取原来的isHot值
				const isHot = this.state.isHot
				//严重注意：状态必须通过setState进行更新,且更新是一种合并，不是替换。
				this.setState({isHot:!isHot,wind: '狂风！'})
				console.log(this);

				//严重注意：状态(state)不可直接更改，下面这行就是直接更改！！！
				//this.state.isHot = !isHot //这是错误的写法
				// 单纯数据更改react不认可
			}
		}
		//2.渲染组件到页面
		ReactDOM.render(<Weather/>,document.getElementById('test'))
				
	</script>
```
  
state的简化写法  
```
		//1.创建组件
		class Weather extends React.Component{
			//初始化状态 可以直接写在构造器外面
			state = {isHot:false,wind:'微风'}

			render(){
				const {isHot,wind} = this.state
				return <h1 onClick={this.changeWeather}>今天天气很{isHot ? '炎热' : '凉爽'}，{wind}</h1>
			}

			//自定义方法————要用赋值语句的形式+箭头函数
			changeWeather = ()=>{
				const isHot = this.state.isHot
				this.setState({isHot:!isHot})
			}
		}
		//2.渲染组件到页面
		ReactDOM.render(<Weather/>,document.getElementById('test'))
			
```
类中可以直接写赋值语句，不需要事先定义   
类中自定义方法使用箭头函数，箭头函数没有自己的this，箭头函数里面的this使用的是外部的this，外部类中的this指的是实例对象 
react渲染组件的时候自动new了实例对象


### props（标签属性）

每个组件对象都会有props(properties)属性  
组件标签的所有属性都保存在props中  

通过标签属性从组件外向组件内传递变化的数据  
注意：所有 React 组件都必须像纯函数一样保护它们的 props 不被更改。
基本使用

```		// 创建组件
		class Person extends React.Component{
	
			render(){
				const {name,age,sex } = this.props
				console.log(this);
				return(
					<ul>
						<li>姓名：{name}</li>	
						<li>性别：{age}</li>	
						<li>年纪：{sex}</li>	
						
					</ul>
				)
			}
		}
		// 渲染组件
		ReactDOM.render(<Person name = 'tom' age = '18' sex = '男'/>,document.getElementById('test1'))
		
		// 批量传输数据时
		const p = {name:'老刘',age:18,sex:'女'}
		// ReactDOM.render(<Person name={p.name} age={p.age} sex={p.sex}/>,document.getElementById('test3'))
		ReactDOM.render(<Person {...p}/>,document.getElementById('test3'))
```



------------------------------------

# 三点运算符复习
对数组
```
			let arr1 = [1,3,5,7,9]
			let arr2 = [2,4,6,8,10]
			console.log(...arr1); //展开一个数组
			let arr3 = [...arr1,...arr2]//连接数组
```
对函数
```
			// ...用于函数传参
			// 求和函数
			function sum(...nums){
				return nums.reduce((preValue,currentValue) => {
					return preValue + currentValue;
				})
			}
			console.log('AAAA'+sum(...arr1));// 25
```

三点运算符不能应用到对象  
但是可以使用{}/[]中的三点运算符实现第一层‘深拷贝’ 
```

			let person = {
				name: 'tom',
				age: 18
			}
			// 浅拷贝
			let person2 = person;
			// 深拷贝
			let person3 = {...person}
			person.name = 'jrj'
			console.log(person2);
			console.log(person3);


			let arr666 = [1,2,3,[1,2,444],{name: '孙悟空'}]
			// 浅拷贝
			let arr777 = arr666;
			// 深拷贝
			// let arr888 = {...arr666}
			let arr888 = [...arr666]
			arr666[3] = 111
			console.log('浅拷贝'+arr777[3]);
			console.log(arr888[3]);
		
```
第二层失效
```
			let arr666 = [1,2,3,[1,2,[666]],{name: '孙悟空'}]
			// 浅拷贝
			let arr777 = arr666;
			// 深拷贝
			// let arr888 = {...arr666}
			let arr888 = [...arr666]
			arr666[3][2] = 111
			console.log('浅拷贝'+arr777[3][2]);
			// 111
			console.log(arr888[3][2]);
			// 111
```

还可以使用三点运算符对对象进行合并

----------------------------------
#### 对props进行限制
```
		//对标签属性进行类型、必要性的限制
		Person.propTypes = {
			name:PropTypes.string.isRequired, //限制name必传，且为字符串
			sex:PropTypes.string,//限制sex为字符串
			age:PropTypes.number,//限制age为数值
			speak:PropTypes.func,//限制speak为函数 必须是func，因为function是关键字
		}
```
设置数据的默认值
```
		//指定默认标签属性值
		Person.defaultProps = {
			sex:'男',//sex默认值为男
			age:18 //age默认值为18
		}
```
### state与props的区别

state：组件自身`内部`可变化的数据   
props：从组件`外部`向组件内部传递数据，组件内部只读不修改

### refs（元素标识）

组件内的标签都可以定义ref属性来标识自己

`<input type='text' ref=(input => this.msginput = input)` 
回调函数在组件初始化渲染完成或卸载时自动调用
在组件中可以通过this.msginput来得到对应的真实DOM元素
作用：通过ref获取组件内容特定标签对象，进行读取其相关数据

```
<body>
    <div id="test"></div>
    <script src="../js/react.development.js"></script>
    <script src="../js/react-dom.development.js"></script>
    <script src="../js/babel.min.js"></script>
    <script type="text/babel">
        // 定义组件
        class MyComponent extends React.Component {
            constructor(props) {
                super(props)
                // 自定义函数this强制绑定为组件对象
                this.handleClick = this.handleClick.bind(this)
            }
            // 自定义方法中的this默认为null
            handleClick() {
                alert(this.msgInput.value)
            }
            handleBlur(e) {
                alert(e.target.value)
            }
            render() {
                return (
                    <div>
                        <input type="text" ref={input => this.msgInput = input}/> 
                        <button onClick={this.handleClick}>提示已输入内容</button> 
                        <input type="text" placeholder='失去焦点提示内容' onBlur={this.handleBlur}/>  
                    </div>
                )
            }
        }
        ReactDOM.render(<MyComponent/>, document.getElementById('test'))
    </script>
</body>
```

## 组件的组合

### 功能界面的组件化编码流程（无比重要）

1.拆分组件：拆分界面，抽取组件

2.实现静态组件：使用组件实现静态页面效果

3.实现动态组件
    1.动态显示初始化数据
    2.交互功能（从绑定事件监听开始）

问题1：数据保存在哪个组件内？
    看数据是某个组件需要（给它）
    还是某些组件需要（给共同的父组件）

问题2：需要在子组件中改变父组件的状态
    子组件不能直接改变父组件的状态
    状态在哪个组件，更新状态的行为就应该在哪个组件
    解决：父组件定义函数，传递给子组件，子组件调用

```
<body>
  <div id="example"></div>
  <script type="text/javascript" src="../js/react.development.js"></script>
  <script type="text/javascript" src="../js/react-dom.development.js"></script>
  <script type="text/javascript" src="../js/prop-types.js"></script>
  <script type="text/javascript" src="../js/babel.min.js"></script>
  <script type="text/babel">
    /*
    1)拆分组件: 拆分界面,抽取组件
    2)实现静态组件: 使用组件实现静态页面效果
    3)实现动态组件
        ① 动态显示初始化数据
        ② 交互功能(从绑定事件监听开始)
     */
    // 应用组件
    class App extends React.Component {
      constructor (props) {
        super(props)
        // 初始化状态
        this.state = {
          todos: ['吃饭', '睡觉', '打豆豆']
        }
        this.add = this.add.bind(this)
      }
      add (todo) {
        const {todos} = this.state
        todos.unshift(todo)
        //更新状态
        this.setState({todos})
      }
      render () {
        const {todos} = this.state
        return (
          <div>
            <TodoAdd add={this.add} count={todos.length} />
            <TodoList todos={todos} />
          </div>
        )
      }
    }

    // 添加todo组件
    class TodoAdd extends React.Component {
      constructor (props) {
        super(props)
        this.addTodo = this.addTodo.bind(this)
      }
      addTodo () {
        // 读取输入数据
        const text = this.input.value.trim()
        // 查检
        if(!text) {
          return
        }
        // 保存到todos
        this.props.add(text)
        // 清除输入
        this.input.value = ''
      }
      render () {
        return (
          <div>
            <h2>Simple TODO List</h2>
            <input type="text" ref={input => this.input=input}/>
            <button onClick={this.addTodo}>Add #{this.props.count}</button>
          </div>
        )
      }
    }
    TodoAdd.propTypes = {
      add: PropTypes.func.isRequired,
      count: PropTypes.number.isRequired
    }

    // todo列表组件
    class TodoList extends React.Component {
      render () {
        const {todos} = this.props
        return (
          <ul>
            {
              todos.map((todo, index) => <li key={index}>{todo}</li>)
            }
          </ul>
        )
      }
    }
    TodoList.propTypes = {
      todos: PropTypes.array.isRequired
    }

    // 渲染应用组件标签
    ReactDOM.render(<App />, document.getElementById('example'))

  </script>
</body>
```

### 收集表单数据

问题：在React应用中，如何收集表单输入数据

包含表单的组件分类：
1.受控组件：表单输入数据能自动收集成状态
2.非受控组件：需要时才手动读取表单输入框中的数据
```
<div id="example"></div>
<script type="text/javascript" src="../js/react.development.js"></script>
<script type="text/javascript" src="../js/react-dom.development.js"></script>
<script type="text/javascript" src="../js/babel.min.js"></script>
<script type="text/babel">
  class LoginForm extends React.Component {
    constructor(props) {
      super(props)
      this.state = {
        username: ''
      }
      this.handleSubmit = this.handleSubmit.bind(this)
      this.handleChange = this.handleChange.bind(this)
    }

    handleChange(event) {
      this.setState({username: event.target.value})
    }

    handleSubmit(event) {
      alert(`准备提交的用户名为: ${this.state.username}, 密码:${this.pwdInput.value}`)

      // 阻止事件的默认行为: 提交表单
      event.preventDefault()
    }
    render () {

      return (
        <form onSubmit={this.handleSubmit} action="/test">
          <label>
            用户名:
            <input type="text" value={this.state.username} onChange={this.handleChange} />
          </label>&nbsp;
          <label>
            密码:
            <input type="password" ref={(input) => this.pwdInput = input} />
          </label>&nbsp;
          <input type="submit" value="登陆" />
        </form>
      )
    }
  }
  
  ReactDOM.render(<LoginForm />, document.getElementById('example'))
</script>
```

## 组件生命周期

### 理解

1.组件对象从创建到死亡它会经历特定的生命周期阶段
2.React组件对象包含一系列的钩子函数（生命周期回调函数），在生命周期特定时刻回调
3.我们在定义组件时，可以重写特定的生命周期回调函数，做特定的工作

### 生命周期流程图

![](_v_images/20200505214549285_24697.png =454x)

### 生命周期详述

1.组件的三个生命周期状态：
    Mount：挂载，插入真实DOM
    Update：被重新渲染
    Unmount：解除挂载，被移出真实DOM

2.React为每个状态都提供了钩子函数
    componentWillMount()
    componentDidMount()
    componentWillUpdate()
    componentDidUpdate()
    componentWillUnmount()

3.生命周期流程

第一阶段：第一次初始化渲染显示:ReactDOM.render()
    constructor():创建对象初始化state
    componentWillMount():将要挂载回调
    render():虚拟DOM挂载回调
    componentDidMount:已经挂载

第二阶段：.每次更新state:this.setState()
    componentWillUpdate():将要更新回调
    render():更新（重新渲染）
    componentDidUpdate():已经更新回调

第三阶段：ReactDOM.unmountComponentAtNode(containerDom)
    componentWillUnmount():组件解除挂载前回调

### 重要的钩子

1.render():初始化渲染以及更新渲染调用
2.componentDidMount():开启监听，发送Ajax请求
3.componentWillUnmount:做一些收尾工作，如：清除定时器
4.componentWillReceiveProps()

```
<div id="example"></div>

<script type="text/javascript" src="../js/react.development.js"></script>
<script type="text/javascript" src="../js/react-dom.development.js"></script>
<script type="text/javascript" src="../js/babel.min.js"></script>
<script type="text/babel">
  /*
  需求: 自定义组件
    1. 让指定的文本做显示/隐藏的动画
    2. 切换时间为2S
    3. 点击按钮从界面中移除组件界面
   */
  class Fade extends React.Component {

    constructor (props) {
      super(props)
      console.log('constructor(): 创建组件对象')
      this.state = {
        opacity: 1
      }
      this.removeComponent = this.removeComponent.bind(this)
    }

    componentWillMount () {
      console.log('componentWillMount(): 初始化将要挂载')
    }

    componentDidMount () {// 在此方法中启动定时器/绑定监听/发送ajax请求
      console.log('componentDidMount(): 初始化已经挂载')
      // 保存到当前组件对象中
      this.intervalId = setInterval(function () {
        console.log('--------')
        // 得到当前opacity
        let {opacity} = this.state
        // 更新opacity
        opacity -= 0.1
        if(opacity<=0) {
          opacity = 1
        }
        // 更新状态
        this.setState({opacity})
      }.bind(this), 200)
    }

    componentWillUpdate () {
      console.log('componentWillUpdate(): 将要更新')
    }
    componentDidUpdate () {
      console.log('componentDidUpdate(): 已经更新')
    }

    componentWillUnmount () {// 清除定时器/解除监听
      console.log('componentWillUnmount(): 将要被移除')
      clearInterval(this.intervalId)
    }

    removeComponent () {
      ReactDOM.unmountComponentAtNode(document.getElementById('example'))
    }

    render() {
      console.log('render() 渲染组件')
      return (
        <div>
          <h2 style={{opacity:this.state.opacity}}>{this.props.content}</h2>
          <button onClick={this.removeComponent}>不活了</button>
        </div>
      )
    }
  }
  ReactDOM.render(<Fade content="react学不会, 怎么办?"/>, document.getElementById('example'))
</script>
```

# 虚拟DOM与DOM diff 算法

![](_v_images/20200505233336106_14597.png)

# React脚手架

```
npm i -g create-react-app 
create-react-app react_demo
cd react_demo
npm start
```

# React网络请求

## axios

```
1) GET 请求
axios.get('/user?ID=12345')
    .then(function (response) {
        console.log(response);
    })
    .catch(function (error) {
        console.log(error);
    });
axios.get('/user', {
    params: {
        ID: 12345
    }
})
    .then(function (response) {
        console.log(response);
    })
    .catch(function (error) {
        console.log(error);
    });

2) POST 请求
axios.post('/user', {
    firstName: 'Fred',
    lastName: 'Flintstone' 
})
    .then(function (response) {
        console.log(response);
    })
    .catch(function (error) {
        console.log(error);
    });
```

## fetch

```
1) GET 请求
fetch(url)
    .then(function(response) {
        return response.json()
    })
    .then(function(data) {
        console.log(data)
    })
    .catch(function(e) {
        console.log(e)
    });

2) POST 请求
fetch(url, {method: "POST", body: JSON.stringify(data), })
    .then(function(data) {
        console.log(data)
    })
    .catch(function(e) {
        console.log(e)
    })
```

# 组件间通信

## 方式一：通过props传递

1.共同的数据放在父组件上，特有的数据放在自己组件内部state

2.通过props可以传递一般数据和函数数据，只能一层一层传递

## 方式二：使用消息订阅subscribe与发布publish机制

1.工具库：PubSubJS

2.npm i pubsub-js

3.
import PubSub from 'pubsub-js' //引入
PubSub.subscribe('delete', function(msg, data){ }); //订阅
PubSub.publish('delete', data) //发布消息

## 方式三：redux

# react-router4

## react-router理解

1.react的一个插件库

2.专门用来实现一个SPA应用

3.基于React的项目基本都会用到此库

## SPA理解

1.单页Web应用（single page web application, SPA）

2.整个应用只有一个完整的页面

3.点击页面中的链接不会刷新页面，本身也不会向服务器发请求

4.当点击链接时，只会做页面的局部更新

5.数据都需要通过ajax请求获取，并在前端异步展现

## 路由的理解

1.什么是路由？
    a.一个路由就是一个映射关系（key:value）
    b.key是路由路径，value可能是function/component

2.路由分类
    a.后台路由：node服务器路由，value是function，用来处理客户端提交的请求并返回一个响应数据
    b.前台路由：浏览器端路由，value是component，当请求的是路由path时，浏览器端没有发送http请求，单界面会更新显示对应的组件

3.后台路由
    a.注册路由：router.get(path,(req, res) => {})
    b.当node接收到一个请求时，根据请求路径找到匹配的路由，调用路由中的函数来处理请求，返回响应数据

4.前台路由
    a.注册路由：`<Route path='/about' component={About}>`
    b.当浏览器的hash变为#about时，当前路由组件就会变为About组件

## react-router使用

`npm i react-router-dom@4`

## react-router相关API

```
1) <BrowserRouter>
2) <HashRouter>
3) <Route>
4) <Redirect>
5) <Link>
6) <NavLink>
7) <Switch>
```

其他
1) props.history 对象
history.push(): 添加一个新的历史记录
history.replace(): 用一个新的历史记录替换当前的记录
history.goBack(): 回退到上一个历史记录
history.goForword(): 前进到下一个历史记录
history.listen(function(location){}): 监视历史记录的变化
2) props.match 对象
3) withRouter 函数

# react-ui

## Ant-Design

### 搭建antd-mobile的基本开发环境

1.npm install antd --save

# redux

## redux是什么?

1.redux是一个独立专门用于做管理状态的JS库

2.它可以用在react，angular，vue项目中，但基本与react配合使用

3.作用：集中式管理react应用中多个组件共享的状态

## redux工作流程

![riadAin](_v_images/20200509154116279_5307.gif =616x)

## redux核心API

### 1.createStore()

作用：创建包含指定reducer的store对象

### 2.store对象

作用：redux库最核心的管理对象
它内部维护着：state与reducer函数

核心方法：getState() dispatch(action) subscribe(listener)

### 3.applyMiddleware()

作用：基于redux的中间件

### 4.combineReducers()

作用：合并多个reducer函数

## redux的三个核心概念

### 1.action

标识要执行行为的对象
包含两个方面的属性
    type：标识属性，值为字符串，唯一，必要属性
    data：数据属性，值类型任意，可选属性

Action Creator(创建Action的工厂函数)

### 2.reducer

根据老的state和action，产生新的state纯函数

注意：返回一个新的状态，不修改原来的状态

### 3.store

将state, action与reducer联系在一起的对象

getState()：得到state

dispatch(action)：分发action，触发reducer调用，产生新的state

subscribe(listener)：注册监听，当产生新的state时，自动调用

## 问题

1.redux与react组件的代码高度耦合
2.编码不够简洁

## react-redux

### 理解

1.一个react插件库
2.专门用来简化react应用中使用redux

### 所有组件分为两大类

1.UI组件

只负责UI的呈现，不带有任何业务逻辑
通过props接收数据（一般数据和函数）
不适用任何Redux的API
一般保存在components文件夹下

2.容器组件

负责管理数据和业务逻辑，不负责UI的呈现
使用Redux的API
一般保存在containers文件夹下

### 相关API

#### Provider

让所有组件都能得到state数据
```
<Provider store={store}>
<App />
</Provider>
```

#### connect()

用于包装UI组件生成容器组件

例：
`connect(state => ({count: state}),{increment, decrement})(UI组件)`

### 问题

1.redux默认是不能进行异步处理的（ajax，定时器）

## redux异步编程（使用异步中间件）

npm i redux-thunk

### store.js

```
import {createStore, applyMiddleware} from 'redux'
import thunk from 'redux-thunk'
// 根据 counter 函数创建 store 对象
const store = createStore(
reducer,
applyMiddleware(thunk) // 应用上异步中间件
)
```

### actions.js

```
// 异步action creator（返回一个函数）
export const ActionCreator = number => {
return dispatch => {
setTimeout(() => {
dispatch(increment(number))
}, 1000)
}
}
```

## redux-devtools

安装chrome插件redux-devtools

下载工具依赖包

npm i redux-devtools-extension

```
import { composeWithDevTools } from 'redux-devtools-extension'
const store = createStore(
counter,
composeWithDevTools(applyMiddleware(thunk))
)
```
