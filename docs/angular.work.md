Angular 工作原理
======================

```html
    <!doctype html>
    <html ng-app>
      <head>
        <script src="angular.js"></script>
      </head>
      <body>
        <p ng-init=" name='World' ">Hello {{name}}!</p>
      </body> 
    </html>
```

当你用浏览器去访问index.html的时候，浏览器依次做了如下一些事情：

* 加载html，然后解析成DOM；
* 加载angular.js脚本；
* 页面文档完成加载并解析完毕之后DOMContentLoaded事件的触发；
* AngularJS寻找ng-app指令，确定应用程序的边界；
* 使用ng-app中指定的模块配置$injector；
    > (在引导启动是,AngularJs创建了一个$injector,
    > 并且使用这个$injector来调用控制函数,service函数,filter函数等,其它可能依赖到的函数)
* 使用injector创建compile服务和$rootScope；
    > ($rootScope是其它所有作用域的父级,作用域的形式类似于父子、树状的关系，并且最根部的就是 $rootScope 实例。
    > 就像作用域是被DOM树驱动着创建的一样，作用域树也是在模仿 DOM 的结构。)
* 使用compile服务编译DOM并把它链接到rootScope上；
* ng-init指令对scope里面的变量name进行赋值；
* 对表达式{{name}}进行替换，于是乎，显示为“Hello World!”   

整个过程可以用这张图来表示：

![ng 渲染流程](http://images.cnitblog.com/blog/93149/201311/26231509-35460094427943cda3fd99197ff1e775.jpg)

好了，通过上面的例子我们清楚了AngularJS是怎样一步一步渲染出一个页面的。
那么它又是如何和浏览器的事件回路来交互的呢？
或者说是如何跟用户来交互的呢？
粗略来讲，主要分为三个阶段：
* 浏览器的事件回路一直等待着事件的触发，事件包括用户的交互操作、定时事件或者网络事件（如服务器的响应等）；
* 一旦有事件触发，就会进入到Javascript的context中，一般通过回调函数来修改DOM；
* 等到回调函数执行完毕之后，浏览器又根据新的DOM来渲染新的页面。

正如下面一张图所示，交互过程主要由几个循环组成：

![ng 渲染流程](http://images.cnitblog.com/blog/93149/201311/26231629-fc0579af8b164e65befa05d1d9e357a6.jpg)

 AngularJS修改了一般的Javascript工作流，并且提供了它自己的事件处理机制。
 这样就把Javascript的context分隔成两部分，一部分是原生的Javascript的context，另一部分是AngularJS的context。
 只有处在AngularJS的context中的操作才能享受到Angular的data-binding、exception handling、property watching等服务，
 但是对于外来者（如原生的Javascript操作、自定义的事件回调、第三方的库等）Angular也不是一概不接见，
 可以使用AngularJS提供的$apply()函数将这些外来者包进AngularJS的context中，
 让Angular感知到他们产生的变化。
 
 * Scope提供$watch方法监视Model的变化。
 * Scope提供$apply方法传播Model的变化。
 * Scope可以继承，用来隔离不同的application components和属性访问权限。
 * Scope为Expressions的计算提供上下文。
 
接下来，让我们一起来看看交互过程中的这几个循环是怎么工作的？

* 首先，浏览器会一直处于监听状态，一旦有事件被触发，就会被加到一个event queue中，event queue中的事件会一个一个的执行。
* event queue中的事件如果是被$apply()包起来的话，就会进入到AngularJS的context中，
  这里的fn()是我们希望在AngularJS的context中执行的函数。
* AngularJS将执行fn()函数，通常情况下，这个函数会改变应用的某些状态。
* 然后AngularJS会进入到由两个小循环组成的digest循环中，
    一个循环是用来处理evalAsync队列（用来schedule一些需要在渲染视图之前处理的操作，
    通常通过setTimeout(0)实现，速度会比较慢，可能会出现视图抖动的问题）的，
    一个循环是处理watch列表（是一些表达式的集合，一旦有改变发生，那么watch函数就会被调用）的。
    digest循环会一直迭代知道evalAsync队列为空并且$watch列表也为空的时候，即model不再有任何变化。
* 一旦$digest循环结束，整个执行就会离开AngularJS和Javascript的context，紧接着浏览器就会把数据改变后的视图重新渲染出来。

###$digest 
digest像是Angularjs的心跳,每隔50ms刷新一次,
刷新的时候会触发所属的所有scope和其所有的scope下的dirty checking,dirtychecking又会触发$watch(),
整个Angularjs双向绑定数据就活了起来.

###$watch
在digest观察是如果watch监视的value有变化就会被触发,Angularjs内部实现的model的实时更新

###$apply
$scope.$apply会触发digest,当执行序列不是被angular序列创建的时候,我们可以用scope.apply把这个函数包起来

###event loop (事件回路)
Event Loop是一个程序结构，用于等待和发送消息和事件

简单说，就是在程序中设置两个线程：一个负责程序本身的运行，称为"主线程"；
另一个负责主线程与其他进程（主要是各种I/O操作）的通信，被称为"Event Loop线程"

```html
    <!doctype html>
    <html ng-app>
      <head>
        <script src="angular.js"></script>
      </head>
      <body>
        <input ng-model="name">
        <p>Hello {{name}}!</p>
      </body> 
    </html>
```

这段代码和上一段代码唯一的区别就是有了一个input来接收用户的输入。
在用浏览器去访问这个html文件的时候，input上的ng-model指令会给input绑上keydown事件，
并且会给name变量建议一个$watch来接收变量值改变的通知。在交互阶段主要会发生以下一系列事件：

* 当用户按下键盘上的某一个键的时候（比如说A），触发input上的keydown事件；
* input上的指令察觉到input里值的变化，调用$apply(“name=‘A’”)更新处于AngularJS的context中的model；
* AngularJS将’A’赋值给name；
* digest循环开始，watch列表检测到name值的变化，然后通知{{name}}表达式，更新DOM；
* 退出AngularJS的context，然后退出Javascript的context中的keydown事件；
* 浏览器重新渲染视图。

> 一旦AngularJS应用引导完毕，它将继续侦听浏览器的HTML触发事件，如鼠标点击事件、按键事件、HTTP传入响应等
> 改变DOM模型的事件。这类事件一旦发生，AngularJS将会自动检测变化，并作出相应的处理及更新。

