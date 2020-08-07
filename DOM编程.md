# DOM 编程

简介：DOM一般指文档对象模型。文档对象模型（Document Object Model，简称DOM），是W3C组织推荐的处理可扩展置标语言的标准编程接口。
它是一种与平台和语言无关的应用程序接口(API),它可以动态地访问程序和脚本,更新其内容、结构和www文档的风格(目前,HTML和XML文档是通过说明部分定义的)。

网页其实是一棵树，DOM提供document对象，为JS操作网页提供了API。

## 获取元素的API

### 获取所有元素

* window.id（在控制台的快捷操作）

控制台调试时，通过元素ID快速获取元素的方式

* document.getElementById()

通过ID获取元素

* document.getElementsByTagName()

通过标签名获取元素，获取到的是一个伪数组，通过下标获取到指定元素。

* document,getElementsByClassName()

通过类名获取元素，获取到的是一个伪数组，通过下标获取到指定元素。

* document.querySelector()

更加灵活的获取元素的方式，上面的接口传入的参数这个方法都可以。获取满足条件的第一个元素

* document.querySelectorAll()

获取满足条件的所有元素，获取到的是一个伪数组，缓存文档中元素集合的一个快照。（当网页中元素个数变动时不会更新）

### 获取特定元素

* document.documentElement -- 获取html元素

* document.head -- 获取head元素

* document.body -- 获取body元素

* window -- 获取window对象（window不是元素）

* document.all -- 获取所有元素（IE发明的，document.all比较奇葩，是JS的第六个falsy值(在非IE环境下为false)，这个方法可用来识别IE浏览器。）

## 元素的六层原型链

div(栗子元素) -> HTMLDivElement -> HTMLElement -> Element -> Node -> EventTarget -> Object

![元素的六层原型链](./src/images/Element_prototype_chain.png)

### 节点Node的类型

1. Node.ELEMENT_NODE(1) -- 元素节点
2. Node.TEXT_NODE(3) -- 文本节点
3. Node.CDATA_SECTION_NODE(4) -- CDATA节点
4. Node.PROCESSING_INSTRUCTION_NODE(7) -- 一个用于XML文档的processingInstruction
5. Node.COMMENT_NODE(8) -- 注释节点
6. Node.DOCUMENT_NODE(9) -- 文档节点
7. Node.DOCUMENT_TYPE_NODE(10) -- 文档类型节点
8. Node.DOCUMENT_FARGMENT_NODE(11) -- 文档片段节点

## 元素增删改查的API

### 元素的增删改查

* document.createElement() -- 创建元素
* document.createTextNode() -- 创建文本
* appendChild() -- 元素里面插入内容
* cloneNode() -- 克隆元素（传入一个布尔值，true 为深克隆；false 为浅克隆）
* removeChild() -- 删除元素（老方法，需要父元素来调用）
* remove() -- 删除元素（新方法，要删除的元素调用）
* innerHTML() -- 写入HTML结构（可读可写）
* innerText() -- 写入文本（可读可写）

* node.parentNode / node.parentElement -- 得到父元素节点
* node.childNode / node.children -- 得到子元素节点（伪数组）
* node.firetChild / node.lastChild 
* node.previousSibling / node.nextSibling -- 前后相邻兄弟节点
* node.previousElementSibling / node.nextElementSibling -- 前后相邻兄弟元素节点

### 修改与读取属性

* Element.attr -- 读取属性/修改属性
* Element.className -- 修改属性（修改时会全覆盖）
* Element.classList -- 读取类名
* Element.classList.add() -- 添加类名（不会覆盖）
* Element.style -- 读取/修改（修改时会全覆盖）
* Element.style.attr -- 修改style里面的具体属性，不会造成覆盖
* Element.getAttribute() -- 读取属性

DOM操作是跨线程的，JS执行线程和渲染线程是两个独立的线程，JS对DOM操作时需要通过浏览器跨线程通信，所以DOM操作慢。


