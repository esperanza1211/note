#   state

在一个组件的内部会有不同的位置来存储数据

组件传入属性 : props，这个数据来源是调用该组件的时候传入的参数

组件自身属性

但是，无论是 props，还是自身属性，都有一个问题，当数据变化的时候，都不会重新渲染视图

React为我们组件的设计制定一套方案：

1.  props 为外部传入数据，组件内部对该数据最好使用只读方式

2.  自身属性/方法，作为静态数据，工具函数来使用

以上两种数据都不会重新渲染视图

3.  React 定义了一个专门与视图有密切关系的属性：state，他是一个对象，我们把和视图的更新有关的数据放到该属性下存储，如果有某数据变化了，我们希望他重新渲染视图，那么我们就把该数据放到 state 中进行存储

但是直接修改state也不会触发视图的渲染，需要手动调用 setState() 方法来对 state 数据进行更新，该方法只能更新 state 数据

```
class App extends React.Component {

    constructor(args) {
        super(args);

        this.username = 'zMouse';

        this.state = {
            username: '钟毅'
        }
    }

    say() {
        return 'Hello'
    }

    changeSelfValue() {
        this.username = 'MoTao';
    }

    getSelfValue() {
        console.log(this.username);
    }

    changeStateValue() {
        // 如果对state中数据进行直接赋值或修改操作，是不能重新渲染视图的
        // this.state.username = '莫涛';
        // 如果我们希望state数据更新要重新渲染视图，那么就需要使用他提供的一个方法：setState

        // 当我们调用setState方法修改某个state数据的时候，该方法并没有立即去修改对应的数据，而是把修改操作保存到了一个更新队列中
        this.setState({
            username: '莫涛'
        });
        this.setState({
            username: '莫涛1'
        });
        // 当我们一次业务处理完成以后，然后再统一的修改state，渲染视图

        console.log( this.state.username );
    }

    getStateValue() {
        console.log(this.state.username);
    }

    render() {
        console.log('...');
        return(
            <div>
                <button
                    onClick={this.changeSelfValue.bind(this)}
                >更新自身属性</button>
                <button
                    onClick={this.changeStateValue.bind(this)}
                >更新state</button>

                {/*<h1>内容 - {this.username}, {this.say()}</h1>*/}
                <h1>自身属性：{this.username}</h1>
                <h1>state：{this.state.username}</h1>

                <button
                    onClick={this.getSelfValue.bind(this)}
                >获取自身属性</button>
                <button
                    onClick={this.getStateValue.bind(this)}
                >获取state</button>
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
