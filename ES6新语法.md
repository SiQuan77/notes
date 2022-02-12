

# ES6语法详解

> 参考bilibili用户**訾博ZiBo**的PDF笔记ES6+学习笔记，感谢发布者和撰写者！

## ES6介绍

### ECMA是什么

ECMA（European Computer Manufacturers Association）中文名称为欧洲计算机制造商协会，这个组织的目标是评估、开发和认可电信和计算机标准。1994 年后该组织改名为 Ecma 国际。

而ES全称**EcmaScript**，是脚本语言的**规范**，而平时经常编写的JavaScript，是EcmaScript的**一种实现**，所以ES新特性其实指的就是JavaScript的新特性。

## 什么是ES6

ES6指的是ECMA-262(ECMAScript)的第六版，其推出于2015年。从ES6开始，每年发布一个版本，版本号比年份最后一位大1.

因为ES6版本变动内容最多，具有里程碑意义并且其加入许多新的语法特性，编程实现更简单、高效，所以ES6值得我们去学习



## 新特性1----let关键字

let关键字的使用：

```javascript
// let关键字使用示例：
let a; // 单个声明
let b,c,d; // 批量声明
let e = 100; // 单个声明并赋值
let f = 521, g = 'iloveyou', h = []; // 批量声明并赋值
```

let 关键字用来声明变量，使用 let 声明的变量有几个特点：

1.不允许重复声明

```javascript
// 1. 不允许重复声明；
            let dog = "狗";
            let dog = "狗";
// 报错：Uncaught SyntaxError: Identifier 'dog' has already been declared

```

2.块儿级作用域

```java
// 2. 块儿级作用域（局部变量）；
            {
                let cat = "猫";
                console.log(cat);
            }
            console.log(cat);
// 报错：Uncaught ReferenceError: cat is not defined
```

3.不存在变量提升

```javascript
            // 3. 不存在变量提升；
            // 什么是变量提升：就是在变量创建之前使用（比如输出：输出的是默认值），let不存在，var存在；
            console.log(people1); // 可输出默认值 
            console.log(people2); // 报错：Uncaught ReferenceError: people2 is not defined
            var people1 = "大哥"; // 存在变量提升
            let people2 = "二哥"; // 不存在变量提升
```



比如我在声明前就调用了变量

```javascript
console.log(cat)
var cat="橘猫"
//这时浏览器并不会报错，只会打印出null
```

因为var存在变量提升的特性，上段代码的本质就是

```javascript
var cat  //这行代码是var的提升变量特性自动完成的
console.log(cat)
var cat="橘猫"
```

4.不影响作用域链

什么是作用域链：很简单，就是代码块内有代码块，跟常规编程语言一样，**上级代码块中的局部变量下级可用**

```javascript
// 4. 不影响作用域链；
{
  let p = "大哥";
   function fn(){
      console.log(p); // 这里是可以使用的
   }
 fn();
}
```

### 总结：以后变量声明均使用let即可

## 新特性2----const关键字

const 关键字用来声明常量，const 声明有以下特点：
1.声明必须赋初始值；

```javascript
const CAT;//这么声明会报错
```

2.标识符一般为大写（习惯上这么做，当然你用小写也是ok的）；

3.不允许重复声明；

```javascript
// 3. 不允许重复声明；
const CAT = "喵喵";
const CAT = "喵喵";
//Uncaught SyntaxError: Identifier 'CAT' has already been declared
```

4.值不允许修改，不过对**数组元素**的修改和对**对象内部**的修改是可以的（数组和对象存的是引用地址）；

```javascript
// 4. 值不允许修改；
const CAT = "喵喵";
CAT = "咪咪";
//Uncaught TypeError: Assignment to constant variable.
```

不过这样是可以的：

```javascript
const RNG=["xiaohu","wei","cryin","Ming"]
RNG.push("GALA")
//这样并不会报错
```

5.块儿级作用域（局部变量）；

```javascript
// 5. 块儿级作用域（局部变量）；
{
	const CAT = "喵喵";
	console.log(CAT);
}
console.log(CAT);
//Uncaught ReferenceError: CAT is not defined
```

## 新特性3----变量的解构赋值

ES6 允许按照一定模式，从数组和对象中提取值，对变量进行赋值，这被称为解构赋值；

1.数组的解构赋值

```javascript
const F4 = ["大哥","二哥","三哥","四哥"];
let [a,b,c,d] = F4;//注意：解构数组的时候用的是[]
// 这就相当于我们声明4个变量a,b,c,d，其值分别对应"大哥","二哥","三哥","四哥"
console.log(a + b + c + d); // 大哥二哥三哥四哥
```

2.对象的解构赋值

```javascript
const F3={
    name:"大哥",
    age:22,
    sex:"男",
    xiaopin:function(){
        console.log("我爱演小品！")
    }
}
let {name,age,sex,xiaopin}=F3  //注意，解构对象的时候需要用{}
//上面相当于
//let name=F3.name
//以此类推
```

应用场景：频繁使用对象方法、数组元素，就可以使用解构赋值形式；

## 新特性4----模板字符串

模板字符串（template string）是增强版的字符串，用反引号（`）标识，特点如下：

1.字符串内可以出现**换行符**

```javascript
// 特性
// 1、字符串中可以出现换行符,而不用像单引号双引号那样换行后需要用加号拼接起来
let str =
`<ul>
	<li>大哥</li>
	<li>二哥</li>
	<li>三哥</li>
	<li>四哥</li>
</ul>`;
```

2.可以使用${xxx}形式引用变量

```javascript
let s = "大哥";
let out = `${s}是我最大的榜样！`;//大哥是我最大的榜样
```

总结：以后字符串的声明尽量都是用模板字符安次的反引号``，其按钮再键盘的esc下方一格，数字1键的左边一格。

## 新特性5----简化对象和函数写法

ES6 允许在大括号里面，**直接写**入变量和函数，作为对象的**属性**和**方法**。这样的书写更加简洁；

```javascript
let name = "訾博";
let change = function(){
	console.log("活着就是为了改变世界！");
}
//创建对象
const school = {
	// 完整写法
	// name:name,
	// change:change
	// 简化写法
	name,
	change,
	// 声明方法的简化
	say(){
		console.log("言行一致！");
	}
}
school.change();
school.say();
```

## 新特性6----箭头函数

### 概述

ES6允许使用箭头（=>）定义函数，箭头函数提供了一种更加简洁的函数书写方式，箭头函数多用于匿 名函数的定义； 箭头函数的注意

```javascript
// ES6允许使用箭头（=>）定义函数
// 传统写法：无参数
var say = function(){
	console.log("hello！");
}
say();
//ES写法：
let speak = () =>{
    console.log("hello 哈哈！");
} 
speak();
```

当箭头函数中只有一行执行语句时，可以简略地写成：

```javascript
let speak = () => console.log("hello 哈哈！");
```

### 特点

1.如果形参只有一个，则**小括号**可以省略；

```javascript
// 传统写法：一个参数
var hello = function(name){
	return "hello " + name;
}
console.log(hello("訾博"));

// ES6箭头函数：一个参数
//不省略小括号的写法：
let hi1 = (name) => "hi " + name;
//省略小括号的写法：
let hi2= name =>"hi"+name;
```

若形参有多个，则**小括号不能省略**。

```javascript
// 传统写法：多个参数
var sum = function(a,b,c){
	return a + b + c;
}
console.log(sum(1,2,3));
// ES6箭头函数：多个参数
let he = (a,b,c) => a + b + c;
console.log(he(1,2,3));
```

2.函数体如果**只有一条语句**，则花括号可以省略，函数的**返回值**为该条语句的**执行结果**

```javascript
let sum = (a,b) => a + b;
sum(1,2);//结果为3
```

3.箭头函数 this 指向**声明时所在作用域**下 this 的值，箭头函数中的this是静态的。

```javascript
const school = {
    name:"小弟"
}

function getName(){
    console.log(this.name);
}
let getName1 = () => console.log(this.name); 

window.name="大哥"
getName()//输出 大哥
getName1()//输出 大哥
```

当我们用call方法调用时（call可以改变函数调用时内部的this的值的）：

```javascript
getName.call(school)//输出 小弟
getName1.call(school)//输出 大哥
//箭头函数中的this无法被改变，是静态指向声明时作用域下的this值
```

4.箭头函数不能作为构造函数实例化；

```javascript
let Person = (name, age) =>{
	this.name = name;
	this.age = age;
}
let me = new Person('xiao' ,30);
console.log(me);
//这么写会报错：Uncaught TypeError: Persion is not a constructor
```

5 .不能使用 arguments；

```javascript
let fn = () => console.log(arguments);
fn(1,2,3);
// 报错：Uncaught ReferenceError: arguments is not defined
```

### 代码例子

需求：点击div，2秒后颜色变成粉色



传统写法：（有错误）

```javascript
// 需求-1 点击 div 2s 后颜色变成『粉色』
// 获取元素
let ad = document.getElementById('ad');
// 绑定事件
ad.addEventListener("click", function(){
// 传统写法
// 定时器：参数1：回调函数；参数2：时间；
   setTimeout(function(){
       console.log(this);
       this.style.background = 'pink';
   },2000);
// 报错Cannot set property 'background' of undefined
});
```

这里报错是因为this指向的是window。



传统写法改进：

```javascript
// 需求-1 点击 div 2s 后颜色变成『粉色』
// 获取元素
let ad = document.getElementById('ad');
// 绑定事件
ad.addEventListener("click", function(){
// 传统写法
// 定时器：参数1：回调函数；参数2：时间；
    let _this=this;//在这里保存外层的this对象即可
   setTimeout(function(){
       console.log(this);
       _this.style.background = 'pink';
   },2000);
// 报错Cannot set property 'background' of undefined
});
```



使用箭头函数实现的话，则无需考虑this指向的问题，因为this指定的是创建声明时的this对象

```javascript
let ad=document.getElementById("ad");
ad.addEventListener("click",function (){
    setTimeout(()=> this.style.background='pink',2000);
})
```

## 新特性7----函数参数的默认值设置

ES允许给函数的参数赋初始值；



1.形参初始值具有默认值的参数, 一般位置要靠后(潜规则)。

```javascript
function add(a,b,c=10) {
    return a + b + c; 
}
let result = add(1,2); 
console.log(result); // 13
```

2.与解构赋值结合，当参数为对象时可以进行解构赋值，并且可以给对象里的属性赋上初始值

```javascript
function connect({host="127.0.0.1", username,password, port}){ 
    console.log(host);
    console.log(username);
    console.log(password);
    console.log(port);
}
connect({ host: 'atguigu.com', username: 'root', password: 'root', port: 3306 })
```

## 新特性8----rest参数

ES6 引入 rest 参数，用于获取函数的实参，用来代替 **arguments**；



1.在ES5中，获取实参的方式：

```javascript
function data(){
   console.log(arguments)
}
data("大哥","二哥","三哥","四哥")
```

结果如下图所示，打印出来的是一个对象

![QQ20220112103405.png](https://img.pterclub.com/images/2022/01/12/QQ20220112103405.png)

```javascript
function data(...args){
    console.log(args);
} // fliter some every map }
data("大哥","二哥","三哥","四哥");
```

结果如下图所示，打印出来的是一个数组，这样就可以使用数组的一系列api，例如fliter,map等等

![QQ20220112103646.png](https://img.pterclub.com/images/2022/01/12/QQ20220112103646.png)

## 新特性9----拓展运算符

... 扩展运算符能将数组转换为逗号分隔的参数序列；

扩展运算符（spread）也是三个点（...）。它好比 rest 参数的**逆运算**，将一个数组转为用逗号分隔的**参**

**数序列**，对数组进行**解包**；

### 将数组转换为参数序列

```javascript
//声明一个数组 ... 
const tfboys = ['易烊千玺', '王源', '王俊凯']; 
// 用拓展运算符将数组转为参数类型=> '易烊千玺','王源','王俊凯'
// 声明一个函数
function chunwan(){
    console.log(arguments);
}
chunwan(...tfboys);
```

结果如下图所示：

![QQ20220112104435.png](https://img.pterclub.com/images/2022/01/12/QQ20220112104435.png)

### 合并数组

```javascript
//1. 数组的合并 情圣 误杀 唐探 
const kuaizi = ['王太利','肖央']; 
const fenghuang = ['曾毅','玲花'];
const zuixuanxiaopingguo = [...kuaizi, ...fenghuang];
console.log(zuixuanxiaopingguo);//['王太利','肖央','曾毅','玲花']
```

### 克隆数组

```javascript
const sanzhihua = ['E','G','M'];
const sanyecao = [...sanzhihua];
console.log(sanyecao);// ['E','G','M']
```

### 将伪数组转为真正的数组

```javascript
const divs = document.querySelectorAll('div');
const divArr = [...divs];
console.log(divArr); // arguments
```

divs对象如下图所示：

![QQ20220112104859.png](https://img.pterclub.com/images/2022/01/12/QQ20220112104859.png)

转换后的divArr对象如下：

![QQ20220112104941.png](https://img.pterclub.com/images/2022/01/12/QQ20220112104941.png)

## 新特性10----Symbol

> 该块参考[(73条消息) 详解Symbol（自定义值，内置值）-------小小的Symbol，大大的学问_codingWeb的博客-CSDN博客_symbol值](https://blog.csdn.net/fesfsefgs/article/details/108354248)，感谢codingWeb！

ES6 引入了一种新的原始数据类型 Symbol，表示独一无二的值。它是JavaScript 语言的第七种数据类型。

### Symbol的特点

#### 1.Symbol的值是唯一的，用来解决命名冲突的问题，即使参数相同。

```javascript
// 没有参数的情况
let name1 = Symbol();
let name2 = Symbol();
name1 === name2  // false
name1 === name2 // false

// 有参数的情况
let name1 = Symbol('flag');//此处的flag可以理解为symbol的注释
let name2 = Symbol('flag');
name1 === name2  // false
name1 === name2 // false
```

#### 2.Symbol不能与其他数据（包括自己）进行运算

 - 数学计算：不能转换为数字

 - 字符串拼接：隐式转换不可以，但是可以显示转换

 - 模板字符串

![QQ20220112115017.png](https://img.pterclub.com/images/2022/01/12/QQ20220112115017.png)

#### 3.Symbol定义的对象属性不参与for...in/of遍历

但是可以使用Reflect.ownKeys/Object.getOwnPropertySymbols()来获取对象的所有键名。

- Object.getOwnPropertySymbols 方法会返回一个数组，成员是当前对象的所有用作属性名的 Symbol 值。

```javascript
let sy = Symbol();
let obj = {
	name:"zhangsan",
	age:21
};
obj[sy] = "symbol";
console.log(obj);   //{name: "zhangsan", age: 21, Symbol(): "symbol"}

for(let key in obj) {
	console.log(key);
}  //只输出了name，age,而不会输出Symbol

Object.getOwnPropertySymbols(obj);	 //[Symbol()]
Reflect.ownKeys(obj); 	//["name", "age", Symbol()]

Object.keys(obj);					 //["name", "age"]
Object.getOwnPropertyNames(obj) 	 //["name", "age"]
Object.keys(obj) 		//["name", "age"]
Object.values(obj) 		//["zhangsan", 21]
JSON.stringify(obj)		//{"name":"zhangsan","age":21}
```

### Symbol的方法

#### 1.Symbol.for()

(1)作用：用于将**描述相同**的Symbol变量指向**同一个**Symbol值,这样的话，就方便我们通过描述（标识）**区分开不同的Symbol**了，阅读起来方便

```javascript
Symbol.for("foo"); // 因为注册表中没有键位"foo"的symbol创建一个 symbol 并放入 symbol 注册表中，键为 "foo"
Symbol.for("foo"); // 从 symbol 注册表中读取键为"foo"的 symbol

Symbol.for("bar") === Symbol.for("bar"); // true，证明了上面说的
Symbol("bar") === Symbol("bar"); // false，Symbol() 函数每次都会返回新的一个 symbol

let sym = Symbol.for("mario");
sym.toString(); 
// "Symbol(mario)"，mario 既是该 symbol 在 symbol 注册表中的键名，又是该 symbol 自身的描述字符串
```

(2)Symbol()和Symbol.for()的**相同点**：它们定义的值类型都为"symbol"；

不同点在于：

①Symbol()定义的值不放入全局 symbol 注册表中，**每次都是新建**，即使**描述相同值**也不相等；

②<u>用 Symbol.for() 方法创建的 symbol 会被放入一个全局 symbol 注册表中</u>。Symbol.for() **并不是每次**都会创建一个新的 symbol，它会首先**检查**给定的 key 是否已经在注册表中了。假如是，则会直**接返回**上次存储的那个。否则，它会再**新建一个**。

#### 2.Symbol.keyFor()

（1）作用：作用： 方法用来获取 symbol 注册表中与某个 symbol 关联的键。如果全局注册表中查找到该symbol，则返回该symbol的key值，**形式为string**。如果symbol未在注册表中，返回undefined。

```javascript
// 创建一个 symbol 并放入 Symbol 注册表，key 为 "foo"
let globalSym = Symbol.for("foo"); 
Symbol.keyFor(globalSym); // "foo"

// 创建一个 symbol，但不放入 symbol 注册表中
let localSym = Symbol(); 
Symbol.keyFor(localSym); // undefined，所以是找不到 key 的
```

### Symbol的属性

Symbol.prototype.description是一个**只读**属性，它会返回 Symbol 对象的**可选描述**的字符串。

```javascript
// Symbol()定义的数据
let a = Symbol("acc");
a.description  // "acc"
Symbol.keyFor(a);  // undefined

// Symbol.for()定义的数据
let a1 = Symbol.for("acc");
a1.description  // "acc"
Symbol.keyFor(a1);  // acc

// 未指定描述的数据
let a2 = Symbol();
a2.description  // undefined

Symbol('desc').toString();   // "Symbol(desc)"
Symbol('desc').description;  // "desc"
Symbol('').description;      // ""
Symbol().description;        // undefined
```

直接将带有描述xxx的Symbol通过toString转为字符串的话，会得到Symbol(xxx)的字符串，如果直接调用.description的属性，则会得到xxx的字符串，而没有Symbol。



description属性和Symbol.keyFor()方法的区别是：

​		description能返回**所有Symbol类型数据**的描述，而Symbol.keyFor()只能返回**Symbol.for()在全局注册**过的描述

### Symbol的内置值

除了定义自己使用的 Symbol 值以外，ES6 还提供了 11 个内置的 Symbol 值，指向语言**内部使用**的方法。可以称这些方法为**魔术方法**，因为它们会在**特定的场景下自动执行**。Symbol内置值的使用，都是作为**某个对象类型的属性去使用**。

![QQ20220112120641.png](https://img.pterclub.com/images/2022/01/12/QQ20220112120641.png)

#### 1.Symbol.hasInstance

对象的Symbol.hasInstance属性，指向一个内部方法，<u>当其他对象使用instanceof运算符</u>，**判断是否为该对象的实例时**，会自动调用这个方法。

```javascript
class Person {}
let p1 = new Person;
console.log(p1 instanceof Person); //true
// instanceof  和  [Symbol.hasInstance]  是等价的
console.log(Person[Symbol.hasInstance](p1)); //true
console.log(Object[Symbol.hasInstance]({})); //true
//Symbol内置值得使用，都是作为某个对象类型的属性去使用
class Person {
	static[Symbol.hasInstance](params) {
	console.log(params)
	console.log("有人用我来检测类型了")
	//可以自己控制 instanceof 检测的结果
	return true
	//return false
	}
}
let o = {}
console.log(o instanceof Person)    //重写为true
```

#### 2.Symbol.isConcatSpreadable

值为布尔值，表示该对象用于Array.prototype.concat()时，是否可以展开。

```javascript
let arr = [1, 2, 24, 23]
let arr2 = [42, 25, 24, 235]
//控制arr2是否可以展开
arr2[Symbol.isConcatSpreadable] = false
console.log(arr.concat(arr2)) //(5)[1, 2, 24, 23, Array(4)]
```

#### 3.Symbol.iterator

ES6 创造了一种新的遍历命令 for...of 循环，<u>Iterator 接口主要供 for...of 消费</u>，这个内置值是比较常见的，也是一个对象可以被for of被迭代的原因，我们可以查看对象是否存在这个Symbol.iterator值，判断是否可被for of迭代，**拥有此属性的对象被誉为可被迭代的对象**，可以使用for…of循环。



若我随意创建一个对象，其不存在Symbol.iterator值，故{}对象是无法被for ... of迭代。

![20200902125208657.png](https://img.pterclub.com/images/2022/01/12/20200902125208657.png)

但是[]数组是可以的，因为其有Symbol.iterator属性

![20200902125513715.png](https://img.pterclub.com/images/2022/01/12/20200902125513715.png)

原生就具备iterator接口的数据都可以用for of进行遍历：

Array,Arguments,Set,Map,String,TypedArray,NodeList



那么我们可不可以手动给{}对象加上Symbol.iterator属性，使其可以被for of遍历出来

```javascript
// 让对象变为可迭代的值，手动加上数组的可迭代方法
let obj = {
	0: 'zhangsan',
	1: 21,
	length: 2,
	[Symbol.iterator]: Array.prototype[Symbol.iterator]
};
for(let item of obj) {
	console.log(item);
}
```

打印出来的结果：

![QQ20220112152027.png](https://img.pterclub.com/images/2022/01/12/QQ20220112152027.png)

发现可以手动实现Symbol的iterator接口来使其可以被for of遍历。不过上面我们使用的是数组原型上的Symbol.iterator，所以对象必须是个伪数组才能遍历。

```javascript
let arr = [1, 52, 5, 14, 23, 2]
let iterator = arr[Symbol.iterator]()
console.log(iterator.next())  //{value: 1, done: false}        
console.log(iterator.next())  //{value: 52, done: false}       
console.log(iterator.next())  //{value: 5, done: false}    
console.log(iterator.next())  //{value: 14, done: false}       
console.log(iterator.next())  //{value: 23, done: false}       
console.log(iterator.next())  //{value: 2, done: false}        
console.log(iterator.next())  //{value: undefined, done: true}
```

那我们自定义对象的Symbol.iterator，使得对象可以通过for of遍历.

```javascript
//自定义[Symbol.iterator]，使得对象可以通过for of 遍历
let obj = {
	name: "Ges",
	age: 21,
	hobbies: ["ESgsg", "Sfgse", "Egs", "SEGSg"],
	[Symbol.iterator]() { 
		console.log(this)
		let index = 0
		let Keyarr = Object.keys(this)
		let len = Keyarr.length
		return {
				next: () => {
				if(index >= len) return {
					value: undefined,
					done: true
				}
				let result = {
					value: this[Keyarr[index]],
					done: false
				}
				index++
				return result
			}
		}
	}
}

for(let item of obj) {
	console.log(item)
}
```

![QQ20220112152831.png](https://img.pterclub.com/images/2022/01/12/QQ20220112152831.png)

我们可以使用**generator**和**yield**进行简化：

```javascript
//简洁版
let obj = {
	name: "Ges",
	age: 21,
	hobbies: ["ESgsg", "Sfgse", "Egs", "SEGSg"],
	*[Symbol.iterator]() {
		for(let arg of Object.values(this)) {
			yield arg;
		}
	}
}
for(let item of obj) {
	console.log(item)
}
```

#### 4.Symbol.toPrimitive

该对象被转为原始类型的值时，会调用这个方法，**返回该对象对应的原始类型值**。

```javascript
/*
 * 对象数据类型进行转换：
 * 1. 调用obj[Symbol.toPrimitive](hint)，前提是存在
 * 2. 否则，如果 hint 是 "string" —— 尝试 obj.toString() 和 obj.valueOf()
 * 3. 否则，如果 hint 是 "number" 或 "default" —— 尝试 obj.valueOf() 和 obj.toString()
 */
let a = {
    value: 0,
    [Symbol.toPrimitive](hint) {
        switch (hint) {
            case 'number': //此时需要转换成数值 例如:数学运算`
                return ++this.value;
            case 'string': // 此时需要转换成字符串 例如:字符串拼接
                return String(this.value);
            case 'default': //此时可以转换成数值或字符串 例如：==比较
                console.log("调用了default")
                return ++this.value;
        }
    }
};
if (a == 1 && a == 2 && a == 3) {
    console.log('OK');
}
```

![QQ20220112153818.png](https://img.pterclub.com/images/2022/01/12/QQ20220112153818.png)



当然自定义一个valueOf/toString 都是可以的，数据类型进行转换时，调用优先级最高的还是Symbol.toPrimitive。

```javascript
    //存在[Symbol.toPrimitive] 属性，优先调用
    let a = {
        value: 0,
        [Symbol.toPrimitive](hint) {
            console.log(`此时的hint是${hint}`)
            switch(hint) {
                case 'number': //此时需要转换成数值 例如:数学运算时触发
                    console.log("调用了number")
                    return ++this.value;
                case 'string': // 此时需要转换成字符串 例如:字符串拼接时触发
                    console.log("调用了string")
                    return String(this.value);
                case 'default': //此时可以转换成数值或字符串 例如：==比较时触发
                    console.log("调用了default")
                    return ++this.value;
            }
        },
        valueOf: function() {
            console.log("valueOf")
            return a.i++;
        },
        toString: function() {
            console.log("toString")
            return a.i++;
        }
    };
    console.log(`${a}`+`concat`)//string场景
    console.log(+a)//number场景
    console.log(a==2)//default场景
	console.log(a+1)//default场景
```

![QQ20220112154832.png](https://img.pterclub.com/images/2022/01/12/QQ20220112154832.png)

#### 5.Symbol.toStringTag

在该对象上面调用Object.prototype.toString方法时，如果这个属性存在，**它的返回值会出现在toString方法返回的字符串之中**，表示**对象的类型**。

```javascript
class Person {
    get [Symbol.toStringTag]() {
        return 'Person';
    }
}
let p1 = new Person;
console.log(Object.prototype.toString.call(p1)); //"[object Person]"
```

### Symbol用法举例

> 该用法举例引用于[JS 中的 Symbol 是什么？ - apple78 - 博客园 (cnblogs.com)](https://www.cnblogs.com/apple78/p/12786700.html)，感谢原作者apple78！

ES 6 引入了一个新的数据类型 Symbol，它是用来做什么的呢？

为了说明 Symbol 的作用，我们先来描述一个使用场景。

我们在做一个游戏程序，用户需要选择角色的种族。

```javascript
var race = {
  protoss: 'protoss', // 神族
  terran: 'terran', // 人族
  zerg: 'zerg' // 虫族
}

function createRole(type){
  if(type === race.protoss){创建神族角色}
  else if(type === race.terran){创建人族角色}
  else if(type === race.zerg){创建虫族角色}
}
```

那么用户选择种族后，就需要调用 createRole 来创建角色：

```javascript
// 传入字符串
createRole('zerg') 
// 或者传入变量
createRole(race.zerg)
```

一般传入字符串被认为是不好的做法，所以使用 createRole(race.zerg) 的更多。

如果使用 createRole(race.zerg)，那么聪明的读者会发现一个问题：race.protoss、race.terran、race.zerg 的值为多少并不重要。



改为如下写法，对 createRole(race.zerg) **毫无影响**：

```javascript
var race = {
  protoss: 'askdjaslkfjas;lfkjas;flkj', // 神族
  terran: ';lkfalksjfl;askjfsfal;skfj', // 人族
  zerg: 'qwieqwoirqwoiruoiwqoisrqwroiu' // 虫族
}
```

也就是说：

race.zerg 的值是多少**无所谓**，<u>只要它的值跟 race.protoss 和 race.terran 的值**不一样**就行</u>。

 

Symbol 的用途就是如此：**Symbol 可以创建一个独一无二的值（但并不是字符串）。**

用 Symbol 来改写上面的 race：

```javascript
var race = {
  protoss: Symbol(),
  terran: Symbol(),
  zerg: Symbol()
}

race.protoss !== race.terran // true
race.protoss !== race.zerg // true
```

你也可以给每个 Symbol 起一个名字，不过这个名字仅仅只是描述Symbol的description：

```javascript
var race = {
  protoss: Symbol('protoss'),
  terran: Symbol('terran'),
  zerg: Symbol('zerg')
}
```

不过这个名字跟 Symbol 的值并**没有关系**，你可以认为这个名字就是个**注释**。如下代码可以证明 Symbol 的名字与值无关，如果用Symbol.for('a')来创建，他们就是相等的。

```javascript
var a1 = Symbol('a')
var a2 = Symbol('a')
a1 !== a2 // true
```

**所以Symbol的本质是生成一个全局唯一的值。**

### 总结

总的来说Symbol用的最多的地方，还是它作为一个**唯一值去使用**，但我们需要知道，它**不仅仅只是代表一个唯一值**，Symbol难的地方在于它的**内置值**，它玩的都是底层。

## 新特性11----迭代器

### 概述

遍历器（Iterator）就是一种机制。它是一种接口，为各种不同的数据结构提供统一的访问机制。**任何数据结构只要部署 Iterator 接口，就可以完成遍历操作**；

### 特点

ES6 创造了一种新的遍历命令 for...of 循环，Iterator 接口主要供 for...of 消费；

原生具备 iterator 接口的数据(可用 for of 遍历)：Array,Arguments,Set,Map,String,TypedArray,NodeList。

### 工作原理

1.创建一个**指针对象**，指向当前数据结构的起始位置；

2.第一次调用对象的 next 方法，指针自动指向数据结构的第一个成员；

3.接下来**不断调用 next 方法**，指针一直**往后移动**，直到指向最后一个成员；

4.每调用 next 方法返回**一个包含 value 和 done 属性的对象**；

### 代码

1.直接迭代数组

```javascript
// 声明一个数组
const xiyou = ['唐僧', '孙悟空', '猪八戒', '沙僧'];

// 使用 for...of 遍历数组
for(let v of xiyou){
    console.log(v);
}
let iterator = xiyou[Symbol.iterator]();

// 调用对象的next方法
console.log(iterator.next());
console.log(iterator.next());
console.log(iterator.next());
console.log(iterator.next());
console.log(iterator.next());

// 重新初始化对象，指针也会重新回到最前面 
let iterator1 = xiyou[Symbol.iterator](); 
console.log(iterator1.next());
```

结果如下图所示：

![QQ20220112210702.png](https://img.pterclub.com/images/2022/01/12/QQ20220112210702.png)

2.自定义迭代器来遍历数据

```javascript
// 声明一个对象
const banji = 
{
    name : "终极一班", stus : [ 'xiaoming', 'xiaoning', 'xiaotian', 'knight' ], [Symbol.iterator]() {
        // 索引变量
        let index = 0;
        // 保存this
        let _this = this;
        return {
            next : function () {
                if (index < _this.stus.length) {
                    const result = {
                        value : _this.stus[index], done : false 
                    };
                }
            }
        }
    }
}
// 下标自增
```

结果如下图所示：

![QQ20220112211716.png](https://img.pterclub.com/images/2022/01/12/QQ20220112211716.png)

## 新特性12----生成器

### 概述

生成器函数是 ES6 提供的一种**异步编程解决方案**，语法行为与传统函数完全不同。生成器本质上就是一个**特殊的函数**。

### 何为同步何为异步？

同步和异步关注的是消息通信机制 (synchronous communication/ asynchronous communication)。同步，就是调用某个东西是，**调用方得等待这个调用返回结果才能继续往后执行**。异步，和同步相反，**调用方不会立即得到结果，而是在调用发出后调用者可用继续执行后续操作**，被调用者通过状体来通知调用者，或者通过回掉函数来处理这个调用

打比方：

你去商城买东西，你看上了一款手机，能和店家说你一个这款手机，他就去仓库拿货，你得在店里等着，不能离开，这叫做同步。现在你买手机赶时髦直接去京东下单，下单完成后你就可用做其他时间（追剧、打王者、lol）等货到了去签收就ok了.这就叫异步。

### 代码

1.生成函数的声明与调用，yield关键字可以看做是代码的分隔符。

```javascript
// 生成器其实就是一个特殊的函数
// 异步编程  纯回调函数  node fs  ajax mongodb
// yield：函数代码的分隔符
function * gen() 
{
    console.log(111);
    yield '一只没有耳朵';
    console.log(222);
    yield '一只没有尾部';
    console.log(333);
    yield '真奇怪';
    console.log(444);
}
let iterator = gen();
console.log(iterator.next());
console.log(iterator.next());
console.log(iterator.next());
console.log(iterator.next());


console.log("遍历：");
//遍历
for (let v of gen()) {
    console.log(v);
}
```

结果如下图所示：

![QQ20220112214146.png](https://img.pterclub.com/images/2022/01/12/QQ20220112214146.png)

yield与return的区别：普通函数只**可以return一次**，而生成器函数可以**yield多次**（当然也可以只yield一次）。在生成器的执行过程中，遇到yield表达式**立即暂停**，后续可**恢复执行状态**。



2.生成器函数的参数传递，可以通过迭代器来传递

```javascript
function * gen(arg)
{
    console.log(arg);
    let one = yield 111;
    console.log(one);
    let two = yield 222;
    console.log(two);
    let three = yield 333;
    console.log(three);
}
let iterator = gen("AAA");
console.log(iterator.next());// 会执行yield 111及之前的代码
// next()方法是可以传入参数的，传入的参数作为第一条(上一条)语句yield 111的返回
结果 console.log(iterator.next("BBB"));
// 会执行yield 222;
console.log(iterator.next("CCC"));
// 会执行yield 333;
console.log(iterator.next("DDD"));
// 继续往后走，未定义;
```

代码部分说明：

![QQ20220112214718.png](https://img.pterclub.com/images/2022/01/12/QQ20220112214718.png)

运行结果：

![QQ20220112214827.png](https://img.pterclub.com/images/2022/01/12/QQ20220112214827.png)

### 实例1

需求：1s后控制台输出111 再过2s后控制台输出222 再过3s后控制台输出333

1.传统做法：

```javascript
setTimeout(() => 
{
    console.log(111);
    setTimeout(() => {
        console.log(222);
        setTimeout(() => {
            console.log(333);
        }, 3000) 
    }, 2000) 
}, 1000)
```

但是如果又有新的异步任务需要加入，那么就会造成**回调地狱**！

2.使用生成器函数来避免回调地狱

```javascript
// 另一种做法
function one()
{
    setTimeout(() => {
        console.log(111);
        iterator.next();
    }, 1000) 
}
function two()
{
    setTimeout(() => {
        console.log(222);
        iterator.next();
    }, 1000) 
}
function three()
{
    setTimeout(() => {
        console.log(333);
        iterator.next();
    }, 1000) 
}
function * gen()
{
    yield one();
    yield two();
    yield three();
}
// 调用生成器函数
let iterator = gen();
iterator.next();
```

只需调用一次next就会自动执行下去，因为one(执行完毕后再次调用iterator.next()进而调用two()。

### 实例2

模拟获取: 用户数据 订单数据 商品数据

```javascript
// 模拟获取: 用户数据 订单数据 商品数据
function getUsers()
{
    setTimeout(() => {
        let data = "用户数据";
        // 第二次调用next，传入参数，作为第一个的返回值
        iterator.next(data);
        // 这里将data传入
    }, 1000);
}
function getOrders()
{
    setTimeout(() => {
        let data = "订单数据";
        iterator.next(data);
        // 这里将data传入
    }, 1000);
}
function getGoods()
{
    setTimeout(() => {
        let data = "商品数据";
        iterator.next(data);
        // 这里将data传入
    }, 1000);
}
function * gen()
{
    let users = yield getUsers();
    console.log(users);
    let orders = yield getOrders();
    console.log(orders);
    let goods = yield getGoods();
    console.log(goods);
    // 这种操作有点秀啊！
}
let iterator = gen();
iterator.next();
```

## 新特性13----Promise

### 概述

Promise 是 ES6 引入的异步编程的新解决方案。语法上 Promise 是一个构造函数，用来封装异步操作并可以获取其成功或失败的结果；

其中的关键方法：

​	Promise 构造函数: Promise (excutor) {}；
​	Promise.prototype.then 方法；
​	Promise.prototype.catch 方法；

### 代码

1.基本使用：

实例化 Promise 对象,Promise对象有三种状态分别是初始化、成功和失败。

（1）当调用resolve方法时，对象就会变成成功，并且走promise对象的then方法中的成功方法。

```javascript
    const p = new Promise(function (resolve, reject) {
        setTimeout(function () {
            // 成功
            let data = "数据成功！";
            // 调用resolve，这个Promise 对象的状态就会变成成功
            resolve(data);
        }, 1000);
    });
    // Promise封装读取文件： 一般写法： 运行结果： // 成功
    // 调用 Promise 对象的then方法，两个参数为函数
    p.then(function (value) {
            // 成功
            console.log(value);
        },
        function (reason){
            // 失败
            console.error(reason);
        });
```

成功结果如下：

![QQ20220113201721.png](https://img.pterclub.com/images/2022/01/13/QQ20220113201721.png)

（2）调用reject方法就会走失败的方法

```javascript
 const p = new Promise(function (resolve, reject) {
        setTimeout(function () {
            let err = `失败了`
            reject(err)
        }, 1000);
    });
    // Promise封装读取文件： 一般写法： 运行结果： // 成功
    // 调用 Promise 对象的then方法，两个参数为函数
    p.then(function (value) {
            // 成功
            console.log(value);
        },
        function (reason){
            // 失败
            console.error(reason);
        });
```

失败结果如下，因为我用了console.error，所以显示的信息是以报错形式呈现的。

![QQ20220113202149.png](https://img.pterclub.com/images/2022/01/13/QQ20220113202149.png)

（3）promise封装原生的ajax操作

```javascript
// 请求地址：https://api.apiopen.top/getJoke
// 原生请求
// 1、创建对象
const xhr = new XMLHttpRequest();
// 2、初始化
xhr.open("GET", "https://api.apiopen.top/getJoke");
// 3、发送
xhr.send();
// 4、绑定事件，处理响应结果
xhr.onreadystatechange = function (){
    // 判断状态
    if (xhr.readyState == 4){
        // 判断响应状态码 200-299
        if (xhr.status >= 200 && xhr.status <= 299) {
            // 成功
            console.log(xhr.response);
        }
        else {
            // 失败
            console.error(xhr.status);
        }
    }
}
p.then(function (value){
    console.log(value.toString());
},
function (reason){
    console.log(reason);
    // 读取失败
})
```

(4)promise中的then方法详解：

先创建Promise对象，then方法的返回也是一个promise对象，有三种返回结果：

①若then方法返回的结果是非promise类型的数据，则状态为成功，返回值为对象的成功值resolve。例如返回字符串或者数字，甚至不写return语句（不写return语句的话返回的就是undefined），返回的类型**都是成功**，返回值与return的对象**无关**。

```javascript
const p = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve("用户数据");
    }, 1000);
});
const result = p.then(value => 
{
    console.log(value);
    return "iloveyou!"
},
reason => {
    console.error(reason);
})
console.log(p)
```

结果如下：

![QQ20220113205715.png](https://img.pterclub.com/images/2022/01/13/QQ20220113205715.png)

②如果返回的promise类型的数据，则返回的promise对象的状态决定对象p的状态

```javascript
const result = p.then(value => 
{
	return new Promise((resolve,reject) =>{
        reject("子promise是失败的状态")
    })
},
reason => {
    console.error(reason);
})
console.log(p)
```

结果：

![QQ20220113210503.png](https://img.pterclub.com/images/2022/01/13/QQ20220113210503.png)

③还可以直接throw抛出错误

```javascript
const result = p.then(value => 
{
	throw "出错啦！"
},
reason => {
    console.error(reason);
})
console.log(p)
```

结果：

![QQ20220113210712.png](https://img.pterclub.com/images/2022/01/13/QQ20220113210712.png)

（5）promise中的catch方法



### 实践练习

1.回调地狱写法：

```javascript
// 1、引入 fs 模块
const fs = require("fs");
// 2、调用方法，读取文件
fs.readFile("resources/text.txt",(err,data1)=>{
    fs.readFile("resources/test1.txt",(err,data2)=>{
        fs.readFile("resources/test2.txt",(err,data3)=>{
            let result = data1 + data2 + data3;
            console.log(result);
        });
    });
});
```

结果：

![QQ20220113211822.png](https://img.pterclub.com/images/2022/01/13/QQ20220113211822.png)

2.promise实现

```javascript
// 1、引入 fs 模块
const fs = require("fs");
// 2、使用Promise实现
const p = new Promise((resolve,reject)=>{
    fs.readFile("resources/text.txt",(err,data)=>{
        resolve(data);
 });
});
p.then(value=>{
    return new Promise((resolve,reject)=>{
        fs.readFile("resources/test1.txt",(err,data)=>{
            resolve([value,data]);
        });
    })
}).then(value=>{
    return new Promise((resolve,reject)=>{
        fs.readFile("resources/test2.txt",(err,data)=>{
            // 存入数组
            value.push(data);
            resolve(value);
        });
    })
}).then(value=>{
    console.log(value.join("\r\n"));
})
```

结果：

![QQ20220113211947.png](https://img.pterclub.com/images/2022/01/13/QQ20220113211947.png)



## 新特性14----Set集合

### 概述

ES6 提供了新的数据结构 Set（集合）。**它类似于数组，但成员的值都是唯一的**，集合实现了 iterator

接口，所以可以使用『扩展运算符』和『for…of…』进行遍历，集合的属性和方法：

1.size 返回集合的**元素个数**；

2.add **增加**一个新元素，返回当前集合；

4.has **检测**集合中是否包含某个元素，返回 boolean 值；

5.clear **清空**集合，返回 undefined；

### 代码

```javascript
// Set集合 
let s = new Set(); 
console.log(s,typeof s); 
let s1 = new Set(["大哥","二哥","三哥","四哥","三哥"]); 
console.log(s1); // 自动去重 
// 1. size 返回集合的元素个数； 
console.log(s1.size); 
// 2. add 增加一个新元素，返回当前集合； 
s1.add("大姐"); 
console.log(s1); 
// 3. delete 删除元素，返回 boolean 值； 
let result = s1.delete("三哥"); 
console.log(result); 
console.log(s1); 
// 4. has 检测集合中是否包含某个元素，返回 boolean 值； 
let r1 = s1.has("二姐"); 
console.log(r1); 
// 5. clear 清空集合，返回 undefined； 
s1.clear(); 
console.log(s1);
```

结果：

![QQ20220114221100.png](https://img.pterclub.com/images/2022/01/14/QQ20220114221100.png)

### 实践

1.利用Set集合可以对数组进行去重操作

```javascript
let arr=[1,2,3,4,5,4,3,2,1];
let s1=new Set[arr];
```

2.求集合的交集，下面使用了拓展运算符和箭头函数的简便写法，即如果箭头函数只有一个返回值，可以省略大括号。

```javascript
let arr=[1,2,3,4,5,4,3,2,1];
let arr2=[3,4,5,6,5,4,3];
let result = [...new Set(arr)].filter(item=>new Set(arr2).has(item));
```

3.求并集

```javascript
let union = [...new Set([...arr,...arr2])];
```

4.求差集，比如集合1和集合2求差集的结果就是1里面有的但是2里面没有的。

```javascript
let result1 = [...new Set(arr)].filter(item=>!(new Set(arr2).has(item)));
```

## 新特性15----Map集合

### 概述

ES6 提供了 Map 数据结构。它类似于对象，也是键值对的集合。**但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键**。Map 也实现了iterator 接口，所以可以使用『扩展运算符』和『for…of…』进行遍历；

### 属性和方法

1.size 返回 Map 的元素个数；

2.set 增加一个新元素，返回当前 Map； 

3.get 返回键名对象的键值；

4.has 检测 Map 中是否包含某个元素，返回 boolean 值；

5.clear 清空集合，返回 undefined；

### 代码

```javascript
// Map集合 
// 创建一个空 
map let m = new Map(); 
// 创建一个非空 map 
let m2 = new Map([ ['name','尚硅谷'], ['slogon','不断提高行业标准'] ]); 
// 1. size 返回 Map 的元素个数； 
console.log(m2.size); 
// 2. set 增加一个新元素，返回当前 Map； 
m.set("皇帝","大哥"); 
m.set("丞相","二哥"); 
console.log(m); 
// 3. get 返回键名对象的键值； 
console.log(m.get("皇帝")); 
// 4. has 检测 Map 中是否包含某个元素，返回 boolean 值； 
console.log(m.has("皇帝")); 
// 5. clear 清空集合，返回 undefined；
m.clear(); 
console.log(m);
```

结果：

![QQ20220114223142.png](https://img.pterclub.com/images/2022/01/14/QQ20220114223142.png)

## 新特性16----class类

### 概述

ES6 提供了更接近传统语言的写法，引入了 Class（类）这个概念，作为对象的模板。通过 class 关键字，可以定义类。基本上，ES6 的 class 可以看作只是一个**语法糖**，<u>它的绝大部分功能，ES5 都可以做到</u>，新的 class 写法只是让对象原型的写法**更加清晰**、**更像面向对象编程**的语法而已；

### 代码

1.类的实现

（1）**ES5的写法**来实现类

```javascript
function Phone(brand,price){ 
   this.brand = brand; 
   this.price = price; 
   } 
// 添加方法 
Phone.prototype.call = function(){ 
   console.log("我可以打电话！"); 
} 
// // 实例化对象
let HuaWei = new Phone("华为",5999); 
HuaWei.call(); 
console.log(HuaWei);
```

结果：

![QQ20220114225057.png](https://img.pterclub.com/images/2022/01/14/QQ20220114225057.png)



（2）用ES6的写法来实现

```javascript
// ES6写法 
class Phone{ 
    // 构造方法，名字是固定的 
    constructor(brand,price) { 
        this.brand = brand; 
        this.price = price; 
    }
    // 打电话，方法必须使用该方式写。直接方法名加括号，不能使用
    //call:function(){...}来实现
    call(){ 
        console.log("我可以打电话！"); 
    } 
}
let HuaWei = new Phone("华为",5999); 
HuaWei.call(); 
console.log(HuaWei);
```

2.函数对象和实例对象并不相通，使用ES5语法的话，换句话说Phone.name和Phone.change都是类的**静态成员**。

```javascript
function Phone(){
    
}
Phone.name='手机';//函数对象
Phone.change = function(){
    console.log("我可以改变时间");
}

let nokia = new Phone();//实例对象
console.log(nokia.name);
nokia.cahange();
```

结果如下：

![QQ20220114225729.png](https://img.pterclub.com/images/2022/01/14/QQ20220114225729.png)

但是实例对象与函数的原型对象相通。

```javascript
function Phone(){
    
}
Phone.protoptype.size="5.5inch";
let nokia = new Phone();
console.log(nokia.size);//打印的出来，结果就是5.5inch
```

对于第一个function Phone()，可以换种写法，如下：

```javascript
class Phone{
    //静态属性
    static name = '手机';
	static change(){
        console.log("我可以改变世界");
    }
}

let nokia = new Phone();
console.log(nokia.name);//显示为undefined
console.log(Phone.name);//正常显示为“手机”
```

3.类的**继承**

（1）因为ES5写类的继承太复杂了，所以这里直接呈现使用ES6的方法！

```javascript
// ES6class类继承 
class Phone{ 
    constructor(brand,price) { 
        this.brand = brand; 
        this.price = price; 
    }
    call(){ 
        console.log("我可以打电话！"); 
    } 
}
class SmartPhone extends Phone{ 
    // 构造函数 
    constructor(brand,price,color,size) { 
        super(brand,price); 
        // 调用父类构造函数 
        this.color = color; 
        this.size = size; 
    }
    photo(){ 
        console.log("我可以拍照！"); 
    }
    game(){ 
        console.log("我可以玩游戏！");
    } 
}
```

（2）复写父类的方法，直接覆盖命名即可，注意在子类中无法使用super()来调用相应的父类中的方法！

```javascript
class Person{
    constructor(name,age){
        this.name=name;
        this.age=age;
    }
    work(){
        console.log("工作！");
    }
}

class student extends Person{
    constructor(name,age,nianji){
        super(name,age);//构造方法可以调用父类的
        this.nianji=nianji;
    }
    work(){
        console.log("复写父类的方法，我是学生我要学习！")
    }
}
let wxm = new student("王小明",12,"初一");
wxm.work()
```

结果：

![QQ20220114231554.png](https://img.pterclub.com/images/2022/01/14/QQ20220114231554.png)



若子类中的成员方法（非构造方法）调用了父类方法（通过super()），那么就会报错！

```javascript
    class student extends Person{
        constructor(name,age,nianji){
            super(name,age);//构造方法可以调用父类的
            this.nianji=nianji;
        }
        work(){
            super();
            console.log("复写父类的方法，我是学生我要学习！")
        }
    }
```

work方法中有super()，则结果如下：

![QQ20220114231831.png](https://img.pterclub.com/images/2022/01/14/QQ20220114231831.png)

4.js中class中的get和set方法。

get方法是在获取成员变量时会自动触发调用，若get有返回值则返回值就是属性的值，若没有返回值就是undefined，一般用作动态属性的get，比如求总和等等...

set方法与get方法同理，可以在设置值之前先对设置的值做判断。

```javascript
class Phone{
    get price(){
        console.log("价格属性被读取！")
        return 123;//返回值
    }
    set price(new_val){//注意set方法必须要有一形参，不然会报错
        console.log("价格属性被修改！")
    }
}
let s = new Phone();
console.log(`默认调用get函数获取成员变量就是返回值${s.price}`);
s.price=1515;
console.log(`修改后再调用${s.price}`)
```

结果：

![QQ20220114232817.png](https://img.pterclub.com/images/2022/01/14/QQ20220114232817.png)

比较正确的用法，类中还是有构造函数比较好，get后面不要直接就跟属性名字，容易导致回调栈的溢出！

```javascript
    class Phone{
        constructor(name,price) {
            this.name=name;
            this.price=price;
        }
        get getprice(){
            console.log("价格属性被读取！")
            return this.price
        }
        set setprice(new_val){     //注意set方法必须要有一形参，不然会报错
            console.log("价格属性被修改！")
            if(new_val>2000){
                console.log("进来了")
                return false;
            }else{
                this.price=new_val
            }
        }
    }
    let s = new Phone("小米","100");
    console.log(`默认调用get函数获取成员变量就是返回值${s.getprice}`);
    s.setprice=1515;
    console.log(`修改后再调用${s.getprice}`)
    s.setprice=2200;
    console.log(`修改后再调用,但是修改不生效${s.getprice}`)
```

结果：

![QQ20220114234055.png](https://img.pterclub.com/images/2022/01/14/QQ20220114234055.png)

## 新特性17----数值拓展

### Number.EPSILON:

Number.EPSILON 是 JavaScript 表示的**最小精度**；

EPSILON 属性的值接近于 2.2204460492503130808472633361816E-16；



因为js中的浮点数是有误差的，比如：

```javascript
console.log(0.1+0.2);
console.log(0.1+0.2 === 0.3);//false
```

结果发现是不相等的！

![QQ20220115170634.png](https://img.pterclub.com/images/2022/01/15/QQ20220115170634.png)

在常识下，0.1+0.2=0.3，这种情况下我们使用EPSILON来判断相等。

```javascript
equal = (a,b) => return Math(a-b)<Number.EPSILON;
console.log(equal(0.1 + 0.2,0.3));//true
```

### 二进制与八进制

```javascript
console.log("1、二进制和八进制"); 
let b = 0b1010; //二进制
let o = 0o777; //八进制
let d = 100; //十进制
let x = 0xff;//十六进制
```

###  Number.isFinite 检测一个数值是否为有限数

```javascript
console.log(Number.isFinite(100)); //true
console.log(Number.isFinite(100/0));//false
console.log(Number.isFinite(Infinity));//false
```

### Number.isNaN 检测一个数值是否为 NaN

```javascript
console.log(Number.isNaN(123));//false
```

 

### Number.parseInt Number.parseFloat字符串转整数

就算字符串里有除数字以外的字符也可以转换，转换函数会自动截掉。

```javascript
console.log(Number.parseInt('5211314love')); //5211314
console.log(Number.parseFloat('3.1415926神奇'));//3.1415926
```

### Number.isInteger 判断一个数是否为整数

```javascript
console.log(Number.isInteger(5)); //true
console.log(Number.isInteger(2.5));//false
```

### Math.trunc 将数字的小数部分抹掉

```javascript
console.log(Math.trunc(3.5));//3
```

### Math.sign 判断一个数到底为正数,负数还是零

```javascript
console.log(Math.sign(100)); //1
console.log(Math.sign(0)); //0
console.log(Math.sign(-20000));//-1
```

## 新特性18----对象拓展

### 概述

ES6 新增了一些 Object 对象的方法：

1.Object.is 比较两个值是否**严格相等**，与『===』行为基本一致（+0 与 NaN）；

2.Object.assign 对象的合并，将源对象的所有可枚举属性，复制到目标对象；

3.**proto**、setPrototypeOf、 setPrototypeOf 可以直接设置对象的原型；

### 代码

```javascript
// 对象扩展 
// 1. Object.is 比较两个值是否严格相等，与『===』行为基本一致（+0 与 NaN）
console.log(Object.is(120,120)); // === 
// 注意下面的区别 
console.log(Object.is(NaN,NaN)); //true
console.log(NaN === NaN); //true
// NaN与任何数值做===比较都是false，跟他自己也如此！ 
// 2. Object.assign 对象的合并，将源对象的所有可枚举属性，复制到目标对象； 
const config1 = { 
    host : "localhost", 
    port : 3306, 
    name : "root", 
    pass : "root", 
    test : "test" // 唯一存在 
}
const config2 = { 
    host : "http://zibo.com", 
    port : 300300600, 
    name : "root4444", 
    pass : "root4444", 
    test2 : "test2" 
}// 如果前边有后边没有会添加，如果前后都有，后面的会覆盖前面的 
console.log(Object.assign(config1,config2)); 
// 3. __proto__、setPrototypeOf、 getPrototypeOf 可以直接设置对象的原型； 
const school = { name : "尚硅谷" }
const cities = { xiaoqu : ['北京','上海','深圳'] }
// 并不建议这么做 
Object.setPrototypeOf(school,cities); 
console.log(Object.getPrototypeOf(school));
console.log(school);
```

## 新特性19----模块化

### 概述

模块化是指将一个大的程序文件，拆分成许多小的文件，然后将小文件组合起来；

### 优点

模块化的优势有以下几点：

1.防止命名冲突；

2.代码复用；

3.高维护性；

### 模块化规范产品

ES6 之前的模块化规范有：

1. CommonJS => NodeJS、Browserify； 

2. AMD => requireJS； 

   3.CMD => seaJS；

### 模块化的语法

1.模块化的使用主要由导入模块和导出模块构成：

- export 命令用于规定模块的对外接口（导出模块）；
- import 命令用于输入其他模块提供的功能（导入模块）；



首先是**导出模块**

（1）m.js(导出模块)：

几种暴露方式的效果是一致的，但是使用默认暴露的话，调用方法前要加个default

①分别暴露

```javascript
export let school = "尚硅谷"; 
export function teach(){ 
    console.log("我们可以教你开发技术！"); 
}
```

②统一暴露

```javascript
let school = "尚硅谷"; 
function teach(){ 
    console.log("我们可以教你开发技术！"); 
}
export{school,teach}
```

③默认暴露

```javascript
export default{
    let school = "尚硅谷"; 
	function teach(){ 
    	console.log("我们可以教你开发技术！"); 
	}
}
```



(2)模块化.html，导入和使用模块

```javascript
<script type = "module" > // 引入m.js模块内容 
	import * as m from "./js/m.js";
	console.log(m);
	console.log(m.school);
	m.teach();
	//m.default.teach();如果是默认暴露的话，就需要这样调用
</script> 
```

运行结果：

![QQ20220115173951.png](https://img.pterclub.com/images/2022/01/15/QQ20220115173951.png)

**引入模块**的语法如下：

1.通用方式：

```javascript
import * as m from "./js/m.js";
console.log(m);
m.teach();
```

2.解构赋值形式：

```javascript
import {school,teach} from "./js/m.js";
// 重名的可以使用别名
import {school as xuexiao,findJob} from "./js/n.js";
// 导入默认导出的模块，必须使用别名
import {default as one} from "./js/o.js";
// 直接可以使用 
console.log(school);
teach();
```

3.简便形式，只能针对默认导出：

```javascript
import oh from "./js/o.js";
console.log(oh);
console.log(oh.school);
oh.change();
```

4.通过js文件，创建一个入口js文件来引入

比如创建一个app.js文件

```javascript
// 通用方式 
// 引入m.js模块内容 
import * as m from "./m.js"; 
console.log(m); 
console.log(m.school); 
m.teach();
```

在html页面里直接引用app.js文件

```html
<!DOCTYPE html>
<html>
    <head>
    	<meta charset="utf-8">
        <title>使用模块化的另一种方式</title>
	</head>
	<body>
            <script src="./js/app.js" type="module"></script>
	</body>
</html>
```

运行结果：

![QQ20220115175908.png](https://img.pterclub.com/images/2022/01/15/QQ20220115175908.png)

## 新特性20----Babel

### 概述

Babel 是一个 JavaScript 编译器；**Babel 能够将新的ES规范语法转换成ES5的语法**；

因为不是所有的浏览器都支持最新的ES规范，所以，一般项目中都需要使用Babel进行转换；

步骤：使用Babel转换JS代码——打包成一个文件——使用时引入即可；

### 步骤

第一步：安装工具babel-cli（命令行工具） babel-preset-env（ES转换工具） browserify（打包工具，

项目中使用的是webpack）；

第二步：初始化项目

```bash
npm init -y
```

第三步：安装

```bash
npm i babel-cli babel-preset-env browserify
```

第四步：

```bash
npx babel js（js目录） -d dist/js（转化后的js目录） --presets=babel-preset-env
```

第五步：打包

```bash
npx browserify dist/js/app.js -o dist/bundle.js
```

第六步：在使用时引入bundle.js

```html
<script src="./js/bundle.js" type="module"></script>
```

### 转换前后对比

转换前：

```javascript
export let school = '尚硅谷';
export function teach() {
    console.log("我们可以教给你开发技能"); 
}
```

转换后：

```javascript
"use strict";

Object.defineProperty(exports, "__esModule", {
    value:true
});
exports.teach = teach;
var school = exports.school = '尚硅谷';
function teach() {
    console.log("我们可以教给你开发技能");
}
```

## 新特性21----ES6模块化引入NPM包

第一步：安装jquery

```bash
npm i jquery
```

第二步：在app.js使用jquery

```javascript
//入口文件
//修改背景颜色为粉色
import $ from 'jquery';// 相当于const $ = require("jquery");
$('body').css('background','pink');
```
