#   call和apply

##  call

```
function.call(obj[,arg1[, arg2[, [,.argN]]]]])
```

*   调用call的对象必须是个函数function

*   call的第一个参数将会是function改变上下文后指向的对象，也就是上面例子里的小刚，也就是上上面例子里的老婆大人，如果不传，将会默认是全局对象window

*   第二个参数开始可以接收任意个参数，这些参数将会作为function的参数传入function

*   调用call的方法会立即执行

##  apply

```
function.apply(obj[,argArray])
```

与call方法的使用基本一致，但是只接收两个参数，其中第二个参数必须是一个数组或者类数组，这也是这两个方法很重要的一个区别

### apply应用：

1.  `Math.max`可以实现得到数组中最大的一项：

因为Math.max不支持`Math.max([param1,param2])`也就是数组，但是它支持`Math.max(param1,param2...)`，所以可以根据apply的特点来解决`var max=Math.max.apply(null,array)`，这样就轻易的可以得到一个数组中的最大项（apply会将一个数组转换为一个参数接一个参数的方式传递给方法）

这块在调用的时候第一个参数给了null，这是因为没有对象去调用这个方法，我只需要用这个方法帮我运算，得到返回的结果就行，所以直接传递了一个null过去。

用这种方法也可以实现得到数组中的最小项：`Math.min.apply(null,array)`

2.  Array.prototype.push可以实现两个数组的合并

同样push方法没有提供push一个数组，但是它提供了push(param1,param2...paramN)，同样也可以用apply来转换一下这个数组，即：

```
var arr1=new Array("1","2","3");
var arr2=new Array("4","5","6");
Array.prototype.push.apply(arr1,arr2);    //得到合并后数组的长度，因为push就是返回一个数组的长度
```

也可以这样理解，arr1调用了push方法，参数是通过apply将数组转换为参数列表的集合

通常在什么情况下，可以使用apply类似Math.max等之类的特殊用法：

一般在目标函数只需要n个参数列表，而不接收一个数组的形式，可以通过apply的方式巧妙地解决这个问题。

##  call和apply的异同

*   相同点：

都能够改变方法的执行上下文（执行环境），将一个对象的方法交给另一个对象来执行，并且是立即执行

*   不同点：

call方法从第二个参数开始可以接收任意个参数，每个参数会映射到相应位置的func的参数上，可以通过参数名调用，但是如果将所有的参数作为数组传入，它们会作为一个整体映射到func对应的第一个参数上，之后参数都为空

```
function func (a,b,c) {}

func.call(obj, 1,2,3)
// function接收到的参数实际上是 1,2,3

func.call(obj, [1,2,3])
// function接收到的参数实际上是 [1,2,3],undefined,undefined
```

apply方法最多只有两个参数，第二个参数接收数组或者类数组，但是都会被转换成类数组传入func中，并且会被映射到func对应的参数上

```
func.apply(obj, [1,2,3])
// function接收到的参数实际上是 1,2,3

func.apply(obj, {
    0: 1,
    1: 2,
    2: 3,
    length: 3
})
// function接收到的参数实际上是 1,2,3
```
