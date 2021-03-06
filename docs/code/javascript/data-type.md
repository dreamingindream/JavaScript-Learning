# Data Type

ES 6 之前已有的数据类型：String、Number、Boolean、undefined、null、object

Array、function、Date 等都属于 Object

ES 6 新增的数据类型：Symbol

除了 Object 是复杂数据类型以外，其他的数据类型都是基本数据类型，Symbol 是一个基本数据类型

ES 6 对于 Object 类型下新增的类型：Set/WeakSet、Map/WeakMap、TypedArray

## Symbol

```javascript
// 每个从 Symbol() 返回的 Symbol 值都是唯一的
let a = window.Symbol(); 
let b = window.Symbol();

a === b; // false
a == b; // false

// Symbol 可以作为一个对象的属性名
let obj = new Object();
obj[a] = 'aaaaa';

// Symbol 可以传参数，参数只用于调试，没有代码执行意义
Symbol('test') === Symbol('test'); // false
```

Symbol 的用途：实现对象的私有属性，ES 6 之前做不到隐藏，一般以 `_` 去开头来装作是私有属性

```javascript
// window 全局下可以访问到 obj，可以访问到 obj.name，但是访问不到 key 是 Symbol 的那个属性
{
    let symbol = Symbol();
    let obj = {
        name: 'Jack',
        [a]: '隐藏属性'
    }
    obj[a] = '修改后的隐藏属性'; // 在代码块里面，可以访问到这个属性
    window.testObj = obj;
}
```

## Set

是对象的一种，很像数组，但是不是数组：储存任何类型的唯一值，无论是原始值还是对象引用，用来做数组去重

```javascript
let set1 = new Set([1, 2, 3, 4, 5, 5, 5, 5, 5, ]);
console.log(set1);

let set2 = new Set([1, 2, 3, 3, 3, 'aaa', 'aaa', undefined, undefined, null, null]);
console.log(set2);

let a = {};
let set3 = new Set([a, a, a]);
console.log(set3);

// 注意是仅储存唯一的“对象引用”，而不是唯一的对象
let set4 = new Set([{}, {}]);
console.log(set4);
Boolean({} === {}); // false，内存中存的地址（也就是对象引用）并不一样
```

面试题：实现数组去重：

ES 6 之前的简单写法，有缺点：只支持字符串，算法使用条件很有限

```javascript
var arr1 = [1, 2, 3, 3, 2, 1, 4, 4, 5, '5', {'name': 'Jack'}];
function uniqArr (arr) {
   var hash = {},
       result = []
   for (var i = 0; i < arr.length; i++) {
       hash[arr[i]] = true;
   }
   for (var key in hash) {
       result.push(key);
   }
   return result;
}

uniqArr(arr1); // 结果乱七八糟
```

Set 的写法：

```javascript
let arr2 = [1, 2, 3, 3, 2, 1, 4, 4, 5, '5', {'name': 'Jack'}];
let uniqArr2 = (arr) => {
    return Array.from(new Set(arr));
    // return [...new Set(arr)];
}

uniqArr2(arr1); // 结果完美
```

Set 的 API：.add(), .delete(), .has(), .size

## Map

普通对象的 key 只能是字符串，Map 的 key 可以是任何值

```javascript
let map1 = new Map();
map1.set('key1', 'value1');
map1.set({}, 'value2');
```

## WeakSet & WeakMap

1. 对象会占内存
2. 内存很贵
3. 要做垃圾回收
4. “弱引用”不在垃圾回收的算法中干扰是否回收内存

WeakSet 与 Set 基本相同，但是如果在 WeakSet 中引用一个对象，是弱引用，不干扰垃圾回收；比 Set 少了一个 API

WeakMap 基本同上

## TypedArray

todo
