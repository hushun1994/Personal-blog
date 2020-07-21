# CSS布局

## 布局分类

* 固定宽度布局，一般宽度为960px / 1000px / 1024px。
* 不固定宽度布局，主要靠文档流的原理来布局。（文档流本来就是自适应的，不需要加额外的样式）
* 响应式布局，pc上固定布局，手机上不固定布局，是一种混合式布局。

## 布局的两种思路

### 1. 从大到小

* 先定下大局
* 然后每个部分的小布局

### 2. 从小到大

* 先从小的入手，完成局部的布局
* 然后再组合成大布局

两种布局思路均可，新人更适合第二种，从小的入手会简单一些。老手一般用第一种，因为有成型的大局观。

## 布局方案

### 1. float布局

### 实现原理

* 子元素上加float（left/right）属性和width属性
* 父元素上加 .clearfix类（清除浮动）

经验：有经验者会留一些空间或者最后一个不设width不需要做响应式，因为手机上没有IE，这个布局是专门为IE准备的。

### 不同布局

* 用float 做两栏布局（如顶部条）
* 用float 做三栏布局（如内容区）
* 用float 做四栏布局（如导航）
* 用float 做平均布局（如产品展示区）

经验：

1. 加上头尾，即可满足所有PC页面需求。
2. 手机页面傻子采用float。
3. float要自己计算宽度，不灵活。
4. float足以用来应付IE。

### flex布局（一维布局）

* 脑图:

![flex盒模型概念图](./src/images/flex.png)


#### flex盒模型概念



* 主轴（main axis）
* 交叉轴（cross axis）
* 容器（container）
* item（项目）

用于放置内容的容器container, 水平方向的主轴main axis, 垂直方向的交叉轴cross axis, 还有需要布局的项目item。
flex布局意为弹性布局，为盒模型提供最大的灵活性。任何一个容器都可以指定为flex布局。

设置flex布局： 

```
  .container {
     display: flex | inline-flex;
  }
```



#### 容器container

container的相关属性

1. flex-direction: 主轴方向（items的流动方向）

```
  flex-direction: row | row-reverse | column |column-reverse;
```

* row：主轴在水平方向，从左往右排列；默认值；
* row-reverse：主轴在水平方向，从右往左排列；
* column：主轴在垂直方向，从上往下；
* column-reverse：主轴在垂直方向，从下往上；

2. flex-wrap: 设置换行方式

```
  flex-wrap: nowrap | wrap | wrap-reverse;
````

* nowrap：不换行；
* wrap：换行，第一行在上方，剩下的往下排；
* wrap-reverse：换行，第一行在下方，剩下的往上排；

3. justify-content: 主轴对齐方式

```
  justify-content: flex-start | flex-end | center | space-between | space-around | space-evenly;
```

* flex-start：从左往右
* flex-end：从右往左
* center：水平居中
* space-between：每个item之间是等宽的
* space-around： 每个item左右侧的宽度都是相等的
* space-evenly： ......

4. align-items：次轴对齐

```
  align-items: flex-start | flex-end | center |stretch | baseline;
```

* flex-start: 顶部对齐
* flex-end: 底部对齐
* center: 垂直居中
* baseline: 基线对齐
* stretch: 将item拉到一般高对齐

5. align-content: 多行内容分布

```
  align-content: flex-start | flex-end | center | stretch | space-between |space-around;
```

#### item的相关属性

1. order: 元素的排序，按从小到大排列，默认值为0，可取负值。

2.flex-grow: 空间膨胀系数，指定空间变宽时如何分配，按每个元素的flex-grow的值的比例进行分配，默认值为0。

3.flex-shrink: 空间压缩系数，指定空间变窄时如何分配，只有当空间小于原始宽度总和时，按压缩系数比进行压缩，默认值为1，值为0表示不接受压缩。

4.flex-basis: 元素的基准宽度。

5.align-self: 定制某个元素自己的次轴对齐方式，和align-items的可取值是相同的。

### grid布局（二维布局）

网格布局（Grid）是最强大的 CSS 布局方案。

它将网页划分成一个个网格，可以任意组合不同的网格，做出各种各样的布局。以前，只能通过复杂的 CSS 框架达到的效果，现在浏览器内置了。
















