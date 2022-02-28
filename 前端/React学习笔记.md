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

##### 不使用高级函数和柯里化

我们研究一下JSX或者说reac中标签里onChange后面跟的东西，首先跟着的必须是一个函数，但是如果是传统写法即函数名加上()的话就会直接调用，使用传统方式的话必须不能加括号，这就导致了不能传递type的值。

如果使用箭头函数，因为箭头函数写出来并不是调用的，在箭头函数的函数体内部写一个统一的处理data的函数，该函数接收event和type做参数，则就可以解决问题了。

代码如下：

```react
用户名：<input type="texnCht" onChange={event => this.saveFormData(event, "username")} /><br />
密码：<input type="password" onChange={event => this.saveFormData(event, "password")} /><br />
```

同时saveFormData函数如下所示：

```javascript
saveFormData = (event, type) => {
       this.setState({ [type]: event.target.value})
}
```

这样就解决了，既没有返回一个函数，又没有以函数作为参数。

## 组件的生命周期

### 旧生命周期

#### 图示

![QQ20220223152421.jpg](https://img.pterclub.com/images/2022/02/23/QQ20220223152421.jpg)

简而言之，在render函数执行的前后阶段react会自动调用一些函数，只不过我们没有写的话就默认是没有函数体的函数。

比如componentWillMount就是在render之前要执行的，那个函数的意思就是组件将要挂载时执行。

#### 例子

假设现有一个需求，要实现页面上的一段文字渐变成透明的，并且还有一个按钮，点击按钮之后组件就卸载并且消失。

渐变可以通过定时器循环执行来递减文字的透明度，但是这个递减过程放在哪里比较关键，不能放在render中。

```react
<script type="text/babel">
    class Life extends React.Component {
        state = {
            opacity:1
        }
        render() {  // 1+n次，随着状态改变即调用
            console.log('render');
            const {opacity} = this.state
            return (
                <div>
                    <h1 style={{opacity}}>分手了怎么办？</h1>
                    <button onClick={this.death}>不活了</button>
                </div>
            )
        }
        componentDidMount(){ // 1次
            console.log('componentDidMount');
            this.timer = setInterval(() => {
                //1.获取原来的opacity
                let {opacity} = this.state
                //2.递减
                opacity -= 0.1
                if(opacity <= 0) opacity = 1
                //3.赋回去
                this.setState({opacity})
            }, 200);
        }
        componentWillUnmount(){ // 1次
            console.log('componentWillUnmount');
            clearInterval(this.timer)
        }
        death = ()=>{
            ReactDOM.unmountComponentAtNode(document.getElementById('test'))
        }
    }
    ReactDOM.render(<Life />, document.getElementById('test'))
</script>
```

componentWillUnmount()是将要卸载时执行的函数，componentDidMount()是已经挂载完毕后执行的函数，这些生命周期函数（钩子函数）都仅执行一次。

#### 总结钩子函数

1.初始化阶段：由ReactDOM.render()触发 --- 初次渲染
      （1） constructor()
      （2）componentWillMount()（**在新版本中被不推荐使用了**）
      （3）render()
      （4）componentDidMount()，重要，比如开启定时器、发送ajax请求、消息订阅等等

2. 更新阶段：由组件内部this.setState()或父组件重新render触发
      （1） shouldComponentUpdate()
      （2）componentWillUpdate()也比较重要，主要做一些收尾的事情，例如关闭定时器。（**在新版本中被不推荐使用了**）
      （3）render()，老大哥地位！
      （4）componentDidUpdate()
3. 卸载组件：由ReactDOM.unmountComponentAtNode()触发
     （1）componentWillUnmount()（**在新版本中被不推荐使用了**）

#### 注意点

1.render函数会执行**1+n**次，其中的1表示一上来就会调用1次，n次表示如果组件里的state改变了，那就会render一次。

2.透明度递减函数不能放在render里，因为会递归调用很多很多次，会导致页面**频繁渲染**。放在构造器里虽然可行但是并不是正确的放置方式。正确的放置位置应在钩子函数中即组件的生命周期函数中。

3.shouldComponentUpdate可以看做是组件更新的一个**阀门**，该函数返回为**true**时，组件才能**继续更新**否则组件不会更新。不过forceUpdate()可以**绕过钩子**，强制更新

4.阀门关闭之后，调用setState()只是不render但是内部的state值还是会**根据具体setState()函数进行修改调整**。如果强制更新的话，会直接更新为最新的state值。

5.componentWillReceiveProps表示的是父组件给子组件传props参数时在子组件中调用的函数，并且只有在父组件**第二次及以上调用**render时才会调用这个函数，父组件**第一次调用render时并不会自动调用这个钩子函数**。

### 新生命周期

从react17.0之后就是新生命周期了，但是依然可以用旧钩子，不过并不推荐，在18.0版本及以后，旧钩子必须加上UNSAFE_前缀才能正常奏效工作了。（此处添加UNSAFE与安全性并无直接关系，而是表示使用这些生命周期的代码在React的未来版本中有可能出现bug，尤其是在启用异步渲染之后） 

componentWillMount()，componentWillUpdate()，componentWillUnmount()

![QQ20220223163500.jpg](https://img.pterclub.com/images/2022/02/23/QQ20220223163500.jpg)

官网上，把不常用的钩子函数去掉之后的生命周期图如下所示：

![QQ20220223191927.jpg](https://img.pterclub.com/images/2022/02/23/QQ20220223191927.jpg)

因为新生命周期中，getDerivedStateFromProps和getSnapshotBeforeUpdate很少用。

getDerivedStateFromProps可以接收到props，然后可以由props派生状态以及值并且更新原有的state值，通过return状态对象的方式。使用这个方法之后，setstate和初始化等改变状态的方法都不管用了，最终还是以getDerivedStateFromProps的return的状态对象为准。
使用这个函数的场景是：**当组件中的state完全取决于外部传来的props时。** 
简单来说<u>没锤子用</u>。

getSnapshotBeforeUpdate用的也很少，所以就不多介绍了。

# React脚手架

## 有关概念

1.xxx脚手架：用来帮助程序员快速创建一个基于xxx库的模板项目

（1）包含了所有需要的配置（语法检查、jsx编译、devServer...）

（2）下载好了所有相关的依赖

（3）可以直接运行一个简单效果

2.react提供了一个用于创建react项目的脚手架库：create-react-app

3.项目的整体技术架构为：react+wbpack+es6+eslint

4.使用脚手架开发的项目的特点：模块化、组件化、工程化

## 有关命令

### 创建项目并启动

1.全局安装：npm install -g create-react-app

2.切换到想创项目的目录：使用命令：create-react-app hello-react

3.进入项目文件夹：cd hello-react

4.启动项目：npm start

### 官方项目目录分析

![QQ20220223213759.jpg](https://img.pterclub.com/images/2022/02/23/QQ20220223213759.jpg)

1.分析示例代码可以得到以下信息
（1）所有组件都当做是App组件的孩子，这样渲染组件的时候只需要渲染App即可
（2）使用了大量的模块化语句进行编写，使用了默认暴露
（3）reportWebVitals主要用于分析网页性能
（4）App组件外层包了一对<React.StrictMode></React.StrictMode>用于将代码开启react的严格模式，只要写了不被建议的写法，就会飘红报错！学的时候我们并不开启
（5）setupTests.js主要用于单元测试
（6）index.js是webpack打包的入口，而App.js是react的App根组件，这两个js文件是我们最需要关注的两个文件。
（7）App.test.js也是做测试用的，不推荐使用了。
（8）robots.txt，爬虫协议文件，用于说明哪些爬虫可以获取，哪些是爬虫无法获取的
2.他的id为root的div是写在index.html内，下面是对该html的一些分析
（1）<link rel="icon" href="%PUBLIC_URL%/favicon.ico" />这一行中的href后面跟了%PUBLIC_URL%，**表示的是public文件夹路径**，该写法仅在react脚手架中奏效。
（2）<meta name="viewport" content="width=device-width, initial-scale=1" />是在开启理想视口，一般用于移动端网页的开发（后期会详细讲解）
（3）<meta name="theme-color" content="#000000" />主要是调整浏览器地址栏的颜色，仅用于调整原生安卓手机上浏览器的地址栏颜色。**很鸡肋不用太管**。

![QQ20220223212544.jpg](https://img.pterclub.com/images/2022/02/23/QQ20220223212544.jpg)
![QQ20220223212536.jpg](https://img.pterclub.com/images/2022/02/23/QQ20220223212536.jpg)

（4）meta name="description"主要用于描述网页，主要用于提供给爬虫
（5）    <link rel="apple-touch-icon" href="%PUBLIC_URL%/logo192.png" />ios系统中网页添加到桌面后的图标
（6）<link rel="manifest" href="%PUBLIC_URL%/manifest.json" />用于加壳的，给网页加个壳，然后当做app发布（ios和安卓都有），其实质上就是一个网页。而manifest主要用于配置一些加壳后的app的一些特征，比如开启app后的要显示的图片
（7）<noscript>标签里的内容在浏览器不支持js时会显示出来

### 功能界面的组件化编码流程

1.拆分组件：拆分界面（拆组件的原则：按功能点拆分并且适于取名），抽取组件

2.实现静态组件：使用组件实现静态页面效果

3.实现动态组件

（1）动态显示初始化数据

​			①先思考数据是什么类型

​			②数据名称

​			③保存在哪个组件？比如有一个状态数据A组件用，B组件也用，C组件也用，那么就适合放在A,B,C共同的父亲组件里（还没学高级组件通信时），即状态提升

（2）交互（从绑定事件监听开始）

### 天气案例

首先把官方案例不需要的文件都删了，只留下的文件结构如图所示：

![QQ20220224110337.jpg](https://img.pterclub.com/images/2022/02/24/QQ20220224110337.jpg)

App.jsx，根组件名称

```react
import React, {Component} from 'react';
import Weather from "./components/Weather";
export default class App extends Component {
    render() {
        return (
            <div>
                <Weather/>
            </div>
        );
    }
}
```

Weather.jsx

```react
import React, {Component} from 'react';
export default class Weather extends Component {
    state={
        isHot:true
    }
    changeWeather = ()=>{
        const {isHot} = this.state
        this.setState({isHot:!isHot})
    }
    render() {
        return (
            <div>
                <h1>今天天气很{this.state.isHot ? '炎热':'凉爽'}</h1>
                <button onClick={this.changeWeather}>切换天气</button>
            </div>
        );
    }
}
```

index.js，该文件主要作为入口文件使用

```react
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

ReactDOM.render(<App />, document.getElementById('root'));
```

index.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <link rel="icon" href="%PUBLIC_URL%/favicon.ico" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <meta name="theme-color" content="#000000" />
    <meta
      name="description"
      content="Web site created using create-react-app"
    />
    <link rel="apple-touch-icon" href="%PUBLIC_URL%/logo192.png" />
    <link rel="manifest" href="%PUBLIC_URL%/manifest.json" />
    <title>React App</title>
  </head>
  <body>
    <noscript>You need to enable JavaScript to run this app.</noscript>
    <div id="root"></div>
  </body>
</html>
```

### todolist案例

#### 代码部分

1.app.jsx

```react
import React, { Component } from 'react'
import Add from './components/Add'
import List from './components/List'
import Footer from './components/Footer'
import './App.css'

export default class App extends Component {
  //初始化状态，因为Add要用todos(添加)，List也要读取数据
  state = {
    tasklist: [
      { id: '001', name: '抽烟', done: true },
      { id: '002', name: '喝酒', done: false },
      { id: '003', name: '烫头', done: false },
    ]
  }
  add = (newtask)=>{
    const {tasklist} = this.state
    this.setState({tasklist:[newtask, ...tasklist]})
  }
  delete = (id)=>{
    const {tasklist} = this.state
    const newList = tasklist.filter((todoObj)=>{
      return todoObj.id !== id
    })
    this.setState({tasklist:newList})
  }  
  update = (id,done)=>{
    const {tasklist} = this.state
    const newList = tasklist.map((todoObj)=>{
      if(todoObj.id === id) todoObj.done = done
      return todoObj
    })
    this.setState({tasklist:newList})
  }
  checkAbove = (done)=>{
    const {tasklist} = this.state
    const newList = tasklist.map((todoObj)=>({...todoObj,done}))
    this.setState({tasklist:newList})
  }
  clearDone = ()=>{
    const {tasklist} = this.state
    const newList = tasklist.filter((todoObj)=>{
      return !todoObj.done
    })
    this.setState({tasklist:newList})
  }
  render() {
    return (
      <div className="todo-container">
        <div className="todo-wrap">
          <Add add={this.add}/>
          <List 
            todos={this.state.tasklist} 
            deleteItem={this.delete}
            updateItem={this.update}
          />
          <Footer
            todos={this.state.tasklist}
            checkAbove={this.checkAbove}   
            clearDone={this.clearDone}        
          />
        </div>
      </div>
    )
  }
}
```

2.Add组件

```react
import React, { Component } from 'react'
import { v4 as uuidv4 } from 'uuid';
import './index.css'
export default class Add extends Component {
  handleKeyUp = (event)=>{
    if(event.keyCode === 13){
      if(event.target.value.trim() === ''){
        alert('输入内容不能为空')
      } else {
        const todoObj = {
          id: uuidv4(),
          name: event.target.value,
          done: false,
        }
        this.props.add(todoObj)
        event.target.value = ''
        
      }
    }
  }
  render() {
    return (
      <div className="todo-header">
        <input type="text" onKeyUp={this.handleKeyUp} placeholder="请输入你的任务名称，按回车键确认" />
      </div>
    )
  }
}
```

3.Footer组件

```react
import React, { Component } from 'react'
import './index.css'
export default class Footer extends Component {
  checkAll = (event)=>{
    this.props.checkAbove(event.target.checked)
  }
  clearAllDone = ()=>{
    if(window.confirm('确定删除全部已完成的任务吗？')){
      if(this.props.todos.length > 0){
        this.props.clearDone()
      } else {
        alert('抱歉，没有可删除的任务')
      }
    }
  }
  render() {
    const {todos} = this.props
    const doneCount = 
      todos.reduce((preValue,current)=>{
        return preValue + (current['done'] === true ? 1 : 0)
      },0)
    const all = todos.length
    return (
      <div className="todo-footer">
        <label>
          <input
           type="checkbox"
           checked={all === doneCount && all > 0}
           onChange={this.checkAll}/>
        </label>
        <span>
          <span>已完成{doneCount}</span> / 全部{all}
        </span>
        <button className="btn btn-danger" onClick={this.clearAllDone}>清除已完成任务</button>
      </div>
    )
  }
}
```

4.Item组件

```react
import React, { Component } from 'react'
import './index.css'
export default class Item extends Component {
  state = {mouseIsEnter:false}
  handleMouse = (mouseIsEnter)=>{
    return ()=>{
      this.setState({mouseIsEnter})
    }
  }  
  handleDelete = (id)=>{
    return () => {
      if(window.confirm('确定删除吗？')){
        this.props.deleteItem(id)
      }
    }
  }
  handleCheck = (id)=>{
    return (event) =>{
      this.props.updateItem(id,event.target.checked)
    }
  }
  render() {
    const {id, name, done} = this.props
    const {mouseIsEnter} = this.state
    return (
      <li 
        onMouseEnter={this.handleMouse(true)} 
        onMouseLeave={this.handleMouse(false)}
        className={mouseIsEnter? 'active' : ''}
      >
        <label>
          <input
           type="checkbox"
           checked={done} 
           onChange={this.handleCheck(id)} />
          <span>{name}</span>
        </label>
        <button 
          className="btn btn-danger" 
          style={{ display: mouseIsEnter ? "block" : "none" }}
          onClick={this.handleDelete(id)}
        >删除</button>
      </li>
    )
  }
}
```

5.List组件

```react
import React, { Component } from 'react'
import Item from '../Item'
import "./index.css" 
export default class List extends Component {
  render() {
    const {todos,deleteItem,updateItem} = this.props
    return (
      <ul className="todo-main">
        {
          todos.map((todoObj,index)=>{
            return <Item 
              key={todoObj.id} 
              index={index}
              {...todoObj}
              deleteItem={deleteItem}
              updateItem={updateItem}
            />
          })
        }
      </ul>
    )
  }
}
```

#### 注意事项

1.组件拆分后可以按照文件夹划分，在文件夹中可以默认创建index.js和index.css等，当引入时不指定文件夹里的哪个js，那么react就会**默认引用**index.js。

2.【父组件】给【子组件】传递数据使用props传递

【子组件】给【父组件】传递数据：通过props传递，要求父组件提前给子组件传递一个函数

【兄弟组件】之间通信可以借助共同的父亲

3.JSX标签里的一些onClick或者onChange属性值后面跟的函数一旦要传数据进去，那么这个函数就得写成**高阶函数**+**箭头函数**的形式，即函数的返回值又是一个函数。

![QQ20220224214140.jpg](https://img.pterclub.com/images/2022/02/24/QQ20220224214140.jpg)

4.reduce函数复习：
arr.reduce((preValue, current, index, arr)=>{},initialValue)
		arr: 当前操作的数组。
		preValue:第一次执行回调时为给定的初始值initialValue,以后是上一次执行回调的返回值。
		备注：若没有传入initialValue，则第一次的preValue值是数组中第一个元素的值。
		current: 表示当前正在处理的元素。
		index：表示当前正在处理的数组元素的索引，若传入了initialValue值，则为0，否则为1。
		array: 当前操作的数组（就是arr）。
		initialValue： 表示初始值，一般做数学运算时设置为0，若筛选最值可以不传。

```javascript
<script type="text/javascript">
    let person = [
      { id: "001", name: "Tom", age: "16" },
      { id: "002", name: "John", age: "17" },
      { id: "003", name: "Rechael", age: "18" },
      { id: "004", name: "Hank", age: "19" },
    ]
    let arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

    //reduce 可以进行累加/累乘
    const result =
      arr.reduce((preValue, current, index, arr) => {
        console.log(
          'preValue:', preValue,
          '| current：', current,
          '| index:', index,
          '| arr:', arr
        );
        return preValue + current
      })
    console.log(result); // 55

    //reduce 可以进行条件求和
    const result2 =
      arr.reduce((preValue, current) => {
        return preValue + ( current % 2 == 0 ? current : 0)
      },0)
    console.log('数列偶数之和为',result2);
    
    //reduce 可以进行条件统计
    const result3 =
      arr.reduce((preValue, current) => {
        return preValue + ( current % 2 !== 0 ? 1 : 0)
      },0)
    console.log('数列奇数个数为',result3,'个');

    //reduce 可以筛选最值
    const result4 =
      arr.reduce((preValue, current) => {
        return Math.max(preValue,current)
      })
    console.log('数列最大值为',result4);
  </script>
```

5.在JSX中，箭头函数只有一个语句，即返回语句且返回的是一个对象时，简写时**不能用花括号**，使用花括号会被当成**函数体**，应该在花括号外面加一层**小括号**即可！

```javascript
todos.map((todoObj)=>({...todoObj,done}))
```

6.defaultchecked只能执行一次（<u>适合用于勾选框不会改变的情形</u>）。

**写了checked就必须要写onchange**！因为数据状态驱动着页面。总结下来就是onchange**不能配合**defaultChecked使用。

7.爷爷组件想给孙子组件传函数的话，现在必须得通过父亲组件来传，但是以后有新的解决办法！

## 跨域问题

### 定义及发生时机

1.定义和发生实际：

只要http（对应不同的是https），ip地址，端口号不同，就会产生跨域，但仅限于在**浏览器端**借助Ajax（也就是xhr）发送请求给**服务器**。

注意跨域问题只会导致浏览器无法获得数据但是**发送请求是可以正常发送**的，服务器也能接受到这个请求。

2.特殊情况：

（1）服务器与服务器之间不同源且互相请求时不会产生跨域问题

（2）使用form表单请求时不会产生跨域问题，因为form表单不是通过xhr实现的。

### 如何解决问题

在react脚手架中有以下几种方式

1.jsonp
2.cor
3.借助代理：原理是借助代理，代理与目标服务器之间是**服务器与服务器之间**的对话，所以不会有跨域问题，若是浏览器与服务器之间的交互，则会有跨域问题。

#### 第一种方式，直接在package.json中追加一行配置

在package.json中追加如下配置（端口号是目标服务器的端口号）：

```json
"proxy":"http://localhost:5000"
```

 请求的地址改为本地地址+目标后缀

```javascript
url:'http://localhost:3000/students',
method:'GET'
```

 说明：

1. 优点：配置简单，前端请求资源时可以不加任何前缀
  2. 缺点：**不能配置多个代理**。
  3. 工作方式：上述方式配置代理，当用Ajax请求了3000不存在的资源时，该请求会转发给5000（如果3000存在资源，则优先匹配前端资源，localhost:3000 即是public路径）

#### 第二种方式，编写setupProxy.js配置具体代理规则

1.需要安装http-proxy-middleware插件，使用npm安装即可

2.编写setupProxy.js配置具体代理规则：

```js
const {createProxyMiddleware} = require('http-proxy-middleware')

module.exports = function(app) {
  app.use(
    createProxyMiddleware( 
      '/api1', // 只要/api 开头的请求，才转发给后端服务器
      {
        target:'http://localhost:5000',
        changeOrigin:true, // 控制服务器接收到的请求头中host字段的值
          // false(默认值)：服务器请求来自于原地址 localhost:3000
          // true：服务器请求来自于5000（请求目标地址），可迷惑目标服务器
        pathRewrite:{'^/api1':''} // 重写路径（目的：去掉api前缀）
      }),
    createProxyMiddleware( 
      '/api2',
      {
        target:'http://localhost:5001',
        changeOrigin:true, 
        pathRewrite:{'^/api2':''} 
      })
  )
}
```

**额外说明**：

​	pathRewrite可以**覆盖替换**用于标识该地址是用于转发的部分。

​		举个例子：假如有个一个腾讯的api，这个腾讯api的位置是（不关注地址）/OCR_text，现在我本地想请求这个api，我需要给它做个标识，我请求的可能就是	http://localhost:3000/tx/OCR_text，这个时候脚手架知道/tx开头的都需要转发给腾讯的api地址，但是如果不加pathRewrite的话，直接转发到腾讯服务器的就	是/tx/OCR_text，但是正确的地址应该是/OCR_text，那这个时候就出现问题了；使用pathRewrite就可以把前面的/tx去掉，然后正常访问腾讯的api地址。



(提示：目前的场景是3000通过代理去跨域请求5000里的数据）

changeOrigin:true加了之后，服务器收到的请求头中的host是localhost:5000，设置为     	false时，请求头收到的就是**原来的地址**localhost:3000。
	changeOrigin默认值为false但我们**一般把它设置为true**，可以撒谎欺骗5000即请求服务器。

#### 注意事项

1.在脚手架中，会自动处理浏览器访问不存在资源时的情况：如果要访问的资源不存在（通过浏览器中输入资源地址访问时），脚手架会自动重定向去index.html。如果是ajax请求不存在的地址，那么会正常地显示404错误，

2..在react脚手架里，public文件夹就是http://localhost:3000的根目录，访问http://localhost:3000/a.jpg就等于在访问public下的a.jpg。所以会出现问题，如果前端地址里有这个资源并且后端地址也有这个资源，那么代理不生效，ajax会自动取到本地也就是前端地址的资源。

## 消息订阅机制

通过消息订阅机制可以解决兄弟组件之间通信需要通过父亲组件的问题 。消息订阅机制可以适用于**任意两个组件**之间的通信。

### 安装以及使用

我们这里使用pubsub消息订阅插件

1.首先安装这个插件

```shell
npm install pubsub-js
```

2.先订阅再发布。需要接收信息的组件是订阅方，需要传送数据出去的组件是发布方。

```js
PubSub.publish('status',data)
this.msgis = PubSub.subscribe('status',函数(_,data))
PubSub.unsubscribe(this.msgid) // 取消订阅
```

### github搜索用户名案例

项目结构如下

![QQ20220225182703.jpg](https://img.pterclub.com/images/2022/02/25/QQ20220225182703.jpg)

1.App.jsx

```js
import React, { Component } from 'react'
import Search from './components/Search'
import List from './components/List'
export default class App extends Component {
  render() {
    return (
      <div className="container">
        <Search/>
        <List/>
      </div>
    )
  }
}
```

2.Search组件

```react
import React, {Component} from 'react';
import axios from 'axios'
import PubSub from 'pubsub-js'
export default class Search extends Component {
    keyWordContainer = React.createRef()
    //通过createRef来使用Ref
    search = ()=> {
        // 1. 获取用户输入
        const {value} = this.keyWordContainer.current
        // 2. 校验数据
        if(!value.trim()) return alert('please input a word')
        // this.props.updateAppState({isFirst:false, isLoading:true})
        PubSub.publish("user_date_of_github",{isFirst:false, isLoading:true})

        // 3. 发送请求获取数据
        axios.get(`https://api.github.com/search/users?q=${value}`).then(
            response => {
                const {items} = response.data
                // 请求成功后，通知app存储用户数据, 更改isLoading
                // this.props.updateAppState({users:items, isLoading:false})
                PubSub.publish("user_date_of_github",{users:items, isLoading:false})
            },
            error => {
                console.log(error);
                // 请求失败后，存储错误信息、将isLoading变为false
                // 注意：此处的error是一个对象，真正的错误信息在error.message
                // this.props.updateAppState({errorMsg:error.message, isLoading:false})
                PubSub.publish("user_date_of_github",{errorMsg:error.message, isLoading:false})
            }
        )
    }
    render() {
        return (
            <section className="jumbotron">
                <h3 className="jumbotron-heading">Search Github Users</h3>
                <div>
                    <input type="text" ref={this.keyWordContainer} placeholder="enter the name you search"/>&nbsp;
                    <button onClick={this.search}>Search</button>
                </div>
            </section>
        )
    }
}
```

3.List组件

```react
import React, {Component} from 'react';
import PubSub from 'pubsub-js'
export default class List extends Component {
    state = {
        users:[],
        isFirst:true,
        isLoading:false,
        errorMsg:''
    }
    componentDidMount() {
        //这个组件一挂载完毕就开始订阅
        this.pub_id = PubSub.subscribe('user_date_of_github',(_,data)=>{
            this.setState(data)
        })
    //    data前面必须有一个顶位的标识，因为消息发布传过来给回调函数的参数是(msg,data)，
    //    所以第二个参数才是data
    }

    componentWillUnmount() {
        PubSub.unsubscribe(this.pub_id)
    }
    render() {
        const {isFirst,isLoading,errorMsg,users} = this.state
        return (
            <div className="row">
                {
                    isFirst ? <h1>Welcome!</h1> :
                        isLoading ? <h1>正在加载</h1> :
                            errorMsg ? <h1>{errorMsg}</h1> :
                                users.map((userObjs)=>{
                                    // 函数体
                                    return (
                                        <div className="card" key={userObjs.id} style={{width:"100px"}}>
                                            <a href={userObjs.html_url} target="_blank" rel="noreferrer">
                                                <img alt='avatar' src={userObjs.avatar_url} style={{width:'100px'}} />
                                            </a>
                                            <p className="card-text">{userObjs.login}</p>
                                        </div>
                                    )
                                })
                }
            </div>
        )
    }
}
```

#### 注意事项

1.react脚手架会预先检查通过ES6引入的CSS里的所有资源**哪怕没用到**，只要没找到其中某一个资源，它就会**报错**。如果是引入第三方的css库，建议放到public中，在index.html中通过link的形式引入css库。 

2.三元表达式可以嵌套使用。

3.对象是**不可以直接**在react中显示的，会报错：

![QQ20220225153808.jpg](https://img.pterclub.com/images/2022/02/25/QQ20220225153808.jpg)

![QQ20220225153824.jpg](https://img.pterclub.com/images/2022/02/25/QQ20220225153824.jpg)

## React路由

这里主要介绍的是六代路由了，npm install react-route-dom默认安装的是六代路由。

官方在这里更推崇函数式组件！函数式组件里this的残疾现象被hooks改进了，这个部分会在后面详细介绍。

### 概念理解

#### SPA

SPA指的是Single Page Web Application SPA，整个应用只有**一个完整的页面**，点击页面中的链接**不会刷新**页面，只会做页面的**局部更新**，数据都需要通过ajax请求获取，并在前端**异步**展现。

#### 路由

1.何为路由？

​	一个路由就是一个映射关系（key:value），key为路径，value可能是element（element里可以有component或者Navigate）

2.路由分类：

（1）后端路由：

​	value 是 function, 用来处理客户端提交的请求。

​	工作过程：当node接收到一个请求时，根据请求路径找到匹配的路由，调用路由中的函数来处理请求，返回响应数据。

（2）前端路由

浏览器端路由，value是component，用于展示页面内容。可以使用Route路由组件实现或者使用路由表实现。

### 路由使用的原则

1.明确好界面中的导航区、展示区。

2.按照实际需求将a标签改为Link或者NaviLink路由组件（即 **编写路由链接**）

3.展示区写Route标签或者在路由表里写好对应的路径之后通过Outlet插槽组件来显示（即 **注册路由**）。

4.<App/>组件外部应当包裹一个`<BrowserRouter>`或`<HashRouter>`

### NavLink和Link

1.NavLink和Link都可以实现编写路由链接的过程，区别是NavLink可以更加自由地控制点击后该标签的class的内容，比如点击后class中多一个active属性或者其他的属性值。

```js
<NavLink className={({isActive}) => {
    return isActive ? "list-group-item atcsq" : "list-group-item"
}} to="/home">Home</NavLink>
```

注意这里接受的是一个对象，点击NavLink后，NavLink会给回调函数传一个对象{isActive:true}，所以接收参数的时候要注意！

2.Link组件写法类似

```js
<Link children={m.title} to={"details"}/>
```

### Navigate

该组件主要是用于重定向，Navigate只要被渲染就会修改路径从而导致视图的切换。

```js
<Navigate to={"/About"}/>
```

### Route和Routes

1.Route和Routes必须搭配使用，且必须使用Routes包裹Route，这样在匹配路由的时候，一旦匹配到响应的路由，react就不会继续往下匹配了，提高了效率

2.Route是用于注册路由，写了Route的地方，在路由链接被点击的时候，Route组件就会被替换成Route里element里面的组件。

```react
<Routes>
    <Route path="/about" element={<About/>}/>>
	<Route path="/home" element={<Home/>}/>>
	<Route path={"/"} element={<Navigate to={"about"} />}/>
    {/*用于重定向的Navigate，Navigate还可以写replace属性，写上了之后就是replace模式*/}
</Routes>
```

### 路由表和嵌套路由

#### 路由表

使用路由表对路由进行统一管理会比较方便。

假如我们想把上述路由转换成路由表的形式的话：

我们需要使用到**useRoutes**这个模块，然后我们可以把路由写在另一个路由文件中以默认方式暴露

我们在src目录下创建routes文件夹，再在routes文件夹中创建index.js

```js
import About from "../pages/About";
import Home from "../pages/Home";
import News from "../pages/News";
import Details from "../pages/Details";
import Message from "../pages/Message";
import {Navigate} from "react-router-dom";
import React from "react";
export default [
    {
        path:'/about',
        element:<About/>
    },
    {
        path:'/home',
        element:<Home/>,
        children:[
            {
                path:'news',
                element:<News/>
            },
            {
                path:'message',
                element: <Message/>,
                children:[
                    {
                        path:'details',
                        element:<Details/>
                    }
                ]

            }
        ],
    },
    //    用于重定向的route
    {
        path:'/',
        element:<Navigate to={"/About"}/>
    },
    {
        //这里用于home组件内部的重定向，默认转到home组件后转到news
        path:'/home/',
        element: <Navigate to={"/home/news"}/>
    }
]
```

回到需要使用路由表的App.js，引入useRoutes后，往useRoutes传入路由数组（即 src/routes/index.js中默认暴露的内容），接收为变量后，写在原先Routes的位置。

```react
import React from 'react';
import {NavLink,useRoutes} from "react-router-dom";
import routes from "./routes"
import Header from "./pages/Header";
export default function App(props) {
    //路由表，写在routes文件夹下了
    const routes_table = useRoutes(routes)
    return (
        <div>
            <div className="row">
                <Header/>
            </div>
            <div className="row">
                <div className="col-xs-2 col-xs-offset-2">
                    <div className="list-group">
                        {/*<NavLink className="list-group-item" to="/about">About</NavLink>*/}
                        {/*<NavLink className="list-group-item " to="/home">Home</NavLink>*/}
                        {/*NavLink在被点击的时候自动给自己加上active类名，如果想实现自定义的话，
                        需要把className写成一个函数，函数接受的就是一个对象，即{isActive:true}*/}
                        {/*这里atcsq就是我自己自定义的样式*/}
                        <NavLink className={({isActive}) => {
                            return isActive ? "list-group-item atcsq" : "list-group-item"
                        }} to="/home">Home</NavLink>
                        <NavLink className={({isActive}) => {
                            return isActive ? "list-group-item atcsq" : "list-group-item"
                        }} to="/about" children={"About"}/>
                    </div>
                </div>
                <div className="col-xs-6">
                    <div className="panel">
                        <div className="panel">
                                {routes_table}
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    );
}
```

#### 嵌套路由

假如home路径下还有嵌套路由，可以在路由表里以children的形式呈现出来。

不过要注意：嵌套路由需要使用<Outlet/>组件将需要呈现的位置标注出来，因为我们都在路由表里写好了路由，那么在页面的哪个位置安放组件是需要我们指出的。

比如下面Message组件就是使用<Outlet/>指出Details组件要出现的位置。

```react
import React,{useState} from 'react';
import {Link,Outlet,useNavigate} from "react-router-dom";
export default function Message(props) {
    //使用useNavegate可以实现编程式路由，即通过编程来触发路由的跳转，
    // 而不一定非得通过用户点击来触发路由
    const Navigate = useNavigate()
    const [messages]=useState([
        {id:"001",title:"消息一",content:"我爱你中国"},
        {id:"002",title:"消息二",content:"亲爱的母亲"},
        {id:"003",title:"消息三",content:"我为你自豪"}
    ])


    function showDetail(m){
        //实现了编程式路由，同时还可以通过state方式来传递参数
        Navigate('details',{
            replace:false,
            state:m
        })
    }
    return (
        <div>
            <ul>
                {
                    messages.map((m)=>{
                        return (
                            <li key={m.id}>
                                <Link children={m.title} to={"details"} state={m}/>
                                <button onClick={()=>{showDetail({...m})}}>查看</button>
                            {/*    state里等价于state={{id:m.id,title:m.title,content:m.content}}*/}
                            </li>
                        )
                    })
                }
            </ul>
            <Outlet/>
        {/*    指出组件呈现的位置*/}
        </div>
    );
}
```

#### 解决样式丢失问题

在二级或者嵌套路由可能会出现样式丢失的问题，为了避免这个问题，

我们需要把index.html中引入的css写成/xxx的格式，不要写成./xxx的格式。

也可以使用%PUBLIC_URL%。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>路由实现</title>
  <link rel="icon" href="%PUBLIC_URL%/favicon.ico">
  <link rel="stylesheet" href="/bootstrap.css">
  <style>
    .atcsq{
      background-color: #c7254e !important;
      color: #4cae4c !important;
    /*  可以通过!important来将样式优先级提升到最高为了避免被bootstrap样式覆盖的情况*/
    }
  </style>
</head>
<body>
  <div id="root"></div>
</body>
</html>
```

#### 编程式路由

之前我们进行路由跳转都是需要用户点击路由再进行跳转，如何用编程实现跳转呢？

比如我想实现一个功能，在一个页面展示5秒后自动跳转到另一个页面。

这时我们需要使用**useNavigate**组件。

在函数体内部使用 const Navigate = useNavigate()接收变量之后:

Navigate(1)命令式前进1个页面，Navigate(-1)就是退后一个页面。

```js
Navigate('路径',{
	replace:false,
    state:{xxxxx}
})
```

上面的命令就是跳转到指定路径后并且携带上state属性值。

#### 给路由传递参数

这里只介绍使用state传递

在六代里非常方便，只需在Link或者NaviLink组件中多写一个state属性即可：

```react
<Link children={m.title} to={"details"} state={{id:"002",title:"消息一",content:"我爱你中国"}}/>
```

下一级路由接收state参数时需要使用useLocation组件

```react
import React from 'react';
import {useLocation} from "react-router-dom";
export default function Details(props) {
    //使用useLocation来读取路由通过state传递过来的信息
    //这里使用解构赋值
    const {id,title,content} = useLocation().state
    return (
        <div>
            <ul>
                <li>消息编号：{id}</li>
                <li>消息名称：{title}</li>
                <li>消息内容：{content}</li>
            </ul>
        </div>
    );
}
```

#### BrowserRouter与HashRouter的区别

1. 底层原理不一样：

- BrowserRouter使用的是H5的history API，不兼容IE9及以下版本。
- HashRouter使用的是URL的哈希值

2. path表现形式不一样

- BrowserRouter的路径中没有#
- HashRouter的路径包含#

3. 刷新对路由state参数的影响

- （1）BrowserRouter无影响，因为state保存在history对象中
- （2）HashRouter刷新后会导致路由state参数的丢失！！！

4. 备注：HashRouter可以用于解决一些路径错误相关的问题。

# ReactUI组件库

​	这里主要介绍antd，除了antd外还有ElementUI for react和vant（专门用于移动端开发）。

## ant-design

​	蚂蚁金服开发的用于react的UI组件库。

​	官方网址：[Ant Design - 一套企业级 UI 设计语言和 React 组件库](https://ant.design/index-cn)

### 使用方法

​	首先先在脚手架里安装该模块。

```bash
npm install antd
```

​	随后在使用过程中不仅要引入模块，也要引入对应的样式

```js
import {Button} from 'antd';
import 'antd/dist/antd.css';
```

​	具体各个组件的样式和使用方法可以参考官网：[组件总览 - Ant Design](https://ant.design/components/overview-cn/)

这里以Button为例：

```react
import React from 'react';
import {useNavigate} from "react-router-dom";
import {Button} from 'antd';
import 'antd/dist/antd.css';
//不仅要引入组件，而且还要引入样式
export default function Header(props) {
    const Navigate = useNavigate()
    return (
            <div className="col-xs-offset-2 col-xs-8">
                <div className="page-header"><h2>React Router Demo</h2></div>
                &nbsp;&nbsp;&nbsp;
                <Button type="primary" onClick={()=>{Navigate(1)}}>前进</Button>
                {/*通过Navigate(1)来实现前进和后退*/}
                &nbsp;
                <Button type="primary" danger onClick={()=>{Navigate(-1)}}>后退</Button>
            </div>
    );
}
```

### 按需引入组件

[在 create-react-app 中使用 - Ant Design](https://3x.ant.design/docs/react/use-with-create-react-app-cn)参考这篇文章里的高级配置一栏。

​	直接引入antd.css可能会太大，如果想要继续优化的可以采用按需引入的方式，但是需要暴露脚手架的默认配置（暴露的行为是不可逆的）。

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/20220228105943.png)



![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/20220228110002.png)



![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/20220228110024.png)

### 自定义主题

​	因为antd的默认主题颜色是与支付宝一致的蓝色，如果想改成其他颜色的话，我们需要进行自定义主题，同样这部分的具体操作参考[在 create-react-app 中使用 - Ant Design](https://3x.ant.design/docs/react/use-with-create-react-app-cn)下的自定义主题部分。

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/20220228110216.png)



PS：less是啥？

> Less 是一门 CSS 预处理语言，它扩展了 CSS 语言，增加了变量、Mixin、函数等特性，使 CSS 更易维护和扩展。
>
> Less 可以运行在 Node 或浏览器端。

# Redux

redux的内容暂时跳过，下面一段引用阮一峰的话：



​	首先明确一点，Redux 是一个有用的架构，但不是非用不可。事实上，大多数情况，你可以不用它，只用 React 就够了。

​	曾经有人说过这样一句话。

> "如果你不知道是否需要 Redux，那就是不需要它。"

​	Redux 的创造者 Dan Abramov 又补充了一句。

> "只有遇到 React 实在解决不了的问题，你才需要 Redux 。"



# 打包react项目

​	把我们写的react项目打包成起来，放在服务器上运行。

​	使用下面的命令进行打包：

```
npm run build
```

​	打包完成后在同目录下回多一个build文件夹，该文件夹内部就是打包完毕的内容。接下来我们可以把它放到服务器上运行，可以放在node或者java编写的服务器，也可以借助serve模块快速开启一台服务器。

​	node服务器和java服务器的部分之后再补充。

## node服务器



## java服务器



## serve模块

​	首先全局安装serve模块。

```bash
npm install serve -g
```

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/20220228111634.png)

之后运行下面命令

```bash
serve build
```

该命令会把当前文件夹作为服务器的根目录进行启动。

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/20220228113753.png)

之后可以在浏览器访问3000端口，显示正常：

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/20220228114031.png)



想要关闭服务器的话直接ctrl+c即可！

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/20220228114152.png)



### 遇到的问题

1.全局安装serve后

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/20220228113836.png)

> 参考[(82条消息) npm : 无法加载文件 D:\nodejs\npm.ps1，因为在此系统上禁止运行脚本。_WebView-CSDN博客_nodejs 因为在此系统上禁止运行脚本](https://blog.csdn.net/weixin_45416217/article/details/105860904)

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/20220228113909.png)2.npm全局安装的模块组件都在C:\Users\Administrator.DESKTOP-VDATQMB\AppData\Roaming\npm这个目录下，需要打开查看隐藏目录，因为AppData是隐藏的。

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/20220228113945.png)

# 拓展部分

## lazy_load懒加载

### 定义

​	顾名思义，懒加载的意思就是我需要或者说我请求的时候再加载，如果我还没有请求那就不要加载。最典型的应用就是用在路由组件上，如果我们没有点击路由，就先不加载路由对应的组件，当我们点击路由了再进行加载。

​	如何判断是否是懒加载呢？以我们做的路由案例为例。如果点击路由之后**network请求了相应的组件就是懒加载**，说明是点击的时候再请求，如果**network没有任何请求信息**，则说明之前就已经加载完毕了，



未实现懒加载：

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/20220228144901.png)

实现了懒加载：

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/20220228152055.png)

### 实现方法

​	我们需要lazy函数和suspense组件

1.引入lazy函数和suspense组件

（1）使用路由表

①在路由表的js文件里引入lazy和Suspense，在路由表里将组件的引入用lazy函数包装起来。

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/20220228151616.png)

②在路由表的地方用Suspense包裹起来即可

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/20220228152134.png)



其中Loading组件是我写的用来实现Loading加载的小组件，引用了antd里的<Spin>组件。

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/20220228152149.png)

当我把网速调成3G时，就会调用Suspense里的Loading组件：

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/20220228152308.png)

嵌套路由同理，在路由表里用lazy，在outlet组件外部包裹Suspense



（2）不使用路由表

①引入lazy和Suspense，将引入方式用lazy函数包装起来。

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/20220228150658.png)

②用Suspense包裹起来并且指定一个回调组件，当加载过慢时就会调用这个组件。

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/20220228151414.png)

2.如果不写suspense则会报如下错误

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/20220228150415.png)

​	这是因为如果懒加载了，并且网速很慢的情况下，在网络请求组件返回之前需要给react一个组件或者标签先显示着，可以理解为loading
