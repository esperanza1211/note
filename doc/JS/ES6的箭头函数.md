#   ES6的箭头函数

##  基本用法

ES6允许使用`=>`定义函数。

如果箭头函数只有一个参数，那么圆括号可以省略。

        var f = v => v;

如果箭头函数不需要参数或需要多个参数，就用一个圆括号代表参数部分。

        var f = () => 5;

如果箭头函数的代码块部分多于一条语句，就要使用大括号将它们括起来，并且使用return语句返回。

        var sum = (num1, num2) => { return num1 + num2; };

由于大括号被解释为代码块，所以如果箭头函数直接返回一个对象，必须在对象外面加上括号。

        var getTempItem = id => ({ id: id, name: "Temp" });

箭头函数可以与变量解构结合使用。

```
const full = ({ first, last }) => first + ' ' + last;

// 等同于
function full(person) {
  return person.first + ' ' + person.last;
}
```

##  使用注意点

箭头函数有几个使用注意点。

*   函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象。

*   不可以当作构造函数，也就是说，不可以使用new命令，否则会抛出一个错误。

*   不可以使用arguments对象，该对象在函数体内不存在。如果要用，可以用Rest参数代替。

*   不可以使用yield命令，因此箭头函数不能用作Generator函数。

**this指向的固定化**，并不是因为箭头函数内部有绑定this的机制，实际原因是箭头函数根本没有自己的this，导致**内部的this就是外层代码块的this**。正是因为它没有this，所以也就不能用作构造函数。

除了this，以下三个变量在箭头函数之中也是不存在的，指向外层函数的对应变量：arguments、super、new.target。

```
function foo() {
  setTimeout(() => {
    console.log('args:', arguments);
  }, 100);
}

foo(2, 4, 6, 8)
// args: [2, 4, 6, 8]
```

上面代码中，箭头函数内部的变量arguments，其实是函数foo的arguments变量。

另外，由于箭头函数没有自己的this，所以当然也就不能用call()、apply()、bind()这些方法去改变this的指向。

```
(function() {
  return [
    (() => this.x).bind({ x: 'inner' })()
  ];
}).call({ x: 'outer' });
// ['outer']
```

上面代码中，箭头函数没有自己的this，所以bind方法无效，内部的this指向外部的this。

##  函数绑定(ES7)

箭头函数可以绑定this对象，大大减少了显式绑定this对象的写法（call、apply、bind）。但是，箭头函数并不适用于所有场合，所以ES7提出了“函数绑定”（function bind）运算符，用来取代call、apply、bind调用。

函数绑定运算符是并排的两个双冒号（::），双冒号左边是一个对象，右边是一个函数。该运算符会自动将左边的对象，作为上下文环境（即this对象），绑定到右边的函数上面。

```
foo::bar;
// 等同于
bar.bind(foo);

foo::bar(...arguments);
// 等同于
bar.apply(foo, arguments);

const hasOwnProperty = Object.prototype.hasOwnProperty;
function hasOwn(obj, key) {
  return obj::hasOwnProperty(key);
}
```

如果双冒号左边为空，右边是一个对象的方法，则等于将该方法绑定在该对象上面。

```
var method = obj::obj.foo;
// 等同于
var method = ::obj.foo;

let log = ::console.log;
// 等同于
var log = console.log.bind(console);
```

由于双冒号运算符返回的还是原对象，因此可以采用链式写法。

##  尾调用优化

### 什么是尾调用？

尾调用（Tail Call）是函数式编程的一个重要概念，本身非常简单，一句话就能说清楚，就是指某个函数的最后一步是调用另一个函数。

        function f(x){
          return g(x);
        }

上面代码中，函数f的最后一步是调用函数g，这就叫尾调用。

**“尾调用优化”（Tail call optimization），即只保留内层函数的调用帧。如果所有函数都是尾调用，那么完全可以做到每次执行时，调用帧只有一项，这将大大节省内存。这就是“尾调用优化”的意义。**

### 严格模式

ES6的尾调用优化只在严格模式下开启，正常模式是无效的。

这是因为在正常模式下，函数内部有两个变量，可以跟踪函数的调用栈。

*   func.arguments：返回调用时函数的参数。

*   func.caller：返回调用当前函数的那个函数。

尾调用优化发生时，函数的调用栈会改写，因此上面两个变量就会失真。严格模式禁用这两个变量，所以尾调用模式仅在严格模式下生效。

```
function restricted() {
  "use strict";
  restricted.caller;    // 报错
  restricted.arguments; // 报错
}
restricted();
```

##  箭头函数与常规函数对比

一个箭头函数与一个普通的函数在两个方面不一样：

*   下列变量的构造是词法的： arguments ， super ， this ， new.target

*   不能被用作构造函数：没有内部方法 [[Construct]] （该方法允许普通的函数通过 new 调用），也没有 prototype 属性。因此， new (() => {}) 会抛出错误。

