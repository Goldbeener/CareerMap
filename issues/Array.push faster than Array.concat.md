# Array.push比Array.concat快1000倍左右

> 原文 [Javascript Array.push is 945x faster than Array.concat](https://dev.to/uilicious/javascript-array-push-is-945x-faster-than-array-concat-1oki)

## 表现
```javascript
  let arr1 = [...]
  let arr2 = [...]


  // action1
  let final_arr = arr1.concat(arr2)

  // action2  速度是上述做法的将近1000倍
  let _final_arr = Array.prototype.push.apply(arr1, arr2) 
  let _final_arr = arr1.push(...arr2)
```

## 为什么？
`Array.concat` 创建了一个新的数组，然后把要合并的几个数组元素全部收集其中，然后返回新的数组；
`Array.push` 是将其他的数组元素收集于第一个数组之中，

相比来说，`Array.concat`做了额外的工作，将第一个数组中的元素拷贝到新数组中，这是导致它速度缓慢的原因


## `Array.push`注意点
+ 使用for循环将元素依次push比使用`apply`将数组整体push慢
+ 预先分配目标数组的length，可以额外提速2-3倍

```js
  let arr1 = [...]
  let arr2 = [...]

  arr1.length = arr1.length + arr2.length  // 提速2-3倍

  arr1.push(...arr2)

```

## `Array.concat`做了什么？
``Array.concat`其实还是做了一些额外的工作, 
+ 支持重载 (传入不同类型的参数)
+ 参数可以是单独的数字 `[1, 2].concat(2, 3, 4)`
+ 参数可以是 数字+ 数组 混合 `[1, 2].concat(2, 3, [4, 5])`







