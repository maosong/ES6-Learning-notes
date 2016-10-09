# Class

本质上，ES6的类只是ES5构造函数的一层包装，但也有个别差异。

我比较关注类的继承，ES5通过修改原型链实现继承，而ES6通过extends关键字实现。区别是前者`先创建父类实例`，后者`先创建子类实例`。因此，ES6的构造函数中必须先调用`super()`才能使用`this`关键字。

既然无法控制父类构造函数执行顺序，我们编写`init()`方法提高灵活性。

```
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  init() {
    console.log('class Point');
  }
}

class ColorPoint extends Point {
  constructor(x, y, color) {
    this.color = color; // ReferenceError
    super(x, y);
    this.color = color; // 正确

    this.init();
  }

  init() {
    console.log('class ColorPoint');
    super.init();
  }
}
```

super关键字有两种用法，含义不同。

1. 作为函数调用时（即super(...args)），super代表父类的构造函数。
2. 作为对象调用时（即super.prop或super.method()），super代表父类。注意，此时super即可以引用父类实例的属性和方法，也可以引用父类的静态方法。

```
class A {
  constructor() {
    this._p = 1;
  }
  resetP() {
    this._p = 2;
  }
}
class B extends A {
  constructor(p) {
    super();
    this.p = p;
  }
  get p() {
    super.resetP();
    return this._p * super._p;
  }
}
```
