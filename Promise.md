# Promise相关讲解

1.Promise是ES6加入标准的一种异步解决方案,通常来表示一个异步操作过程的成功或失败，可以解决地狱回调问题。

```javascript
var p = new Promise(function(resolve,reject){...})
p.then(()=>{})
p.catch(()=>{})
```

当resolve被调用时，将promise的状态改为fulfilled

当reject被调用时，将promise的状态改为rejected

2.方法 `Promise.all(iterable)`

这个方法会返回一个新的promise对象，参数为一个promise列表,当列表中所有promise触发成功后才会触发成功，一旦有一个失败，则会马上停止其他promise的执行。当iterable里面的promise里面的结果都执行成功了，这个新的promise对象会将所有的结果以数组的形式一次返回，当一个失败时，这个新的promise对象会将失败信息返回。

3.方法`Promise.race(iterable)`

当 iterable 参数里的任意一个子 promise 被成功或失败后，父 promise 马上也会用子 promise 的成功返回值或失败详情作为参数调用父 promise 绑定的相应句柄，并返回该 promise 对象。

4.方法`Promise.reject(rease)`

返回一个状态为失败的Promise对象，并将给定的失败信息传递给对应的处理方法。

## Promise面试题

[Promise面试题](https://blog.csdn.net/qq_42033567/article/details/108129645)

任务分为 同步任务和异步任务

同步任务：在主线程上排队执行的任务，只有前一个任务执行完毕，才能执行后一个任务；

异步任务：不进入主线程，而进入任务队列的任务，只有任务队列通知主线程该任务可以执行，某个异步任务才会进入主线程执行。

宏任务:每次执行栈执行的一个代码就是一个宏任务，包括每次从任务队列中获取一个事件并将其对应的回调放入到执行栈中执行。宏任务需要多次事件循环才能执行完，**任务队列中的每一个事件都是一个宏任务**。

微任务:当前宏任务结束后立即执行的任务。微任务是一次性执行完的，在下一个宏任务执行完毕后，就会将它执行期间产生的微任务全部执行完毕，如果在微任务执行期间微任务队列加入了新的任务，就会将新的微任务放到队列尾部，之后会依次执行。

宏任务主要有：script代码段，setTimeout,setInterval,I/O,setImmediate

微任务主要有：process.nextTick(node),Promise的回调(then,catch,finally)