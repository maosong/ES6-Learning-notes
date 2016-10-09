# 数组

**Array.from()**

```
let arrayLike = {
    '0': 'a',
    '1': 'b',
    '2': 'c',
    length: 3
};
// ES5的写法
var arr1 = [].slice.call(arrayLike); // ['a', 'b', 'c']
// ES6的写法
let arr2 = Array.from(arrayLike); // ['a', 'b', 'c']

// NodeList对象
let ps = document.querySelectorAll('p');
Array.from(ps).forEach(function (p) {
  console.log(p);
});

// arguments对象
function foo() {
  var args = Array.from(arguments);
  // ...
}

Array.from('hello')
// ['h', 'e', 'l', 'l', 'o']

let namesSet = new Set(['a', 'b'])
Array.from(namesSet) // ['a', 'b']
```

```
// arguments对象
function foo() {
  var args = [...arguments];
}

// NodeList对象
[...document.querySelectorAll('div')]
```

```
Array.from([1, 2, 3], (x) => x * x)
//等同于
Array.from([1, 2, 3]).map(x => x * x);
```

```
//取出一组DOM节点的文本内容
let spans = document.querySelectorAll('span.name');
let names = Array.from(spans, s => s.textContent)
```

```
//将数组中布尔值为false的成员转为0
Array.from([1, , 2, , 3], (n) => n || 0)
// [1, 0, 2, 0, 3]
```

```
Array.from({ length: 3 }, () => Math.random())
```

```
//统计字符串的长度，避免JavaScript将大于\uFFFF的Unicode字符，算作两个字符的bug。
function countSymbols(string) {
  return Array.from(string).length;
}
```

**Array.find()和findIndex()**

```
[1, 4, -5, 10].find((value, index, arr) => value < 0)
// -5

[1, 4, -5, 10].findIndex((value, index, arr) => value < 0)
// 2

[NaN].findIndex(y => Object.is(NaN, y))
// 0
```

**Array.entries()，keys()和values()**

```
for (let index of ['a', 'b'].keys()) {
  console.log(index);
}
// 0
// 1

for (let elem of ['a', 'b'].values()) {
  console.log(elem);
}
// 'a'
// 'b'

for (let [index, elem] of ['a', 'b'].entries()) {
  console.log(index, elem);
}
// 0 "a"
// 1 "b"

let letter = ['a', 'b', 'c'];
let entries = letter.entries();
console.log(entries.next().value); // [0, 'a']
console.log(entries.next().value); // [1, 'b']
console.log(entries.next().value); // [2, 'c']
```

**Array.includes()**

```
[1, 2, 3].includes(2);     // true
[1, 2, 3].includes(4);     // false
[1, 2, NaN].includes(NaN); // true

[1, 2, 3].includes(3, 3);  // false
[1, 2, 3].includes(3, -1); // true
```
