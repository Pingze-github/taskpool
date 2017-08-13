# taskpool
A easy-use nodejs concurrency control module.

#### Usage

```
const Taskpool = require('./taskpool');
const taskpool = new Taskpool();

function delayPrint(i) {
    // this func delay i s and then print i
    // it must return a Promise object
    // you can use 'return new Promise()' or 'async function'
}

taskpool
    .option({
        endsWhenEmpty: false
    })
    .init([1,2,3,4,5])
    .limit(2)
    .task(delayPrint)
    .process()
    .on('success', (result, params) => {
        console.log(`${params} print success`);
    })
    .then((results) => {
        console.log(`all results: ${results}`);
    })
    .start();

setTimeout(() => {
   taskpool.push(1);
   taskpool.waitend();
}, 10 * 1000);
```

output: <br>
    after 1s, print 1 <br>
    after 2s, print 2 <br>
    after 3+1s, print 3 <br>
    after 4+2s, print 4 <br>
    after 5+3+1s, print 5 <br>
    after 10+1s, print 1 <br>
    then process exit

#### features
+ 面向对象设计，使用组合模式
+ 异常处理机制
+ 全面的设置
+ 使用Promise
+ 最低兼容到ES6
+ 链式调用
+ 事件机制
+ 进度查看

