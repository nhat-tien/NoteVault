---
date: 2023-08-24
tags:
  - javascript
---

## AND `&&`

- link: [tài liệu của MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_AND)
- Nó sẽ kiểm tra các toán hạng từ trái sang phải
- Toán tử này sẽ trả về giá trị *falsy* đầu tiên, hoặc giá trị cuối cùng nếu tất cả đều *truthy* .
- Xem thêm [[Truthy&Falsy]]

```js
result = '' && 'foo';  // result is assigned "" (empty string)
result = 2 && 0;       // result is assigned 0
result = 'foo' && 4;   // result is assigned 4

```

## OR `||`

- link [Tài liệu của MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_OR)
- Nó sẽ kiểm tra các toán hạng từ trái sang phải
- Chỉ trả về giá trị **Truthy** đầu tiên gặp được, hoặc giá trị cuối cùng nếu tất cả đều Falsy.
- Ngược với AND operator.
- Đọc thêm [[Truthy&Falsy]]

```js
o1 = true  || true       // t || t returns true
o2 = false || true       // f || t returns true
o3 = true  || false      // t || f returns true
o4 = false || (3 === 4)  // f || f returns false
o5 = 'Cat' || 'Dog'      // t || t returns "Cat"
o6 = false || 'Cat'      // f || t returns "Cat"
o7 = 'Cat' || false      // t || f returns "Cat"
o8 = ''    || false      // f || f returns false
o9 = false || ''         // f || f returns ""
o10 = false || varObject // f || object returns varObject

```


## Nullish Coalescing Operator `??`

- Sẽ trả về toán hạng bên phải nếu toán hạng bên trái là `null` hoặc `undefined`, nếu không sẽ trả về toán hạng bên trái.

```js
const foo = null ?? 'default string';
console.log(foo);
// expected output: "default string"

const baz = 0 ?? 42;
console.log(baz);
// expected output: 0

```
