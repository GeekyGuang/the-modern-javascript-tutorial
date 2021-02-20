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
