#   Set

*   Set本身提供一个构造函数，用来生成Set数据结构。

```
var s = new Set();

[2,2,2,5,8,16,2,1].map(x => s.add(x))

for(i of s){console.log(i)}
//2,5,8,16,
```

*   Set()函数可以接受一个数组，作为构造参数，用于做初始化。

```
var s = new Set([1,2,3,4,2,4,3]);
[...s]
//[1,2,3,4]
```

注意：向Set中加入值的时候不会发生类型转换，所以5和”5”是两个不同的值，Set内部判断两个值是否相等，使用的是 ===，这就意味着这两个对象总是不相等。唯一列外的是NaN本身（精确相等运算符认为NaN不等于自身）

```
let set = new Set();
set.add({})
set.size//1
set.add({})
set.size//2
```

上面的代码表示，由于这两个空对象不是精确相等，所以是两个不同的值。

##　 Set的方法和属性

### Set的属性

*   Set.prototype.size:返回Set实例的成员数量。 

*   Set.prototype.constructor:默认的构造Set函数。

### Set的方法


*   add(value):添加某个值，返回Set结构本身。 

*   delete(value):删除某个值，返回一个布尔值，表示删除成功。
 
*   has(value):返回一个布尔值，表示参数是否为Set的成员。
 
*   clear():清除所有成员，没有返回值。

```
var set = new Set();
set.add(1).add(2).add(22).add(22);
set.size//3

set.hae(22)//true
set.has(4)//false
set.delete(2)//true
```

### Set遍历操作

Set有四个遍历方法。可以用于遍历成员。
 
*   keys() :返回一个键名的遍历器 

*   values() :返回一个值的遍历器 

*   entries() :返回一个键值对的遍历器
 
*   forEach():使用回调函数遍历每个成员

注意：由于Set没有键名，只有值名，keys()和values()返回的结果是一样。

```
let set = new Set(['red','green','blue']);

for(let item of set.keys()){
console.log(item);
}
//red,green,blue

for(let item of set.values()){
console.log(item);
}
//red,green,blue

for(let item of set.entries()){
console.log(item);
}
//["red","red"]
//["green","green"]
//["blue","blue"]
```

entries方法返回的遍历器同时包括键名和值，所以每次输出的是一个数组。其实成员都是完全一样的。

注意：Set默认的可遍历，其默认遍历器生成函数就是它的values方法。 

这就意味着，可以省略values方法，直接用for…of遍历。

```
var set = new Set([1,2,3,4]);
for(let x of set){
console.log(x);
}
//1, 2, 3, 4
```

如果使用扩展运算符（…）内部使用for…of 循环，所以也可以用于Set结构。

```
let set = new Set(['red','green','blue']);
let arr = [...set];
//['red','green','blue'];
```

### Set实现并集，交集，差集

```
let set1  = new Set([1,2,3,4,5,6]);
let set2  = new Set([4,5,6,7,8,9]);

//并集
let union = new Set([...set1,...set2]);
//[1,2,3,4,5,6,7,8,9]
//交集
let intersect = new Set([...set1].filter(x => b.has(s)));
//[4,5,6]
//差集
let intersect = new Set([...set1].filter(x => !b.has(s)));
//[1,2,3,4]
```

### Set实现forEach的使用

```
let set = new Set([1,2,3,4,5,6]);
set.forEach(value,key)=>consloe.log(vlaue+1);
//2, 3, 4, 5, 6, 7
```

注意：forEach方法的参数就是一个处理函数，该函数依次为（键值，键名）集合本身。另外，forEach方法还有第二个参数，表示绑定this的对象。
