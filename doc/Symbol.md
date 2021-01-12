# Symbol

> Symbol 值通过 Symbol 函数生成。这就是说，对象的属性名现在可以有两种类型，一种是原来就有的字符串，另一种就是新增的 Symbol 类型。凡是属性名属于 Symbol 类型，就都是独一无二的，可以保证不会与其他属性名产生冲突。

## 声明方式

```js
let s = Symbol();

typeof s;
// "symbol"
```

- 两个 Symbol()就一定是不相等的

```js
let s1 = Symbol();
let s2 = Symbol();
console.log(s1);
console.log(s2);
console.log(s1 === s2); // false
```

> Symbol 函数前不能使用 new 命令，否则会报错。这是因为生成的 Symbol 是一个原始类型的值，不是对象。也就是说，由于 Symbol 值不是对象，所以不能添加属性。基本上，它是一种类似于字符串的数据类型。  
> Symbol 函数可以接受一个字符串作为参数，表示对 Symbol 实例的描述，主要是为了在控制台显示，或者转为字符串时，比较容易区分

```js
let s1 = Symbol("foo");
let s2 = Symbol("foo");
console.log(s1);
console.log(s2);
console.log(s1 === s2); // false
```

## Symbol.for()

> Symbol.for() 接受一个字符串作为参数，然后搜索有没有以该参数作为名称的 Symbol 值。如果有，就返回这个 Symbol 值，否则就新建一个以该字符串为名称的 Symbol 值，并将其注册到全局。

```js
let s1 = Symbol.for("foo");
let s2 = Symbol.for("foo");
console.log(s1 === s2); // true
```

## Symbol.keyFor()

> Symbol.keyFor()方法返回一个已登记的 Symbol 类型值的 key。

```js
const s1 = Symbol("foo");
console.log(Symbol.keyFor(s1)); // undefined

const s2 = Symbol.for("foo");
console.log(Symbol.keyFor(s2)); // foo
```

## 作为属性名

> 使用对象来描述信息的时候，key 值重复会覆盖；使用 Symbol，相同的 key 就不会被覆盖

```js
const stu1 = Symbol("李四");
const stu2 = Symbol("李四");
const grade = {
  [stu1]: {
    address: "yyy",
    tel: "222",
  },
  [stu2]: {
    address: "zzz",
    tel: "333",
  },
};
console.log(grade);
console.log(grade[stu1]);
console.log(grade[stu2]);
```

## 属性遍历

```js
const sym = Symbol("mooc");
class User {
  constructor(name) {
    this.name = name;
    this[sym] = "mooc.com";
  }
  getName() {
    return this.name + this[sym];
  }
}
const user = new User("dd");
console.log(user.getName());

for (let key in user) {
  console.log(key);
}

for (let key of Object.keys(user)) {
  console.log(key);
}

// 给定对象自身的所有 Symbol 属性的数组
for (let key of Object.getOwnPropertySymbols(user)) {
  console.log(key);
}
// 目标对象自身的属性键组成的数组
for (let key of Reflect.ownKeys(user)) {
  console.log(key);
}
```

## 消除魔术字符串

```js
const shapeType = {
  triangle: "Triangle",
  circle: "Circle",
};
// Symbol
const shapeType = {
  triangle: Symbol(),
  circle: Symbol(),
};

function getArea(shape) {
  let area = 0;
  switch (shape) {
    case shapeType.triangle:
      area = 1;
      break;
    case shapeType.circle:
      area = 2;
      break;
  }
  return area;
}
console.log(getArea(shapeType.triangle));
```
