#JavaScript学习笔记

在HTML中引用 .js 文件：
`<script src="/static/js/abc.js"></script>`

JavaScript不区分整数和浮点数，统一用Number表示
逻辑运算符：和c++一样（ && || ! ）
JavaScript的设计缺陷：**必须**用`===`判断是否相等。`===`两边类型不同才能判断。
表达式`NaN === NaN`返回的是`false`
如果要判断一个数是不是`NaN`：函数`isNaN(x);`接受一个Number类型的数x。如果x是NaN，返回true、反之返回false
比较两个浮点数是否相等，只能计算它们之差的绝对值，看是否小于某个阈值

JavaScript的数组可以包括任意数据类型
创建数组的方法

- `var arr[a, b, ..., z];`
- `var arr = new Array(a, b, ..., z);` *不直观*

JavaScript的对象是一组由键-值组成的无序集合，例如：

```JavaScript
var person = {
    name: 'Bob',
    age: 20,
    tags: ['js', 'web', 'mobile'],
    city: 'Beijing',
    hasCar: true,
    zipcode: null
};
```

在strict模式下运行的JavaScript代码，强制通过var申明变量，未使用var申明变量就使用的，将导致运行错误。
开启strict模式：在第一行加上`'use strict';`

字符串相关

- 转移字符：`\n, \t, \\`
- ASCII字符：`'\x##'`, ##为一个十六进制的数。eg:`'\x41' === 'A'`
- Unicode字符：`'\u####'`。eg:`'\u4e2d' == '中'`
- 多行字符串：用反引号（ESC下面的键扩起来的可以随便拍回车）
- 模板字符串：两行代码等价：
```JavaScript
var message = '你好, ' + name + ', 你今年' + age + '岁了!';
var message = `你好, ${name}, 你今年${age}岁了!`;
```

对字符串操作（都不会对原串进行修改，而是返回一个新的字符串）

- 获取长度：s.length
- 获取某一位：s[pos]
- **不能**通过索引改变某个字符
- 全大写：s.toUpperCase()
- 全小写：s.toLowerCase()
- 搜索索引在原串中出现的位置：s.indexOf(Index_str)，不存在返回-1
- 获取字串，函数原型：substring(int l, int r = s.length - 1)

数组相关

- 获取长度：arr.length
- **可以**通过索引改变某个字符，如果索引>arr.length，则会扩充arr的大小
- 可以对arr.length赋值以改变arr
- 查找某个元素的位置：indexOf()，不存在返回-1
- 获取子数组，函数原型：slice(int l = 0, int r = arr.length - 1)
- pop()：删除数组最后一个元素
- push()：在数组最后添加元素
- unshift()：删除数组最开始的一个元素
- shift()：在数组最开始添加元素
- arr.sort()：排序（会改变原数组）
- arr.reserve()：反转（会改变原数组）
- arr.splice(int index, int numOfDelete, numOfAdd个元素)：从index开始，删除numOfDelete个元素，再加上numOfAdd个元素。返回删除的元素们
- A.concat(B)：返回A+B
- join(char s)：用s连接数组

对象
用`{...}`表示对象，每个键值对用`key: value`表示。用`obj_name.key`读取键对应的值。
JavaScript中所有的属性都是字符串，val可以是任意类型
访问不存在的属性会返回`undefined`
可以在对象外自由的添加删除属性

- 添加属性：A.age = 20;
- 删除属性：delete A.age;
- 判断是否有某一属性：`'age' in A;`。有返回true，没有返回false。继承而来的属性也会加入in的判断
- 判断是否独有某一属性：`A.hasOwnProperty('age')`

if, else, for：和c++差不多
for...in...语句：和python差不多
例：读取一个对象的所有key:
```JavaScript
for (var key in obj) {
    console.log(key);
}
```
过滤出非继承的key:
```JavaScript
for (var key in obj) {
    if (obj.hasOwnProperty(key))
        console.log(key);
}
```

数组也是对象，key代表index，val代表arr[index]

Map

- 初始化一个Map要用一个二维数组，或者直接用函数初始化
- 建立map: var Map = new map();
- 添加键值对：Map.set(key, val);
- 查询是否存在键：Map.has(key);
- 获取val：Map.get(key);
- 删除键值对：Map.delete(key);
- 一个key被多次添加：后面的冲掉前面的

Set

- 自带去重
- 只有key, 没有val
- 建立set: `var Set = new set();`或者`var Set = new set([1, 2, 3, 3, 3, '3']);`
- 添加元素：Set.add(key);
- 删除元素：Set.delete(key);

iterable
用于遍历array, map和set
遍历方法：

- `for (var x of m)`
- foreach方法
```JavaScript
//对于Array
a.forEach(function (element, index, array) {
    // element: 指向当前元素的值
    // index: 指向当前索引
    // array: 指向Array对象本身
    console.log(element + ', index = ' + index);
});

//对于Set
var s = new Set(['A', 'B', 'C']);
s.forEach(function (element, sameElement, set) {
    console.log(element);
});

//对于Map
var m = new Map([[1, 'x'], [2, 'y'], [3, 'z']]);
m.forEach(function (value, key, map) {
    console.log(value);
});
```

定义函数

- function abs(x) {...}
- var abs = function (x) {...} ;

两者完全等价。
传入参数 可以> 需要的参数
传入的参数被放在arguments中。可以通过arguments.length判断传入参数的个数。

例：函数原型是f(a[, b], c)。就可以这样使b变成可选参数
```JavaScript
function foo(a, b, c) {
    if (arguments.length === 2) {
        c = b;
        b = null;
    }
}
```

变量的作用域和c++一样
变量提升：只提升定义，不提升赋值
全局对象：window。全局变量都是window的一个属性
namespace：多个js文件使用经常会出现全局变量名相同。解决方案：将所有变量/函数封装到一个变量中。
在函数的语句块中定义**面向整个语句块 而不是 整个函数**的局部变量：`let`
eg:
```JavaScript
function f() {
    var sum = 0;
    for (let i = 0; i < 100; i++) {
        sum += i;
    }
    i += 1;//会出错
}
```

定义常量：`const`关键字。通常变量名全大写

解构赋值：

- 一般的
`var [x, y, z] = ['hello', 'JavaScript', 'ES6'];`
x = 'hello', y = 'JavaScript', z = 'ES6'。
- 嵌套关系
`[x, [y, z]] = ['hello', ['JavaScript', 'ES6']];`
- 忽略元素
`[, , z] = ['hello', 'JavaScript', 'ES6'];`

解构的嵌套关系
变量名和属性名不一致时的做法：`属性名: 变量名`
解构时使用默认值：`变量名 = 默认名`

使用场景：

- 利用解构交换变量的值
- 快速获取对象的信息
- 函数的参数是对象时，可以使用解构将对象的属性绑定变量中

---
###JavaScript中this的指向问题
如果函数中调用了this, this的指向视情况而定

- 用对象的形式调用函数，this指向这个对象
- 单独的调用函数，this指向window

也不能先获取对象调用的函数，再调用函数。这样this还是没有指向对象。

解决方案：

- 使用that变量捕获this，在函数中对that进行操作
- apply函数：接受两个参数。第一个参数代表this指向的对象，第二个参数是Array类型，代表函数的参数表。
- call函数：和apply差不多。使用的时候不传Array，而是一个一个传。
这两个等价
```JavaScript
Math.max.apply(null, [3, 5, 4]);
Math.max.call(null, 3, 5, 4);
```

对于普通函数，apply和call函数第一个参数都是null。

---

##高阶函数：参数接受了函数的函数

###map函数
map函数在Array的方法中，是对数组中的每一个数进行函数对应的操作
例:
```JavaScript
function f(x) {
    return x * x;
}
var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
var result = arr.map(f);
//result = [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```
map函数接受一个参数，是函数对象本身。返回一个数组，其中每一个值都是原数组的值对于函数的返回值。
reduce函数: `[x1, x2, x3, x4].reduce(f) = f(f(f(x1, x2), x3), x4)`

字符串转数字：s * 1。利用js内部会自动转化格式这一特点
大小写不规律的名字转化成首字母大写的名字：分隔首字母和其他字母，首字母大写其他字母小写。

filter：基于Array，接受一个bool类型的函数。如果函数返回true，则相当于map。反之，丢弃这个数。
例子：
数组元素去重：
```js
r = arr.filter(function (element, index, self) {
    return self.indexOf(element) === index;
});
```
删除偶数：
```js
var r = arr.filter(function (x) {
    return x % 2 !== 0;
});
```

sort：基于Array，默认对字符串的ASCII码排序
对数字的排序（升序）：
```js
arr.sort(function (x, y) {
    if (x < y)
        return -1;
    if (x > y)
        return 1;
    return 0;
});
```
sort会对原Array进行修改。返回值是原Array。

---
##闭包
没看懂

##箭头函数（=>）
两个东西等价
```js
x => x * x;

function (x) {
    return x * x;
}
```
没有参数：() => 3.14
两个参数：(x, y) => x * x + y * y;
多个参数：
```js
(x, y, ...rest) => {
    var i, sum = x + y;
    for (i = 0; i < rest.length; i++)
        sum += rest[i];
    return sum;
}
```

返回一个对象：`x => ({foo: x});`一定要加括号
在箭头函数中，this的作用域被绑定，就不再需要that捕获this了。使用call/apply()函数第一个参数可以直接忽略。

##generator(生成器)
例子
```js
function* fib(max) {
    var
        t,
        a = 0,
        b = 1,
        n = 0;
    while (n < max) {
        yield a;
        [a, b] = [b, a + b];
        n ++;
    }
    return;
}
```
返回值的读取：
```js
var f = fib(5);
f.next(); // {value: 0, done: false}
f.next(); // {value: 1, done: false}
f.next(); // {value: 1, done: false}
f.next(); // {value: 2, done: false}
f.next(); // {value: 3, done: false}
f.next(); // {value: undefined, done: true}
---------------------------------------------------
for (var x of fib(10)) {
    console.log(x); // 依次输出0, 1, 1, 2, 3, ...
}
```

##标准化对象
###Date

```js
var now = new Date();
now; // Wed Jun 24 2015 19:49:22 GMT+0800 (CST)
now.getFullYear(); // 2015, 年份
now.getMonth(); // 5, 月份，注意月份范围是0~11，5表示六月
now.getDate(); // 24, 表示24号
now.getDay(); // 3, 表示星期三
now.getHours(); // 19, 24小时制
now.getMinutes(); // 49, 分钟
now.getSeconds(); // 22, 秒
now.getMilliseconds(); // 875, 毫秒数
now.getTime(); // 1435146562875, 以number形式表示的时间戳
```

###RegExp
利用正则表达式匹配字符串，分割字符串，分组，全局搜索。
不想看了。另择吉日

JS中创建正则表达式的方法：

- 用//括起来一个正则表达式。
- `var re = new RegExp('正则表达式')`。这种方法要注意字符串的转义问题。

正则表达式匹配：
re.test(str)。返回true就是匹配

切割字符串：字符串自带的split方法可以接受一个RegExp，用来切割字符串

eg：切割任意数量的空格/,/;
`'a,b;; c  d'.split(/[\s\,\;]+/); // ['a', 'b', 'c', 'd']`

分组是正则表达式的内容
提取分组：exec()方法。
eg:提取原串和他的分组们
```js
var re = /^(\d{3})-(\d{3,8})$/;
re.exec('010-12345'); // ['010-12345', '010', '12345']
re.exec('010 12345'); // null
```

全局搜索：定义正则表达式的时候加上'g'参数 或者 用'//'定义的时候改为'//g'
其他参数：i忽略大小写，m多行匹配

###JSON
对象名：JSON
stringify方法可以格式化对象的显示，接受多个参数。第一个参数是被格式化的对象，第二个参数分多种情况

- null：不过滤对象，按顺序输出
- 存key值的Array：只输出Array里面对应的键值对
- 函数：对每个键值对都进行函数运算后输出

第三个参数接受一个字符串，表示缩进内容。
也可以在原对象中写一个toJSON()方法。这样调用stringify()方法时输出的是toJSON()的返回值。

JSON格式的字符串转化成JS对象：JSON.parse(str);
也接受一个函数，用来转化解析的属性

##面向对象编程
###原型
`实例/派生类.__proto__ = 对象/基类;`
推荐的继承/实例化方式
```js
function createStudent(name) {// 基于Student原型创建一个新对象:
    var s = Object.create(Student);// 初始化新对象:
    s.name = name;
    return s;
}
var xiaoming = createStudent('小明');
```

原型链
Array：arr ----> Array.prototype ----> Object.prototype ----> null
Function：foo ----> Function.prototype ----> Object.prototype ----> null
原型链不宜过长

构造函数：用new调用函数，会返回一个对象this
constructor属性：指向基类
eg: 
```js
Student.prototype.constructor === Student // true
xiaoming instanceof Student; // true
```
