Promise
构造函数
该函数有一个参数：函数，需要处理的异步任务，这个函数还接收Promise在执行过程传入的两个数据，这两个都是函数
    resolve
    reject

Promise会维护一个内部状态，该状态表示Promise处理的任务情况：
默认：pending，表示未完成，正在处理
     resolved: 已完成
     rejected: 失败的

在上面我们提到的两个函数的作用就是改变Promise内部状态的，当我们调用的 resolve() 就是把 Promise 的状态改为 resolved，当我们调用的 reject() 就是把 Promise 的状态改为 rejected，当一个Promise的状态被改变的时候，后续会自动调用 Promise 对象下其他对应的方法
    resolved : .then()
    rejected : .catch()
