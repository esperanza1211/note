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

##  模板字符串``

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

### 方法的简洁表示

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

通过程序内部处理，当参数缺省的时候，做一些默认处理

```
function add(x, y) {
    var x = x || 0;
    var y = y || 0;
}
```

在定义函数的时候，可以在形参上设置参数的默认值

注意：如果有多个参数，那么把有默认值的参数定义在参数列表的最后面

```
function add2(x=0,y=0) {
    console.log(x, y);
}
add2();//0 0

function add3(x=0,y) {
    console.log(x, y);
}
add3(0,1);    // 函数x参数的默认值没有任何的意义
```

##  函数的剩余参数

有些时候，函数的参数是不定参，通常情况下我们在函数内部是arguments，而不是定义形参列表

```
function arrSplice() {
    var arr = arguments[0];
    var start = arguments[1];
    var count = arguments[2];

    //从下标3开始的参数就是要添加的内容
}
```

...newValues : 表示参数中剩余的所有实参都赋值给newValues

```
function arrSplice2(arr, start, count, ...newValues) {
    console.log(arr, start, count, newValues);
}

arrSplice2([1,2,3], 1, 2, 'a','b','c');
```

##  扩展运算符...

扩展运算符和rest剩余参数效果正好相反

*   rest: 把参数转成数组

*   ...: 把数组转成参数

```
function add(a, b) {
    console.log(a, b);
}
add(1,2);
var arr = [10, 20];
add(arr[0], arr[1]);
add(...arr);//add(10,20)


var arr2 = [5,23,4345,65,123];
console.log( Math.max(...arr2) );//4345
```

把类数组集合转成数组

```
var elements = document.querySelectorAll('*');

console.log( [...elements] )
```

数组拼接

```
var arr1 = [1,2,3];
var arr2 = ['a','b','c'];
var arr3 = [...arr1, 'miaov', ...arr2];

console.log(arr3);//[1,2,3,'miaov','a','b','c']
```

##  箭头函数=>

箭头函数的声明只能是表达式形式，不支持函数声明的形式

1.  没有参数或参数大于1个的时候，需要使用 () ，有且仅有一个参数的时候可以省略 ()

2.  如果函数有且仅有一条语句，且返回的不是对象的时候，可以省略 {}，同时不需要使用 return，直接把该语句执行后的结果作为返回值

3.  箭头函数没有 arguments 对象

4.  箭头函数的 this 是声明期绑定，而不是执行期。**别把箭头函数作为事件函数直接调用**

5.  不能作为构造函数

[深入了解ES6的箭头函数](https://github.com/esperanza1211/note/blob/master/doc/JS/ES6%E7%9A%84%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.md)

##  对象扩展

*   Object.is()

```
console.log(NaN == NaN);//false

console.log( Object.is( NaN, NaN ) );//true

console.log( Object.is( +0, -0 ) );//false
```

*   对象的prototype

```
var arr = [1,2,3];
console.dir( arr.constructor.prototype );
console.dir( arr.__proto__ );   //这个方式并不是标准的

//标准推荐我们使用另外两个方法来获取和设置prototype
console.dir( Object.getPrototypeOf( arr ) );

Object.setPrototypeOf(arr, {
   a() {
       console.log('a')
   }
});
console.dir( Object.getPrototypeOf( arr ) );
```

##  Proxy

实例：通过Proxy代理了p1的访问

```
function Person(name, age) {
    this.name = name;
    this.age = age;
}

let p1 = new Person('莫涛', 10);

let p2 = new Proxy(p1, {
    get(target, name) {
        // target：被代理的对象
        // name : 当前被访问的属性
        console.log(target, name);
        if (name == 'age') {
            return '保密';
        }
        return target[name];
    },
    set(target, name, value) {
        // target : 被代理的对象
        // name : 设置的属性名
        // value : 值
        if (name == 'age') {
            console.log('不允许设置');
            return;
        }
        target[name] = value;
    }
});

console.log(p2.age);
//Person{name:"莫涛",age:10} "age"
//保密

console.log(p2.name);
//Person{name:"莫涛",age:10} "name"
//莫涛

p2.name = '陌陌';
p2.age = 1000;//不允许设置

console.log(p2.age);
//Person{name:"陌陌",age:10} "age"
//保密

console.log(p2.name);
//Person{name:"陌陌",age:10} "name"
//陌陌
```

*   Reflect

反射对象信息，通过这个对象可以获取到某个对象的所有元信息数据

```
console.log(Reflect)
console.log(Reflect.ownKeys(p2));//["name", "age"]

Object.freeze(p2);
console.log( Reflect.isExtensible(p2));//false
```

##  可迭代协议与迭代器

### for...of

不是所有的对象都可以被for...of的，只有实现了迭代器（迭代协议）的对象才可以for...of

当我们去for...of一个对象的时候，内部会调用该对象的迭代器函数

```
var obj = {
    left: 100,
    top: 200
};
for (var property in obj) {
   console.log(property);
}
//left top
for (var property of obj) {
   console.log(property);
}
//报错


var arr = 'abcde'.split('');
for (var property in arr) {
   console.log(property);
}
//0 1 2 3 4
for (var value of arr) {
   console.log(value);
}
//a b c d e
```

新的数据类型，symbol，对应有一个包装对象，Symbol.iterator：产生一个唯一值（迭代器名称）

    console.log(Symbol.iterator);//Symbol(Symbol.iterator)

```
var obj = {
    left: 100,
    top: 200
};

obj[Symbol.iterator] = function() {
    let keys = Object.keys(obj);
    var n = keys.length;
    var i = 0;
    return {
        next() {
            if (i < n) {
                let key = keys[i];
                i++;
                return {done: false, value: {k: key, v: obj[key]}}
            } else {
                return {done: true}
            }
        }
    }
};

for (var {k, v} of obj) {
    console.log(k, v);
}
//left 100 top 200
```

`obj[Symbol.iterator]()` => `{next(){}}` => `next()` => `{done,value}` => 根据该对象的done来处理后续行为

如果done为false，则把该对象的value赋值给of前面的变量，继续调用next

##  Set

Set与数组非常相似，但是Set数据结构的成员都是唯一的。

[ES6的Set数据结构详解](https://github.com/esperanza1211/note/blob/master/doc/JS/ES6%E7%9A%84Set.md)

##  WeakSet

WeakSet类似于Set，也是不重复的值的集合。但是它只能用于存储对象。而不能是其他类型的值。

WeakSet是一个个构造函数。可以接受数组和类似数组的对象作为参数。（实际上，任何具作为iterable接口的对象都可以作为WeakSet的参数）。该数组的所有成员都会自动成为WeakSet的实例对象的成员。 

```
var a = new [[1,2],[3,4]]; 
var ws = new WeakSet(a);
```

WeakSet数据结构有以下的上方法：

*   WeakSet.protoptype.add(value)：向WeakSet实例添加一个新成员。 

*   WeakSet.protoptype.delete(value)：删除WeakSet实例指定成员。 

*   WeakSet.protoptype.has(value)：返回一个布尔值，表示某个值是否在WeakSet实例中。

```
var ws = new WeakSet();
var obj = {};
var foo = {};
ws.add(window);
ws.add(obj);
ws.has(window);//true
ws.has(foo);false
ws.delete(window);//true
ws.has(window);//false
```

```
function fn() {
    // 当我们把obj返回出去的时候，外部有个变量和当前的obj引用的是同一个地址，导致函数的局部变量obj不会被销毁
    var obj = {x: 1};
    return obj;
}

function fn2() {
    var ws = new WeakSet();
    ws.add([1,2,3]);
    return ws;
}

var o = fn();
var w = fn2();
```

WeakSet 不能遍历，是因为成员都是弱引用，随时可能消失，遍历不能保证成员的存在。可能刚刚遍历结束，成员就取不到了。WeakSet的一个用处是存储DOM节点，而不用担心这些节点从文档移除时，会引起内存的泄露。

```
var weakset = new WeakSet()
let aObj = {a:'aa'}
let bObj = new String('你好')
let cObj = new Number(8)
 
weakset.add(aObj)
weakset.add(bObj)
weakset.add(cObj)

weakset.delete(aObj)
bObj = null   // 把对象删除，weakset中的对象也没了，垃圾回收机制，置空
console.log(weakset.has(bObj))  //false

//weakset不能取值，也不能显示，只用来表示是否有重复的对象
```

### Set与WeakSet的不同：

1.  WeakSet 成员只能够是对象 

2.  作为 WeakSet 成员的对象都是弱引用，即垃圾回收机制不考虑 WeakSet 对该对象的引用，也就是说，如果其他对象都不再引用该对象，那么垃圾回收机制会自动回收该对象所占用的内存，不考虑该对象还存在与WeakSet之中。这个特点意味着，无法引用WeakSet的成员，**因此WeakSet是不可遍历的。**

3.  使用WeakSet存储对象实例的好处是，由于是对对象实例的引用，不会被计入内存回收机制，所以删除实例的时候，不用考虑weaket，也不会出现内存泄漏。

##  Promise

[深入了解Promise]()

##  class

