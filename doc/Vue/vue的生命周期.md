#   Vue的生命周期

![index](https://raw.githubusercontent.com/esperanza1211/note/master/image/vue%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F.png)

##  说明

*   beforeCreate

    在实例初始化之后，数据观测（date observer）和 event/watcher 事件配置之前被调用。

*   created

    在实例创建完成后被立即调用。在这一步，实例已完成以下的配置：数据观测（date observer），属性和方法的运算，watch/event 事件回调。然而，挂载阶段还没开始，$el 属性目前不可见。

*   beforeMount

    在挂载开始之前被调用：相关的render 函数首次被调用。
    
    该钩子在服务器端渲染期间不被调用。

*   mounted

    el 被新创建的 vm.$el 替换，并挂载到实例上去之后调用该钩子。如果 root 实例挂载了一个文档内元素，当 mounted 被调用时 vm.$el 也在文档内。

    注意 mounted 不会承诺所有的子组件也都一起被挂载。如果你希望等到整个视图都渲染完毕，可以用 vm.$nextTick 替换掉 mounted：

    mounted: function () {
      this.$nextTick(function () {
        // Code that will run only after the
        // entire view has been rendered
      })
    }

    该钩子在服务器端渲染期间不被调用。

*   beforeUpdate

    数据更新时调用，发生在虚拟 DOM 打补丁之前。这里适合在更新之前访问现有的 DOM，比如手动移除已添加的事件监听器。

    该钩子在服务器端渲染期间不被调用，因为只有初次渲染会在服务端进行。

*   updated

    由于数据更改导致的虚拟 DOM 重新渲染和打补丁，在这之后会调用该钩子。

    当这个钩子被调用时，组件 DOM 已经更新，所以你现在可以执行依赖于 DOM 的操作。然而在大多数情况下，你应该避免在此期间更改状态。如果要相应状态改变，通常最好使用计算属性或 watcher 取而代之。

    注意 updated 不会承诺所有的子组件也都一起被重绘。如果你希望等到整个视图都重绘完毕，可以用 vm.$nextTick 替换掉 updated：

    updated: function () {
      this.$nextTick(function () {
        // Code that will run only after the
        // entire view has been re-rendered
      })
    }

    该钩子在服务器端渲染期间不被调用。
    

*   activated

    keep-alive 组件激活时调用。

    该钩子在服务器端渲染期间不被调用。

*   deactivated

    keep-alive 组件停用时调用。

    该钩子在服务器端渲染期间不被调用。

*   beforeDestroy

    实例销毁之前调用。在这一步，实例仍然完全可用。

    该钩子在服务器端渲染期间不被调用。

*   destroyed

    Vue 实例销毁后调用。调用后，Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。

    该钩子在服务器端渲染期间不被调用。

*   errorCaptured
>   2.5.0+ 新增

    当捕获一个来自子孙组件的错误时被调用。此钩子会收到三个参数：错误对象、发生错误的组件实例以及一个包含错误来源信息的字符串。此钩子可以返回 false 以阻止该错误继续向上传播。

    >   你可以在此钩子中修改组件的状态。因此在模板或渲染函数中设置其它内容的短路条件非常重要，它可以防止当一个错误被捕获时该组件进入一个无限的渲染循环。


    错误传播规则:

    *   默认情况下，如果全局的 config.errorHandler 被定义，所有的错误仍会发送它，因此这些错误仍然会向单一的分析服务的地方进行汇报。

    *   如果一个组件的继承或父级从属链路中存在多个 errorCaptured 钩子，则它们将会被相同的错误逐个唤起。

    *   如果此 errorCaptured 钩子自身抛出了一个错误，则这个新错误和原本被捕获的错误都会发送给全局的 config.errorHandler。

    *   一个 errorCaptured 钩子能够返回 false 以阻止错误继续向上传播。本质上是说“这个错误已经被搞定了且应该被忽略”。它会阻止其它任何会被这个错误唤起的 errorCaptured 钩子和全局的 config.errorHandler。


