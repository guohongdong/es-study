# 新的声明方式

## 作用域

对象      | 类型
---------|----------
 global/window | 全局作用域
 function | 函数作用域（局部作用域）
 {}       | 块状作用域
 this     | 动态作用域

### 全局作用域

> 变量在函数或者代码块 {} 外定义，即为全局作用域。

```javascript
var course = "es"

// 此处可调用 course 变量
function myFunction() {
    // 函数内可调用 course 变量
}
```

```javascript
// 此处可调用 course 变量
// 将作为 global 或者 window 的属性存在。
function myFunction() {
    course = "es"
    // 此处可调用 course 变量
}
```

> 在函数内部或代码块中没有定义的变量实际上是作为 window/global 的属性存在，而不是全局变量。换句话说没有使用 var 定义的变量虽然拥有全局作用域，但是它是可以被 delete 的，而全局变量不可以。

### 函数作用域

> 在函数内部定义的变量，就是局部作用域。

```javascript
function bar() {
    var testValue = 'inner'
}

console.log(testValue)
```

> 如果想读取函数内的变量，必须借助 return 或者闭包。

```javascript
function bar(value) {
    var testValue = 'inner'

    return testValue + value
}

console.log(bar('fun')) // "innerfun"
```

```javascript
function bar(value) {
    var testValue = 'inner'

    var rusult = testValue + value

    function innser() {
        return rusult
    }

    return innser()
}

console.log(bar('fun')) // "innerfun"
```

### 块状作用域

```javascript
// {} 之外是无法访问这个变量的。
if (true) {
    let a = 1
    console.log(a)
}
```

### 动态作用域

```javascript
window.a = 3

function test() {
    console.log(this.a)
}

test.bind({
    a: 2
})() // 2
test() // 3
```

## let

### let 声明的全局变量不是全局对象window的属性

```javascript
var a = 5
console.log(window.a) // 5

let a = 5
console.log(window.a) // undefined
```

### 用let定义变量不允许重复声明

```javascript
var a = 5
var a = 6

console.log(a) // 5

//
let a = 5
let a = 6
// VM131:1 Uncaught SyntaxError: Identifier 'a' has already been declared
//   at <anonymous>:1:1
```

### let声明的变量不存在变量提升

```javascript
function foo() {
    console.log(a)
    var a = 5
}

foo() //undefined

//
function foo() {
    console.log(a)
    let a = 5
}

foo()
// Uncaught ReferenceError: Cannot access 'a' before initialization
```

### let声明的变量具有暂时性死区

> 只要块级作用域内存在 let 命令，它所声明的变量就绑定在了这个区域，不再受外部的影响。  
> 在代码块内，使用 let 命令声明变量之前，该变量都是不可用的。这在语法上，称为“暂时性死区”

```javascript
var a = 5
if (true) {
    a = 6
    let a
}
// Uncaught ReferenceError: Cannot access 'a' before initialization

function foo(b = a, a = 2) {
    console.log(a, b)
}
foo()

```

### let 声明的变量拥有块级作用域

```javascript
if (false) {
    var a = 5
}
console.log(a) // undefined
// 
if (false) {
    let a = 5
}
console.log(a)
// Uncaught ReferenceError: a is not defined
```

## Const

> const 声明的变量必须进行初始化，不然会抛出异常 Uncaught SyntaxError: Missing initializer in const declaration

```javascript
// ES5
Object.defineProperty(window, 'PI', {
    value: 3.14,
    writable: false
})
console.log(PI)
PI = 5
console.log(PI)

// ES6
const PI = 3.1415
console.log(PI)
PI = 5
console.log(PI)
// Uncaught TypeError: Assignment to constant variable.
```

### 重点

```javascript
const obj = {
    name: 'dd',
    age: 34
}
obj.school = 'mooc'
console.log(obj)
// {name: "dd", age: 34, school: "mooc"}
```

![JS中的变量是如何存储](http://es.xiecheng.live/assets/img/stack-heap.a163c957.png)

> const 实际上保证的并不是变量的值不得改动，而是变量指向的那个内存地址所保存的数据不得改动。

```javascript
// 如何让对象或者数组这种引用数据类型也不被改变呢？
Object.freeze(obj)
```

> Object.freeze() 只是浅层冻结，只会对最近一层的对象进行冻结，并不会对深层对象冻结。