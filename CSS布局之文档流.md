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

* 其中有些元素比较特殊，如img，input。这些元素是内联元素，却可以设置宽高。

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

```
  .float_brotherElement {
     clear: left | right | both;
  }

```

#### 2. 伪类（clearfix）
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

#### 定位（position 不为static（默认值））








