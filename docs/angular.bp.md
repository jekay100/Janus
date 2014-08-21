Angular 最佳实践
========

## 优化 digest cycle

* 只监听必要的变量(例如：在进行实时通讯时，不要在每次接收到消息时触发 digest loop)
* 尽可能使 $watch 中的运算简单。在单个 $watch 中进行繁杂的运算将使得整个应用延缓(由于JavaScript的单线程特性，$digest loop 只能在单一线程进行)

>当你使用 ng-model， ng-repeat 等等来绑定一个元素的值时， 
>AngularJS 为那个值创建了一个 $watch，只要这个值在 AngularJS 的范围内有任何改变，所有的地方都会同步更新。
>而你在写自定义的 directive 时，你需要定义你自己的 $watch 来实现这种自动同步。
>有时候你在代码中改变了 model 的值 view 却没有更新，这在自定义事件绑定中经常遇到。
>这时你就需要手动调用 scope.$apply() 来触发界面更新。


## 尽量使用ng封装service替代原生方法

* $timeout 替代 setTimeout
* $window 替代 window
* $document 替代 document
* $http 替代 $.ajax

这将使你更易于在测试时处理代码异常 (例如：你在 setTimeout 中忘记 $scope.$apply)

* 使用 promise ($q) 而非回调。这将使你的代码更加优雅、直观，并且免于回调地狱。
* 尽可能使用 $resource 而非 $http。更高的抽象可以避免冗余。
* 使用AngularJS的预压缩版 (像 ngmin 或 ng-annotate) 避免在压缩之后出现问题。
* 不要使用全局。通过依赖注入解决所有依赖。
* 不要污染 $scope。仅添加与视图相关的函数和变量。
* 使用 controllers 而非 ngInit

## 模块

* 按照功能组织模块

## 控制器

* 不要在控制器里操作 DOM。通过指令完成。
* 通过控制器完成的功能命名控制器 (如：购物卡，主页，控制板)，并以字符串Ctrl结尾。控制器采用驼峰命名法 (HomePageCtrl, ShoppingCartCtrl, AdminPanelCtrl, etc.).
* 控制器不应该在全局中定义 (尽管 AngularJS 允许，但污染全局空间是个糟糕的实践)。
* 使用数组语法定义控制器
> 使用控制器依赖的原名
> 这将提高代码的可读性
> 对于包含大量代码的需要上下滚动的文件尤其适用。这可能使你忘记某一变量是对应哪一个依赖

```javascript
    module.controller('MyCtrl', ['dependency1', 'dependency2', ..., 'dependencyn', function (dependency1, dependency2, ..., dependencyn) {
      //...body
    }]);
```

* 使用别名 (需展开说明)

```html

    <!-- Bad: -->
    <div ng-controller="MainCtrl">
      {{ someObject }}
    </div>
    <!-- Good:  -->
    <div ng-controller="MainCtrl as main">
      {{ main.someObject }}
    </div>
    
```

```javascript

    function config ($routeProvider) {
        $routeProvider
        .when('/', {
            templateUrl: 'views/main.html',
            controller: 'MainCtrl',
            controllerAs: 'main'
        });
    }

```

* 尽可能的精简控制器。将通用函数抽象为独立的服务。
* 通过方法引用进行跨控制器通讯 (通常是子控制器与父控制器通讯) 或者 $emit, $broadcast 及 $on 方法。发送或广播的消息应该限定在最小的作用域。
* 制定一个通过 $emit, $broadcast 发送的消息列表并且仔细的管理以防命名冲突和bug。
* 在需要格式化数据时将格式化逻辑封装成 过滤器 并将其声明为依赖

## 指令

* 使用小写字母开头的驼峰法命名指令。
* 在 link function 中使用 scope 而非 $scope。在 compile 中, 你已经定义参数的 post/pre link functions 将在函数被执行时传递, 你无法通过依赖注入改变他们。这种方式同样应用在 AngularJS 项目中。
* 为你的指令添加自定义前缀以免与第三方指令冲突。
* 不要使用 ng 或 ui 前缀，因为这些备用于 AngularJS 和 AngularJS UI。
* DOM 操作只通过指令完成。
* 为你开发的可复用组件创建独立作用域。
* 建议使用属性，而不要使用 class 或 备注 （自定义标签，因要兼容IE8放弃使用）

## 服务

* 用驼峰法命名服务( $MoudleService )。
* 将业务逻辑封装为服务。
* 将业务逻辑封装成 service 而非 factory
* 可以使用 $cacheFactory 进行会话级别的缓存。这应该用于缓存请求或复杂运算的结果。(！以后衍生讲开)

## 模板

* 使用 ng-bind 或者 ng-cloak 而非简单的 {{ }} 以防止页面渲染时的闪烁。
* 避免在模板中使用复杂的代码。
* 当需要动态设置  的 src/href 时使用 ng-src/ng-href 而非 src 中嵌套 {{}} 的模板。
* 通过对象参数和 scope 变量作为值来使用 ng-style 指令，而非将 scope 变量作为字符串通过 {{ }} 用于 style 属性。

## 路由
 
* 在视图展示之前通过 resolve 解决依赖。

## \$scope, \$rootScope

> \$scope 在 templates 模板中应该是 read-only 的，而在 controller 里应该是 write-only 的。
> \$scope 的目的是引用 model，而不是成为 model。model 就是我们定义的 JavaScript 对象。

* \$rootScope 是可以用的，不过很可能被滥用