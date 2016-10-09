# 对象

本章没有详细阅读，但总体感觉ES6的对象操作得到大幅度提升，可以[点击此处查看原文](http://es6.ruanyifeng.com/#docs/object)。

```
var foo = 'bar';
var baz = {foo};
baz // {foo: "bar"}
// 等同于
var baz = {foo: foo};

function f(x, y) {
  return {x, y};
}
// 等同于
function f(x, y) {
  return {x: x, y: y};
}
f(1, 2) // Object {x: 1, y: 2}
```

```
var o = {
  method() {
    return "Hello!";
  }
};

// 等同于

var o = {
  method: function() {
    return "Hello!";
  }
};
```

```
var birth = '2000/01/01';

var Person = {

  name: '张三',

  //等同于birth: birth
  birth,

  // 等同于hello: function ()...
  hello() { console.log('我的名字是', this.name); }

};
```

```
function getPoint() {
  var x = 1;
  var y = 10;
  return {x, y};
}

getPoint()
// {x:1, y:10}
```

```
let propKey = 'foo';

let obj = {
  [propKey]: true,
  ['a' + 'bc']: 123
};

obj // {foo: true, abc: 123}
```

```
let obj = {
  ['h'+'ello']() {
    return 'hi';
  }
};

obj.hello() // hi
```

```
var person = {
  sayName() {
    console.log(this.name);
  },
  get firstName() {
    return "Nicholas";
  }
};

person.sayName.name   // "sayName"
person.firstName.name // "get firstName"
```

```
(new Function()).name // "anonymous"

var doSomething = function() {
  // ...
};
doSomething.bind().name // "bound doSomething"
```

**Object.is**

```
Object.is('foo', 'foo')
// true
Object.is({}, {})
// false

+0 === -0 //true
NaN === NaN // false
Object.is(+0, -0) // false
Object.is(NaN, NaN) // true
```
