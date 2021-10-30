##  一、同步与异步
	1.从代码执行的角度
		（1）同步：代码从上往下依次执行，后面的代码等前面的代码全部执行完，再执行
		（2）异步：代码从上往下依次执行，遇到异步代码，先放一边，等待着，等到全部同步代码执行完(合适的时机)，在执行

##  二、异步的常见编码场景
	1.定时器：window.setTimeout()，延迟执行；window.setInterval() 每隔固定间隔调用
	2.事件处理
	3.Ajax请求
	4.回调函数
##  三、回调函数
	1.有人的地方，就有江湖。有异步的地方，就有回调
	2.回调函数：现在不调，回头再调。等待合适的时机
	3.回调函数的作用：可以放心大胆的去执行异步代码，不用担心错过执行的时机
##  四、回调地狱

##  五、Promise
	1.Promise是什么？Promise是用来【管理异步操作】，可以用同步的方式编写异步代码。
	2.	new Promise 构造函数 = 实例
	3.Promise状态：进行中（pending）、已成功（fulfilled）、已失败（rejected）
		（1）状态切换不可逆，要么成功，要么失败；
			<1> 进行中 -> 已成功
			<2> 进行中 -> 已失败
		（2）状态不受外界干扰，只有异步操作的结果能够决定；
##  六、Promise语法
```
/* Promise的基本语法 */
new Promise((resolve,reject) =>{ // 构造函数的参数，是一个函数。这个函数的参数是resolve()、reject() 函数
	// 可以写同步代码、异步代码。用来决定异步操作何时改变状态
	if(true){ // 模拟异步操作成功
		resolve('成功的数据') // 解决   改变状态：进行中 —> 已成功
	}else{
		reject('失败的数据') // 拒绝	  改变状态：进行中 -> 已失败
	}
})
// 链式，Promise.prototype
.then((data) =>{ // .then() 的第一个参数，是个函数，成功时调用
	console.log('成功时调用',data)
})
.catch((err) =>{ // .catch() 第一个参数，是一个函数，失败时调用
	console.log('失败时调用',err)
})
```
##  七、Axios
	1.Axios库的定位：基于Promise的（面向浏览器和Node.js）的HTTp请求库
	2.调用AxiosAPI，返回Promise实例。

##  八、async与await
```
// async 用来表示函数中有异步操作，它写在函数前面
	async function fn(){
		// 此处写异步操作
	}
	const fn2 = async() =>{
		// 异步操作
	}
	
	//例子：
	async function consoleFn(){
		console.log(1)
		const res = await timer() // 用来等待一个异步操作，一般等待Promise的实例，Promise的状态切换（Promise的操作结果）
		console.log(3)
	}
	
	//异步逻辑的方法
	function timer(){
		return new Promise((resolve) =>{
			window.setTimeout(() =>{
				console.log(2)
				resolve();
			},2000)
			
		})
	}
	
```