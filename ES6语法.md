#### 箭头函数	

函数的语法糖

 ( 参数 ) => 函数体

例：

```js
const getSum1 = function (n) {

​	return n+3

}
```

转化为箭头函数为

getSum1 = ( n ) => n + 3

###### 箭头函数的其他写法

```js
const getSum2 = (n1, n2, ...other) => console.log(n1, n2, other)
```

输入 1，2，30，40，50

输出 1，2，**[30,40,50]**

...other会得到其余参数



### 异步处理

Promise  Async(语法糖)

任务处理顺序：**先处理同步任务，再处理异步任务**

例：

```js
console.log('任务1：同步')

console.log('任务2：同步')

setTimeout(()=>{

​	console.log('任务3：异步')

},0)

console.log('任务4：同步')
```

输出结果

任务1：同步

任务2：同步

任务4：同步

任务3：异步



##### Promise对象的使用

```js
const p1 = new Promise((resolve,reject) => {

​	resolve('任务成功得到的数据')

​    //reject('失败的信息')

})

p1.then(data => {

​	console.log(data)

})

.catch( err => {

​    console.log(err)

})
```

输出：任务成功得到的数据

当promise对象中调用了resolve，就会在后续触发then方法，打印出data的数据。如果是执行了reject方法，就会执行下面的catch，打印出错误数据



##### promise对象在多个异步任务中的使用

```js
const p1 = new Promise((resolve, reject) => {

​	reject('任务1失败的信息')

})



p1.then( data => {

​	console.log(data)

​	return new Promise((resolve, reject) => {

​		reject('任务2失败的信息')

​	})

}, err => {

​	console.log('任务1失败了')

​	throw new Error('任务1失败')//*任务1失败之后必须得抛出异常，否则会默认返回一个成功的promise对象导致任务2失败不能触发*

})

.then( data => {

​	console.log(data)

}, err => {

​	console.log('任务2失败了')

})
```



##### Async await的使用——异步编程

```js
async function main() {

​	console.log('任务1')

​	const data = await asyncTask()

​	console.log(data)

​	console.log('任务3')

}
```

main()

输出

任务1

任务2(asyncTask成功时的结果)

任务3



###### await的使用陷阱

1.多个异步语句

```javascript
async function f() {

​	const promiseA = fetch("http://.../post/1");

​	const promiseB = fetch("http://.../post/2");

​	//以上两个异步语句虽然没有逻辑错误，但处理效果还是和同步语句一样，是先执行完上面的语句再执行下面的，在这个时候就要使用下面这句方法

​	const [a, b] = await Promise.all([promiseA, promiseB])

}
```

2.循环中执行异步操作不能使用forEach()和map()方法

要使用正常的for循环

```javascript
async function f(){

​	for(let i of [1,2,3]) {
​		await someAsyncOperation();

​	}

​	console.log("done")

}
```

或者用for await

```js
async function f() {
	const promise = [
		someAsyncOperation(),
		someAsyncOperation(),
		someAsyncOperation(),
	];
	
	for await (let result of promises) {
		//...
		//这里的for循环会等到所有的异步操作都完成后才继续向后执行
	}
	console.log(done)
}
f();
```



#### promise的微任务队列和宏任务队列

Promise的微任务队列和宏任务队列是JavaScript事件循环机制中用于调度和执行异步任务的两个不同的队列。

1. 微任务队列（Microtask Queue）：
   - 微任务队列用于存储Promise的回调函数（即`.then()`和`.catch()`中的回调函数）、`async/await`的异步函数以及`queueMicrotask()`方法添加的函数等。
   - 微任务队列具有高优先级，即在JavaScript事件循环的每个宏任务结束后，会首先清空微任务队列中的任务，然后再执行下一个宏任务。
   - 常见的微任务包括Promise的回调函数执行、`async/await`的异步函数执行和`queueMicrotask()`方法添加的函数执行。

2. 宏任务队列（Macrotask Queue）：
   - 宏任务队列用于存储大部分的异步任务，如`setTimeout`、`setInterval`、`I/O`操作等。
   - 宏任务队列的优先级低于微任务队列，即在JavaScript事件循环中，宏任务在所有微任务执行完毕后才会执行。
   - 常见的宏任务包括定时器回调函数执行、事件回调函数执行、网络请求等。

在Javascript中，区分微任务和宏任务有几个主要的特点：
- JavaScript事件循环的开始是一个宏任务。
- 在宏任务执行期间，如果有微任务加入，它们会被添加到微任务队列中。
- 一个宏任务执行完毕后，会检查微任务队列中是否有任务，若有则先执行微任务队列中的所有任务。
- 在执行微任务队列过程中，如果又产生了新的微任务，会将这些新微任务添加到微任务队列的末尾。
- 所有微任务执行完毕后，JavaScript事件循环进入下一个宏任务。

需要注意的是，微任务队列中的任务在同一次事件循环中一直执行，直到微任务队列为空后才会执行下一个宏任务。这就保证了微任务的优先级高于宏任务。

总结：微任务队列和宏任务队列都是JavaScript事件循环中用于调度和执行异步任务的两种队列。微任务队列具有高优先级，先于宏任务队列执行，而宏任务队列在每个事件循环中只执行一个任务，之后会执行微任务队列中的任务。

希望这个回答对你有帮助。如果你有任何进一步的问题，请随时提问。





#### reduce函数的用法

`reduce` 是 JavaScript 数组的一个高阶函数，用于对数组中的元素进行累加、计算或转换等操作。

`reduce` 函数接受两个参数：
1. 回调函数：用于指定如何处理数组中的每个元素，它可以接受四个参数：
   - 累加器（accumulator）：用于存储累加的结果。
   - 当前值（current value）：表示当前正在处理的元素。
   - 当前索引（current index）：表示当前正在处理元素的索引。
   - 源数组（source array）：调用 `reduce` 方法的原始数组。
2. 初始值（initial value）：可选参数，表示初始的累加值。如果没有提供初始值，则将使用数组的第一个元素作为初始值，并从第二个元素开始迭代。

回调函数在每次迭代时被调用，它接收累加器和当前值作为参数，并可以根据需求对累加器进行操作。

下面是 `reduce` 函数的基本语法：
```javascript
array.reduce(callback, initialValue)
```

以下是几个常见的用法举例：

1. 累加数组中的所有元素：
```javascript
const numbers = [1, 2, 3, 4, 5];
const sum = numbers.reduce((accumulator, currentValue) => accumulator + currentValue, 0);
console.log(sum); // 输出 15
```

2. 将数组中的元素映射为新的形式：
```javascript
const numbers = [1, 2, 3, 4, 5];
const doubledNumbers = numbers.reduce((accumulator, currentValue) => {
  accumulator.push(currentValue * 2);
  return accumulator;
}, []);
console.log(doubledNumbers); // 输出 [2, 4, 6, 8, 10]
```

3. ##### 查找数组中的最大值：
```javascript
const numbers = [5, 2, 8, 1, 4];
const maxNumber = numbers.reduce((accumulator, currentValue) => {
  return Math.max(accumulator, currentValue);
}, 0);
console.log(maxNumber); // 输出 8
```

需要注意的是，在使用 `reduce` 函数时，回调函数的返回值会成为下一次迭代的累加结果（即下一次回调函数的第一个参数）。因此，根据具体的需求，可以在回调函数中对累加器进行不同的操作。

希望这些示例能帮助你理解 `reduce` 函数的用法。如有任何进一步的问题，请随时提问。





### split函数的用法

```js
//navigator_url:/pages/goods_list?query=服饰
//通过问号？进行分割，得到一个数组['/pages/goods_list','query=服饰']，取分割完的数组的第2项[1],
//取得query=服饰这个
navigator_url.split('?')[1]
```

