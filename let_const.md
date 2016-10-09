# let和const命令

个人认为let和const是es6极大的亮点之一，解决了var变量干扰全局或函数级作用域的问题，同时window全局变量的弊病也得以解决，

使用时要注意 [暂时性死区](http://es6.ruanyifeng.com/#docs/let#暂时性死区) 问题。

**let**

```
var tmp = '1';
var f1 = '2';
var tmpf1 = '3';
{
  let tmp = 'x';
  let f1 = 'y';
  let tmpf1 = 'z';
  if (true) {
    tmp = 'abc';
    let f1 = function(){
      return 'ok';
    };
    let tmpf1 = f1();
    console.log(tmp); // abc
    console.log(f1); // [Function: f1]
    console.log(tmpf1); // ok
  }
  console.log(tmp); // abc
  console.log(f1); // y
  console.log(tmpf1); //z
}
console.log(tmp); // 1
console.log(f1); // 2
console.log(tmpf1); // 3
```

**以下是const使用例子（也是块级作用域）**

```
const PI = 3.1415;
console.log(PI) // 3.1415
PI = 0 // Error
```

```
const foo = {};
foo.prop = 123;

foo.prop
// 123

foo = {}; // TypeError: "foo" is read-only
```

```
const jQuery = require('jQuery')
jQuery; //The jQuery Library
```
