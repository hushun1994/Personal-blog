# jQuery 中的设计模式

## 闭包与链式操作

* window.jQuery 是我们提供的全局函数
* jQuery函数构建了一个对象，这个对象的方法保存着对传入选择器获取到的元素的引用。
* jQuery函数接受一个选择器/元素数组作为参数，返回一个可以操作对应元素的API对象，调用API对象的方法，
对元素进行操作，完成后返回该API对象。这样就可以进行链式操作，继续调用该API的其他方法对对应元素进行操作，
* 用 $ 简化操作代替jQuery函数
```
  window.$ = window.jQuery = (selectorOrArray) => {
    let elements = document.querySelectorAll(selectorOrArray);
    return {
      addClass(className) {
        for (let i = 0; i < elements.length; i++) {
          elements[i].classList.add(className);
        }
        return this;
      },
    };
  };
```

* 或者返回一个新的API对象，对新的API对象进行操作

```
  window.$ = window.jQuery = (selectorOrArray) => {
    let elements;
    if (typeof selectorOrArray === "string") {
      elements = document.querySelectorAll(selectorOrArray);
    } else if (selectorOrArray instanceof Array) {
      elements = selectorOrArray;
    }
    return {
      find(selector) {
        let array = [];
        for (let i = 0; i < elements.length; i++) {
          let elements2 = Array.from(elements[i].querySelectorAll(selector));
          array = array.concat(elements2);
        }
        return jQuery(array);
      }
    };
  };
```

* 如何对前面的API对象进行操作，可以缓存每一个新生成的API对象，就可以对前面生成的API进行操作

```
  const api1 = $('selector1')
  api1.addClass('xxx')
  
  const api2 = api1.find('selector2')
  api2.addClass('xxx')
  
  const api3 = $('selector3')
  api.addClass('xxx')
```

* 在链式操作时无法做到对前面的API进行缓存，可以在API对象中设置一个oldAPI属性用于缓存之前的API对象，
在调用find()方法时对旧的API进行缓存，在调end()方法时返回旧的API。

```
  window.$ = window.jQuery = (selectorOrArray) => {
    let elements;
    if (typeof selectorOrArray === "string") {
      elements = document.querySelectorAll(selectorOrArray);
    } else if (selectorOrArray instanceof Array) {
      elements = selectorOrArray;
    }
    return {
      oldAPI: null,
      addClass(className) {
        for (let i = 0; i < elements.length; i++) {
          elements[i].classList.add(className);
        }
        return this;
      },
      find(selector) {
        let array = [];
        for (let i = 0; i < elements.length; i++) {
          let elements2 = Array.from(elements[i].querySelectorAll(selector));
          array = array.concat(elements2);
        }
        const newAPI = jQuery(array);
        newAPI.oldAPI = this;
        return newAPI;
      },
      end() {
        return this.oldAPI;
      },
    };
  };
```

## 命名风格

如何区分一个对象是DOM对象还是jQuery对象

* DOM对象命名时在变量名前面加上'el'或者什么都不加 -- 可以使用DOM的API
* jQuery对象命名时在变量名前面加上'$'符号用以确定它为jQuery对象 -- 可以使用jQuery的API

## 用jQuery的原型对象 jQuery.prototype 存放所有共用的属性和方法

```
  window.$ = window.jQuery = (selectorOrArray) => {
    let elements;
    if (typeof selectorOrArray === "string") {
      elements = document.querySelectorAll(selectorOrArray);
    } else if (selectorOrArray instanceof Array) {
      elements = selectorOrArray;
    }
    const api = Object.create(jQuery.prototype);
    Object.assign(api, {
      elements: elements,
      oldAPI: null,
    });
    return api;
  };

  jQuery.prototype = {
    constructor: jQuery,
    addClass(className) {
      for (let i = 0; i < this.elements.length; i++) {
        this.elements[i].classList.add(className);
      }
      return this;
    },
  };
```

## jQuery用到了哪些设计模式

* 不用new的构造函数
* jQuery函数支持各种参数，这个模式叫函数重载
* 用闭包隐藏细节
* 实现元素属性的可读可写，getter/setter
* $.fn = $.prototype $.fn 是 $.prototype 的别名
* 针对不同浏览器使用不同的代码，这叫适配器

## jQuery 常用API

### 1. 选择网页元素

选择表达式可以是CSS选择器：

```
  $(document) //选择整个文档对象

  $('#myId') //选择ID为myId的网页元素

  $('div.myClass') // 选择class为myClass的div元素

  $('input[name=first]') // 选择name属性等于first的input元素
```
也可以是jQuery特有的表达式：

```
  $('a:first') //选择网页中第一个a元素

  $('tr:odd') //选择表格的奇数行

  $('#myForm :input') // 选择表单中的input元素

  $('div:visible') //选择可见的div元素

  $('div:gt(2)') // 选择所有的div元素，除了前三个

  $('div:animated') // 选择当前处于动画状态的div元素
```

### 2. 改变结果集

jQuery设计思想之二，就是提供各种强大的过滤器，对结果集进行筛选，缩小选择结果。

```
  $('div').has('p'); // 选择包含p元素的div元素

  $('div').not('.myClass'); //选择class不等于myClass的div元素

  $('div').filter('.myClass'); //选择class等于myClass的div元素

  $('div').first(); //选择第1个div元素

  $('div').eq(5); //选择第6个div元素
```
有时候，我们需要从结果集出发，移动到附近的相关元素，jQuery也提供了在DOM树上的移动方法：

```
  $('div').next('p'); //选择div元素后面的第一个p元素

  $('div').parent(); //选择div元素的父元素

  $('div').closest('form'); //选择离div最近的那个form父元素

  $('div').children(); //选择div的所有子元素

  $('div').siblings(); //选择div的同级元素
```

### 3. 链式操作

jQuery设计思想之三，就是最终选中网页元素以后，可以对它进行一系列操作，并且所有操作可以连接在一起，以链条的形式写出来，比如：

```
  $('div').find('h3').eq(2).html('Hello');
```
分解开来，就是下面这样：

```
  $('div') //找到div元素

    .find('h3') //选择其中的h3元素

    .eq(2) //选择第3个h3元素

    .html('Hello'); //将它的内容改为Hello
```
这是jQuery最令人称道、最方便的特点。它的原理在于每一步的jQuery操作，返回的都是一个jQuery对象，所以不同操作可以连在一起。

jQuery还提供了.end()方法，使得结果集可以后退一步：

```
  $('div')

    .find('h3')

    .eq(2)

    .html('Hello')

    .end() //退回到选中所有的h3元素的那一步

    .eq(0) //选中第一个h3元素

    .html('World'); //将它的内容改为World
```

### 4. 元素的操作：取值和赋值

操作网页元素，最常见的需求是取得它们的值，或者对它们进行赋值。

jQuery设计思想之四，就是使用同一个函数，来完成取值（getter）和赋值（setter），即"取值器"与"赋值器"合一。到底是取值还是赋值，由函数的参数决定。

```
  $('h1').html(); //html()没有参数，表示取出h1的值

  $('h1').html('Hello'); //html()有参数Hello，表示对h1进行赋值
```
常见的取值和赋值函数如下：

```
  .html() 取出或设置html内容

  .text() 取出或设置text内容

  .attr() 取出或设置某个属性的值

  .width() 取出或设置某个元素的宽度

  .height() 取出或设置某个元素的高度

  .val() 取出某个表单元素的值
```
需要注意的是，如果结果集包含多个元素，那么赋值的时候，将对其中所有的元素赋值；取值的时候，则是只取出第一个元素的值（.text()例外，它取出所有元素的text内容）。

### 5. 元素的操作：移动

jQuery设计思想之五，就是提供两组方法，来操作元素在网页中的位置移动。一组方法是直接移动该元素，另一组方法是移动其他元素，使得目标元素达到我们想要的位置。

假定我们选中了一个div元素，需要把它移动到p元素后面。

第一种方法是使用.insertAfter()，把div元素移动p元素后面：

```
  $('div').insertAfter($('p'));
```
第二种方法是使用.after()，把p元素加到div元素前面：

```
  $('p').after($('div'));   
```

表面上看，这两种方法的效果是一样的，唯一的不同似乎只是操作视角的不同。但是实际上，它们有一个重大差别，那就是返回的元素不一样。
第一种方法返回div元素，第二种方法返回p元素。你可以根据需要，选择到底使用哪一种方法。

使用这种模式的操作方法，一共有四对：

```
  .insertAfter()和.after()：在现存元素的外部，从后面插入元素

  .insertBefore()和.before()：在现存元素的外部，从前面插入元素

  .appendTo()和.append()：在现存元素的内部，从后面插入元素

  .prependTo()和.prepend()：在现存元素的内部，从前面插入元素
```

### 6. 元素的操作：复制、删除和创建

除了元素的位置移动之外，jQuery还提供其他几种操作元素的重要方法。

复制元素使用.clone()。

删除元素使用.remove()和.detach()。两者的区别在于，前者不保留被删除元素的事件，后者保留，有利于重新插入文档时使用。

清空元素内容（但是不删除该元素）使用.empty()。

创建新元素的方法非常简单，只要把新元素直接传入jQuery的构造函数就行了：

```
  $('<p>Hello</p>');

  $('<li class="new">new list item</li>');

  $('ul').append('<li>list item</li>');
```
