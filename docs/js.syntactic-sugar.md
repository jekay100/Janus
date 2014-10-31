ES6 语法糖之我见
=========

### 箭头操作符

在ES6中有许多新特性，其中新添了箭头操作符

```javascript

var array = ['ho', 'hd', 'hr'];

array.forEach(function(v){
    console.log(v);
});

//ES6
//array.forEach(v = > console.log(v));
array.forEach((v) = > console.log(v));

```

这里 ＂= >＂就是一个典型的语法糖　

那什么是语法糖？

** 计算机语言中添加的某种语法，这种语法对语言的功能并没有影响，但是更方便程序员使用 **

>> 简单的理解就是：语法糖是某种特性的语法块的简写方式

其实我们一直在接触语法糖， 如

```javascript

var o = {
    'x': 'Hunteron',
    'y': 'HunterDrive',
    'x.y': 'HunterDrive in Hunteron'
}

```

>> 正常情况下，大家都习惯用  o.x 读取对象o属性x的值；
>> 其实这个时候 ”.“ 就是一个语法糖符号
>> 真正的属性读法是  o['x']

### 又一个语法糖特性 延伸操作符 "..."

```javascript

var array = ['ho', 'hd', 'hr'];

//遍历打印 array 的子项
console.log.apply(window, array);

//延伸操作符 
console.log(...array);

/** 在函数中 */
var logName = function( name ){
    var others = [].slice.call(arguments,1);
    others.forEach(function(name){
        console.log(name);
    });
};

var logName = function(name, ...others){
    others.forEach(function(name){
        console.log(name);
    });
};
 
var logName = function(name, ...others){
    others.forEach((name) = > console.log(name));
};

var logName = (name, ...others) = >  others.forEach((name) = > console.log(name));

```

### 语法糖，语法盐

语法糖一定好吗？

>> 语法糖精， 语法海洛因 又是什么？

** 为什么会有人提出语法盐？ 语法盐就是什么东西？

语法盐： 为避免容易犯的语法错误加上的额外语法限制

>> ** 不管是语法糖还是语法盐，并不是矛盾的，互相不可兼容的；他们可以配合，可以相容的，一切都是为了简单易懂；
>> ** 如果一定要在简单和易懂中找出着重点，那肯定易懂为先。

### 语法糖和语法盐的相互合作， 类

在ES6 出现了类写法  class ClassName

```javascript

class Person{
    public name: 'John Doe'

    initialize(name){
        this.name = name;
    }

    say(message){
        return this.name + ': ' + message;
    }
};

```

虽然 ES6 有了类写法，但大家不要天真的认为ES6支持了类

class ClassName 其实也是一种ES6 的语法糖；

类中定义的所有方法都被加入这个类的原型prototype中;

