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

```react
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

```react
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

## React编程所需的工具

需要浏览器的一个插件，名叫React Developer Tools，可以直接从插件商店里下载。

![QQ20220220142327.png](https://img.pterclub.com/images/2022/02/20/QQ20220220142327.png)

## 定义组件的两种方式

组件的定义：**实现页面局部功能全部代码和<u>资源</u>的集合**。

### 使用函数定义

该方法便捷，但是有缺陷，虽然有补救措施，但是不推荐。

#### js中调用函数的几种方式

1.直接调用

```javascript
function test(){
    console.log(this);
}
```

直接使用函数名加小括号的方式调用该函数。

```javascript
test();
```

此时test函数里的this指向的就是window。

![QQ20220220144808.png](https://img.pterclub.com/images/2022/02/20/QQ20220220144808.png)



2.通过函数名.call()方式调用，这种调用方式会改变函数中的this指向，**参数依次传入**，完整调用格式如下：

最直接的体现就是如果第一个例子中改为test.call(1)，控制台就会打印如下：

![QQ20220220145500.png](https://img.pterclub.com/images/2022/02/20/QQ20220220145500.png)

3.通过函数名.apply()调用，同样可以改变this指向，参数以数组方式传入。

4.通过bind函数返回一个新的函数再调用



以上四种具体区别可以总结为以下几点：

> 该部分参考[(80条消息) JS中的call()和apply()方法和区别_世平那个张的博客-CSDN博客_js中apply和call的作用和区别是什么](https://blog.csdn.net/weixin_42321292/article/details/82352997)，感谢作者世平那个张！

![QQ20220220150247.png](https://img.pterclub.com/images/2022/02/20/QQ20220220150247.png)


![QQ20220220150254.png](https://img.pterclub.com/images/2022/02/20/QQ20220220150254.png)

![QQ20220220150304.png](https://img.pterclub.com/images/2022/02/20/QQ20220220150304.png)



#### 具体写法

```react
<body>
    <div id="test"></div>

    <script type="text/babel">
        // 1.定义一个组件(函数式)
        function Demo(){
            console.log(this) // 此处的this是undefined，因为经过babel翻译，开启了严格模式
            return <h2>我是用函数定义的组件（适用于【简单组件】的定义）</h2> // 组件标签
        }

        // 2.渲染组件到页面
        ReactDOM.render(<Demo/>,document.getElementById('test'))
    </script>
</body>
```

注意点：

（1）构成组件的函数名称的首字母必须大写，具体原因与babel翻译有关。

> 此处参考[(80条消息) react声明组件时，第一个字母必须大写，为什么呢_codingWeb的博客-CSDN博客_react 组件大写](https://blog.csdn.net/fesfsefgs/article/details/105599570)，感谢作者codingWeb！

总结来说，如果不首字母大写，babel在转义时就会把其当成一个字符串传入React.createElement()这个方法，如果首字母大写了，babel在转义时就会传入一个变量。具体如下图所示：

![QQ20220220163329.png](https://img.pterclub.com/images/2022/02/20/QQ20220220163329.png)



（2）在渲染时，组件名必须使用<组件名/>的这种**闭包形式**（当然<组件名></组件名>也可以）。

（3）在执行了ReactDOM.render(<Demo/>....)后发生了什么?

①React解析组件标签，寻找Demo组件的定义位置

②React发现Demo组件是用函数定义的，随后React去直接调用Demo函数，将【**返回的值**】渲染到页面

（4）该函数形式定义组件所存在的**残疾**的部分就是：函数内部的this是undefined，具体原因是babel翻译时开启了严格模式，不允许直接指向window。

### 使用类定义

写法较为繁琐，但是功能完备，不残疾，推荐。

#### 复习js中的类

1.类中的构造器**不是必须**要写的，如果想给实例添加一些自己独有的属性，那么就要写构造器；

2.如果A类继承了B类，且A类写了构造器，那么在A类的构造器中**必须调用super**。

3.类中的方法是放在类的原型对象上的，供实例使用，如果是通过实例调用的方法，那么方法中的this就是实例对象。

#### 具体写法

```react
<div id="test"></div>
    <script type="text/babel">
        // 1.定义一个组件（类式）
      class Demo extends React.Component{
          /**
           * 1. render方法是放在哪里的？ ———— Demo的原型对象上，供实例使用
           * 2. render中的this是谁？ ———— Demo的实例对象
          */
        render(){
            console.log(this); // Demo类的实例对象 <=> Demo组件的实例对象 <=> 也称“Demo组件对象”
            return <h2>我是用类定义的组件（适用于【复杂组件】的定义）</h2>
        }
      }
      // 2.渲染组件到页面
      ReactDOM.render(<Demo/>, document.getElementById('test'))
    </script>
```

注意点：

①类组件必须继承React.Component。

②类组件内部必须重新render方法，同时该render方法必须有返回值，因为React会**调用**该组件的render方法来获取返回值。

③执行了ReactDOM.render(<Demo/>...后发生了什么)
1.React解析组件标签，寻找Demo组件的定义
2.React发现Demo组件是用类定义的，React实例创建了一个Demo的实例对象-D
3.通过D去调用到了render方法，D.render()。

## 组件实例三大属性

注意：这里的三大属性主要是针对通过**类定义**的组件！

### state

#### 简介

1.state是组件对象最重要的相互ing，值是对象（可以包含多个key-value的组合）

2.组件又被称为‘状态机’，通过更新组件的state来更新对应的页面显示（重新渲染组件）

### 代码

实现需求：现在有一段话“今天天气很凉爽”，当鼠标点击凉爽时，这两个字就会变成炎热，点击炎热时这两个字就会变成凉爽。

#### 一般实现

```react
<script type="text/babel">
        class Weather extends React.Component{
            constructor(props) {
                super(props)
                this.state = {isHot:false} // 初始化状态
            }
            render(){
                return <h1 onClick={this.changeWeather}>今天天气很{this.state.isHot ? '炎热' : '凉爽'}</h1>
            }
            changeWeather(){
                const isHot = this.state.isHot
                this.setState({isHot:!isHot})
            }
        }
        ReactDOM.render(<Weather/>,document.getElementById('test'))

    </script>
```

##### 注意点：

1.原生属性比如是onclik在react中需要写成onClick，以驼峰的方式命名！

```react
render(){
                return <h1 onClick={this.changeWeather}>今天天气很{this.state.isHot ? '炎热' : '凉爽'}</h1>
            }
```

2.react中事件绑定的方式与原生js有些不同。

在原生js和html中，可以直接写函数名加小括号，这样的效果是当我们点击时才会调用show函数，不会主动调用。

```html
<h1 onclick="show()">今天天气不错</h1>
```

但是在react中，要想实现以上效果，则函数名后面不能加小括号。若加了小括号，函数就会自动调用无论你是否有点击事件的发生。

```react
            render(){
                return <h1 onClick={this.changeWeather}>今天天气很{this.state.isHot ? '炎热' : '凉爽'}</h1>
            }
```

3..在JSX代码里，在组件类外部直接写function，然后function中的this因为babel的严格模式，指向的会是undefined！即：**在严格模式下禁止this关键字指向全局对象**！

4.在js中，类中函数方法的调用者是类的实例对象，如果类中的一个函数方法中内部要调用另一个函数方法，必须要用this.函数名()的形式来调用。

```javascript
class dog{
    bark(){
        console.log("bark");
    }
    cry(){
        this.bark();//必须加上this，才能调用一个类中的另一个方法
        console,log("bark");
    }
}
```

5.js中的类中的this详解，此处代码没有被babel包裹

```javascript
class Dog {
    constructor(name,age){
        this.name = name
        this.age = age
    }
    bark(){
        console.log('bark的this是：',this);
    }
}
const d = new Dog('DOGE',4)
d.bark();//此时this指向的就是dog
```

（1）当类中的函数方法被类的实例对象调用时，this指向的就是类的实例。但是如果通过<u>第二个变量得到了堆中函数的位置</u>，直接通过**第二个变量**直接**调用**，虽然是全局调用，但是这里this指向的就是undefined了，因为类中所有定义的方法，浏览器在运行时，全都加上了use strict，**在严格模式禁止this关键字指向全局对象**。

```javascript
const d = new Dog('DOGE',4)
const x = d.bark
x() 
```

![QQ20220220220535.jpg](https://img.pterclub.com/images/2022/02/20/QQ20220220220535.jpg)

（2）但如果是直接是对象的话，同样条件下调用，this得到的就是window了

```javascript
let obj = {
     a:1,
     b:2,
     c:function(){
         console.log(this);
     }
}
const y = obj.c
y()//会打印windo
```

(3)严格模式可以局部开启的，如下面的代码所示

```javascript
function demo1(){
        'use strict' //局部开启严格模式
        console.log('demo1:',this);
   }
   function demo2(){
        console.log('demo2:',this);
   }
demo1()
demo2()
```

![QQ20220220220949.jpg](https://img.pterclub.com/images/2022/02/20/QQ20220220220949.jpg)

可以看到，开启了**严格模式**的函数直接调用this的话指向的就不是window了。

6.类中定义的函数方法都是在原型上的

![QQ20220220222100.jpg](https://img.pterclub.com/images/2022/02/20/QQ20220220222100.jpg)

7.通过bind改变this指向，bind改完this指向后会返回一个新的改过this的函数
this.changeWeather = this.changeWeather.bind(this)
这句话先读赋值语句的右侧，先从构造器的this指向(就是Weather)的**原型**中找到changeWeather，把该changeWeather中的this改好了之后再赋值给自己，这样Weather的实例对象就有了changeWeahter方法了。做完上述步骤后，就会有两个changeWeather，一个在对象的内部原型外部，还有一个在原型内部，前面一个的this是正常的不受严格模式约束的，后面一个this是受严格模式约束的。

![QQ20220220205448.jpg](https://img.pterclub.com/images/2022/02/20/QQ20220220205448.jpg)

8.state**无法直接修改**，需要用setState来修改。这是state的一大特性！

#### 简便写法

```react
    <div id="test"></div>

    <script type="text/babel">
        class Weather extends React.Component {
            state = { isHot: false }
            render() {
                console.log('render里的this:', this)
                return <h1 onClick={this.changeWeather}>今天天气很{this.state.isHot ? '炎热' : '凉爽'}</h1>
            }

            // 组件类中程序员定义的事件回调，必须写成赋值语句+箭头函数
            // 避免了this为undefined的问题
            changeWeather = ()=> {
                console.log('changeWeather里的this', this);
                const isHot = this.state.isHot
                this.setState({isHot:!isHot})
            }
        }
        ReactDOM.render(<Weather />, document.getElementById('test'))

    </script>
```

##### 说明

1.在类中直接写一个赋值语句例如a=1，等价于给这个类新增一个属性a，其值为1。
2.changeWeather也可以用同样的方式简写，但是**不能用传统的function的方式声明**，这样会被babel强制应用严格模式。所以必须使用箭头函数，**箭头函数内部没有this**，当在箭头函数内部使用this时会调用箭头函数外部的this。

这样就是不行的！

```javascript
changeWeather = function() {
                console.log('changeWeather里的this', this);
                const isHot = this.state.isHot
                this.setState({isHot:!isHot})
            }
```



### props

#### 定义

props是专门设计为从组件外部收集信息传递给组件内部的类组件里的对象。

#### 用法

##### 在类组件中使用props

目前有个需求就是在网页上显示两个人的姓名、性别和年龄。



1.分别传递标签属性

```react
	<div id="test"></div>
    <div id="test2"></div>
    <script type="text/babel">
        // 1.定义一个Person组件
        class Person extends React.Component{
          render(){
              const {name,sex,age} = this.props
              return (
                  <ul>
                      <li>NAME: {name}</li>
                      <li>GENDER: {sex}</li>
                      <li>AGE: {age}</li>
                  </ul>
              )
          }
        }
        // 2.渲染组件到页面（分别传递标签属性）
        ReactDOM.render(<Person name="老刘" sex="female" age="23" />,document.getElementById('test'))
</script>
```

效果图：

![QQ20220221213421.jpg](https://img.pterclub.com/images/2022/02/21/QQ20220221213421.jpg)

2.批量传递标签属性

```react
// （模拟一个服务器返回人的数据）
const p1 = {
     name:'强哥',
     sex:'女',
     age: 19
}
// 批量传递标签属性
ReactDOM.render(<Person {...p1}/>, document.getElementById('test2'))
```

##### 在函数式组件中使用props

可以通过函数参数的形式把props传入到函数内部，但是对props的限制的语句就只能写在外部了，不能像类组件那样写在组件的内部。

```react
    <script type="text/babel">
        function Person(props) {  // 用参数传入props
            const { name, age, sex } = props
            return (
                <ul>
                    <li>姓名：{name}</li>
                    <li>性别：{sex}</li>
                    <li>年龄：{age}</li>
                </ul>
            )
        }
        // 限制只能写在外面
        Person.propTypes = {
            name: PropTypes.string.isRequired, // .isRequired要求必须传
            age: PropTypes.number,
            asex: PropTypes.string
        }
        Person.defaultProps = { // 默认值
            age: 18
        }

        const p1 = {
            name: 'Nicolas',
            sex: 'male',
            age: 27,
        }
        ReactDOM.render(<Person {...p1} />, document.getElementById('test'))
    </script>
```

#### 对props进行限制

react提供方法给props进行限制，不过需要引入prop-types.js。

对props限制既可以限制类型，也可以限制必须传哪些属性，也可以设置属性的默认值。

```react
<script type="text/babel">
        class Person extends React.Component {
            state = {} // 任何时候状态放第一
            static propTypes = {
                name: PropTypes.string.isRequired, // .isRequired要求必须传
                age: PropTypes.number,
                sex: PropTypes.string
            }
            static defaultProps = { // 默认值
                age: 18
            }
            render() {
                let { name, sex, age } = this.props
                return (
                    <ul>
                        <li>姓名：{name}</li>
                        <li>性别：{sex}</li>
                        <li>年龄：{age + 1}</li>
                    </ul>
                )
            }
        }
        const p1 = {
            name: 'Nicolas',
            sex: 'male',
            age: 27,
        }
        ReactDOM.render(<Person {...p1} />, document.getElementById('test'))
</script>
```

static propTypes中可以限制props属性的类型和是否是必须传入的，static defaultProps可以设置props的默认值。假如没有传入指定类型，虽然页面可以显示但是浏览器控制台就会报错！

比如给age传入了一个字符串

![QQ20220221223032.jpg](https://img.pterclub.com/images/2022/02/21/QQ20220221223032.jpg)

#### 注意点和补充复习知识

1.props对象中的属性里的值是**只读**的，在赋值之后无法再修改。

比如props里有一个name属性，则以下代码会在浏览器中报错！

![QQ20220221213949.jpg](https://img.pterclub.com/images/2022/02/21/QQ20220221213949.jpg)

![QQ20220221214004.jpg](https://img.pterclub.com/images/2022/02/21/QQ20220221214004.jpg)

2.关于ES7中的打包和拆包功能复习：

有关具体的展开功能的详细介绍，可以查看MDN的链接：[展开语法 - JavaScript | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Spread_syntax)

（1）拆包

①...展开语法**可以对数组使用**。

```javascript
let arr = [4,5,6,7]
console.log(arr); // (5) [1, 3, 5, 7, 9]
console.log(...arr); // 1 3 5 7 9  （拆包）

let arr2 = [1,2,3,...arr,8] // 拆包
console.log(arr2);// (8) [1, 2, 3, 4, 5, 6, 7, 8]
```

②在原生js中，展开语法无法对对象展开，因为对象并没有迭代器。

```javascript
let obj = {name:'圆圆的海峰',age:18,sex:'女'}
let obj2 = {nationality:'Chinese',height:'180cm'}
console.log(...obj)//这样写就会报错
```

![QQ20220221214352.jpg](https://img.pterclub.com/images/2022/02/21/QQ20220221214352.jpg)

③展开语法可以对对象使用，条件是要包在一个对象内部。比如

```javascript
console.log(...obj); // {name:'圆圆的海峰',age:18,sex:'女'}
console.log({...obj,...obj2}); // {name: '圆圆的海峰', age: 18, sex: '女', nationality: 'Chinese', height: '180cm'}
console.log({...obj,name:'LX'}); // {name: 'LX', age: 18, sex: '女'}
```

（2）打包，最典型的使用场景就是当一个函数不知道自己接受的参数有多少个时，可以用...params来将参数打包起来。

```javascript
function demo(...params){ // 打包
   console.log('我收到的参数为：', params);
}
demo(1,2,3)
```

![QQ20220221214932.jpg](https://img.pterclub.com/images/2022/02/21/QQ20220221214932.jpg)

3.在原生里...无法展开对象，但是在react里可以，但仅适用于**传递标签属性**，为什么要加{}呢？是因为是模板语法，JSX的基本语法中遇到 HTML 标签（以 < 开头），就用 HTML 规则解析；遇到代码块（以 { 开头），就用 JavaScript 规则解析；
所以在react中{...obj}就等价于js中的...obj。

4.关于class中的static属性

在class中，未加static的属性会出现在类的实例对象的属性中,而加了static的属性就会出现在类的属性中，例如：

```javascript
class Dog {
   constructor(){
	}
    run(){
	}
    a = 1
    static b = 2
}
const d = new Dog()
console.log(d);
console.log(Dog.b);//2  即 b是在Dog类上的，可以通过类名加上属性名进行调用
```

![QQ20220221223548.jpg](https://img.pterclub.com/images/2022/02/21/QQ20220221223548.jpg)

这也是限制props的几个属性前面要加static的原因，因为加了的话就会随着类走，也比较方便。

5.类式组件中的构造器**完全可以省略**。若写了构造器则super必须调用，且当需要在构造器中通过this.props取值时，那么props要传给super。

### refs与事件处理

简单来说ref就是react中标签中id的替代者，不过react建议能不用ref就不用ref，因为ref会占用的内存比较大！下面会有解决办法的！

#### 字符串形式的refs

不推荐使用，略过。

#### 回调形式的refs

refs写成函数形式后，react来帮我们调用，函数的参数就是包含ref属性的标签。但也有点问题，不推荐。

#### createRef形式的ref 

使用React.createRef()在类内部创建容器后，将需要操作的ref存入容器中，最后再在函数内部直接调用容器内部的ref。

```react
    <script type="text/babel">
    class Demo extends React.Component{
        container = React.createRef()
        container2 = React.createRef()
        render(){
            return(
                <div>
                    <input type="text" ref={this.container} />
                    <button onClick={this.show}>点我提示左侧数据</button>
                    <input type="text" ref={this.container2} onBlur={this.show2} placeholder="失去焦点提示数据"/>
                </div>
            )
        }
        
        show = ()=>{
            console.log(this.container); // {current: input}
            alert(this.container.current.value)
        }
        show2 = ()=>{
            alert(this.container2.current.value)
        }

    }
    ReactDOM.render(<Demo/>,document.getElementById('test'))
    </script>
```

#### 事件处理

1. 通过onXxxx属性指定事件处理函数（注意大小写）
   (1) React使用的是自定义（合成）事件，而不是使用的原生DOM事件这样有利于**提高效率**，因为原生事件中如果有用不到的属性，它还是会给你显示出来，而react的自定义事件中的属性，用到了才会给你，若没有用到就不会给，提高了效率。
   (2) React中的事件是通过**事件委托**方式处理的（委托给组件**最外层**的元素）
2. 通过**event.target**得到事件发生的DOM元素对象

## 非受控组件和受控组件

### 非受控组件

#### 定义

表单中的数据，在需要的时候“现用现取”，即通过ref获得到节点，进而访问到value值。这里的非受控主要指的是数据与组件的state没有建立起联系来，如果一输入，value值就往状态state里面跑，那就不是非受控组件了。

#### 示例代码

这里的ref使用了回调形式。

```react
<script type="text/babel">
      class Login extends React.Component{
          render(){
              return(
                  <form onSubmit={this.handleLogin}>
                    {
                }
                    用户名：<input type="text" ref={c => this.userNameNode = c} /><br/>
                    密码：<input type="password" ref={c => this.passwordNode = c}/><br/>
                    <button>登陆</button>
                    </form>
              )
          }
          handleLogin = ()=>{
              const {userNameNode,passwordNode} = this
              console.log(userNameNode);
              alert(`用户名：${userNameNode.value}, 密码：${passwordNode.value}` ) 
          }
      }
      ReactDOM.render(<Login/>,document.getElementById('test'))
</script>
```

### 受控组件

#### 定义

表单中输入类的DOM，随着用户的输入，将值**自动收集**到State中，那么就称为受控组件。

#### 代码

##### 最垃圾的写法，有一个属性就写一个函数

1.以下代码有弊端，有一个属性就要写一个save函数比较繁琐。 

为什么不写this.saveDate("password")来用一个函数来完成各个函数的功能呢？因为如果写了saveDate("password")的话就是一个函数调用了，react就会**自动调用**这个函数，并把这个函数的返回值给onchange，在这里的场景下与我们的需求相悖。

```react
class Login extends React.Component{
          state = {
              username: "",
              password: "123"
          }
          render(){
              return(
                  <form onSubmit={this.handleLogin}>
                    {
                }
                    用户名：<input type="text" onChange={this.saveUsername} /><br/>
                    密码：<input type="password" onChange={this.savePassword} /><br/>
                    <button>登陆</button>
                    </form>
              )
          }
          // 保存用户名到State中
          saveUsername = (event)=>{
              this.setState({username:event.target.value})
              //setState不会造成其他state属性值的改变或者丢失，只会改变setState函数传入的属性值。
          }
          // 保存密码到state中
          savePassword = (event)=>{
              this.setState({password:event.target.value})
          }
          handleLogin = (event)=>{
              event.preventDefault()
              const {username,password} = this.state
              alert(`用户名：${username}, 密码：${password}`) 
          }
      }
ReactDOM.render(<Login/>,document.getElementById('test'))
```

**注意**：setState**不会**造成其他state属性值的改变或者丢失，只会改变setState函数传入的属性值。

##### 使用高级函数和函数的柯里化

1.高级函数和函数柯里化的定义：

（1）高阶函数：如果一个函数符合下面2个规范中的任意一个，该函数即为高阶函数

​		①若A函数**接收的参数**是一个**函数**，那么A即为高阶函数
​		②若A函数调用的**返回值**依然是一个**函数**，那么A为高阶函数
​		常见的高阶函数：Promise,setTimeout,arr.map(),bind

（2）函数的柯里化：通过函数调用继续返回函数的方式，实现多次接收参数最后统一处理的函数编码形式。

比如：

```javascript
//正常函数写法
function sum(a,b,c){
     return a+b+c
}
```

如果使用柯里化写法和高级函数：

```javascript
function sum(a)
{
    return (b) => {
        return (c) => {
            return a + b + c ;
        }
    }
}
```

2.使用这两项技术来解决受控组件问题

```javascript
 class Login extends React.Component{
          state = { // 初始化状态
              username: "",
              password: "123"
          }
          render(){
              return(
                  <form onSubmit={this.handleLogin}>
                    {
                }
                    用户名：<input type="texnCht" onChange={this.saveFormData("username")} /><br/>
                    密码：<input type="password" onChange={this.saveFormData("password")} /><br/>
                    <button>登陆</button>
                    </form>
              )
          }
          saveFormData = (type) =>{
              return (event)=>{
                  this.setState({[type]:event.target.value})
                  {/*这里的type加中括号的原因看下面的备注*/}
                }
          }
          handleLogin = (event)=>{
              event.preventDefault()
              const {username,password} = this.state
              alert(
                  `用户名：${username}, 密码：${password}`
              ) 
          }

      }
      ReactDOM.render(<Login/>,document.getElementById('test'))
```

3.在对象中，我们给对象的属性赋值有两种方式，假如我想给一个Person对象赋值一个属性，属性名字叫name而其中的value值是张三

（1）第一种赋值方式，直接用对象.加上属性名的方式给对象添加属性。

```javascript
let Person = {}
Person.name="张三"
```

注意如果有一个字符串变量叫name，用.的方式的话就会失效！

```javascript
let a='name'
Person.a="张三"//这样就会变成Person里有个属性a，这个属性的值为张三
```

（2）第二赋值属性的方式，使用中括号，这种方式可以读取变量作为属性的名称

```javascript
Person['name']='张三'
//等价于
let a = 'name'
Person[a]='张三'
```

所以这里也是上面的type要加**中括号**的原因！
