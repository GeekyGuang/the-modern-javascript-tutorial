## 5. 动画

### 5.1 贝塞尔曲线

贝塞尔曲线的特点:

1. 控制点不总是在曲线上。
2. 曲线的阶次等于控制点的数量减一。 对于两个点我们能得到一条线性曲线（直线），三个点 — 一条二阶曲线，四个点 — 一条三阶曲线。
3. 曲线总是在控制点的凸包内部

**贝塞尔曲线沿控制点的顺序延伸**

贝塞尔曲线的两种定义方法：

- 使用数学方程式。
- 使用绘图过程：德卡斯特里奥算法

贝塞尔曲线的优点：

- 我们可以通过控制点移动来用鼠标绘制平滑线条。
- 复杂的形状可以由多条贝塞尔曲线组成。

工具：https://cubic-bezier.com/

### 5.2 CSS 动画

#### transition

css 动画结束之后，会触发 transitionend 事件
**有多少个 transition-property,就会触发多少次 transitionend 事件**

```javascript
boat.onclick = function () {
  //...
  let times = 1;

  function go() {
    if (times % 2) {
      // 向右移动
      boat.classList.remove("back");
      boat.style.marginLeft = 100 * times + 200 + "px";
    } else {
      // 向左移动
      boat.classList.add("back");
      boat.style.marginLeft = 100 * times - 200 + "px";
    }
  }

  go();

  boat.addEventListener("transitionend", function () {
    times++;
    go();
  });
};
```

练习题 1: 放大图片动画

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <style>
      img {
        cursor: pointer;
      }
    </style>
    <style>
      #flyjet {
        width: 40px;
        /* -> 400px */

        height: 24px;
        /* -> 240px */
      }
      /* ID选择器优先级大于类选择器 */
      #flyjet.enlarge {
        width: 400px;
        height: 240px;
        transition: all 3s cubic-bezier(0.1, 0.65, 0.72, 1.49);
      }
    </style>
  </head>

  <body>
    <img id="flyjet" src="https://en.js.cx/clipart/flyjet.jpg" />
    <script>
      flyjet.onclick = function () {
        this.classList.add("enlarge");

        // 有多少个transition-property就触发多少次
        let transFlag = false;
        flyjet.addEventListener("transitionend", function () {
          if (!transFlag) {
            alert("done!");
          }
          transFlag = true;
        });
      };
    </script>
  </body>
</html>
```

练习题 2: 画一个圆圈动画

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <style>
      .circle {
        transition-property: width, height, margin-left, margin-top;
        transition-duration: 2s;
        position: fixed;
        transform: translateX(-50%) translateY(-50%);
        background-color: red;
        border-radius: 50%;

        /* transition必须有初始值，否则看不到变化 */
        width: 0;
        height: 0;
      }
    </style>
  </head>

  <body>
    <div class="circle"></div>
    <script>
      function showCircle(cx, cy, radius) {
        let circle = document.getElementsByClassName("circle")[0];
        circle.style.width = 2 * radius + "px";
        circle.style.height = 2 * radius + "px";
        circle.style.top = cy + "px";
        circle.style.left = cx + "px";
      }

      let button = document.createElement("button");
      button.innerText = "showCircle(150,150,100)";
      button.onclick = function () {
        showCircle(150, 150, 100);
      };

      document.body.append(button);
    </script>
  </body>
</html>
```

### 5.3 JavaScript 动画

JavaScript 动画应该通过 requestAnimationFrame 实现。该内置方法允许设置回调函数，以便在浏览器准备重绘时运行。那通常很快，但确切的时间取决于浏览器。

callback 得到一个参数 —— 从页面加载开始经过的毫秒数。这个时间也可通过调用 performance.now() 得到。

当页面在后台时，根本没有重绘，因此回调将不会运行：动画将被暂停并且不会消耗资源。那很棒。

这是设置大多数动画的 helper 函数 animate：

```javascript
function animate({ timing, draw, duration }) {
  let start = performance.now();

  requestAnimationFrame(function xxx(time) {
    // timeFraction 从 0 增加到 1
    let timeFraction = (time - start) / duration;
    if (timeFraction > 1) timeFraction = 1;

    // 计算当前动画状态
    let progress = timing(timeFraction);

    draw(progress); // 绘制

    if (timeFraction < 1) {
      requestAnimationFrame(xxx);
    }
  });
}
```

参数：

- duration —— 动画运行的总毫秒数。
- timing —— 计算动画进度的函数。获取从 0 到 1 的小数时间，返回动画进度，通常也是从 0 到 1。
- draw —— 绘制动画的函数。

当然我们可以改进它，增加更多花里胡哨的东西，但 JavaScript 动画不是经常用到。它们用于做一些有趣和不标准的事情。因此，您大可在必要时再添加所需的功能。

JavaScript 动画可以使用任何时序函数。与 CSS 不同，我们不仅限于 Bezier 曲线。

draw 也是如此：我们可以将任何东西动画化，而不仅仅是 CSS 属性。
