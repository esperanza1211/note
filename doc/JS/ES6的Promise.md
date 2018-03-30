#   Promise
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


#   async和await

在ES7中新增的方法

await后面必须返回Promise对象

使用await语法的地方必须是一个async函数

await 必须在函数中使用

```
var arr = [
    'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1513334879066&di=6c3314c64e6a71e7e381bea73ae76d3a&imgtype=0&src=http%3A%2F%2Fb.hiphotos.baidu.com%2Fimage%2Fpic%2Fitem%2F5bafa40f4bfbfbedd2d8739072f0f736aec31f5f.jpg',
    'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1513932576&di=dde850bb404539a1664a9e757cb67c3e&imgtype=jpg&er=1&src=http%3A%2F%2Fimgsrc.baidu.com%2Fimage%2Fc0%253Dshijue1%252C0%252C0%252C294%252C40%2Fsign%3D6b1f594cf9deb48fef64a99d9876505c%2F8d5494eef01f3a29bb1016e39325bc315d607cc7.jpg'
];

function loadImage(src) {
    return new Promise( (resolve, reject) => {
        let img = new Image();
        img.onload = function() {
            resolve({w: this.width, h: this.height});
        };
        img.onerror = function() {
            reject();
        };
        img.src = src;
    } );
}

document.onclick = async function() {
    let rs1 = await loadImage(arr[0]);
    console.dir(rs1);

    let rs2 = await loadImage(arr[1]);
    console.dir(rs2);
}
```
