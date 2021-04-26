## 如果有多个条件

```js
//Longhand
if (x === 'abc' || x === 'def' || x === 'ghi' || x ==='jkl') {
  //logic
}

//Shorthand
if (['abc', 'def', 'ghi', 'jkl'].includes(x)) {
  //logic
}
```

## 重点：很实用的一个技巧：Null, Undefined，空检查

```js
// Longhand
if (test1 !== null || test1 !== undefined || test1 !== '') {
    let test2 = test1;
}

// Shorthand
let test2 = test1 || '';
```

## 将值分配给多个变量

当我们处理多个变量并希望将不同的值分配给不同的变量时，此简写技术非常有用。

```js
//Longhand 
let test1, test2, test3;
test1 = 1;
test2 = 2;
test3 = 3;

//Shorthand 
let [test1, test2, test3] = [1, 2, 3];
```

## 多个条件的AND（&&）运算符

如果仅在变量为 `true` 的情况下才调用函数，则可以使用 `&&` 运算符。

```js
//Longhand 
if (test1) {
 callMethod(); 
} 

//Shorthand 
test1 && callMethod();
```

## foreach循环简写(常用)

这是迭代的常用简写技术之一。

```js
// Longhand
for (var i = 0; i < testData.length; i++)

// Shorthand
for (let i in testData) or  for (let i of testData)
```

## 箭头函数变成有名字的函数

```js
function callMe(name) {
  console.log('Hello', name);
}
callMe = name => console.log('Hello', name);
```

## 三元运算符之函数的调用

```js
// Longhand
function test1() {
  console.log('test1');
};
function test2() {
  console.log('test2');
};
var test3 = 1;
if (test3 == 1) {
  test1();
} else {
  test2();
}

// Shorthand
#重点：
(test3 === 1? test1:test2)();
```

## switch简写

switch基础语法：

```js
switch(x) {
  case 'value1':  // if (x === 'value1')
    ...
    [break]

  case 'value2':  // if (x === 'value2')
    ...
    [break]

  default:
    ...
    [break]
}

```



```js
// Longhand
switch (data) {
  case 1:
        //test1()是一个函数
    test1();
  break;

  case 2:
    test2();
  break;

  case 3:
    test();
  break;
  // And so on...
}

// Shorthand
var data = {
  1: test1,
  2: test2,
  3: test
};

data[something] && data[something]();
```

## return函数的简写方法

```js
//longhand
function calculate(diameter) {
  return Math.PI * diameter
}

//shorthand
calculate = diameter => (
  Math.PI * diameter;
)
```

## 小数基数指数

```js
// Longhand
for (var i = 0; i < 10000; i++) { ... }

// Shorthand
for (var i = 0; i < 1e4; i++) {
```

## 默认参数值

```js
//Longhand
function add(test1, test2) {
  if (test1 === undefined)
    test1 = 1;
  if (test2 === undefined)
    test2 = 2;
  return test1 + test2;
}

//shorthand
add = (test1 = 1, test2 = 2) => (test1 + test2);
add() //output: 3
```

## concat的简写

```js
//longhand

// joining arrays using concat
const data = [1, 2, 3];
const test = [4 ,5 , 6].concat(data);

//shorthand

// joining arrays
const data = [1, 2, 3];
const test = [4 ,5 , 6, ...data];
console.log(test); // [ 4, 5, 6, 1, 2, 3]
```

克隆也可以这样用

```js
//longhand

// cloning arrays
const test1 = [1, 2, 3];
const test2 = test1.slice()

//shorthand

// cloning arrays
const test1 = [1, 2, 3];
const test2 = [...test1];
```

## 字符串转数字

```html
//Longhand 
let test1 = parseInt('123'); 
let test2 = parseFloat('12.3'); 

//Shorthand 
let test1 = +'123'; 
let test2 = +'12.3';
```

## ~运算符

```js
//longhand
if(arr.indexOf(item) > -1) { // item found 
}
if(arr.indexOf(item) === -1) { // item not found
}

//shorthand
if(~arr.indexOf(item)) { // item found
}
if(!~arr.indexOf(item)) { // item not found
}
```

按位（`〜`）运算符将返回除-1以外的任何值的真实值。否定它就像做 `~~` 一样简单。另外，我们也可以使用 `include()` 函数：

```js
if (arr.includes(item)) { 
    // true if the item found
}
```

## 重复字符串多次

```js
//longhand 
let test = ''; 
for(let i = 0; i < 5; i ++) { 
  test += 'test '; 
} 
console.log(str); // test test test test test 

//shorthand 
'test '.repeat(5);
```

## 数组中最大值 最小值

```js
const arr = [1, 2, 3]; 
Math.max(…arr); // 3
Math.min(…arr); // 1
```

