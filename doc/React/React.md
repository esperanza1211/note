#   React

##  React

用于构建用户界面的 JavaScript 库。

https://reactjs.org/

https://doc.react-china.org/

##  安装与使用

- `<script>` 引入式
- 模块化方式

##  脚手架工具

- vue-cli : vue官方提供
- create-react-app : 官方推荐
- angular-cli : 官方提供

##  组成

- react : 底层基本操作
    - react-dom : 提供 操作 html DOM
    - react-native : 提供 APP 操作

##  `<script>` 引入式

- react.js
- react-dom.js

##  ReactDOM.render

ReactDOM : ReactDOM.js 框架提供的一个核心对象，该对象下封装一些用于操作 DOM 的方法

ReactDOM.render(要渲染的内容, 容器)
把指定的内容解析完成以后，然后到指定的容器中，body不能作为容器

如果我们要解析的内容是一个字符串的话，那么react并不会对他进行任何的解析操作，主要是为了防范：XSS
React 提供了一个专门的语法来处理文档结构问题 - JSX

```
ReactDOM.render(
    '<h1>Hello React!</h1>',
    document.querySelector('#app')
);
```

##  JSX

JavaScript XML，允许我们在js中直接书写 xml，在xml中也可以方便的使用javascript，但是浏览器并不能直接识别该语法，我们需要用一个JSX的解析器来对该语法进行解析，解析成浏览器识别的语法 - babel -> jsx语法解析库。

注意：不要把包含有jsx语法的代码直接放置在`script`标签中，这样浏览器还是会解析，还是会报错。我们只需要在`script`标签添加一个`type="text/babel"`。

使用注意：

- 可以在JS中书写XML(HTML)，也可以在 XML 中书写 JS，但是需要包含一个 {} 中，而且只支持 表达式，并且不是所有的结果都能直接输出的
- 可以嵌套，添加子元素
- 一个独立的结构中，有且只能有一个顶级元素
- 支持插值表达式：{表达式}

### 作为内容

不是任何内容都能被输出的

- 字符串：原值
- 数字：转成字符串

- 布尔值：空
- 空：空
- 未定义：空

- 对象：报错
    - 数组对象可以直接输出，但是会使用 join('') 转成字符串

- XML : 在插值表达式中也可以书写xml

### 作为属性值

作为属性输出，我们只要在标签的属性值使用 {}，如果使用了引号，那么就是字符。

在使用 {} 的时候，需要注意下面两个情况：

-   class：标签上不能使用 class 属性，因为他会和 js 中的 类 关键字冲突了，使用className替代

-   style：在jsx中style的值必须是 {}，而且样式是对象结构，style={ {color: 'red'} }，第一组括号是插值表达式的括号，第二组括号是对象的括号

### 循环输出

在react中插值表达式不支持语句：for，也没有指令一说

在jsx中，xml也是一种能够直接输出的值

```
const users = ['莫涛', '童斌', '钟毅'];
const users2 = [<li>莫涛</li>, <li>童斌</li>, <li>钟毅</li>]; 
ReactDOM.render(
    <div>

        <ul>
            <li>{users}</li>
        </ul>

        <ul>
            {users2}
        </ul>

        <ul>
            {
                users.map( user => {
                    return <li>{user}</li>
                } )
            }
        </ul>

    </div>,
    document.querySelector('#app')
);
```

### 条件输出

```
const users1 = ['莫涛','童斌'];
const users2 = [];

function getView(data) {
    if (data.length) {
        return <ul> {data.map(item => <li>{item}</li>)} </ul>;
    } else {
        return <p style={{color: 'red'}}>没有数据</p>;
    }
}

ReactDOM.render(
    <div>

        {
            users1.length === 0 ?
                    <p>没有数据</p>
                :
                    <ul>
                        {
                            users1.map( user => <li>{user}</li> )
                        }
                    </ul>

        }

        <hr />

        {
            users2.length === 0 ?
                    <p>没有数据</p>
                :
                    <ul>
                        {
                            users1.map( user => <li>{user}</li> )
                        }
                    </ul>

        }

        <hr />

        {getView(users1)}

        <hr />

        {getView(users2)}

    </div>,
    document.querySelector('#app')
);
```

##  组件

不管是函数式组件还是类式组件，组件的名称必须是大驼峰，首字母大写

### 函数式组件

组件其实本质上就是一个普通的函数，当我们在jsx中通过函数方式去调用的时候，那么就会执行该函数，然后输出函数返回值。

在react中为了能使调用过程更加高、大、上，所以使用了一种标签方式来调用该函数。

函数的参数通过 标签 的属性进行传递。

```
function List(props) {   //函数的第一个参数，标签上所有属性的集合
    return props.data.map( item => {
        return <li>{item}</li>;
    } );
}

ReactDOM.render(
    <div>

        <h1>组件</h1>

        <ul>
            <List data={teachers} />
        </ul>

        <hr />

        <ul>
            <List data={students} />
        </ul>

    </div>,
    document.querySelector('#app')
);
```

### 类式组件

通过类的形式来定义可复用的组件。

不是任意一种类都是组件类，在react中，要创建一个组件类，这个必须是继承 `React.Component`，组件的一个重要作用就是输出结构，函数组件，函数的返回值就是结构，如果组件是一个类，那么就必须实现该类的一个约定的方法：`render`。

组件传入的参数，是这个类的一个属性。

```
const teachers = ['莫涛','童斌'];
const students = ['张三', '李四', '王五'];

class List extends React.Component {

    render() {

        return this.props.data.map( item => {
            return <li>{item}</li>;
        } );
    }

};

ReactDOM.render(
    <div>

        <h1>组件</h1>

        <ul>
            <List data={teachers} />
        </ul>

        <hr />

        <ul>
            <List data={students} />
        </ul>

    </div>,
    document.querySelector('#app')
);
```

##  事件

事件绑定：使用类似行间事件绑定，注意事件名称驼峰命名，值为表达式。

我们可以帮该函数通过 bind 方法绑定到 当前组件上，而不是触发该事件的元素上，因为，我们可能更需要在这里调用到当前的组件对象，以及组件对象另外一些数据。

```
class List extends React.Component {

    fn() {
        console.log('我是fn');
    }

    clickHandler(e) {
        // 函数的第一个参数是事件对象，那么我们可以通过事件对象获取到触发该事件的元素
        console.log(e.target);
        // 事件默认行为：e.preventDefault()
        // 事件冒泡：e.stopPropagation()
    }

    render() {
        return (
            <div>
                <button onClick={this.clickHandler.bind(this)}>按钮</button>
            </div>
        )
    }

};

ReactDOM.render(
    <div>

        <List />

    </div>,
    document.querySelector('#app')
);
```


```
const users = '莫涛,童斌'.split(',');

class List extends React.Component {

    remove(index, e) {//如果函数有多余的参数，那么默认的事件对象是作为参数中最后一个传入的。

        this.props.data.splice(index, 1);

        //react 中不是修改了数据就一定会渲染视图，要修改指定的数据才会渲染视图。

        console.dir(this.props.data);

        e.preventDefault();
    }

    render() {
        return (
            <ul>
                {
                    this.props.data.map( (user, index) => {
                        return (
                                <li key={index}>
                                    <span>{user}</span>
                                    <span> - </span>
                                    <a href="" onClick={this.remove.bind(this, index)}>删除</a>
                                </li>
                        );
                    } )
                }
            </ul>
        );
    }

};

ReactDOM.render(
    <div>

        <List data={users} />

    </div>,
    document.querySelector('#app')
);
```

##  state

状态：数据，在react中为组件提供了一个存放私有数据的属性。

一个组件可以接收两种类型的数据：

*   props：由外部传入 - vue.props
*   state：由内部定义的 - vue.data

定义：必须在组件类的构造函数中进行初始化定义。

如果当前组件需要使用state，那么就必须在组件构造函数中进行初始化，state是一个对象，用来存放组件所需要使用的内部数据。

因为react没有实现数据的主动监听，`Object.defineProperty`，要想改变数据的时候同时渲染视图，则需要调用一个react提供的方法来操作：`setState()`。

```
const users = '莫涛,童斌'.split(',');

class List extends React.Component {

    constructor() {
        //因为组件都是继承自 React.Component类，那么子类必须实现父类构造方法
        super();
        
        this.state = {
            data: users
        };
    }

    remove(index, e) {

        //this.state.data.splice(index, 1);//不能渲染视图

        const newData = this.state.data.filter( (item, i) => index != i );

        this.setState({
            data: newData
        });

        e.preventDefault();
    }

    render() {
        console.log('渲染');
        return (
            <ul>
                {
                    this.state.data.map( (user, index) => {
                        return (
                                <li key={index}>
                                    <span>{user}</span>
                                    <span> - </span>
                                    <a href="" onClick={this.remove.bind(this, index)}>删除</a>
                                </li>
                        );
                    } )
                }
            </ul>
        );
    }

};

ReactDOM.render(
    <div>

        <List />

    </div>,
    document.querySelector('#app')
);
```

##  props

如果当前组件重写了constructor，那么就必须在参数中声明props

```
class List extends React.Component {

    constructor(props) {//需要申明props
        super(props);

        this.state = {
            data: this.props.data
        };
    }

    remove(index, e) {

        const newData = this.state.data.filter( (item, i) => index != i );

        this.setState({
            data: newData
        });

        e.preventDefault();
    }

    render() {
        console.log('渲染');
        return (
            <ul>
                {
                    this.state.data.map( (user, index) => {
                        return (
                                <li key={index}>
                                    <span>{user}</span>
                                    <span> - </span>
                                    <a href="" onClick={this.remove.bind(this, index)}>删除</a>
                                </li>
                        );
                    } )
                }
            </ul>
        );
    }

};
```

##  class

如果一个类继承了另外一个类

1.  如果子类没有`constructor`，那么子类调用的时候会调用父类的`constructor`

2.  如果子类有`constructor`，那么子类会调用自己的`constructor`，不会调用父类的

```
class Person {
    constructor(name) {
        console.log('Person constructor');
        this.name = name;
    }
}

class Teacher extends Person {
}

class Student extends Person {
    constructor(name) {
        super(name);
        console.log('Student constructor');
    }
}
```

### 子到父通信

```
const datas = {
    teachers: {
        name: '讲师',
        list: '莫涛,童斌'.split(',')
    },
    students: {
        name: '学员',
        list: '张三,李四,王五'.split(',')
    }
};

class List extends React.Component {

    constructor(arg) {
        super(arg);

        this.state = {
            show: true
        };

        this.toggle = this.toggle.bind(this);
    }

    toggle() {
        this.setState({
            show: !this.state.show
        });
    }

    renderList() {
        return (
            <ul style={{ display: this.state.show ? 'block' : 'none' }}>
                {
                    this.props.data.list.map( (user,index) => {
                        return <li key={index}>{user}</li>
                    } )
                }
            </ul>
        );
    }

    render() {
        return (
            <div className="box">
                <h2 onClick={this.toggle}>{this.props.data.name}</h2>
                {this.renderList()}
            </div>
        );
    }

};

ReactDOM.render(
    <div>

        <List data={datas.teachers} />
        <List data={datas.students} />

    </div>,
    document.querySelector('#app')
);
```

##  React.createElement

```
const h1 = <h1>Hello</h1>;

const h2 = React.createElement('h2', {
    id: 'sub_title',
    style: {
        color: 'red'
    }
}, '内容');

const c = <div>{h1}{h2}</div>;

ReactDOM.render(
    <div>
        <h1>Hello</h1>
        {c}
    </div>,
    document.querySelector('#app')
);
```

##  生命周期

一个组件从被创建到被销毁的过程称为：生命周期
React 在组件的生命周期内的不同阶段会调用一些函数，我们把这些函数又称为：生命周期函数
组件一共有三个阶段：
	Mounting：挂载阶段
	Updating：更新阶段
	Unmounting：卸载阶段
Mounting 和 Unmounting 阶段在组件的整个生命周期中只会出现一次，而Updating 阶段将会在组件每次更新中执行

```
class App extends React.Component {

    constructor(args) {
        console.log('constructor');
        super(args);
    }
    
    //在组件即将被挂载的时候调用一次
    componentWillMount() {
        console.log('componentWillMount');
    }
    
    //在组件被挂载完成的时候调用一次，可以在这里使用refs
    componentDidMount() {
        console.log('componentDidMount');
        console.log(this.refs);
        this.refs.title.style.color = 'red';
    }

    render() {
        console.log('render');
        return(
            <div>
                <h1 ref="title">标题</h1>
                <p ref="content">内容</p>
            </div>
        );
    }

}

ReactDOM.render(
    <div>
        <App/>
    </div>,
    document.querySelector('#app')
);
```

组件挂载之后，每次调用setState后都会调用shouldComponentUpdate判断是否需要重新渲染组件。默认返回true，需要重新render。在比较复杂的应用里，有一些数据的改变并不影响界面展示，可以在这里做判断，优化渲染效率。

```
class List extends React.Component {

    constructor(args) {
        super(args);

        this.state = {
            value: 1.123456
        }
    }

    //当父组件更新导致该组件更新的时候，调用该函数
    componentWillReceiveProps( nextProps ) {
        console.log('componentWillReceiveProps');
    }

    shouldComponentUpdate(nextProps, nextState) {
        console.log('shouldComponentUpdate');
        return true;
    }

    componentWillUpdate(nextProps, nextState) {
        console.log('componentWillUpdate');
    }

    componentDidUpdate(prevProps, prevState) {
        console.log('componentDidUpdate');
    }

    render() {
        console.log('render');
        return(
            <div>
                <button
                    onClick={e=>{
                        this.setState({
                            value: this.state.value + 0.005
                        })
                    }}
                >++</button>
                <h1>value: {this.state.value.toFixed(1)}</h1>
                <h1>data: {this.props.data}</h1>
            </div>
        );
    }

}

class App extends React.Component {

    constructor(args) {
        super(args);

        this.state = {
            v: 1
        }
    }

    render() {
        return(
            <div>
                <button
                    onClick={e=>{
                        this.setState({
                            v: this.state.v + 1
                        })
                    }}
                >++</button>
                {/*<h1>{this.state.v}</h1>*/}
                <hr />
                <List data={this.state.v} />
            </div>
        );
    }

}

ReactDOM.render(
    <div>
        <App/>
    </div>,
    document.querySelector('#app')
);
```

[react生命周期详解](https://github.com/esperanza1211/note/blob/master/doc/React/react%E7%9A%84%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F.md)

##  受控组件和非受控组件

在react中，表单类元素会被react进行托管，这些元素的某些属性会被React进行控制：

*   input: value

*   input.radio、checkbox: checked

*   select: selected

这些属性不能直接响应用户的更改，而是被React所控制，当然有两种方式可以去操作该组件的这些属性

1.  使用非受控属性把组件变成非受控型组件

2.  修改受控组件绑定的数组值

```
class App extends React.Component {

    constructor(args) {
        super(args);

        this.state = {
            v: 1
        }
    }

    render() {
        return(
            <div>

                <button
                    onClick={
                        e => {
                            this.setState({
                                v: this.state.v + 1
                            })
                        }
                    }
                >按钮</button>

                <input type="text" value={this.state.v} onChange={ e => {
                    this.setState({
                        v: e.target.value
                    })
                }} />

                <hr/>

                <input type="text" defaultValue={this.state.v} />
                <input type="checkbox" checked={false} /> 选中
                <input type="checkbox" defaultChecked={false} /> 选中
            </div>
        );
    }

}

ReactDOM.render(
    <div>
        <App/>
    </div>,
    document.querySelector('#app')
);
```

##  children

##  defaultProps

该类添加一个defaultProps属性，这个属性是一个对象，对象中的key对应着组件内部的props，他的作用是给组件的props设置默认值的

```
class Dialog extends React.Component {

    render() {
        return (
            <div className="dialog">
                <h2>{this.props.title}</h2>
                <div>
                    {this.props.children}
                </div>
            </div>
        );
    }

}

Dialog.defaultProps = {
    title: '标题',
    children: '内容'
};

class App extends React.Component {

    constructor(args) {
        super(args);
    }

    render() {
        return(
            <div>
                <h1>App</h1>

                <Dialog>新的内容</Dialog>
            </div>
        );
    }

}

ReactDOM.render(
    <div>
        <App/>
    </div>,
    document.querySelector('#app')
);
```

##  propTypes

该类添加一个defaultProps属性，这个属性是一个对象，对象中的key对应着组件内部的props，他的作用是给组件的props设置默认值的

通过给类添加一个propTypes的属性来进行属性的类型检测

以下是 propTypes 提供的支持的验证类型
    PropTypes.string / PropTypes.number / PropTypes.bool / PropTypes.symbol / PropTypes.object / PropTypes.func / PropTypes.array
    PropTypes.node / PropTypes.element
还可以自定验证类型
    PropTypes.instanceOf( UserType )： UserType 为自定义类型

PropTypes.oneOf(['News', 'Photos'])

PropTypes.oneOfType([
	PropTypes.string,
	PropTypes.instanceOf(Message)
])

PropTypes.arrayOf(PropTypes.number)
PropTypes.objectOf(PropTypes.number)
PropTypes.shape({
	color: PropTypes.string,
	fontSize: PropTypes.number
})

我们还有通过定义一个验证函数来验证我们的 props
value: function(props, propName, componentName) {
    if (props[propName] < 0 || props[propName] > 200) {
        throw new Error('不是人');
    }
}

```
class Dialog extends React.Component {

    render() {
        console.log(this.props.onSubmit)
        return (
            <div className="dialog">
                <h2>{this.props.title}</h2>
                <div>
                    {this.props.children}
                </div>
            </div>
        );
    }

}
Dialog.defaultProps = {
    title: '标题',
    children: '内容'
};
function zmouse(props, propName, componentName) {
    if (props[propName] && props[propName] < 10) {
        throw new Error('小屁孩，通不过');
    }
};
zmouse.isRequired = function() {
    if (!props[propName] || props[propName] < 10) {
        throw new Error('小屁孩，通不过');
    }
};

Dialog.propTypes = {
    v: zmouse.isRequired
};

class App extends React.Component {

    constructor(args) {
        super(args);
    }

    render() {
        return(
            <div>
                <h1>App</h1>
                <Dialog>新的内容</Dialog>
            </div>
        );
    }

}

ReactDOM.render(
    <div>
        <App/>
    </div>,
    document.querySelector('#app')
);
```

##  key

在jsx的循环中，被循环的最外层结构 标签 上最好加上key属性，并且key的是唯一的 => VM -> 虚拟DOM - diff

在react中我们渲染一个列表的时候，我们需要为每一个列表项指定一个唯一的key，当没有指定key时，会收到一个warning， 如果指定的key不唯一，只会渲染第一个指定唯一的key的那个元素。

使用key可以使得DOM diff更加高效，避免不必要的列表项更新。

```
class App extends React.Component {

    constructor(args) {
        super(args);

        this.state = {
            data: ['刘伟','莫涛','童斌']
        }
    }

    render() {
        return(
            <div>
                <button
                    onClick={
                        e => {
                            this.setState({
                                data: ['童斌','莫涛','刘伟']
                            })
                        }
                    }
                >按钮</button>
                <ul>
                    {
                        this.state.data.map( item => {
                            return <li key={item}>{item}</li>;
                        } )
                    }

                </ul>
            </div>
        );
    }

}

ReactDOM.render(
    <div>
        <App/>
    </div>,
    document.querySelector('#app')
);
```
