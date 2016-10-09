# Proxy和Reflect

## Proxy

子类可以覆盖基类的方法，而Proxy允许我们覆盖语言层面的行为，比如对象属性的存取行为。

```
var proxy = new Proxy({}, {
  get: function(target, property) {
    return 35;
  }
});

proxy.time // 35
proxy.name // 35
proxy.title // 35
```

[Proxy概述](http://es6.ruanyifeng.com/#docs/proxy#Proxy概述)和[Proxy实例的方法](http://es6.ruanyifeng.com/#docs/proxy#Proxy实例的方法)中做了详细讲解。

## Reflect

Reflect将逐步替代Object明显属于语言内部的方法，也可以与Proxy配合使用，下面是几个例子

```
 // 老写法
try {
  Object.defineProperty(target, property, attributes);
  // success
} catch (e) {
  // failure
}

// 新写法
if (Reflect.defineProperty(target, property, attributes)) {
  // success
} else {
  // failure
}
```

```
// 老写法
'assign' in Object // true

// 新写法
Reflect.has(Object, 'assign') // true
```

```
var loggedObj = new Proxy(obj, {
  get(target, name) {
    console.log('get', target, name);
    return Reflect.get(target, name);
  },
  deleteProperty(target, name) {
    console.log('delete' + name);
    return Reflect.deleteProperty(target, name);
  },
  has(target, name) {
    console.log('has' + name);
    return Reflect.has(target, name);
  }
});
```
[Reflect对象的方法](http://es6.ruanyifeng.com/#docs/proxy#Reflect对象的方法)中做了详细讲解。
