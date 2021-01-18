# Object

## 属性简洁表示法

```js
let name = 'dd'
  let age = 34
  let obj = {
      name: name,
      age: age,
      study: function() {
          console.log(this.name + '正在学习')
      }
  }

// ES6
let name = 'dd'
  let age = 34
  let obj = {
      name,
      age,
      study() {
          console.log(this.name + '正在学习')
      }
  }
```

## 属性名表达式

> ES6 可以直接用变量或者表达式来定义Object的 key

```js
let s = 'school'
  let obj = {
      foo: 'bar',
      [s]: 'imooc'
  }
```

## Object.is() 判断两个对象是否相等

```js
let obj1 = { // new Object()
    name: 'dd',
    age: 34
}

let obj2 = { // new Object()
    name: 'dd',
    age: 34
}
console.log(obj1 == obj2) // false
console.log(Object.is(obj1, obj2)) // false

let obj2 = obj1
console.log(Object.is(obj1, obj2)) // true
```

## Object.assign()

> Object.assign() 方法用于将所有可枚举属性的值从一个或多个源对象复制到目标对象，它将返回目标对象

```js
const target = {
    a: 1,
    b: 2
}
const source = {
    b: 4,
    c: 5
}
const returnedTarget = Object.assign(target, source)
console.log(target)
// expected output: Object { a: 1, b: 4, c: 5 }

console.log(returnedTarget)
// expected output: Object { a: 1, b: 4, c: 5 }
```

> 如果目的对象不是对象，则会自动转换为对象

```js
let t = Object.assign(2)
// Number {2}
let s = Object.assign(2, {
    a: 2
})
// Number {2, a: 2}

// 多层嵌套
let target = {
    a: {
        b: {
            c: 1
        },
        e: 4,
        f: 5,
        g: 6
    }
}
let source = {
    a: {
        b: {
            c: 1
        },
        e: 2,
        f: 3
    }
}
Object.assign(target, source)
console.log(target)
```

> Object.assign()对于引用数据类型属于浅拷贝。  
> 对象的浅拷贝：浅拷贝是对象共用的一个内存地址，对象的变化相互印象。  
> 对象的深拷贝：简单理解深拷贝是将对象放到新的内存中，两个对象的改变不会相互影响。

## 对象的遍历方式

```js
let obj = {
    name: 'xiecheng',
    age: 34,
    school: 'imooc'
}
// for in
for (let key in obj) {
    console.log(key, obj[key])
}

// Object.keys()用于返回对象所有key组成的数组。
Object.keys(obj).forEach(key => {
    console.log(key, obj[key])
})

// Object.getOwnPropertyNames()用于返回对象所有key组成的数组。
Object.getOwnPropertyNames(obj).forEach(key => {
    console.log(key, obj[key])
})

// Reflect.ownKeys()用于返回对象所有key组成的数组。
Reflect.ownKeys(obj).forEach(key => {
    console.log(key, obj[key])
})
```
