# Array

## ES5 中数组遍历方式

### for循环

```javascript
// 支持 break、continue
for (let i = 0; i < arr.length; i++) {
    console.log(arr[i])
}
```

### forEach()

> forEach 的代码块中不能使用 break、continue，它会抛出异常。

```javascript

arr.forEach(function(elem, index, array) {
    if (arr[i] == 2) {
        continue
    }
    console.log(elem, index)
})

```

### map() 返回新的数组，每个元素为调用func的结果

```javascript
let result = arr.map(function(value) {
    value += 1
    console.log(value)
    return value
})
console.log(arr, result)
```

### filter() 返回符合func条件的元素数组

```javascript
let result = arr.filter(function(value) {
    console.log(value)
    return value == 2
})
console.log(arr, result)
```

### some() 返回boolean，判断是否有元素符合func条件

```javascript
let result = arr.some(function(value) {
    console.log(value)
    return value == 4
})
console.log(arr, result)
```

### every() 返回boolean，判断每个元素都符合func条件

>使用 every 遍历就可以做到 break 那样的效果，简单的说 return false 等同于 break，return true 等同于 continue。如果不写，默认是 return false  
> every 的代码块中不能使用 break、continue，它会抛出异常。

```javascript
let result = arr.every(function(value) {
    console.log(value)
    return value == 2
})
console.log(arr, result)
```

### reduce() 接收一个函数作为累加器

```javascript
let sum = arr.reduce(function(prev, cur, index, array) {
    return prev + cur
}, 0)
console.log(sum)

// 比较大小
let max = arr.reduce(function(prev, cur) {
    return Math.max(prev, cur)
})
console.log(max)

// 数组去重
let res = arr.reduce(function(prev, cur) {
    prev.indexOf(cur) == -1 && prev.push(cur)
    return prev
}, [])
console.log(res)
```

### for...in

> 如果 array 有自定义属性，你发现也会被遍历出来(显然不合理)。这是因为 for...in 是为遍历对象创造的（{a:1, b:2}），不是为数组设计的。  
> for...in不能用于遍历数组。for...in代码块中不能有 return，不然会抛出异常。

## ES6 中数组遍历方式

### for...of

```javascript
for (let item of arr) {
    console.log(item)
}

for (let item of arr.values()) {
    console.log(item)
}

for (let item of arr.keys()) {
    console.log(item)
}

for (let [index, item] of arr.entries()) {
    console.log(index, item)
}
```

> for...of是支持 break、continue、return的，所以在功能上非常贴近原生的 for。

### Array.from()

```javascript
let args = [].slice.call(arguments);
let imgs = [].slice.call(document.querySelectorAll('img'));
// 
let args = Array.from(arguments);
let imgs = Array.from(document.querySelectorAll('img'));

```

> 伪数组具备两个特征，1. 按索引方式储存数据 2. 具有length属性；

```javascript
let arrLike = {
    0: 'a',
    1: 'b',
    2: 'c',
    length: 3
}
```

```javascript
let arr = Array(6).join(' ').split('').map(item => 1)
// [1,1,1,1,1]

// 初始化数组
Array.from({
    length: 5
}, function() {
    return 1
})
```

### Array.of()

```javascript
// Array.of() 和 Array 构造函数之间的区别在于处理整数参数
Array.of(7); // [7]
Array.of(1, 2, 3); // [1, 2, 3]

Array(7); // [ , , , , , , ]
Array(1, 2, 3); // [1, 2, 3]
```

### Array.prototype.fill()

> fill() 方法用一个固定值填充一个数组中从起始索引到终止索引内的全部元素。不包括终止索引

```javascript
let array = [1, 2, 3, 4]
array.fill(0, 1, 2)
// [1,0,3,4]

// 技巧
Array(5).fill(1)
// [1,1,1,1,1]
```

### Array.prototype.find()

> find() 方法返回数组中满足提供的测试函数的第一个元素的值，否则返回 undefined。

```javascript
let array = [5, 12, 8, 130, 44];
let found = array.find(function(element) {
    return element > 10;
});
console.log(found);
// 12
```

### Array.prototype.findIndex()

> findIndex()方法返回数组中满足提供的测试函数的第一个元素的索引。否则返回-1

```javascript
let array = [5, 12, 8, 130, 44];
let found = array.find(function(element) {
    return element > 10;
});
console.log(found);
// 1
```

### Array.prototype.copyWithin()

> 在当前数组内部，将指定位置的成员复制到其他位置（会覆盖原有成员），然后返回当前数组。

```javascript
let arr = [1, 2, 3, 4, 5]
console.log(arr.copyWithin(1, 3))
// [1, 4, 5, 4, 5]
```
