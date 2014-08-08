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
* AngularJS等待DOMContentLoaded事件的触发；
* AngularJS寻找ng-app指令，根据这个指令确定应用程序的边界；
* 使用ng-app中指定的模块配置$injector；
* 使用injector创建compile服务和$rootScope；
* 使用compile服务编译DOM并把它链接到rootScope上；
* ng-init指令对scope里面的变量name进行赋值；
* 对表达式{{name}}进行替换，于是乎，显示为“Hello World!”   

整个过程可以用这张图来表示：

![ng 渲染流程](http://images.cnitblog.com/blog/93149/201311/26231509-35460094427943cda3fd99197ff1e775.jpg)