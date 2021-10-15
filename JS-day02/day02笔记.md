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
4. 事件处理函数中