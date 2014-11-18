JS 中的继承
======

## 继承

> 继承”是面向对象软件技术当中的一个概念
> 继承可以使得子类具有父类的各种属性和方法，而不需要再次编写相同的代码。
> 在令子类继承父类的同时，可以重新定义某些属性，并重写某些方法，即覆盖父类的原有属性和方法，使其获得与父类不同的功能。
> 为子类追加新的属性和方法也是常见的做法

## JS 继承中几种比较常见的方法

### prototype 方式 (原型链式)

> prototype 即为原型，每个构造函数都有一个默认的原型属性，该属性是个对象类型；

> JS读取一个对象属性的时候，对象本身若找不到，则会去读取构造函数的prototype对象的同名属性，若还是继续向上索引盘查，
  直到查到该属性值或最后查不到为止（undefined )；
  
```javascript

    var src = function(){
        this.say = 'Hello';
        this.name = 'World!';
        this.toString = function(){
            return console.log(this.say + ' ' + this.name);
        }
    };
    
    var target = function(){
        this.name = 'Hunteron!';
    };
     
    target.prototype = new src();

    var inst = new target();
    
    inst.toString(); // Hello Hunteron!
    
```

### 对象冒充

> 利用JS中类和函数的模糊性

```javascript

    var src = function(){
        this.say = 'Hello';
        this.name = 'World!';
        this.toString = function(){
            return console.log(this.say + ' ' + this.name);
        }
    };
    
    var target = function(){
        this.method = src;
        this.method();
        delete this.method;
        this.name = 'ho';
    };
    
    var inst = new target();
    
    inst.toString(); // Hello Hunteron!

```

### call, apply

> 更改原方法中的scope, 即 this;

```javascript

    var src = function(){
        this.say = 'Hello';
        this.name = 'World!';
        this.toString = function(){
            return console.log(this.say + ' ' + this.name);
        }
    };
    
    var target = function(){
        src.call(this); // src.apply(this)
        this.name = 'ho';
    }
    
    var inst = new target();
    
    inst.toString();
    
```

### 混合模式

```javascript

    var src = function(){
        this.say = 'Hello';
        this.name = 'World!';
        this.toString = function(){
            return console.log(this.say + ' ' + this.name);
        }
    };
    
    src.prototype.setSay = function(){
        this.say = 'hi';
    };
    
    var target = function(){
        var base = new src();
        for(var key in base){
            this[key] = base[key];
        }
        this.name = 'ho';
    }
    
    var inst = new target();
    
    inst.toString(); // Hello ho;
    
    inst.setSay('Hi');
    
    inst.toString(); // ....
    
```

``` javascript

```
