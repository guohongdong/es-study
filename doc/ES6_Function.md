# Function

## 默认参数

```JavaScript
// bug
function foo(x, y) {
    y = y || 'world'
    console.log(x, y)
}
foo('hello', 'mooc')
foo('hello', 0)

// ES6
function foo(x, y = 'world') {
    console.log(x, y)
}
foo('hello', 0)
```

> 函数参数是从左到右解析，如果没有默认值会被解析成 undefined

* 如果我们想让具体某个参数使用默认值，我们可以使用 undefined 进行赋值

```js
function f(x, y = 7, z = 42) {
    return x + y + z
}
console.log(f(1, undefined, 43)) // 51
```

* 同时参数赋值支持参数的逻辑运算进行赋值

```js
function f(x, y = 7, z = x + y) {
    return z * 0.5
}

console.log(f(1, 7)) // 4
```

### 拓展

> 在函数体内，有时候需要判断函数有几个参数?

* 在 ES5 中可以在函数体内使用 arguments 来判断

```js

function foo(a, b = 1, c) {
    console.log(arguments.length)
}
foo('a', 'b') //2
```

* ES6 中不能再使用 arguments 来判断了，但可以借助 Function.length 来判断

```js
function foo(a, b = 1, c) {
    console.log(foo.length)
}
foo('a', 'b') // 1
```

* Function.length 是统计第一个默认参数前面的变量数

```js
function foo(a = 2, b = 1, c) {
    console.log(foo.length)
}
foo('a', 'b') // 0
```

## Rest 参数

```js
// ES5 求和
function sum() {
    let num = 0
    Array.prototype.forEach.call(arguments, function(item) {
        num += item * 1
    })
    return num
}

console.log(sum(1, 2, 3)) // 6
console.log(sum(1, 2, 3, 4)) // 10

// ES6
function sum(...nums) {
    let num = 0
    nums.forEach(function(item) {
        num += item * 1
    })
    return num
}

console.log(sum(1, 2, 3)) // 6
console.log(sum(1, 2, 3, 4)) // 10

// 和其他参数一起来用
function sum(base, ...nums) {
    let num = base
    nums.forEach(function(item) {
        num += item * 1
    })
    return num
}

console.log(sum(30, 1, 2, 3)) // 36
console.log(sum(30, 1, 2, 3, 4)) // 40
```

## 扩展运算符

## length属性

## name属性

## 箭头函数
