# String 扩展

## Unicode 表示法

> ES6 加强了对 Unicode 的支持，允许采用\uxxxx 形式表示一个字符，其中 xxxx 表示字符的 Unicode 码点。  
> 这种表示法只限于码点在\u0000~\uFFFF 之间的字符。超出这个范围的字符，必须用两个双字节的形式表示

```js
"\u0061";
// "a"

"\uD842\uDFB7";
// "𠮷"

// 如果直接在\u后面跟上超过0xFFFF的数值，JavaScript 会理解成\u20BB+7。由于\u20BB是一个不可打印字符，所以只会显示一个空格，后面跟着一个7
"\u20BB7";
// " 7"

// ES6 对这一点做出了改进，将码点放入大括号，就能正确解读该字符
"\u{20BB7}";
// "𠮷"

```

> 有了这种表示法之后，JavaScript 共有 6 种方法可以表示一个字符。

```js
"z" === "z"; // true
"\172" === "z"; // true
"\x7A" === "z"; // true
"\u007A" === "z"; // true
"\u{7A}" === "z"; // true
```

## 遍历器接口

```js
for (let item of "mooc") {
  console.log(item);
}
```

## 模板字符串

1. 字符串很长要换行
2. 字符串中有变量或者表达式
3. 字符串中有逻辑运算

```js
// String Literals
console.log("string text line 1\n" + "string text line 2");
// "string text line 1
// string text line 2"

console.log(`string text line 1
string text line 2`);
// "string text line 1
// string text line 2"

// Tag Literals

var retailPrice = 20;
var wholesalePrice = 16;
var type = "retail";

var showTxt = "";

if (type === "retail") {
  showTxt += "您此次的购买单价是：" + retailPrice;
} else {
  showTxt += "您此次的批发价是：" + wholesalePrice;
}

//
function Price(strings, type) {
  let s1 = strings[0];
  const retailPrice = 20;
  const wholesalePrice = 16;
  let txt = "";
  if (type === "retail") {
    txt = `购买单价是：${retailPrice}`;
  } else {
    txt = `批发价是：${wholesalePrice}`;
  }
  return `${s1}${txt}`;
}

let showTxt = Price`您此次的${"retail"}`;

console.log(showTxt); //您此次的购买单价是：20
```

## 扩展方法

### String.prototype.fromCodePoint()

> 用于从 Unicode 码点返回对应字符，并且可以识别大于 0xFFFF 的字符。

```js
// ES5
console.log(String.fromCharCode(0x20bb7));

// ES6
console.log(String.fromCodePoint(0x20bb7));
```

### String.prototype.includes()

```js
// ES5中可以使用indexOf方法来判断一个字符串是否包含在另一个字符串中，indexOf返回出现的下标位置，如果不存在则返回-1。
const str = "mooc";
console.log(str.indexOf("mo")); // 0

// ES6提供了includes方法来判断一个字符串是否包含在另一个字符串中，返回boolean类型的值
const str = "mooc";
console.log(str.includes("mo")); // true
```

### String.prototype.startsWith()

> 判断参数字符串是否在原字符串的头部, 返回 boolean 类型的值。

```js
const str = "mooc";
console.log(str.startsWith("m"));
```

### String.prototype.endsWith()

> 判断参数字符串是否在原字符串的尾部, 返回 boolean 类型的值。

```js
const str = "mooc";

console.log(str.endsWith("oc"));
```

### String.prototype.repeat()

> repeat 方法返回一个新字符串，表示将原字符串重复 n 次。

```js
const str = "mooc";

const newStr = str.repeat(2);

console.log(newStr); // 'moocmooc'
```
