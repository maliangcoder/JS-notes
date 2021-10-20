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
const user2 = Object.assign(P{},user1)
console.log(user2)

user2.age = 11;
console.log(user1.age) // 10
user2.like.push('睡觉')
console.log(user1.like) // ['打游戏','睡觉']
```
## 七、JSON方法
1. 将旧对象转成字符串
2. 将字符串解析成新对象
3. 优势：新旧对象互补影响
4. 缺点：没办法拷贝函数类型的属性（对象方法）