#karma
##安装karma及插件
```bash
npm install karma --save-dev
npm install karma-jasmine karma-chrome-launcher --save-dev
npm install -g karma-cli
```
##使用karma管理测试
```bash
#初始化`karma.conf.js`
karma init [<configfile>]

#运行karma
karma start [<configfile>]
```

#Jasmine
##matcher集
[http://jasmine.github.io/2.0/introduction.html#section-Matchers](http://jasmine.github.io/2.0/introduction.html#section-Matchers)
```javascript
#toBe
describe("The 'toBe' matcher", function() {

  it("The 'toBe' matcher compares with ===", function() {
    var a = 12;
    var b = a;

    expect(a).toBe(b);
    expect(a).not.toBe(null);
  });

});

#toEqual
describe("The 'toEqual' matcher", function() {

    it("works for simple literals and variables", function() {
      var a = 12;
      expect(a).toEqual(12);
    });

    it("should work for objects", function() {
      var foo = {
        a: 12,
        b: 34
      };
      var bar = {
        a: 12,
        b: 34
      };
      expect(foo).toEqual(bar);
    });
});

#toMatch
describe("The 'toMatch' matcher", function() {

    it("The 'toMatch' matcher is for regular expressions", function() {
        var message = "foo bar baz";

        expect(message).toMatch(/bar/);
        expect(message).toMatch("bar");
        expect(message).not.toMatch(/quux/);
    });
});

#toBeDefined
describe("The 'toBeDefined' matcher", function() {
    it("The 'toBeDefined' matcher compares against `undefined`", function() {
        var a = {
          foo: "foo"
        };

        expect(a.foo).toBeDefined();
        expect(a.bar).not.toBeDefined();
  });
});

#toBeUnDefined
describe("The 'toBeUnDefined' matcher", function() {
    it("The `toBeUndefined` matcher compares against `undefined`", function() {
        var a = {
            foo: "foo"
        };

        expect(a.foo).not.toBeUndefined();
        expect(a.bar).toBeUndefined();
    });
});

#toBeNull
describe("The 'toBeNull' matcher", function() {
    it("The 'toBeNull' matcher compares against null", function() {
        var a = null;
        var foo = "foo";

        expect(null).toBeNull();
        expect(a).toBeNull();
        expect(foo).not.toBeNull();
    });
});

#toBeTruthy
describe("The 'toBeTruthy' matcher", function() {
    it("The 'toBeTruthy' matcher is for boolean casting testing", function() {
        var a, foo = "foo";

        expect(foo).toBeTruthy();
        expect(a).not.toBeTruthy();
    });
});

#toBeFalsy
describe("The 'toBeFalsy' matcher", function() {
    it("The 'toBeFalsy' matcher is for boolean casting testing", function() {
        var a, foo = "foo";

        expect(a).toBeFalsy();
        expect(foo).not.toBeFalsy();
    });
});

#toContain
describe("The 'toContain' matcher", function() {
    it("The 'toContain' matcher is for finding an item in an Array", function() {
        var a = ["foo", "bar", "baz"];

        expect(a).toContain("bar");
        expect(a).not.toContain("quux");
    });
});

#toBeLessThan
describe("The 'toBeLessThan' matcher", function() {
    it("The 'toBeLessThan' matcher is for mathematical comparisons", function() {
        var pi = 3.1415926,
            e = 2.78;

        expect(e).toBeLessThan(pi);
        expect(pi).not.toBeLessThan(e);
    });
});

#toBeGreaterThan
describe("The 'toBeGreaterThan' matcher", function() {
    it("The 'toBeGreaterThan' matcher is for mathematical comparisons", function() {
        var pi = 3.1415926,
            e = 2.78;

        expect(pi).toBeGreaterThan(e);
        expect(e).not.toBeGreaterThan(pi);
    });
});

#toBeCloseTo
describe("The 'toBeCloseTo' matcher", function() {
    it("The 'toBeCloseTo' matcher is for precision math comparison", function() {
        var pi = 3.1415926,
            e = 2.78;

        expect(pi).not.toBeCloseTo(e, 2);
        expect(pi).toBeCloseTo(e, 0);
    });
});

#toThrow
describe("The 'toThrow' matcher", function() {
    it("The 'toThrow' matcher is for testing if a function throws an exception", function() {
        var foo = function() {
            return 1 + 2;
        };
        var bar = function() {
            return a + 1;
        };

        expect(foo).not.toThrow();
        expect(bar).toThrow();
    });
});
```
##setup and teardown
[http://jasmine.github.io/2.0/introduction.html#section-Setup_and_Teardown](http://jasmine.github.io/2.0/introduction.html#section-Setup_and_Teardown)
```javascript
describe("A spec (with setup and tear-down)", function() {
  var foo;

  beforeEach(function() {
    foo = 0;
    foo += 1;
  });

  afterEach(function() {
    foo = 0;
  });

  it("is just a function, so it can contain any code", function() {
    expect(foo).toEqual(1);
  });

  it("can have more than one expectation", function() {
    expect(foo).toEqual(1);
    expect(true).toEqual(true);
  });
});