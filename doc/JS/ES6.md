# ECMAScript6

##  let
>   声明变量,类似`var`
*   不允许重复声明
*   必须先声明后使用（暂存死区）
*   支持块级作用域

```
//var 支持重复声明
var a = 1;
var a = 2;
console.log(a);//2

//let 不支持重复声明
let b = 1;
let b = 2;//报错
console.log(b);


//变量声明预解析
console.log( a );//undefined
var a = 1;

console.log( b );//报错
let b = 1;
```

##  const
>  常量声明
   - 支持块作用域
   - 先声明后使用
   - 不允许重复声明
   - 常量声明一定需要初始化

常量：固定不变的值，通过 const 声明的，值不能被修改

推荐，约定
**常量名称全大写**

```
const a = 1;
console.log(a);//1

//常量值一点确定，不允许改变
a = 2;//报错
console.log(a);

let a;
a = 1;

const b;
b = 2; // 这一步拆分以后属于修改常量值，所以不被允许

const c;
//c初始化值是undefined，后期有不能去修改，所以，常量声明不初始化没有任何意义，js干脆不允许只声明不赋值


//坑：
const obj = {
    x: 1,
    arr: [1,2,3]
};

// 不允许
obj = [1,2,3];
console.log( obj );//报错

obj.x = 10;
console.log( obj );//{x:10,arr:[1,2,3]}

// 如果你不想一个对象内容有任何的修改，可以冻结该对象
Object.freeze(obj);
// 浅冻结，可以通过递归操作实现深度的冻结
obj.x = 100;
obj.arr.push(4);
console.log(obj);//{x:10,arr:[1,2,3,4]}
```

##  块级作用域`{}`
>es6之前支持两个作用域：
- 全局
- 局部（函数）

>es6新增作用域：
- 块：一对 {} 产生一个块，在 {} 内部就会形成一个独立的作用域：块作用域

```
{
    let a = 1;
    console.log( a );//1

    var b = 2;
    console.log( b );//2
}
console.log( b );//2
console.log( a );//报错

```

### 块作用域实例

```
for (var i=0; i<5; i++) {

   setTimeout(function() {
       console.log(i);//5*5
   }, 1000);

}

for (let i = 0; i<5; i++) {

   setTimeout(function() {
       console.log(i);//0,1,2,3,4
   }, 1000);

}
```

```
var i = 0;
setTimeout(function () {
   console.log(i);//2
}, 1000);
i = 1;
setTimeout(function () {
   console.log(i);//2
}, 1000);
i = 2;
setTimeout(function () {
   console.log(i);//2
}, 1000);


{
   let i = 0;

   setTimeout(function() {
       console.log(i);//0
   }, 1000);

}
{
   let i = 1;

   setTimeout(function() {
       console.log(i);//1
   }, 1000);
}
```

```
html:
<ul>
    <li>000</li>
    <li>111</li>
    <li>222</li>
</ul>

js:

var lis = document.querySelectorAll('li');

for (var i=0; i<lis.length; i++) {

   lis[i].a = i;
   lis[i].onclick = function () {
       console.log(this.a);
   }

}

for (let i=0; i<lis.length; i++) {

    lis[i].onclick = function () {
        console.log(i);
    }

}
```

##  解构赋值

- 解构
- 赋值

对右侧的数据进行解构（解析解构），把值对应的一一赋值给左侧的变量

数组的解构赋值是 [] ，值是一一（位置）对应的
```
var arr = ['a', 'b', 'c'];

let [v1, v2, v3] = arr;

console.log(v1, v2, v3);//a b c
```

对象解构赋值

左侧是 {}，key一一对应

把obj中的y和x解构出来，赋值给y和x，所以左侧变量的名称和右侧对象中属性的名称是有关联的

```
let obj = {x:1,y:2};

let {y, x} = obj;

console.log(x, y);//1 2

let {x} = obj;

console.log(x);//1
```

我们可以给解析出来的属性变量取别名
下面这个等同于
`let mx = obj.x;`

```
let obj = {x:1,y:2};

let x = 100;

let {x: mx, y} = obj;

console.log(x, mx, y);//100 1 2
```

```
var left = document.body.getBoundingClientRect().left;
var right = document.body.getBoundingClientRect().right;

var {left, right} = document.body.getBoundingClientRect();
```

##  字符串扩展

>   es6 加强了对字符串的特性扩展
>   
>   http://unicode.org/Public/emoji/5.0/emoji-data.txt

```
//👰
//console.log( '\u{1F385}'.charCodeAt(0) );
//console.log( '\u{1F385}'.charCodeAt(1) );

//console.log( String.fromCharCode(55356) );

//ES6 推荐使用另外一个方法获取字符编码点
console.log( '\u{1F385}'.codePointAt(0) );
console.log( String.fromCodePoint(127877) );
```

##  模板字符串

>es6新增用于表示字符串的方式: `` ,
基础使用和普通字符串没有什么区别
1. 允许多行并保留编辑格式
2. 支持内嵌表达式
    语法：`${表达式}`

```
var str2 = '哈哈哈' +
            '嘻嘻嘻';
console.log( str2 );//哈哈哈嘻嘻嘻

var str3 = `哈哈哈
            嘻嘻嘻`;
console.log( str3 );
//哈哈哈
            嘻嘻嘻

```

```
var a = 100;
var b = 200;

console.log(`
    a + b = ${a+b}
`);//a+b=300
```

```
var arr = ['a', 'b', 'c'];

var newStr = `<ul>`;

arr.forEach( function(v) {
    newStr += `<li>${v}</li>`;
});

newStr += `</ul>`;

console.log(newStr);//<ul><li>a</li><li>b</li><li>c</li></ul>
```

##  数字扩展

>es6之前数字表示法只支持：10进制、16进制

>es6以后新增两种：2进制、8进制

* 2进制：0b/0B 开头      Binary
* 8进制：0o/0O 开头      Octal
* 10进制：1-9的数字开头   Decimal
* 16进制：0x/0X 开头     Hexadecimal

```
console.log( 0b10 );//2
console.log( 0O10 );//8
console.log( 10 );//10
console.log( 0X10 );//16
console.log( 0b11011 );//27
console.log( Math.hypot(3,4) );//5
```

##  数组扩展
### Array.from()

> 用于将类数组对象转为真正的数组

```
var lis = Array.from(document.querySelectorAll('*'));
console.dir(lis);
```

### Array.of()

>   用于将一组参数，转换为数组。

>   主要是解决 原来 数组中遗留一个 bug

>   当我们使用new Array方式来创建数组的时候，如果参数有且仅有一个并且是数字的时候，该参数不在是数组的值，而是数组的长度

```
var arr = Array.of('a','b','c');
console.dir(arr);

var arr1 = new Array('a','b','c');
console.dir(arr1);

var arr2 = new Array(5);
console.dir(arr2);
console.dir(arr2[0]);

var arr3 = Array.of(5);
console.dir(arr3);
```

### .find()

>   查找满足条件的第一个元素，参数是callback

>   参数：
>   1. 回调函数
>   2. 回调函数内this的指向


>   遍历整个数组，遍历过程中调用回调函数，如果回调函数的返回值为`true`，则返回当前正在遍历的元素。如果所有元素都不符合条件则返回`undefined`

### .findIndex()

>   找出第一个符合条件的数组元素的位置

>   参数：
>   1. 回调函数
>   2. 回调函数内`this`的指向

>   遍历整个数组，遍历过程中调用回调函数，如果回调函数的返回值为`true`，则返回该数组元素的位置。如果所有元素都不符合条件则返回-1

### .fill()

>   用来填充数组

>   参数:
>   1. 填充的内容
>   2. 起始位置
>   3. 结束位置

```
var arr = ['莫涛','童斌','钟毅'];
console.log( arr.find( function(item) {
    // 循环数组，把当前的循环值作为参数传递给item，同时执行该函数，根据该函数的返回来确定是否找到或者继续向后查找  
    return true;
} ) );

var users = [
    {
        name: '莫涛',
        sex: '男'
    },
    {
        name: '钟毅',
        sex: '男'
    },
    {
        name: '朱王洁',
        sex: '女'
    },
    {
        name: '童斌',
        sex: '男'
    }
];

console.log( users.find( function (user) {
    if (user.sex == '女') {
        return true;
    }
    return user.sex == '女';
} ) );

console.log( users[users.findIndex( function (user) {
    return user.sex == '女';
} )] );


console.log( ['a','b','c','d','e','f'].fill(0, 2, 4) );
```

##  对象简洁表达式

### 当一个对象的key与其值引用的变量名一致，可以简写成一个
```
var x = 10;
var y = 20;

var obj1 = {
    x,
    y,
    z: x
};

console.log(obj1);//{x:10, y:20, z:10}

var {left, right} = document.body.getBoundingClientRect();
var obj = {left,right};
console.dir(obj);
```

### 方法的简介表示

```
var obj1 = {
    method1: function(x, y) {
        return x + y;
    }
};

var obj2 = {
    method1(x, y) {
        return x + y;
    }
};
```

### 属性名表达式
*   es6之前，值可以是一个表达式
*   es6之后，键也可以是一个表达式，但是需要使用中括号包含

```
var obj1 = {
    a: 1 + 1,
    [1+1]: 'miaov'
};
console.dir(obj1);//{2:"miaov", a:2}
```

```
// 获取用户信息
const GET_USER_INFO = 1;
// 获取所有用户信息
const GET_USERS = 2;
// 提交用户信息
const POST_USER_INFO = 3;

let api = {
    [GET_USER_INFO]() {
        console.log('GET_USER_INFO');
    },
    [GET_USERS]() {
        console.log('GET_USERS');
    },
    [POST_USER_INFO]() {
        console.log('POST_USER_INFO');
    },
};
console.log(api);//{1:f, 2:f, 3:f}
api[GET_USER_INFO]();//GET_USER_INFO
```

##  函数默认值
```
function add(x, y) {
    // 通过程序内部处理，当参数缺省的时候，做一些默认处理
    var x = x || 0;
    var y = y || 0;
}

/*
* 在定义函数的时候，可以在形参上设置参数的默认值
* 注意：
*   如果有多个参数，那么把有默认值的参数定义在参数列表的最后面
* */
function add2(x=0,y=0) {
    console.log(x, y);
}
add2();

function add3(x=0,y) {
    console.log(x, y);
}
add3(0,1);    // 函数x参数的默认值没有任何的意义
```
