## 一、ES6背景与概念
	1.复习：箭头函数、模板字符串、新增块级作用域、对象方法简写、symbol、let与const、函数的reset参数、函数默认值。
	2.ES6是什么？H5是语言标准，ES6语言标准
	3.ES6：泛指下一代JavaScript语言标准，每年更新，拓展语法

## 二、Babel
	1. 他是一个JS编辑器，能将ES6的代码编译成ES5

## 三、变量的解构赋值
	变量的解构赋值：理解成，按一定【结构】为变量赋值
	1. 数组的解构赋值
	```
	// 解构赋值
	let [a,b,c] = [1,2,3];
	console.log(a,b,c);
	
	//设置默认值
	let [x, y = 'yyy'] = ['xxx','yyy'];
	console.log(x,y)
	```
	2.对象的解构赋值 (限制：属性名一致)
	```
	// 对象的解构赋值
	const user = {
		name:"元宝",
		age:10
	}
	const { name, age } = user
	```
	3. 函数参数的解构赋值
	```
	// 函数参数的解构
	function add ([x,y]){
		return x + y
	}
	console.log(add([1,2]))
	
	// 默认值
	function move({x = 0,y = 1} = {}){
		return [x,y]
	}
	console.log({x:1,y:2})
	```
## 四、展开运算符

1. 函数的rest参数

2. 展开字符串

   ```
   ​```
   	cosnt str = 'iloveyou';
   	console.log(...str) // i l o v e y o u
   	console.log([...str]) // ["i","l","o","v","e","y","o","u"]
   	
   	// 反转字符串的顺序
   	console.log([...str].reverse().join(''))
   ​```
   ```

3. 展开数组

   ```
   let arr = ['a','b','c']
   console.log(...arr)
   
   // 应用：数组的浅拷贝
   const arr2 = [...arr]
   arr2.push('d')
   console.log(arr1)
   
   // 应用2: 数组的拼接
   const arr3 = ['A','B','C'];
   const arr4 = [7,8,9, ...arr2, ...arr3]
   
   // 应用3：伪数组转为真数组
   function fn(){
   	console.log([...arguments]) // 伪数组转为真数组
   }
   ```

4. 展开数组

## 五、模板字符串

1. 使用反引号`` ，换行和空格都会保留，变量使用${} 拼接进去

## 六、对象的简写

```
const user = {
	name, // 如果属性名一样，可以简写
	sayName(){
		console.log('对象的简写')
	}
}
```

## 七、ES6的class

```
// ES5类的实现

//person 类
function Person(name,age){
	// 实例属性
	this.name = name;
	this.age = age;
}
// 原型方法
Person.prototype.show = function(){
	console.log('我是原型方法')
}
 // 类的静态方法：他是构造函数自己的方法，实例调不了
Person.say = function(){
	console.log('我是静态方法')
}
const yuan = new Person('元宝',10)

/* ES6-class */
// 声明一个类
class Person{
	constructor(name,age){ // 构造函数
		// 实例属性
		this.name = name;
		this.age = age；
	}
	// 原型方法
	show(){ // 不需要写prototype
		console.log(this.name);
	}
	
	// 关键字 static 静态方法
	static say(){
		console.log('我是静态方法')
	}
}
const yuan = new Person('元宝',10);
console.log(Objece.prototype.toString.call(Person)) // [object,Function] 类是一个function类型
Person.say(); // 我是静态方法
```

1. class 用它声明一个类，函数类型：

2. constructor：构造函数，可以传参，通过this绑定实例属性

3. 原型方法：不需要使用构造函数 prototype，写在最顶层

4. 静态方法：类的方法，实例不能调，使用static关键字声明在最顶层

5. 实例属性可以直接写在最顶层（固定的值，没有办法传递参数）

   

## 八、ES6模块化背景与概念

模块化解决了什么问题？

	1. 命名冲突
 	2. 职责分离

## 九、ES6模块化

ES6模块化相比传统模块化方案的优势：【编译时】进行模块依赖的处理，执行效率比浏览器运行时更高

## 十、ES6 class实现类的继承

```
/* ES6 - class类的继承 */
// 父类
class Father(){
	constructor(name,age){
		// 实例属性
		this.name = name;
		this.age = age;
	}
	// 实例属性
	skills = ['游泳'，'睡觉','吃食'];
	
	// 原型方法
	getFatherSkills(){
		console.log(this.skills)
	}
}
// 子类
class Son extends Father(){
	constructor(name,age){ // 子类的构造函数
		// super是父类的构造函数
		super(name,age) // 
	}
	// 实例属性
	color = 'blue'
	name = '基因突变的花鲢'
}

const lian1 = new Son('花鲢',5)
```

