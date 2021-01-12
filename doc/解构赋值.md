# 解构赋值

> 解构赋值。允许按照一定模式，从数组和对象中提取值，对变量进行赋值。

## 数组解构赋值

### 赋值元素可以是任意可遍历的对象

```javascript
let [a, b, c] = "abc" // ["a", "b", "c"]
let [one, two, three] = new Set([1, 2, 3])
```

### 被赋值的变量还可以是对象的属性，不局限于单纯的变量

```javascript
let user = {}
[user.firstName, user.secondName] = 'Kobe Bryant'.split(' ')
console.log(user.firstName, user.secondName) // Kobe Bryant
```

### 解构赋值在循环体中的应用，可以配合 entries 使用

```javascript
let user = {
  name: 'John',
  age: 30
}
// loop over keys-and-values
for (let [key, value] of Object.entries(user)) {
  console.log(`${key}:${value}`) // name:John, then age:30
}

// map
let user = new Map()
user.set('name', 'John')
user.set('age', '30')

for (let [key, value] of user.entries()) {
  console.log(`${key}:${value}`) // name:John, then age:30
}
```

### 忽略数组的某个元素对变量进行赋值，可以使用逗号来处理

```javascript
// second element is not needed
let [name, , title] = ['John', 'Jim', 'Sun', 'Moon']
console.log( title ) // Sun
```

### rest 参数

```javascript
let [name1, name2, ...rest] = ["Julius", "Caesar", "Consul", "of the Roman Republic"]

console.log(name1) // Julius
// Note that type of `rest` is Array.
console.log(rest[0]) // Consul
console.log(rest.length) // 2
```

> 我们可以使用 rest 来接受赋值数组的剩余元素，不过要确保这个 rest 参数是放在被赋值变量的最后一个位置上。

### 默认值

> 如果数组的内容少于变量的个数，并不会报错，没有分配到内容的变量会是 undefined

```javascript
let [firstName, surname] = []

console.log(firstName) // undefined
console.log(surname) // undefined

// 给变量赋予默认值
let [name = "Guest", surname = "Anonymous"] = ["Julius"]
console.log(name)    // Julius (from array)
```

## 对象结构赋值

### 基本用法

> 在赋值的左侧声明一个和 Object 结构等同的模板，然后把关心属性的 value 指定为新的变量即可。

```javascript
let options = {
  title: "Menu",
  width: 100,
  height: 200
}

let {title, width, height} = options
console.log(title)  // Menu

let {title: title, width: width, height: height} = options

//自定义变量名
let {width: w, height: h, title} = options

```

> 在这个结构赋值的过程中，左侧的“模板”结构要与右侧的 Object 一致，但是属性的顺序无需一致。

### 默认值设置

```javascript
let options = {
  title: "Menu"
}

let {width = 100, height = 200, title} = options
console.log(title)  // Menu
console.log(width)  // 100
```

### rest 运算符

```javascript
let options = {
  title: "Menu",
  height: 200,
  width: 100
}

let {title, ...rest} = options // now title="Menu", rest={height: 200, width: 100}
```

### 嵌套对象

> 如果一个 Array 或者 Object 比较复杂，它嵌套了 Array 或者 Object，那只要被赋值的结构和右侧赋值的元素一致就好了

```javascript
let options = {
  size: {
    width: 100,
    height: 200
  },
  items: ["Cake", "Donut"],
  extra: true    // something extra that we will not destruct
}

// destructuring assignment on multiple lines for clarity
let {
  size: { // put size here
    width,
    height
  },
  items: [item1, item2], // assign items here
  title = 'Menu' // not present in the object (default value is used)
} = options

console.log(title)  // Menu
console.log(width)  // 100
```

## 字符串解构赋值

```javascript
let str = 'mooc'
let [a, b, c, d, e] = str
console.log(a, b, c, d, e)
```
