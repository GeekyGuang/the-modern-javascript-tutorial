### 2.4 变量

可以将变量想象为盒子，盒子里存放着变量的值，这个值可以是数值，字符串，也可以是对象的地址

常用大写字母表示“硬编码（hard-coded）”的常量。或者，换句话说就是，当值在执行之前或在被写入代码的时候，我们就知道值是什么了。

### 2.5 数据类型

- number 用于任何类型的数字：整数或浮点数，在 ±(253-1) 范围内的整数。

- bigint 类型用于存储任意长度的整数， 在整数后加 n,如 873762671287282863818373n

- string 用于字符串：一个字符串可以包含 0 个或多个字符，所以没有单独的单字符类型。

- boolean 用于 true 和 false。

- null 用于未知的值，typeof null 的结果是 "object"。这是官方承认的 typeof 的行为上的错误，这个问题来自于 JavaScript 语言的早期，并为了兼容性而保留了下来。null 绝对不是一个 object。null 有自己的类型，它是一个特殊值。

- undefined 用于未定义的值

- object 用于更复杂的数据结构。

- symbol 类型用于创建对象的唯一标识符

在 JavaScript 语言中没有一个特别的 “function” 类型。函数隶属于 object 类型。但是 typeof 会对函数区分对待，并返回 "function"。这也是来自于 JavaScript 语言早期的问题。从技术上讲，这种行为是不正确的，但在实际编程中却非常方便。

### 2.6 浏览器交互

alert 显示信息。

prompt 显示信息要求用户输入文本。点击确定返回文本，直接敲回车得到空字符串，点击取消或按下 Esc 键返回 null。

confirm 显示信息等待用户点击确定或取消。点击确定返回 true，点击取消或按下 Esc 键返回 false。

```javascript
"use strict";

let name = prompt("your name?", "name");
let userConfirm = confirm(`Is ${name} your name?`);
if (userConfirm) {
  alert(`hello ${name}`);
}
```

### 2.7 类型转换

Number(undefined) === NaN

Number(null) === 0

5 个 falsy 值：NaN, 0, '', null, undefined

-可以将字符串转换为数值: -'123' === -123

+可以将数值转换为字符串: '1' + 23 === '123'

### 2.8 基础运算

求幂 \*\*

```javascript
alert(4 ** (1 / 2)); // 2（1/2 次方与平方根相同)
alert(8 ** (1 / 3)); // 2（1/3 次方与立方根相同)
```

+可以连接字符串，也可以将非数字转化为数字

```javascript
1 +
  "2" + // "12"
  "1" + // 1
  "2" +
  +"3" + // 5
  true + // 1
  ""; // 0
```

赋值 = 返回一个值

```javascript
let a = 1,
  b = 2;
let c = 1 + (a = b + 1);

a = b = c = 2 + 2; // 链式赋值
```

习题

```javascript
"" + 1 + 0 = "10"; // (1)
"" - 1 + 0 = -1; // (2)
true + false = 1;
6 / "3" = 2;
"2" * "3" = 6;
4 + 5 + "px" = "9px";
"$" + 4 + 5 = "$45";
"4" - 2 = 2;
"4px" - 2 = NaN;
7 / 0 = Infinity;
"  -9  " + 5 = "  -9  5"; // (3)
"  -9  " - 5 = -14; // (4)
null + 1 = 1; // (5)
undefined + 1 = NaN; // (6)
" \t \n" - 2 = -2; // (7)
```

解析

1. 有字符串的加法 "" + 1，首先会将数字 1 转换为一个字符串："" + 1 = "1"，然后我们得到 "1" + 0，再次应用同样的规则得到最终的结果。
2. 减法 -（像大多数数学运算一样）只能用于数字，它会使空字符串 "" 转换为 0。
3. 带字符串的加法会将数字 5 加到字符串之后。
4. 减法始终将字符串转换为数字，因此它会使 " -9 " 转换为数字 -9（忽略了字符串首尾的空格）。
5. null 经过数字转换之后会变为 0。
6. undefined 经过数字转换之后会变为 NaN。
7. 字符串转换为数字时，会忽略字符串的首尾处的空格字符。在这里，整个字符串由空格字符组成，包括 \t、\n 以及它们之间的“常规”空格。因此，类似于空字符串，所以会变为 0。

总结

- +只有在两个元中有一元是字符串，才会把另一个转换为字符串
- +若做一元运算，则会把非数字转换为数字
- -/\*都会试图把元转换为数字，字符串转换为数字时会忽略首尾处的空格

### 2.9 数值比较

- 当对不同类型的值进行比较时，它们会先被转化为数字（不包括严格相等检查）再进行比较。
- 在非严格相等 == 下，null 和 undefined 相等且各自不等于任何其他的值。

### 2.11 逻辑运算

一个或运算 || 的链，将返回第一个真值，如果不存在真值，就返回该链的最后一个值。

&& 与运算返回第一个假值，如果没有假值就返回最后一个值。

与运算 && 的优先级比或运算 || 要高。所以代码 a && b || c && d 跟 && 表达式加了括号完全一样：(a && b) || (c && d)。

两个非运算 !! 有时候用来将某个值转化为布尔类型：

```javascript
alert(!!"non-empty string"); // true
alert(!!null); // false
```

### 2.12 空值合并运算符 ??

null/undefined 为未定义，??返回第一个已定义的值

```javascript
// 当 height 的值为 null 或 undefined 时，将 height 的值设置为 100
height = height ?? 100;
```

### 2.16 函数表达式

#### 回调函数

将函数作为参数传递，当符合某个条件时就调用这个函数

```javascript
function ask(question, yes, no) {
  if (confirm(question)) yes();
  else no();
}

ask(
  "Do you agree?",
  function () {
    alert("You agreed.");
  }, // 匿名函数作为回调函数
  function () {
    alert("You canceled the execution.");
  }
);
```

函数可以被视为一个 行为（action）。

我们可以在变量之间传递它们，并在需要时运行。

代码块内的函数声明外部不可见

### 3.1 debugging 调试

开发者工具 source
按 esc 调出 console
watch 添加表达式可以跟踪表达式的值
在代码中添加 debugger

### 3.3 注释

在好的代码中，“解释性”注释的数量应该是最少的，

有一个很棒的原则：“如果代码不够清晰以至于需要一个注释，那么或许它应该被重写。”

函数具有“自我描述”功能

注释这些内容：

- 整体架构，高层次的观点。
- 函数的用法。
- 重要的解决方案，特别是在不是很明显时。

### 4.1 对象

它们存储属性（键值对），其中：

- 属性的键必须是字符串或者 symbol（通常是字符串）。
- 值可以是任何类型。

我们可以用下面的方法访问属性：

- 点符号: obj.property。
- 方括号 obj["property"]，方括号允许从变量中获取键，例如 obj[varWithKey]。

其他操作：

- 删除属性：delete obj.prop。
- 检查是否存在给定键的属性："key" in obj。
- 遍历对象：for(let key in obj) 循环。

如果对象为空，不会进到循环

```javascript
for (let key in obj) {
  return false;
}
```

使用 Object.assign()进行对象的拷贝，可以拷贝所有属性

### 4.3 垃圾回收

当对象或对象族不具备“可达性”时会被清除

### 4.4 this

this 的值是在代码运行时计算出来的

严格模式下，在没有对象的情况下 this == undefined
非严格模式下，this 是全局对象 window

箭头函数没有 this，他的 this 来自外部上下文

this 只有在函数(方法)被调用时才会有值，且其值为函数(方法)所在对象

### 4.5 new

构造函数，或简称构造器，就是常规函数，但大家对于构造器有个共同的约定，就是其命名首字母要大写。
构造函数只能使用 new 来调用。这样的调用意味着在开始时创建了空的 this，并在最后返回填充了值的 this。

如果 return 返回的是一个对象，则返回这个对象，而不是 this。
如果 return 返回的是一个原始类型，则忽略。

### 4.6 可选链

可选链 ?. 语法有三种形式：

- obj?.prop —— 如果 obj 存在则返回 obj.prop，否则返回 undefined。
- obj?.[prop] —— 如果 obj 存在则返回 obj[prop]，否则返回 undefined。
- obj.method?.() —— 如果 obj.method 存在则调用 obj.method()，否则返回 undefined。

### 4.7 symbol

```javascript
let id = Symbol("id"); // 创建symbol，不用new, 括号里是description
let user = {
  name: "John",
  age: 30,
  [id]: 123, // 要用[],否则变成字符串
};

for (let key in user) alert(key); // name, age (no symbols)

// 使用 Symbol 任务直接访问
alert("Direct: " + user[id]);
```

用 Symbol.for(key) 创建全局 symbol，同名相同

```javascript
// 从全局注册表中读取
let id = Symbol.for("id"); // 如果该 Symbol 不存在，则创建它

// 再次读取（可能是在代码中的另一个位置）
let idAgain = Symbol.for("id");

// 相同的 Symbol
alert(id === idAgain); // true
```

### 5.4 数组

数组的 length 是最大索引+1
清空数组最简单的方法就是：arr.length = 0

push 和 unshift 都接受多个参数: arr.push(1, 2, 3, 4)

### 5.5 数组方法

forEach 和 map 都不会改变数组本身

### 5.6 可迭代对象

可以应用 for..of 的对象被称为 可迭代的。

Array.from(obj[, mapFn, thisArg]) 将可迭代对象或类数组对象 obj 转化为真正的数组 Array，然后我们就可以对它应用数组的方法。可选参数 mapFn 和 thisArg 允许我们将函数应用到每个元素。
