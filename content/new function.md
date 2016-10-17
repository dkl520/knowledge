# new function(){}

```javascript
var x = new function() {
  return "xxxx";
};

console.log(x);            // Object {}
console.log(x.toString()); // [object Object]
```

上面这段代码等价于：

```javascript
function anonymous() {
  return "xxxx";
}

var x = new anonymous();

console.log(x);            // Object {}
console.log(x.toString()); // [object Object]
```

我们对第一段代码进行改造：

```javascript
var x = new function() {
  return new String("xxxx");
};

console.log(x);            // String {0: "x", 1: "x", 2: "x", 3: "x", length: 4, [[PrimitiveValue]]: "xxxx"}
console.log(x.toString()); // xxxx
```

**只要 `new` 表达式之后的 `constructor` 返回（`return`）一个引用对象（数组、对象、函数等），都将覆盖 `new` 创建的匿名对象，如果返回（`return`）一个原始类型（无 `return` 时其实为 `return` 原始类型 `undefined`），那么就返回 `new` 创建的匿名对象。**

由于 `new String` 会构造一个对象，而不是一个 `string` 直接量，且 `new String("xxxx")` 如果带参数，那么 `console.log(x.toString())` 它的时候就会返回 `"xxxx"`。所以 `x` 将返回 `new String("xxxx")` 这个对象，而 `console.log(x.toString())` 则显示 `"xxxx"`。
