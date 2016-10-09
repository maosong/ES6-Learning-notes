# 正则表达式

**第二个参数会覆盖第一个参数的修饰符**

```
new RegExp(/abc/ig, 'i').flags
```

**增加了u修饰符**

用于处理大于\uFFFF的Unicode字符，也就是说，会正确处理四个字节的UTF-16编码。

```
/^\uD83D/u.test('\uD83D\uDC2A')
// false
/^\uD83D/.test('\uD83D\uDC2A')
// true

var s = '𠮷';
/^.$/.test(s) // false
/^.$/u.test(s) // true

/\u{61}/.test('a') // false
/\u{61}/u.test('a') // true
/\u{20BB7}/u.test('𠮷') // true
```

**量词**

```
/a{2}/.test('aa') // true
/a{2}/u.test('aa') // true
/𠮷{2}/.test('𠮷𠮷') // false
/𠮷{2}/u.test('𠮷𠮷') // true

//不使用u修饰符
/^\u{3}$/.test('uuu') // true
```

**预定义模式**

```
/^\S$/.test('𠮷') // false
/^\S$/u.test('𠮷') // true
```

**统计字符串长度**

```
function codePointLength(text) {
  var result = text.match(/[\s\S]/gu);
  return result ? result.length : 0;
}

var s = '𠮷𠮷';

s.length // 4
codePointLength(s) // 2
```

**y修饰符**

```
var s = 'aaa_aa_a';
var r = /a+_/y;
r.exec(s) // ["aaa_"]
r.exec(s) // ["aa_"]

var r = /hello\d/y;
r.sticky // true

const REGEX = /a/g;
// 指定从2号位置（y）开始匹配
REGEX.lastIndex = 2;
// 匹配成功
const match = REGEX.exec('xaya');
// 在3号位置匹配成功
match.index // 3
// 下一次匹配从4号位开始
REGEX.lastIndex // 4
// 4号位开始匹配失败
REGEX.exec('xaxa') // null

// 没有找到匹配
'x##'.split(/#/y)
// [ 'x##' ]
// 找到两个匹配
'##x'.split(/#/y)
// [ '', '', 'x' ]

'#x#'.split(/#/y)
// [ '', 'x#' ]
'##'.split(/#/y)
// [ '', '', '' ]
```

**字符串转义**

```
// escapeRegExp函数

function escapeRegExp(str) {
  return str.replace(/[\-\[\]\/\{\}\(\)\*\+\?\.\\\^\$\|]/g, '\\$&');
}

let str = '/path/to/resource.html?search=query';
escapeRegExp(str)
// "\/path\/to\/resource\.html\?search=query"
```

```
// 垫片模块 regexp.escape
var escape = require('regexp.escape');
escape('hi. how are you?');
// "hi\\. how are you\\?"
```
