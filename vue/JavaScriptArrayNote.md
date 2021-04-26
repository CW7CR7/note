# JavaScriptNote

## indexOf 数组方法

**用途：** 用于**查找数组中是否存在某个值**，如果存在则返回某个值的下标，否则返回`-1`

用来查找数组中是否有某个值

```js
let list = [1, 2, 3];

console.log(list.indexOf(2)) // 1
console.log(list.indexOf("蛙人")) // -1
```

## map 数组方法

**用途：** `map`是一个数组函数方法，接收三个参数，`value`，`index`，`self`，返回值是处理完的结果。

用来加工数组中的每一项

```js
let list = [1, 2, 3];

const res = list.map((value, key, self) => {
   console.log(value) // 1 2 3
   console.log(key) // 0 1 2
   console.log(self) // [1, 2, 3]
   return value * 2
})
console.log(res)

```

### forEach数组方法

**用途：** 用于遍历一个数组，接收三个参数，`value`，`index`，`self`，返回值为`undefined`

和map作用差不多，主要是返回值不同

```js
let list = [1, 2, 3];

const res = list.forEach((value, key, self) => {
    console.log(value) // 1 2 3
    console.log(key) // 0 1 2
    console.log(self) // [1, 2, 3]
    return 123
})
console.log(res) // undefined

```

### splice数组方法 改变原数组

**用途：** 用于数组删除或替换内容，接收三个参数：

- 第一个参数是，删除或添加的位置
- 第二个参数是，要删除的几位，如果为0则不删除
- 第三个参数是，向数组添加内容

splice(下标，删除的个数，删除位置替换的内容)，改变原数组

```js
let list = [1, 2, 3];

list.splice(0, 1) // 把第0个位置，给删除一位
console.log(list) // [2, 3]

list.splice(0, 1, "蛙人") // 把第0个位置，给删除一位，添加上一个字符串
console.log(list) // ["蛙人", 2, 3]

list.splice(0, 2, "蛙人") // 把第0个位置，给删除2位，添加上一个字符串
console.log(list) // ["蛙人", 3]

```

## slice 不改变原数组

**用途：** 用于截取数组值，接收两个参数，第一个参数是要获取哪个值的下标，第二个参数是截取到哪个下标的前一位。

截取数组。slice(开始下标（包含这一项），结束下标（但是不包含这一项）)

```js
let list = [1, 2, 3];

let res = list.slice(1, 3) // 从第一位下标开始截取，到第三位下标的前一位，所以截取出来就是 [2, 3]
console.log(res) // [2, 3]

```

### filter 不改变原数组

**用途：** 用于过滤数组内的符合条件的值，返回值为满足条件的数组对象

接收一个参数，参数是一个函数，函数里的参数是item。需要return。返回值是满足条件的新数组

```js
let list = [1, 2, 3];

let res = list.filter(item => item > 1);
console.log(res) // [2, 3]

```

## every 也就是全真为真

**用途：** 用于检测数组所有元素是否都符合指定条件，返回值为`Boolean` , 该方法是数组中必须全部值元素满足条件返回`true`，否则`false`

记住一定要return

```js
let list = [1, 2, 3];

let res = list.every(item => item > 0)
console.log(res) // true

let res1 = list.every(item => item > 1)
console.log(res1) // false

```

### some 也就是全假为假

**用途：** 用于检测数组中的元素是否满足指定条件，返回值为`Boolean` , 该方法是只要数组中有一项满足条件就返回`true`，否则`false`

```js
let list = [1, 2, 3];

let res = list.some(item => item > 0)
console.log(res) // true
```

### reduce 不改变原数组

**用途：** 该方法接收一个函数作为累加器，数组中的每个值（从左到右）开始缩减，最终计算为一个值。该方法回调函数接收四个参数

- 第一个参数：*初始值*, 或者计算结束后的返回值
- 第二个参数：当前元素
- 第三个参数：当前元素的索引
- 第四个参数：当前元素所属的数组对象，本身

我们一般只用前两个就行，`reduce`第一个参数回调函数，第二个参数是初始值

array.reduce(function(prev, current, currentIndex, arr), initialValue)

1. prev：函数传进来的初始值或上一次回调的返回值
2. current：数组中当前处理的元素值
3. currentIndex：当前元素索引
4. arr：当前元素所属的数组本身
5. initialValue：传给函数的初始值

```js
let list = [1, 2, 3];

let res = list.reduce(( prev, cur ) => prev += cur, 0)
console.log(res) // 6

```

## reverse颠倒数组 不改变原数组

**用途：** 用于数组反转

```js
let list = [1, 2, 3];

let res = list.reverse();
console.log(res) // [3, 2, 1]
```

### join数组转字符串 不改变原数组

**用途：** 用于数据以什么形式拼接

```js
let list = [1, 2, 3];

let res = list.join("-");
console.log(res) // 1-2-3

let sum = eval(list.join("+"))
console.log(sum) // 6
```

## toString 数组转字符串

**用途：** 用于将数组内容转换为字符串

```js
let list = [1, 2, 3];

let res = list.toString()
console.log(res) // 1,2,3
```



### sort

**用途：** 用于将数组排序，排序规则看返回值

- 返回值为正数,后面的数在前面
- 返回值为负数,前面的数不变,还在前面
- 返回值为0,都不动

```js
var arr = [3, 15, 8, 28, 102, 22];

arr.sort((x, y) => {
    console.log(x + '-' + y + '=' + (x - y));
    return x - y;
});
console.log(arr);//[3, 8, 15, 22, 28, 102]
arr.sort((y, x) => x - y)
console.log(arr);//[102, 28, 22, 15, 8, 3]
```

## concat

**用途：** 用于合并数组

## push

**用途：** 向数组后面添加元素，返回值为新数组的`length`

## pop

**用途：** 用于删除数组尾部的元素，返回值为删除的元素

## unshift

**用途：** 向数组的头部添加元素，返回值为数组的`length`

## shift

**用途：** 用于删除数组的头部，返回值为删除的元素

# ES6方法

## find

**用途：** 查找数组的元素，满足条件的返回单个值，按照就近原则返回

返回第一个满足条件的值

```js
let list = [1, 2, 3];

let res = list.find((item) => item > 1)
console.log(res) // 2, 按照就近原则返回

```

## findIndex

**用途：** 查找数组中元素，满足条件的返回数组下标

和find差不多，只不过他返回的是下标

```js
let list = [1, 2, 3];

let res = list.findIndex((item) => item > 1)
console.log(res) // 1, 按照就近原则返回下标

```

## includes

**用途：** 检测数组中是否存在该元素，返回`Boolean`值

```js
let list = [1, 2, 3];
let res = list.includes("蛙人")
let res1 = list.includes(1)
console.log(res, res1) // false true

```

