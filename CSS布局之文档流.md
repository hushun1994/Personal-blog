# CSS布局之文档流，浮动与定位

## 网页布局的定义

* 网页的布局方式就是浏览器如何对网页中的元素进行排版。
主要分为：文档流（normal flow），浮动（float），绝对定位（position）。

### 文档流

* 文档流是文档中可显示对象在排列时所占用的位置。
文档流直观表现：元素在窗口中从左到右，从上到下按顺序排列。元素分为内联元素和块级元素，

#### 块级元素（display：block）

* 块级元素独占一行，默认宽度是100%，从上到下排列，可设置宽高 padding margin，可包含其他块级元素或内联元素，常见的块级元素有
p，h1-h6，div，ul，ol，table等。

#### 内联元素（display：inline）

* 和其他元素都在同一行，从左到右排列，不可设置宽高 margin，可设置padding，内联元素只能容纳文本或者其他内联元素，但容纳块级元
素也不会出错，但不建议。常见的内联元素有span，a，i，em，img，input，select，textarea，button等。

#### 内联块级元素（display：inline-block）
* 其中有些元素比较特殊，如img，input。这些元素是内联元素，却可以设置宽高。于是就有一种特殊属性的元素：内联块级元素（display：inline-block），
既可设置宽高与内外边距，又不会独占一行，可与其他元素同在一行，同时具有块级元素与内联元素的部分特性。

### 脱离文档流

* 脱离文档流的方式有两种：浮动（float），定位（position）。

#### 浮动（float：left/right；）

* 为元素设置float属性可以让元素产生浮动，从而脱离文档流，浮动可以解决图文并排的问题，浮动会造成元素脱离文档流，从而是外部盒子坍
塌而使得浮动元素的内容溢出，浮动还会导致内联元素与块级元素的排列对齐方式变得非常奇怪，解决这个问题的方法就是清除浮动。

* clear：left； -- 清除左浮动
* clear：right； -- 清除右浮动
* clear：both； -- 清除左右浮动

* 清除浮动的方式：

##### 1. clear：left/right/both 

为浮动元素的兄弟元素添加清除浮动属性

```
  .float_brotherElement {
     clear: left | right | both;
  }

```

##### 2. 伪类（clearfix）

为父级元素添加伪类或是为元素

```
  .clearfix:after {
     content: '';
     display: block;
     clear: both;
  } 
```
```
  .clearfix::after {
     content: '';
     display: block;
     clear: both;
  }
  

```

##### 3. overflow（不为visible）

在父级元素上设置overflow 属性

```
  .fatherElement {
     overflow: auto | scroll | hidden;
  }

```

#### 定位 position

position对元素进行定位，其属性值有：static（默认值），relative（相对定位），absolute（绝对定位），fixed（固定定位），sticky（粘滞定位）。
只有当属性值为absolute/fixed时元素才会脱离文档流。

* static -- 默认值，元素处于文档流中本来的位置。
* relative -- 相对定位，元素相对与自身本来位置的定位，通过设置left/right，top/bottom来定位。
* absolute -- 绝对定位，元素相对最近一层的position值不为static的祖先元素的定位，通过设置left/right，top/bottom来定位。
* fixed -- 固定定位，元素相对的视口（viewport）的定位。（有坑 => 当父级容器设置transform：scale（0.8）属性，fixed的元素就不再相对视口定位了）。
* sticky -- 粘性定位，粘性定位可以被认为是相对定位和固定定位的混合。元素在跨越特定阈值前为相对定位，之后为固定定位。

#### z-index（配合position使用）

z-index指定了一个元素及其子元素的 z-order，元素之间有重叠的时候，z-index可以决定让哪一个元素在上方。通常来说 z-index 较大的元素会覆盖较小的一个。
仅对定位的元素有效。元素之间重叠默认的顺序是后面的元素会盖住前面的元素。如果设置了z-index可以改变这个顺序。但只对同级的元素有效。父元素永远在子元素后面。


### BFC（Block Formatting Contexts）

#### BFC概念

Formatting context(格式化上下文) 是 W3C CSS2.1 规范中的一个概念。它是页面中的一块渲染区域，并且有一套渲染规则，它决定了其子元素将如何定位，
以及和其他元素的关系和相互作用。

#### BFC作用

* BFC 即 Block Formatting Contexts (块级格式化上下文)，它属于上述定位方案的普通流。

具有 BFC 特性的元素可以看作是隔离了的独立容器，容器里面的元素不会在布局上影响到外面的元素，并且 BFC 具有普通容器所没有的一些特性。

#### 如何触发BFC

只要元素满足下面任一条件即可触发 BFC 特性：

* body根元素
* 浮动元素：float 除 none 以外的值
* 绝对定位元素：position (absolute、fixed)
* display 为 inline-block、table-cells、flex
* overflow 除了 visible 以外的值 (hidden、auto、scroll)

#### BFC特性及应用

* 同一个 BFC 下外边距会发生折叠

* BFC 可以包含浮动的元素（清除浮动）

* BFC 可以阻止元素被浮动元素覆盖





