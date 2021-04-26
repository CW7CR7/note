## 邮箱：

```js
export const isEmail = (s) => {
    return /^([a-zA-Z0-9_-])+@([a-zA-Z0-9_-])+((.[a-zA-Z0-9_-]{2,3}){1,2})$/.test(s)
}
```

## 手机号码：

```js
export const isMobile = (s) => {
    return /^1[0-9]{10}$/.test(s)
}
```

## 电话号码

```js
export const isPhone = (s) => {
    return /^([0-9]{3,4}-)?[0-9]{7,8}$/.test(s)
}
```

## 是否是url

```js
export const isURL = (s) => {
    return /^http[s]?:\/\/.*/.test(s)
}
```

## 是否是字符串：

```js
export const isString = (o) => {
    return Object.prototype.toString.call(o).slice(8, -1) === 'String'
}
```

## 是否是数字

```js
export const isNumber = (o) => {
    return Object.prototype.toString.call(o).slice(8, -1) === 'Number'
}
```

## 是否boolean

```js
export const isBoolean = (o) => {
    return Object.prototype.toString.call(o).slice(8, -1) === 'Boolean'
}
```

## 是否函数

```js
export const isFunction = (o) => {
    return Object.prototype.toString.call(o).slice(8, -1) === 'Function'
}
```

## 是否为null

```js
export const isNull = (o) => {
    return Object.prototype.toString.call(o).slice(8, -1) === 'Null'
}
```

## 是否undefined

```js
export const isUndefined = (o) => {
    return Object.prototype.toString.call(o).slice(8, -1) === 'Undefined'
}
```

## 是否对象

```js
export const isObj = (o) => {
    return Object.prototype.toString.call(o).slice(8, -1) === 'Object'
}
```

## 是否数组

```js
export const isArray = (o) => {
    return Object.prototype.toString.call(o).slice(8, -1) === 'Array'
}
```



```js

```

