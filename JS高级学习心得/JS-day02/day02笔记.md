## 一、面向对象与面向过程

1.  面向过程(POP): 侧重于分析【步骤】。优势：对流的把控清晰
2.  面向对象(OOP): 侧重于分析【个体】，考虑【职责】、【能力】、【个体间的关系】，优势：更贴近于真实的事物，更能够分析复杂且庞大的问题

```javascript
/* 面向对象封装本地存储 */ 
// 本地存储 sessionStorage、localStorage、cookie

// 增 | 改：
window.localStorage.setItem(key,value);
// 删：
window.localStorage.removeItem(key);
// 查：
window.localStorage.getItem(key);
// 清除：
window.localStorage.clear();

cosnt local = {
    set(key,value){ // 增，改
        window.localStorage.setItem(key,JSON.stringify(value))
    },
    remove(key){ // 删
        window.localStorage.removeItem(key)
    },
    get(key){ // 查
        return JSON.parse(window.localStorage.getItem(key))
    },
    clear(){ // 清空
        window.localStorage.clear();
    }
}
```

## 二、类(class)与实例对象

1. 类：具有【相同特征】的一类事物的抽象。例：[动物、家居、交通工具...]

2. 实例对象：具有【各自差异】的个体
3. 类与实例对象的关系？通过类可以创建具有相同特征的【实例对象】
4. JS总内置的类：Object、Array、String、Date、

## 三、对象的创建

1. 使用内置对象创建
2. 使用对象字面量创建
3. 使用工厂函数创建

```javascript
/* 对象的创建 */
// 1. 使用内置对象创建
const yuan = new Object();
yuan.name = '元宝';
yuan.sex = 1;

// 使用【对象字面量】创建 - 使用{}直接写对象
const yuan1 = {
    name:'元宝',
    sex:1
}

/* 工厂模式 - 设计模式 */
// 工厂函数：批量生产相似对象
function createChessPlayer(name,sex){
    // 1.创建一个空对象
    let obj = {};
    // 2.为对象赋属性和方法
	obj.name = name;
    obj.sex = sex;
    obj.sayName(){
        console.log(this.name);
    }
    // 3.返回对象
    return obj;
}
const yuan3 = createChessPlayer('元宝', 1);
const hong = createChessPlayer('小红', 2);
const pang = createChessPlayer('小胖', 3);

```

## 四、构造函数模式创建对象

1. 工厂模式的缺点：虽然工厂函数解决了对象的批量创建，没有解决【对象的识别的=】的问题 (对象属于哪一类？对象从哪里来的)
2. 语法：new 【构造函数】 = 【实例对象】

```
/* 构造函数模式 */
// 构造函数
fucntion ChessPlayer(name,sex){ // 大驼峰命名
	// 把属性和方法挂到 this 上
	this.name = name; 
	this.sex = sex;
	this.sayName(){
		console.log(this.name)
	}
	 // 构造函数不需要返回
}
//调用
const yuan = new ChessPlayer('元宝'，1); // 实例对象
yuan.sayName(); // 元宝
```

3. 构造函数与一般函数写法的区别：

   1) . 命名采用【大驼峰】

   2) . 把属性和方法挂载的this上，this指向最终创建出来的【实例对象】

   3) . 不需要返回值，默认return最终创建出来的【实例对象】

4. 使用关键字 new 创建对象的过程？

   1）创建一个空对象

   2）this指向空对象

   3）this上挂属性和方法

   4）返回对象

## 五、方法过载

1. 每个方法在不同的实例对象上都不一样，方法没法被共享。【方法过载】

## 六、原型对象

1. 原型对象：构造函数.prototype,它是一个【对象】，保存着被实例所共享的属性和方法。
2. 面试-谈谈对原型对象的理解：
   1. 函数创建时会自动有 `prototype` 属性，它是一个对象，就是原型对象，原型对象中存着被实例共享的属性和方法。
   2. 原型对象中有constructor属性，指向构造函数
   3. 实例对象有一个隐藏属性，`__proto__` 指向原型对象

```
/* 原型对象优化 */
fucntion ChessPlayer(name,sex){ // 大驼峰命名
	// 把属性和方法挂到 this 上
	this.name = name; 
	this.sex = sex;
}
// 把方法挂到原型对象上，解决方法过载的问题
ChessPlayer.prototype.sayName = function(){
	console.log(this.name)
};
yuan.prototype.sayName = hong.prototype.sayName; // true
```

## 七、原型链的形成

![image-20211015000252341](C:\Users\86130\AppData\Roaming\Typora\typora-user-images\image-20211015000252341.png)

## 八、理解原型链

1. 谈谈对于原型链的理解

   1.一个构造函数有它对应的原型，【原型】又可以【是】另一个构造函数创建出来的【实例】，它也有它所对应的原型，这种层层递进的关系形成的链式结构，就是【原型链】

   2.在对象上查找标识符，会先在自己身上找，如果找不到，往原型链上找，直到再回到他Object。

   

## 九、this的前6种指向

1. 全局中 => window对象
2. 一般函数中 => 【调用者】，谁调用就指向谁
3. 对象方法张 => 【调用者】，谁调用就指向谁
4. 事件处理函数中 => 指向事件源，触发事件的元素
5. 构造函数 => 实例对象
6. 定时器中 => 指向 window

## 十、bind()、call()、apply()

1. 作用：修改this的指向
2. bind：Function.prototype.call: 传入要改变的this以及参数列表

```
 /* bind() call()与apply() */
 const yuan = {
 	name:'元宝',
 	sex:1,
 	sayName(type,num){
 		console.log(`我是${this.name},我擅长用${type}，我又${num}枚棋子`)
 	}
 }
 yuan.sayName('黑旗',113);
 
 // 小胖
 const pang = {
 	name:'小胖'，
 	sex：1
 }
 yuan.sayName.call(pang,'耍赖',118)
```

3. Function.prototype.apply:用法与call一样，传入的【参数数组】

```
yuan.sayName.apply(pang,['耍赖',18]); // 一般第二个参数传入arguments

```

4. Function.prototype.bind: 得到一个改变了

```
// 使用bind，得到一个新函数，函数绑定了this
var sayPang = yuan.sayName.bind(pang) // 得到了一个函数
```

5. 谈谈对于bind、call、apply的理解与区别？

   （1）首先，他们都能改变this的指向；

   （2）从执行结果来看，call与apply调用函数，改变了this就会执行一次，，bind改变了this指向是得到了一个新函数（绑定了this），不会自己执行，所以需要自己调用一次

   （3）传参数不同：call与bind都是传递的参数列表，apply接收两个参数，所以第二个参数一般是以数组的形式来传递

## 十一、箭头函数中的this

1. 箭头函数中的this指向【定义时】所在的作用域，而不是调用时

```
/* 箭头函数中的this */
var id = 21;
window.setTimtout(function(){
	console.log(this.id) // 21
},1000)

function logId(){
	console.log(this) 
	// 箭头函数中的this是指向定义是的作用域而不是调用时
	window.setTimeout(() =>{ // 此时还是window再调用，但是箭头函数中的this值指向他的定义时的作用域了。
		console.log(this.id)
	},1000)
}
const obj = {id:42};
logId.call(obj)
```

