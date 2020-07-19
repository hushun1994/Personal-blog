# CSS 盒模型

## 盒模型介绍

* 盒模型分为content-box和border-box。两种盒模型的唯一差异就是对元素宽度width的影响。
* 介绍盒模型之前必须先知道四个概念：content，padding，border，margin。

![盒模型介绍](./src/images/box-sizing.png)

### content

* 元素内部显示内容的区域

### padding

* 内边距或是内填充，内容距离边框的距离。

### border

* 边框，边框区域的大小取决于border-width的值。

## 盒模型分类

### 1. content-box（内容盒模型）

* 内容盒模型元素的宽度就是元素内部内容区域的宽度
* 元素宽度width = content的宽度

### 2. border-box （边框盒模型）

* 边框盒模型元素的宽度等于内部内容区域的宽度与内边距的宽度以及边框宽度的总和。
* 元素宽度width = content的宽度 + 2 x border的宽度 + padding的宽度


