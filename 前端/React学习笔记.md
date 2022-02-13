# 前言

> 此笔记参考[尚硅谷2021版React技术全家桶全套完整版（零基础入门到精通/男神天禹老师亲授）_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1Ey4y1u7vi?p=1)学习视频，感谢视频发布者和天禹老师！

## react是什么？

React是一个将数据渲染为HTML视图的开源JavaScript库。

## 谁开发的？

1.起初由Facebook的软件工程师Jordan Walke 创建。

2.于2011年部署于Facebook 的newsfeed。

3.随后在2012年部署于Instagram.

4.2013年5月宣布开源。

## 为什么要学？

1.原生JavaScript操作DOM繁琐、效率低（**DOM-API操作UI**) 。

2.使用JavaScript直接操作DOM，浏览器会进行大量的**重绘重排**。

3.原生JavaScript没有**组件化**编码方案，代码复用率低。



这里的组件化借用视频里的例子进行说明：

假设一个开发组里，A已经写好了一个导航栏，而B想使用A写好的导航栏，如果在传统的开发模式（未引入组件化概念），则需要拷贝html代码，虽然js和css文件可以复用，但是html代码还是需要写入，如果引入了组件化模块，组件会把导航栏里所需要的一切包括但不限于html、css、js或者img等等，都包含在内，此时导入组件就使得开发十分高效，便捷。

## 特点

1.采用**组件化**模式、**声明式编码**，提高开发效率及组件复用率。传统方式使用的是命令式编码。

2.在React Native中可以使用React语法进行**移动端开发**。

3.使用**虚拟DOM**和优秀的**Diffing算法**（可以简单理解为高效地比较新旧虚拟DOM不同点的算法），尽量减少与真实DOM的交互，所以浏览器的重绘重排次数减少，从而提高效率。

关于第三点的总结：虚拟DOM通过Diffing算法，找出**新旧虚拟DOM的区别**，只将差别部分渲染给真实DOM，从而最大程度使用真实DOM上已经渲染的部分，从而最小化浏览器的重绘重排。

![QQ20220212213006.png](https://img.pterclub.com/images/2022/02/12/QQ20220212213006.png)

# 语法

## React入门使用（不标准）

作为入门，并未使用webpack环境，故只作为一种入门。

使用react实现一个最简单的功能，显示hello react这一段字符串

### 代码

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">

    <title>Hello_react</title>
    <!-- 引入react引入核心库, 需要按顺序引入 -->
    <script type="text/javascript" src="../js/react.development.js"></script>
    <!-- 引入react-dom, 用于支持react操作DOM -->
    <script type='text/javascript' src='../js/react-dom.development.js'></script>
    <!-- 引入babel，用于将jsx转为js -->
    <script type='text/javascript' src='../js/babel.min.js'></script>
</head>
<body>
    <!-- 准备好一个容器 -->
    <div id="test"></div>

    <script type='text/babel'> //此处必须写babel,因为script内部写的是JSX而非JS
        // 1. 创建一个虚拟DOM
        let VDOM = <h1>Hello, React！</h1> // 此处不用加引号，因为是虚拟DOM，而且使用的是JSX语法。JSX可以使得js语法和标签混用
        // 2. 让React 将虚拟DOM（VDOM）插入页面
        // ReactDOM.render(虚拟DOM,目标容器)
        ReactDOM.render(VDOM,document.getElementById('test'))
    </script>
    
</body>
</html>
```

### 两种创建虚拟DOM的方式

每个 JSX 元素只是调用 `React.createElement(component, props, ...children)` 的语法糖。

因此，使用 JSX 可以完成的任何事情都可以通过纯 JavaScript 完成。

#### 使用JSX

```html
<script type='text/babel'> 
    // 1. 创建一个虚拟DOM
    let VDOM = (
        <h1 id="atguigu">
        <span>Hello, React！</span>
        </h1>
       )
     // 2. 让React 将虚拟DOM（VDOM）插入页面
     ReactDOM.render(VDOM,document.getElementById('test'))
</script>
```

#### 使用js语法创建

```html
<script type='text/javascript'>
    // 1.创建虚拟DOM(标签名，属性，内容)
    let VDOM = React.createElement('h1',{id:'atguigu'},'Hello, React!')
    // 2.渲染虚拟DOM到页面
    ReactDOM.render(VDOM,document.getElementById('test'))
</script>
```

### 虚拟DOM和真实DOM

关于虚拟DOM和真实DOM

1.虚拟DOM比较“**轻**”，真实DOM比较“**重**”（这里的轻和重主要体现在属性个数上），因为虚拟DOM是React在用，无需真实DOM上那么多属性。

2.虚拟DOM最终一定会转为真实DOM放入页面。

```javascript
console.log(typeof VDOM); // object
console.log(VDOM instanceof Object); // true

const TDOM = document.getElementById('test')
console.log('虚拟DOM：', VDOM);
console.log('真实DOM：', TDOM);
```

浏览器显示如下：

![QQ20220212225035.png](https://img.pterclub.com/images/2022/02/12/QQ20220212225035.png)

## JSX

### 简介

JSX:全称JavsScript XML。
是react定义的一种类似于XML的JS扩展语法：JS + XML 本质是
React.createElement(component, props, ...children)方法的**语法糖**。

###  jsx语法规则

  1.创建虚拟DOM时，不要写引号；
  2.标签中要混入【js表达式】（函数的调用、变量的调取等等），而非js语句（比如if for while等等），**要使用{}**。

```react
const data = `hello!`
//虚拟DOM
const VDOM = <h1>{data}</h1>
ReactDOM.render(VDOM, document.getElementById('test'));
```

 PS：js表达式和js语句的区别：
	①.JS表达式：**一个表达式会产生一个值**，可以放在任何一个需要值的地方
     （1） a
     （2） a + b
     （3） demo(1)
     （4） arr.map()，用于加工数组，不会影响原数组。
     （5） function test(){}
	②.JS语句（代码）：
     （1） if  判断语句
     （2） for(){}  循环语句
     （3） switch(){case:xxx}  分支语句

 3.标签中样式的类名要用className来指定

```react
const VDOM = <h1 className="title">{data}</h1>
```

  4.标签中的内联样式要用style={{color:'white'}},属性名转为**小驼峰**。比如style里的字体大小font-size在JSX中得转换为fontSize。

- 正常情况下，在html定义内联样式的方式

```html
<div id="test" style="color:white;"></div>
```

-   在JSX下需要用小驼峰和双括号，此处第一对花括号代表第一对花括号里写的是js代码，第二对花括号表示的是js语法里的对象的意思，white加单引号表示字符串而非white变量。

```react
const VDOM = <h1 className="title" style={{color:'white'}}>{data}</h1>
```

- 若有多个style样式，并且需要转换小驼峰时，注意这里font-size是fontSize！！

  ```react
  let VDOM = <h1 style={{ color: 'red', fontSize: '16px' }} className="title">hello~!</h1>
  ```

5.VDOM每次创建**只能有一个根标签**。

（1）如果VDOM有多个标签，必须用div包裹起来才行

```react
const VDOM=(
	<h1>你好</h1>
    <span>中国！</span>
)
```

以上的写法是错误的，**必须用div包裹**起来才可行！

```react
const VDOM = (
	<div>
		<h1>你好</h1>
    	<span>中国！</span>
	</div>
)
```

6.标签必须闭合（单标签加 / 自闭合）

此处以<input>举例，在html中input标签不会自动闭合会以以下形式呈现：

```html
<input type="text">
```

这种写法在html中可以使用，但是在react中，必须要闭合标签，第一种是自闭合（推荐），第二种是用标签对闭合，如果不闭合直接写成上面的形式，则会报错！

```react
const VDOM = (
	<div>
		<h1>你好</h1>
    	<span>中国！</span>
        <input type="text"/>
        <input type="text"></input>
	</div>
)
```

7.关于标签首字母：
    1） 若首字母小写，那么React就会去寻找与之同名的<**html标签**>
          · 若找见，直接转为html同名元素
          · 若未找见，报错
    2） 若首字母大写，那么React就会去寻找与之同名的**组件**（component），
          · 若找到就使用
          · 若没有就会报错
8.注释时先用{}包起来变成js表达式再注释，在html里面注释react语句会比较麻烦，在后期使用脚手架之后，直接在.jsx文件里注释就方便了。

```react
const VDOM = (
	<div>
        {/*<h1>你好</h1>*/}
    	<span>中国！</span>
	</div>
)
```

### JSX练习

1.模拟从数据（此处用数组进行模拟）中取数据再呈现到页面上：

```react
const data=['Angular','React','Vue']

const VDOM = (
	<div>
    	<h1>前端JS框架列表</h1>
        <ul>
        	{
                /*注意这里只能写js表达式，不能写js语句，故使用数组的map方法*/
                data.map((item,idex)=>{
                    return <li key={index}>{item}</li>
                })
                /*因为在react中标签里掺杂js变量的时候需要加{}，这里加key是因为react使用了diffing算法，需要用key来比较，如果添加了相同的key或者不添加key的话，就会弹出警告！*/
            }
        </ul>
    </div>
)
ReactDOM.render(VDOM, document.getElementById('test'))
```

因为只有一个返回值，箭头函数可以进一步简写为：

```javascript
data.map((item,idex)=><li key={index}>{item}</li>)
```

（1）注意点：

①react里只能写js表达式而不能写js语句！

②li标签里需要添加不同的key属性以供react的diffing算法比较

③在JSX或者说react语法中，标签里掺杂js变量的时候需要加{}，这是react的特性与ES6的新特性无关。在ES6中与这个比较相像的特性就是模板字符串中可以用${}来取js变量，正如下面所示！

2.如果用js实现该功能的话

```javascript
const arr = ['Angular','React','Vue']
let arr2 = arr.map((item,index)=>{
     return `<li>${item}</li>`
})
        // map加工数组，但不影响原数组
        document.getElementById("test").innerHTML=arr2.join().replaceAll(",","");
```

