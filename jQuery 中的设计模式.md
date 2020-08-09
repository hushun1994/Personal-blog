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
      for (let i = 0; i < elements.length; i++) {
        elements[i].classList.add(className);
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
