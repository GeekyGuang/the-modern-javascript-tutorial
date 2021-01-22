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

数组去重

```javascript
function unique(arr) {
  // return [...new Set(arr)]
  return Array.from(new Set(arr));
}
```

### 5.9 解构赋值

```javascript
let user = "mark tuwen";
let [firstName, secondName] = user.split(" ");

// 循环
for (let [key, value] of Object.entries(user)) {
  alert(`${key}:${value}`); // name:John, then age:30
}

// 交换两个变量的值
let guest = "Jane";
let admin = "Pete";

[guest, admin] = [admin, guest];

// 对象解构,属性名要对应
let {prop : varName = default, ...rest} = object

// 数组解构，位置要对应
let [item1 = default, item2, ...rest] = array
```

### 6.3 闭包

一个“变量”只是 环境记录 这个特殊的内部对象的一个属性。“获取或修改变量”意味着“获取或修改词法环境的一个属性”。

所有的函数在“诞生”时都会记住创建它们的词法环境。

**闭包** 是指内部函数总是可以访问其所在的外部函数中声明的变量和参数，即使在其外部函数被返回（寿命终结）了之后。

函数将从内到外依次在对应的词法环境中寻找目标变量，它使用最新的值。

### 6.4 var

var 只有函数作用域和全局作用域，没有块级作用域

var 允许重复声明

var 变量声明会提升，但赋值不会

IIFE 立即执行函数创建私有变量(现在已不使用)

```javascript
(function () {
  var message = "Hello";

  alert(message); // Hello
})();

// 其他方式创建
(function () {
  alert("Parentheses around the function");
})();

(function () {
  alert("Parentheses around the whole thing");
})();

!(function () {
  alert("Bitwise NOT operator starts the expression");
})();

+(function () {
  alert("Unary plus starts the expression");
})();
```

### 6.6 函数 NFE

命名函数表达式（NFE，Named Function Expression）

方便函数自己调用自己，且该名称不能在外部访问

```javascript
let sayHi = function func(who) {
  if (who) {
    alert(`Hello, ${who}`);
  } else {
    func("Guest"); // 使用 func 再次调用函数自身
  }
};

sayHi(); // Hello, Guest

// 但这不工作：
func(); // Error, func is not defined（在函数外不可见）
```

### 6.7 new Function([arg1,arg2], functionbody)

使用 new Function 创建的函数，它的 [[Environment]] 指向全局词法环境，而不是函数所在的外部词法环境。
因此，我们不能在 new Function 中直接使用外部变量。

### 6.8 调度函数

任何 setTimeout 都只会在当前代码执行完毕之后才会执行。

### 6.10 函数绑定

一个函数不能被重绑定（re-bound）

```javascript
function f() {
  alert(this.name);
}

f = f.bind({ name: "John" }).bind({ name: "Pete" });

f(); // John
```

bind 的结果是另一个对象。

```javascript
function sayHi() {
  alert(this.name);
}
sayHi.test = 5;

let bound = sayHi.bind({
  name: "John",
});

alert(bound.test); // undefined
```

### 7.2 getter setter

访问器属性（accessor properties）。它们本质上是用于获取和设置值的函数，但从外部代码来看就像常规属性。

```javascript
let user = {
  get name() {
    return this._name;
  },

  set name(value) {
    if (value.length < 4) {
      alert("Name is too short, need at least 4 characters");
      return;
    }
    this._name = value;
  },
};

user.name = "Pete";
alert(user.name); // Pete
```

有一个众所周知的约定，即以下划线 "\_" 开头的属性是内部属性，不应该从对象外部进行访问。

### 8.1 原型继承

for..in 循环也会迭代继承的属性。

```javascript
let animal = {
  eats: true,
};

let rabbit = {
  jumps: true,
  __proto__: animal,
};

// Object.keys 只返回自己的 key
alert(Object.keys(rabbit)); // jumps

// for..in 会遍历自己以及继承的键
for (let prop in rabbit) alert(prop); // jumps，然后是 eats
```

几乎所有其他键/值获取方法，例如 Object.keys 和 Object.values 等，都会忽略继承的属性。
它们只会对对象自身进行操作。不考虑 继承自原型的属性。

在现代引擎中，从性能的角度来看，我们是从对象还是从原型链获取属性都是没区别的。它们（引擎）会记住在哪里找到的该属性，并在下一次请求中重用它。

```javascript
// this.stomach= 不会执行对 stomach 的查找。该值会被直接写入 this 对象。
// this.stomach.push(food); 会
let hamster = {
  stomach: [],

  eat(food) {
    this.stomach.push(food);
  },
};

let speedy = {
  __proto__: hamster,
};

let lazy = {
  __proto__: hamster,
};

// 这只仓鼠找到了食物
speedy.eat("apple");
alert(speedy.stomach); // apple

// 这只仓鼠也找到了食物，为什么？请修复它。
alert(lazy.stomach); // apple
```

### 8.2 F.prototype

F.prototype 属性仅在 new F 被调用时使用，它为新对象的 [[Prototype]] 赋值。

```javascript
let animal = {
  eats: true,
};

function Rabbit(name) {
  this.name = name;
}

Rabbit.prototype = animal;

let rabbit = new Rabbit("White Rabbit"); //  rabbit.__proto__ == animal

alert(rabbit.eats); // true
```

每个函数都有 "prototype" 属性，即使我们没有提供它。

默认的 "prototype" 是一个只有属性 constructor 的对象，属性 constructor 指向函数自身。

```javascript
function Rabbit(name) {
  this.name = name;
  alert(name);
}

let rabbit = new Rabbit("White Rabbit");

let rabbit2 = new rabbit.constructor("Black Rabbit");
```

注意，当 prototype 被修改，constructor 可能就不存在了

### 8.4 现代原型方法

设置和直接访问原型的现代方法有：

Object.create(proto, [descriptors]) —— 利用给定的 proto 作为 [[Prototype]]（可以是 null）和可选的属性描述来创建一个空对象。
Object.getPrototypeOf(obj) —— 返回对象 obj 的 [[Prototype]]（与 **proto** 的 getter 相同）。
Object.setPrototypeOf(obj, proto) —— 将对象 obj 的 [[Prototype]] 设置为 proto（与 **proto** 的 setter 相同）。

```javascript
let animal = {
  eats: true,
};

// 创建一个以 animal 为原型的新对象
let rabbit = Object.create(animal);

alert(rabbit.eats); // true

alert(Object.getPrototypeOf(rabbit) === animal); // true

Object.setPrototypeOf(rabbit, {}); // 将 rabbit 的原型修改为 {}
```

### 9.1 class

基本的类语法看起来像这样：

```javascript
class MyClass {
  prop = value; // 属性

  constructor(...) { // 构造器
    // ...
  }

  method(...) {} // method

  get something(...) {} // getter 方法
  set something(...) {} // setter 方法

  [Symbol.iterator]() {} // 有计算名称（computed name）的方法（此处为 symbol）
  // ...

  // =定义的函数和属性都在对象实例上
  sayHi = function() {
    alert('Hi')
  }
}
```

技术上来说，MyClass 是一个函数（我们提供作为 constructor 的那个），而 methods、getters 和 settors 都被写入了 MyClass.prototype。

### 9.2 类继承

使用 extends 继承

```javascript
class Animal {
  constructor(name) {
    this.speed = 0;
    this.name = name;
  }

  run(speed) {
    this.speed = speed;
    alert(`${this.name} runs with speed ${this.speed}`);
  }

  stop() {
    this.speed = 0;
    alert(`${this.name} stands still`);
  }
}

class Rabbit extends Animal {
  hide() {
    alert(`${this.name} hides`);
  }
}

let rabbit = new Rabbit("White Rabbit");
rabbit.run(5);
rabbit.hide();

rabbit.__proto__ === Rabbit.prototype;
Rabbit.prototype.__proto__ === Animal.prototype;
Animal.prototype.__proto__ === Object.prototype;
```

重写方法，使用 super 调用父类的方法

```javascript
class Rabbit extends Animal {
  hide() {
    alert(`${this.name} hides!`);
  }

  stop() {
    super.stop(); // 调用父类的 stop
    this.hide(); // 然后 hide
  }
}
```

重写 constructor
继承类的 constructor 必须调用 super(...)，并且 (!) 一定要在使用 this 之前调用。

```javascript
class Rabbit extends Animal {
  constructor(name, earLength) {
    super(name);
    this.earLength = earLength;
  }

  // ...
}
```

箭头函数没有自己的 super

### 9.3 静态属性和静态方法

静态方法被用于实现属于整个类的功能。它与具体的类实例无关。
语法如下所示：

```javascript
class MyClass {
  static property = ...;

  static method() {
    ...
  }
}
```

从技术上讲，静态声明与直接给类本身赋值相同：

```javascript
MyClass.property = ...
MyClass.method = ...
```

静态属性和方法是可被继承的。
对于 class B extends A，

```javascript
B.__proto__ === A;
B.prototype.__proto__ === A.prototype;
```

因此，如果一个字段在 B 中没有找到，会继续在 A 中查找。

继承 Object 的问题

```javascript
class Rabbit extends Object {
  constructor(name) {
    super(); // 需要在继承时调用父类的 constructor
    this.name = name;
  }
}

let rabbit = new Rabbit("Rab");

alert(rabbit.hasOwnProperty("name")); // true
```

“extends” 语法会设置两个原型：

1. 在构造函数的 "prototype" 之间设置原型（为了获取实例方法）。
2. 在构造函数之间会设置原型（为了获取静态方法）。

### 9.4 私有的和受保护的属性和方法

面向对象编程最重要的原则之一 —— 将内部接口与外部接口分隔开来。
在面向对象的编程中，属性和方法分为两组：

- 内部接口 —— 可以通过该类的其他方法访问，但不能从外部访问的方法和属性。
- 外部接口 —— 也可以从类的外部访问的方法和属性。

#### 受保护的 waterAmount

```javascript
class CoffeeMachine {
  // 受保护的属性通常以下划线 _ 作为前缀
  _waterAmount = 0;

  set waterAmount(value) {
    if (value < 0) throw new Error("Negative water");
    this._waterAmount = value;
  }

  get waterAmount() {
    return this._waterAmount;
  }

  constructor(power) {
    this.power = power;
  }
}

let coffeeMachine = new CoffeeMachine(100);

coffeeMachine.waterAmount = -10;
```

#### 只读的 power

要让一个属性变得只读，只设置 getter，不设置 setter

```javascript
class CoffeeMachine {
  // ...

  constructor(power) {
    this._power = power;
  }

  get power() {
    return this._power;
  }
}

let coffeeMachine = new CoffeeMachine(100);

coffeeMachine.power = 200; // Error
```

#### 私有字段

私有字段用#开头,是语言级别的实现

```javascript
class CoffeeMachine {
  #waterLimit = 200;

  #checkWater(value) {
    if (value < 0) throw new Error("Negative water");
    if (value > this.#waterLimit) throw new Error("Too much water");
  }
}

let coffeeMachine = new CoffeeMachine();

// 不能从类的外部访问类的私有属性和方法
coffeeMachine.#checkWater(); // Error
coffeeMachine.#waterLimit = 1000; // Error
```

私有属性限制太严重，更多还是用受保护的字段
就面向对象编程（OOP）而言，内部接口与外部接口的划分被称为 封装

## 13 模块

### 13.1 简介

一个模块（module）就是一个文件。一个脚本就是一个模块。

- export 关键字标记了可以从当前模块外部访问的变量和函数。
- import 关键字允许从其他模块导入功能。

必须通过使用 <script type="module"> 特性（attribute）来告诉浏览器，此脚本应该被当作模块（module）来对待。

```javascript
export function sayHi(user) {
  alert(`Hello, ${user}`);
}
```

```html
<script type="module">
  import { sayHi } from "./sayHi.js";
  alert(sayHi);
  sayHi("jack");
</script>
```

模块始终默认使用 use strict

模块只被执行一次。生成导出，然后它被分享给所有对其的导入，所以如果某个地方修改了 admin 对象，其他的模块也能看到这个修改。
在一个模块中，顶级 this 是 undefined

### 13.2 导入、导出

命名导出要花括号，默认导出不要
export class User {...}
import {User} from ...

export default class User {...}
import User from ...

重新导出
export {login, logout} from './helpers.js';
