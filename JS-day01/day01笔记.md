### 一、执行环境关联着变量对象

##### 1. {执行环境}关联着一个{变量对象}，变量对象存着我们声明的变量以及对象

##### 2. 全局执行环境，window对象

```
<script>
    var a = 1;
    funciton add2 (num){
        var b = num + 2；
        function output(c){
            console.log(a,b,c)
        }
        output(b);
    }
    add2(a);
    
</scirpt>
```

### 二、执行环境栈

##### 1.当代码在函数中执行时，函数也有执行环境，环境被推入{执行环境栈}中

##### 2.栈：存放数据的容器，先入后出

### 三、作用域与作用域链

##### 1. 标识符：变量、函数、对象的属性的名字，函数的参数

##### 2. 作用域：{标识符} 以及 {标识符所能访问的范围}

##### 3. 作用域链：作用域一层包裹这一层，形成的链式结果

##### 4. 关系：代码在执行环境中执行时，会创建 {作用域链}， {变量对象}中存着各种作用域的标识符

##### 5. 作用域链的作用：标识符查找，沿着作用域链一级一级地往外层找，知道找到全局作用域window，如果找不到就报错

##### 6. 拓展：作用域链确保了标识符的 {有序访问}

##### 7. 全局作用域、局部作用域、块级作用域

### 四、作用域的分类

##### 1. 全局作用域 window 对象

##### 2. 局部作用与-函数作用域，函数中代码执行后会被自动销毁

##### 3. 块级作用域：ES5没有块级作用域

```
// 块级作用域：用 {} 包裹的代码块
if（true）{
    var a = 10;
}
console.log(a)
// ES6 新增的块级作用域
var str = 'hello';
for(var i = 0; i < str.length; i++){
    console.log(str[i])
}
console.log(i) // 5
```

##### 4.let和const声明变量的特性：它们定义的变量只能在所在的代码块内被访问 => ES6 新增块级作用域

### 五、ES6箭头函数

##### 1. 写法：const sum = (形参1，形参2，形参n) => {...}

```
/*
* 箭头函数的写法
*
* 求和函数，传入的数相加 return 
*/
// ES5的写法
function sum(num1,num2){
    return num1 + num2
}

// ES6 箭头函数
const sum = (num1,num2) => {
    return sum1 + sum2
}
console.log(sum)

// 箭头函数的简写
// 参数：如果传入的参数只有一个 （）可以省略
// 函数体：如果函数体只有一行代码 {}可以省略，如果省略{}，return必须省略
const sum = num => num + 3;
```

### 六、函数的形参与实参

##### 1.形参：函数 {定义时} 所列的 {参数变量}

##### 2.实参：函数 {调用时} 所传递的 {值}

```
// 函数的形参与实参
const sum = (num1,num2) =>{
    return num1 + num2
}
const sum2 = (num3) => num3 + sum(1,2);

console.log(sum2(3))
```

### 七、arguments

##### 1.arguments 是一个类数组对象，它包含着所有传入函数的参数

##### 2.arguments 指的是 [实际传入] 的参数值

```
// 求和函数 - 打印传入参数的个数
function sum(num1,num2){
    console.log(arguments.length)
    return num1 + num2
}
sum(1,2);
```

### 八、函数的默认值

```
// ES5的默认值写法
function log(x,y){
    let y1 = y || 'world'
    console.log(x,y)
}
log('hello','world')

// ES6的默认值写法
function(x,y = 'world'){
    console.log(x,y)
}
log('hello','world')
```

### 九、ES6的rest参数

##### 1.写法: ...变量名 它是一个真正的数组

```
/*
* ES6的rest参数
*/

// ES5 对传入的所有参数求和
function sum(){
    let result = 0;
    for(let i = 0; i<aruments.length; i++){
        result += aruments[i]
    }
    return result;
}
console.log(sum(1,2,3))

// ES6的写法
const sum2 = (...values) =>{
    let result = 0;
    values.forEach( item => {
        result += item
    })
    return reult;
}
console.log(sum2(1,2,3))
```

### 十、函数的调用

##### 1. 一般函数调用

##### 2. 对象方法的调用

##### 3. 回调函数的调用

##### 4. 构造函数调用

##### 5. bind()、 call()、apply()

##### 6. 立即执行函数表达式 IIFE （Immediately Invoked Function Expression）

```
// 一般函数的调用
function sum(){  // 具名函数
    console.log(‘我是一般函数’)
}

// 函数表达式
const sum2 = () =>{ // 匿名函数
    console.log('我是函数表达式')
}

// 对象的方法
const obj = {
    method:function(){
        console.log('我是对象方法')
    }
}
obj.method();

// ES6 对象的扩展，对象方法的简写
const obj2 = {
    method(){
        console.log('我是对象方法简写')
    }
}
obj2.method();

// 回调函数
/* 延迟执行的定时器 */

window.setTimeout(() =>{ // 回调函数:现在不掉，回头（合适时机）再调
    console.log('1秒后执行')
},1000)

// 事件绑定
var ele = document.getElementById('id').addEventListener('click',function(){
    
})
```

### 十一、立即执行函数表达式

##### 1. 写法：(function(){...函数体})() 前一个() 是变成表达式，后一个() 是调用它

```
/* IIFE 立即执行函数表达式 */
(function(){
    console.log('我是立即执行函数表达式')
})()
```

##### 2. 作用：形成了局部函数作用域,避免了直接访问变量，可以实现简单的模块化

```
// 最早的模块化实现方案
;(function(){
    var money = 100;
    window.$me = {
        money:money;
    }
})()
```

### 十二、闭包

###### 1. 闭包的形成：变量的【跨作用域访问】，便形成了闭包；

###### 2. 闭包是什么？【函数】以及【函数内部跨作用域所能访问的变量】

###### 3. 闭包使得函数内部能够访问函数创建时所处作用域的变量

```
/* 一个简单的闭包 */

let money = 500;
function spendMoney(){
    console.log(money) // 数钱
    money -= 100; // 花钱
}

spendMoney() // 500
```

### 十三、闭包的常见使用场景-嵌套函数中使用闭包

###### 1. 父包含子，子访问父，最后再把子函数return或者挂载到window

```
/* 嵌套函数中使用闭包 */
function mom(){
    let money = 500;
    function spendMoney(){ // mom的函数作用域
        console.log(money) // 花钱
        money -= 100; // 花钱
    }
    return spendMoney
    /* 挂到window上 */
    //window.spendMoney = spendMoney;
}
mom();
```

### 十四、IIFE中使用闭包

###### 1. 闭包使得跨作用域访问的变量，不被销毁

```
// 需求：实现永不重复的计数器，需要一个函数，调用它，计数器+1，初始值100

cosnt getNum = (function(){
    let num = 100;  // 变量泄露，num会被释放么？
    return function(){
        return num++
    }
})()
console.log(getNum()) //100
console.log(getNum()) //101
```

### 十五、闭包解决for循环定时器问题

```
// 闭包解决for循环定时器问题

for(var i = 0; i < 5; i++){
    window.setTimeout(() =>{
        console.log(i) // 此时的i访问的是全局作用域上的i就是window上的i
    },1000)
}

// ES6解决此问题 利用ES6中的let声明变量
for(let i = 0; i < 5; i++){
    setTimeout(() =>{
        console.log(i)
    }，1000)
}
// 利用闭包解决此问题
var i;
for(var i = 0; i < 5; i++){
    :(function(k){ // 此处的k是形参
        window.setTimeout(() =>{
            console.log(k)
        },1000)
    })(i) // 此处的i是传递的实参
}
```

### 闭包的作用

###### 1. 闭包的作用：“间接访问变量”，或者“隐藏变量”。

```javascript
// 闭包的作用

;(function(){
    let money = 2000; // 初始值
    
    let photo1 = '1';
    let photo2 = '2';
    let photo3 = '3';
    
    window.$key = {
        consoleMoney(){  // 执行方法
            console.log(money); 
        }
        spendMoney(){
            money -= 100; 
        }
    }
})()
$key.consoleMoney(); // 读取
$key.spendMoney(); // 执行函数，money为1900
```

