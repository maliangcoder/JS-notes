## 一、基本类型与引用类型的内存分配
1. 基本类型（6）：String、Number、Boolean、Null、Symbol（ES6新增）
2. 引用类型（1）：Object（函数、数组，对象）

```
// 基本类型 
let a = 1;
let b = 2;
```

3. 基本类型：存在【栈内存】
4. 引用类型：实际的数据存在【堆内存】，【地址】存在【栈内存】中
5. 作用：在JS中如何访问引用类型数据？先在[栈内存]找地址，然后顺藤摸瓜的找到[堆内存]中的实际数据

## 二、变量的拷贝 （复制）
1. 基本类型拷贝的是【值】
2. 引用类型：拷贝的是【地址】，新旧变量共享【堆内存】中的数据
```
// 基本类型
let a = 100;
let b = a;

// 引用类型
let user1 = {
	name:'元宝',
	age:10
}
let user2 = user1；
user2.age = 11;
console.log(user1.age) // 11 因为共用同一个内存空间，所以一个值修改，另一个跟着改变


```
## 三、函数的传参
1. 函数的传参，相当于把外面的变量【拷贝】给参数
2. 传参时：
 （1）传基本类型：将传递的【值】拷贝的参数
    （2）传引用类型：将传递的【地址】拷贝给参数
```
 // 函数的传参
 // 基本类型，拷贝值
let a = 100;
function fn(b){
	b = 200
}
fn(a)
 console.log(a)
 
 // 引用类型
 let user = {
 	name:'元宝',
 	age:10
 }
 function fn2(b){
 // 参数 b = user,引用类型拷贝的是地址，值改变，另一个值会跟着变
 	b.age = 11
 }
 fn2(user)
 console.log(user.age) // 11 
```
## 四、对象的拷贝（深/浅拷贝）
1. 对象的拷贝，根据拷贝[层级]的不同，区分[深拷贝]和[浅拷贝]
2. 浅拷贝：只拷贝1层，遇到引用类型属性的数据，拷地址
3. 深拷贝：无限层级的拷贝,新旧对象互不影响
## 五、for-in 循环
1. 示例中，for-in循环式浅拷贝。
```
const user1 ={
	name:'元宝',
	age:20,
	like:['打游戏']
}
let user2 = {} // 新对象
for(let key in user1){
	user2[key] = user1[key]
}
console.log(user2)

user2.age = 11;
console.log(user1.age) // 10 基本类型拷贝值

user2.like.push('睡觉')
console.log(user1.like) // ['打游戏','睡觉'] // 引用类型拷贝地址
```
## 六、Object.assign()
1. 将源对象的属性拷贝到目标对象，得到新对象
```
const user1 = {
	name:'元宝', // 基本类型
	age:10,
	like:['打游戏'] // 引用类型
}
const user2 = Object.assign({},user1)
console.log(user2)

user2.age = 11;
console.log(user1.age) // 10
user2.like.push('睡觉')
console.log(user1.like) // ['打游戏','睡觉']
```
## 七、JSON方法
1. 将旧对象转成字符串
2. 将字符串解析成新对象
3. 优势：新旧对象互不影响
4. 缺点：没办法拷贝函数类型的属性（对象方法）
```
const user1 = {
	name:"元宝",
	age:10,
	like:['打游戏']
}
// 1.将旧对象转成字符串
const str = JSON.stringfly(user1);
console.log(str)

// 2.再将字符串解析成新对象
let user2 = JSON.parse(str);
console.log(user2)
```
## 八、lodash()
1. _.cloneDeep 完美实现深拷贝

## 九、typeof 类型检测
```
// typeof 基本类型
	typeof('元宝') // string类型
	typeof(10) // number类型
	typeof(false) // boolean类型
	typeof(undefied) // undefined类型
	typeof(null) //object类型
	
	typeof(Symbol('a')) // symbol类型
	
	// 引用类型
	typeof({}) // object
	typeof([]) // object
	
	
	typeof(function(){}) // function类型
```
typeof 检测：
	（1）检测基本类型相对准确（string、Boolean、number、undefined、symbol）
	（2）typeof(null) 返回的是 "object"
	（3）检测引用类型，除函数（function），其他都是object
## 九、instanceof
	公式：变量 instanceof 类型(构造函数)
	原理：检测【构造函数】的【原型】是否在【实例变量】的原型链上
```
// instanceof

	let variable
	variable = {};
	variable instanceof Object // true
	
	variable = [];
	variable instanceof Array // true
	
	variable = function(){};
	variable instanceof Function // true
```
## 十、Object.prototype.toString.call()
	借用 Object.prototype 上的 toSting() 方法，不是将数据值转成字符串，将【类型信息】以"[object Type]" 格式输出
```
Object.prototype.toString.call('元宝') //[object String]
```
## 十一、Array.isArray （只能检测数组）

## 十二、ES5继承
	子类继承父类   父类 => 子类 => 实例
```
// 父类 - 鱼类
function Father(){
	this.skill = '游泳' //技能,实例属性
	
}
Father.prototype.getFatherSkill = function(){
	console.log(this.skill)
}

// 子类 - 花鲢
function Son(){
	this.name = '花鲢'
}

// 子类继承父类 - 令子类原型 = 父类的实例
Son.prototype = new Father()

const lian1 = new Son() // 得到花鲢1的实例
lian1.getFatherSkill()  // '游泳' 继承成功
```
## 十三、原型继承
	最大的问题：原型上引用类型属性的数据，会被所有实例所共享，一旦数据改变，影响所有实例
## 十四、寄生组合式继承
	思想：
		寄生式：通过Object.create()链接子类原型与父类原型，避免了多余的父类构造函数的执行;
		组合式：通过调用父类构造函数，来继承【继承属性】，通过父类原型来【继承方法】;