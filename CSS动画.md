# CSS动画

## 动画的定义

由许多静止的画面（帧），以一定的速度（30张/秒）连续播放，肉眼因视觉残像产生错觉而以为是活动的画面。

## 浏览器的渲染原理

渲染过程： 

* 根据HTML构建DOM树（DOM）
* 根据CSS构建CSS树（CSSOM）
* DOM树与CSS树合并形成渲染树（Render Tree）
* Layout 布局 （文档流，文字颜色，计算大小和位置等）
* Paint 绘制（把边框颜色，文字颜色，阴影等画出来）
* Composite 合成（根据层叠关系展示画面）

三种更新方式：

* JS/CSS -> Style -> Layout -> Paint -> Composite
* JS/CSS -> Style -> Paint -> Composite
* JS/CSS -> Style -> Composite

CSS动画优化：

* JS优化：使用requestAnimationFrame代替setTimeout或setInterval
* CSS优化：使用will-change或transform: translate();

## 容易混淆的四个CSS属性

* animation（动画）用于设置动画属性，它是一个简写的属性，包含6个属性
* transition（过渡）	用于设置元素的样式过度，和animation有着类似的效果，但细节上有很大的不同
* transform（变形）	用于元素进行旋转、缩放、移动或倾斜，和设置样式的动画并没有什么关系，就相当于color一样用来设置元素的“外表”
* translate（移动）	translate只是transform的一个属性值，即移动。

### 使用transition完成动画

transition完成动画效果一般要配合transform一起使用，需要某种条件触发到另一状态，只用定好初始状态和结束时的状态，transition自动补充中间帧。

语法：transition: property, duration, timing-function, delay;

属性描述：

* 规定设置过渡效果的 CSS 属性的名称
* 规定完成过渡效果需要多少秒或毫秒
* 规定速度效果的速度曲线
* 定义过渡效果何时开始

定义样式：

```
  .demo {
    box-sizing: border-box;
    width: 200px;
    height: 200px;
    border: 1px solid #f00;
    transition: all 1s;
  }
  .demo_click {
    transform: translateX(400px);
  }
```

JS绑定click事件触发状态改变：

```
  demo.addEventListener('click', () => {
    demo.classList.add('demo_click')
  })
```

定义好先后状态，通过click事件触发为元素新增类名更改状态，然后由transition完成动画。

### 使用animation完成动画

animation完成动画需要声明关键帧，使用@keyframes定义关键帧，动画名称，并添加动画。

语法：animation: animation-name, animation-duration, animation-timing-function, animation-delay, 
     animation-iteration-count, animation-direction, animation-fill-mode, animation-play-state;
     
属性描述： 

* animation-name：动画名称
* animation-duration： 完成一次动画需要的事件
* animation-timing-function： 动画时间函数，过度方式
* animation-delay：动画的延迟时间
* animation-iteration-count：动画的次数
* animation-direction：动画的方向
* animation-fill-mode：填充模式
* animation-play-state：动画的播放状态，暂停或者播放

定义样式：

```
  .demo {
    box-sizing: border-box;
    width: 200px;
    height: 200px;
    border: 1px solid #f00;
    animation: move, 2s, 3, alternate;
  }
  @keyframes move {
    0% {
      transform: translateX(0);
    }
    50% {
      transform: translateX (400px);
    }
    100% {
      transform: translateX(400px) translateY(200px);
    }
  }
```

使用@keyframes定义了名为move的动画，该动画定义了三个关键帧，第一帧为元素本来在的位置，中间帧水平向右位移了400px，
结束帧为水平向右位移400px以后然后向下位移了200px。然后给动画添加animation属性定义如何完成该动画。
