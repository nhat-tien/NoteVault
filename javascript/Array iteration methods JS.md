---
tags:
  - javascript
date: "2023-08-24"
---

## forEach()
- The `forEach()` method calls a function once for each array element.
- ==Không thay đổi array==
- Chỉ đơn giản là lặp qua các giá trị
- ==không trả về cái gì cả==

```js
const numbers = [45, 4, 9, 16, 25];  
let txt = "";  
numbers.forEach(myFunction);  
  
function myFunction(value, index, array) {  
  txt += value + "<br>";  
}
```

## map()

- `map()` method sẽ ==tạo ra một array mới== bằng cách thực thi function được gọi trên mỗi array element.
- `map()` method sẽ ==không thực thi function cho array element nào không có giá trị.==
- `map()` method ==không thay đổi array==
```js
const numbers1 = [45, 4, 9, 16, 25];  
const numbers2 = numbers1.map(myFunction);  
  
function myFunction(value, index, array) {  
  return value * 2;  
}
```

## filter() 
- `filter()` method sẽ ==tạo ra một array mới== với những array element nào vượt qua được bộ lọc.
```js
// ví dụ tạo array mới với những giá trị nào lớn hơn 18
const numbers = [45, 4, 9, 16, 25];  
const over18 = numbers.filter(myFunction);  
  
function myFunction(value, index, array) {  
  return value > 18;  
}
```

## reduce()
