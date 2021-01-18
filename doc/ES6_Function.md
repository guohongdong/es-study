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

> 简单的来说 Rest Parameter 是把不定的参数“收敛”到数组，而 Spread Operator 是把固定的数组内容“打散”到对应的参数。

```js
function sum(x = 1, y = 2, z = 3) {
    return x + y + z
}

console.log(sum.apply(null, [4])) // 9
console.log(sum.apply(null, [4, 5])) // 12
console.log(sum.apply(null, [4, 5, 6])) // 15

// ES6
function sum(x = 1, y = 2, z = 3) {
    return x + y + z
}

console.log(sum(...[4])) // 9
console.log(sum(...[4, 5])) // 12
console.log(sum(...[4, 5, 6])) // 15
```

## length属性

> 函数指定了默认值以后，函数的length属性，将返回没有指定默认值的参数个数

```js
function foo(x = 1, y = 2, z = 3) {
    console.log(x, y)
}
console.log(foo.length)
// 0
```

## name属性

> 函数的name属性，返回该函数的函数名。

```js
function foo() {}
foo.name // "foo"
```

## 箭头函数

```js
function hello() {
    console.log('say hello')
}
// 或

let hello = function() {
    console.log('say hello')
}

// ES6
let hello = () => {
    console.log('say hello')
}
```

* 如果返回值是表达式可以省略 return 和 {}
* 如果返回值是字面量对象，一定要用小括号包起来

### 拓展内容

```js
let foo = {
    name: 'es',
    say: function() {
        console.log(this.name)
    }
}

console.log(foo.say()) // es

// ES6
let foo = {
    name: 'es',
    say: () => {
        console.log(this.name, this)
    }
}
console.log(foo.say()) // undefined
```

1. 箭头函数中this指向定义时所在的对象，而不是调用时所在的对象
2. 箭头函数不可以当作构造函数
3. 箭头函数不可以使用arguments对象
