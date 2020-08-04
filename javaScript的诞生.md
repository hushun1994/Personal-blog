# javaScript 的诞生

javaScript 是什么：

JavaScript（通常缩写为JS）是一种高级的、解释型的编程语言。JavaScript是一门基于原型、函数先行的语言，是一门多范式的语言，它支持
面向对象编程，命令式编程，以及函数式编程。它提供语法来操控文本、数组、日期以及正则表达式等，不支持I/O，比如网络、存储和图形等，但
这些都可以由它的宿主环境提供支持。它已经由ECMA（欧洲电脑制造商协会）通过ECMAScript实现语言的标准化。它被世界上的绝大多数网站所使用，
也被世界主流浏览器（Chrome、IE、Firefox、Safari、Opera）支持。

虽然JavaScript与Java这门语言不管是在名字上，或是在语法上都有很多相似性，但这两门编程语言从设计之初就有很大的不同，JavaScript的
语言设计主要受到了Self（一种基于原型的编程语言）和Scheme（一门函数式编程语言）的影响。在语法结构上它又与C语言有很多相似（例如if条件
语句、switch语句、while循环、do-while循环等）。

在客户端，JavaScript在传统意义上被实现为一种解释语言，但在最近，它已经可以被即时编译（JIT）执行。随着最新的HTML5和CSS3语言标准的
推行它还可用于游戏、桌面和移动应用程序的开发和在服务器端网络环境运行，如Node.js。

## javaScript 的历史

* 肇始于网景

1993年，伊利诺伊大学厄巴纳-尚佩恩分校的国家超级电脑应用中心（NCSA）发表了NCSA Mosaic，这是最早流行的图形接口网页浏览器，它在万维网
的普及上发挥了重要作用。1994年，一家名为Mosaic Communications的公司在加州芒廷维尤成立了，并雇用了许多原来的NCSA Mosaic开发者用来
开发Mosaic Netscape，该公司的目标是取代NCSA Mosaic成为世界第一的网页浏览器。第一个版本的网页浏览器Mosaic Netscape 0.9于1994年底
发布。在四个月内，已经占据了四分之三的浏览器市场，并成为1990年代互联网的主要浏览器。为避免NCSA的商标所有权问题，该浏览器于同年更名为
Netscape Navigator，该公司命名为Netscape Communications。网景预见到网络需要变得更动态。公司的创始人马克·安德森认为HTML需要一种
胶水语言，让网页设计师和兼职程序员可以很容易地使用它来组装图片和插件之类的组件，且代码可以直接编写在网页标记中。

1995年，网景招募了布兰登·艾克，目标是把Scheme语言嵌入到Netscape Navigator浏览器当中。但更早之前，网景已经跟昇阳合作在Netscape Navigator
中支持Java，这时网景内部产生激烈的争论。后来网景决定发明一种与Java搭配使用的辅助脚本语言并且语法上有些类似，这个决策导致排除了采用现有的语言，
例如Perl、Python、Tcl或Scheme。为了在其他竞争提案中捍卫JavaScript这个想法，公司需要有一个可以运作的原型。艾克在1995年5月仅花了十天时间就把
原型设计出来了。

最初命名为Mocha，1995年9月在Netscape Navigator 2.0的Beta版中改名为LiveScript，同年12月，Netscape Navigator 2.0 Beta 3中部署时被
重命名为JavaScript，当时网景公司与昇阳电脑公司组成的开发联盟为了让这门语言搭上Java这个编程语言“热词”，因此将其临时改名为JavaScript，日后这
成为大众对这门语言有诸多误解的原因之一。

* 微软采纳

JavaScript推出后在浏览器上大获成功，微软公司在不久后就为Internet Explorer 3浏览器推出了JScript，以与处于市场领导地位的网景产品同台竞争。
JScript也是一种JavaScript实现，这两个JavaScript语言版本在浏览器端共存意味着语言标准化的缺失，发展初期，JavaScript的标准并未确定，同期有
网景的JavaScript，微软的JScript双峰并峙。除此之外，微软也在网页技术上加入了不少专属对象，使不少网页使用非微软平台及浏览器无法正常显示，导致
在浏览器大战期间网页设计者通常会把“用Netscape可达到最佳效果”或“用IE可达到最佳效果”的标志放在主页。随着Internet Explorer 4的发布，微软引入
了动态HTML的概念，但语言实现和不同专有化的文档对象模型的差异仍然存在，成为网络上普及使用JavaScript的阻碍。

* 标准化

1996年11月，网景正式向ECMA（欧洲计算机制造商协会）提交语言标准。1997年6月，ECMA以JavaScript语言为基础制定了ECMAScript标准规范ECMA-262。
JavaScript成为了ECMAScript最著名的实现之一。除此之外，ActionScript和JScript也都是ECMAScript规范的实现语言。尽管JavaScript作为给非程序
人员的脚本语言，而非作为给程序人员的脚本语言来推广和宣传，但是JavaScript具有非常丰富的特性。

## javaScript 的诞生记

### 诞生背景

1994年，网景公司（Netscape）发布了Navigator浏览器0.9版。这是历史上第一个比较成熟的网络浏览器，轰动一时。但是，这个版本的浏览器只能用来浏览，
不具备与访问者互动的能力。......网景公司急需一种网页脚本语言，使得浏览器可以与网页互动。

网页脚本语言到底是什么语言？网景公司当时有两个选择：一个是采用现有的语言，比如Perl、Python、Tcl、Scheme等等，允许它们直接嵌入网页；另一个是发明一种全新的语言。

这两个选择各有利弊。第一个选择，有利于充分利用现有代码和程序员资源，推广起来比较容易；第二个选择，有利于开发出完全适用的语言，实现起来比较容易。

到底采用哪一个选择，网景公司内部争执不下，管理层一时难以下定决心。

就在这时，发生了另外一件大事：1995年Sun公司将Oak语言改名为Java，正式向市场推出。

Sun公司大肆宣传，许诺这种语言可以"一次编写，到处运行"（Write Once, Run Anywhere），它看上去很可能成为未来的主宰

网景公司动了心，决定与Sun公司结成联盟。它不仅允许Java程序以applet（小程序）的形式，直接在浏览器中运行；甚至还考虑直接将Java作为脚本语言嵌入网页，
只是因为这样会使HTML网页过于复杂，后来才不得不放弃。

总之，当时的形势就是，网景公司的整个管理层，都是Java语言的信徒，Sun公司完全介入网页脚本语言的决策。因此，Javascript后来就是网景和Sun两家公司一起
携手推向市场的，这种语言被命名为"Java+script"并不是偶然的。

### 发明人：Brendan Eich

此时，34岁的系统程序员Brendan Eich登场了。1995年4月，网景公司录用了他。

Brendan Eich的主要方向和兴趣是函数式编程，网景公司招聘他的目的，是研究将Scheme语言作为网页脚本语言的可能性。Brendan Eich本人也是这样想的，以为
进入新公司后，会主要与Scheme语言打交道。

仅仅一个月之后，1995年5月，网景公司做出决策，未来的网页脚本语言必须"看上去与Java足够相似"，但是比Java简单，使得非专业的网页作者也能很快上手。这个
决策实际上将Perl、Python、Tcl、Scheme等非面向对象编程的语言都排除在外了。

Brendan Eich被指定为这种"简化版Java语言"的设计师。

但是，他对Java一点兴趣也没有。为了应付公司安排的任务，他只用10天时间就把Javascript设计出来了。由于设计时间太短，语言的一些细节考虑得不够严谨，导致
后来很长一段时间，Javascript写出来的程序混乱不堪。如果Brendan Eich预见到，未来这种语言会成为互联网第一大语言，全世界有几百万学习者，他会不会多花一点时间呢？

### 设计思路

总的来说，他的设计思路是这样的：

```
* 借鉴C语言的基本语法；
* 借鉴Java语言的数据类型和内存管理；
* 借鉴Scheme语言，将函数提升到"第一等公民"（first class）的地位；
* 借鉴Self语言，使用基于原型（prototype）的继承机制。
```

所以，Javascript语言实际上是两种语言风格的混合产物----（简化的）函数式编程+（简化的）面向对象编程。这是由Brendan Eich（函数式编程）与网景公司（面向对象编程）共同决定的。

### Brendan Eich的观点

多年以后，Brendan Eich还是看不起Java。

他说：

```
  "Java（对Javascript）的影响，主要是把数据分成基本类型（primitive）和对象类型（object）两种，比如字符串和字符串对象，
  以及引入了Y2K问题。这真是不幸啊。"
```

把基本数据类型包装成对象，这样做是否可取，这里暂且不论。Y2K问题则是直接与Java有关。根据设想，Date.getYear()返回的应该是年份的最后两位：

```
  var date1 = new Date(1999,0,1);

　var year1 = date1.getYear();

　alert(year1); // 99
```

但是实际上，对于2000年，它返回的是100！

```
  var date2 = new Date(2000,0,1);

　var year2 = date2.getYear();

　alert(year2); // 100
```

如果用这个函数生成年份，某些网页可能出现"19100"这样的结果。这个问题完全来源于Java，因为Javascript的日期类直接采用了java.util.Date函数库。Brendan Eich显然
很不满意这个结果，这导致后来不得不添加了一个返回四位数年份的Date.getFullYear()函数。

如果不是公司的决策，Brendan Eich绝不可能把Java作为Javascript设计的原型。作为设计者，他一点也不喜欢自己的这个作品：

```
  "与其说我爱Javascript，不如说我恨它。它是C语言和Self语言一夜情的产物。十八世纪英国文学家约翰逊博士说得好：'它的优秀之处并非原创，
  它的原创之处并不优秀。'（the part that is good is not original, and the part that is original is not good.）"
```

## javaScript 的十个设计缺陷

有三个客观原因，导致Javascript的设计不够完善。

* 设计阶段过于仓促
* 没有先例
* 过早的标准化

### 1. 不适合开发大型程序

Javascript没有名称空间（namespace），很难模块化；没有如何将代码分布在多个文件的规范；允许同名函数的重复定义，后面的定义可以覆盖前面的定义，很不利于模块化加载。

### 2. 非常小的标准库

Javascript提供的标准函数库非常小，只能完成一些基本操作，很多功能都不具备。

### 3. null和undefined

null属于对象（object）的一种，意思是该对象为空；undefined则是一种数据类型，表示未定义。

```
  typeof null; // object

　typeof undefined; // undefined
```

两者非常容易混淆，但是含义完全不同。

```
  var foo;

　alert(foo == null); // true

　alert(foo == undefined); // true

　alert(foo === null); // false

　alert(foo === undefined); // true
```

在编程实践中，null几乎没用，根本不应该设计它。

### 4. 全局变量难以控制

Javascript的全局变量，在所有模块中都是可见的；任何一个函数内部都可以生成全局变量，这大大加剧了程序的复杂性。

```
  a = 1;

  (function(){

    b=2;

    alert(a);

  })(); // 1

  alert(b); //2
```

### 5. 自动插入行尾分号

Javascript的所有语句，都必须以分号结尾。但是，如果你忘记加分号，解释器并不报错，而是为你自动加上分号。有时候，这会导致一些难以发现的错误。

比如，下面这个函数根本无法达到预期的结果，返回值不是一个对象，而是undefined。

```
  function(){
    return
      {
        i=1
      };
  }
```

原因是解释器自动在return语句后面加上了分号。

```
  function(){
    return;
      {
        i=1
      };
  }
```

### 6. 加号运算符

+号作为运算符，有两个含义，可以表示数字与数字的和，也可以表示字符与字符的连接。

```
  alert(1+10); // 11

  alert("1"+"10"); // 110
```

如果一个操作项是字符，另一个操作项是数字，则数字自动转化为字符。

```
  alert(1+"10"); // 110

  alert("10"+1); // 101
```

这样的设计，不必要地加剧了运算的复杂性，完全可以另行设置一个字符连接的运算符。

### 7. NaN

NaN是一种数字，表示超出了解释器的极限。它有一些很奇怪的特性：

```
  NaN === NaN; //false

　NaN !== NaN; //true

　alert( 1 + NaN ); // NaN
```

与其设计NaN，不如解释器直接报错，反而有利于简化程序。

### 8. 数组和对象的区分

由于Javascript的数组也属于对象（object），所以要区分一个对象到底是不是数组，相当麻烦。

```
  if ( arr &&
    typeof arr === 'object' &&
    typeof arr.length === 'number' &&
    !arr.propertyIsEnumerable('length')){

    alert("arr is an array");

  }
```

### 9. == 和 ===

==用来判断两个值是否相等。当两个值类型不同时，会发生自动转换，得到的结果非常不符合直觉。

```
  "" == "0" // false

  0 == "" // true

  0 == "0" // true

  false == "false" // false

  false == "0" // true

  false == undefined // false

  false == null // false

  null == undefined // true

  " \t\r\n" == 0 // true
```

因此，推荐任何时候都使用"==="（精确判断）比较符。

### 10. 基本类型的包装对象

Javascript有三种基本数据类型：字符串、数字和布尔值。它们都有相应的建构函数，可以生成字符串对象、数字对象和布尔值对象。

```
  new Boolean(false);

  new Number(1234);

  new String("Hello World");
```

与基本数据类型对应的对象类型，作用很小，造成的混淆却很大。

```
  alert( typeof 1234); // number

　alert( typeof new Number(1234)); // object  
```

关于Javascript的更多怪异行为，请参见Javascript Garden和wtfjs.com。
