#   前端MVC架构

##  经典MVC模式

MVC包括三类对象，将它们分离以提高灵活性和复用性。
1.  模型model用于封装与应用程序的业务逻辑相关的数据以及对数据的处理方法，会有一个或多个视图监听此模型。一旦模型的数据发生变化，模型将通知有关的视图。

2.  视图view是它在屏幕上的表示，描绘的是model的当前状态。当模型的数据发生变化，视图相应地得到刷新自己的机会。

3.  控制器controller定义用户界面对用户输入的响应方式，起到不同层面间的组织作用，用于控制应用程序的流程，它处理用户的行为和数据model上的改变。

![index]()

经典MVC模式

实现：方法调用
虚线：时间通知

其中设计两种设计模式：

1.  view和model之间的观察者模式，view观察model，事先在此model上注册，以便view可以了解在数据model上发生的改变。

2.  view和controller之间的策略模式

>   一个策略是一个表述算法的对象，MVC允许在不改变视图外观的情况下改变视图对用户输入的响应方式。例如，你可能希望改变视图对键盘的响应方式，或希望使用弹出菜单而不是原来的命令键方式。MVC将响应机制封装在controller对象中。存在着一个controller的类层次结构，使得可以方便地对原有的controller做适当改变而创建新的controller。

>   view使用controller子类的实例来实现一个特定的响应策略。要实现不同的响应的策略只要用不同种类的controller实例替换即可。甚至可以在运行时刻通过改变view的controller来改变用户输入的响应方式。例如，一个view可以被禁止接受任何输入，只需给他一个忽略输入事件的controller。

##  前端MVC模式

![index]()
javascript MVC模式

如图所示，view承接了部分controller的功能，负责处理用户输入，但是不必了解下一步做什么。它依赖于一个controller为她做决定或处理用户事件。事实上，前端的view已经具备了独立处理用户事件的能力，如果每个事件都要流经controller，势必增加复杂性。同时，view也可以委托controller处理model的更改。model数据变化后通知view进行更新，显示给用户。这个过程是一个圆，一个循环的过程。

这种从经典MVC到Javascript MVC的1对1转化，导致控制器的角色有点尴尬。MVC这样的结构的正确性在于，任何界面都需要面对一个用户，而controller “是用户和系统之间的链接”。在经典MVC中，controller要做的事情多数是派发用户输入给不同的view，并且在必要的时候从view中获取用户输入来更改model，而Web以及绝大多数现在的UI系统中，controller的职责已经被系统实现了。由于某种原因，控制器和视图的分界线越来越模糊，也有认为，view启动了action理论上应该把view归属于controller。比如在Backbone中，Backbone.View和Backbone.Router一起承担了controller的责任。这就为MVC中controller的衍变埋下了伏笔。

##  MVVM

![index]()
MVVM模式

首先，view和model是不知道彼此存在的，同MVP一样，将view和model清晰地分离开来。 其次，view是对viewmodel的外在显示，与viewmodel保持同步，viewmodel对象可以看作是view的上下文。view绑定到viewmodel的属性上，如果viewmodel中的属性值变化了，这些新值通过数据绑定会自动传递给view。反过来viewmodel会暴露model中的数据和特定状态给view。 所以，view不知道model的存在，viewmodel和model也觉察不到view。事实上，model也完全忽略viewmodel和view的存在。这是一个非常松散耦合的设计。
