# JS 语法

## 1. 表达式与语句

* 表达式 

表达式一般都是可计算出值的，下面两种都是表达式：

```
  1 + 2
  
  fn(1,2)
  
```

* 语句

语句可能有值也可能没有，语句一般会改变当前环境（变量申明/赋值）：

```
  var a = 1
  
  var obj = {x: 1}
```

## 2. 标识符的规则

* 标识符就是指变量、函数、属性的名字，或者是函数的参数。
* 第一个字符必须是一个字母、下划线（_）、美元符（$）或中文。
* 其他字母可以是以上几种或是数字。

## 3. if else语句

```if (condition) statement1 else statement2 ```

* condition是判断条件，可以是任意表达式，为非布尔值时会自行转换为布尔值。
* statement1和statement2为可执行语句。条件为true时执行statement1，否则执行statement2。

```
  if(score > 60){
    console.log('及格')
  }else {
    console.log('不及格')
  }
```

## 4. while / for语句

* while语句是前测试循环语句，在循环体执行之前就会对出口条件做判断。因此循环体内的代码可能一次都不执行。

```
  var i = 0;
  
  while(i < 10) {
    i += 1
  }
```

* do while语句是后测试循环语句，也就是在循环体代码执行之后，才对出口条件做判断，因此循环体内代码至少执行一次。

```
  var i = 0;
  do{
    i += 2
  } while (i < 10);
```

* for语句也是前测试循环语句，但它具有在执行循环之前初始化变量和定义循环后要执行的代码的能力。

```
  for(var i = 0; i < 10; i++) {
    console.log(i)
  }
```

## 5. break 和 continue

* break语句和continue语句用于在循环中精确地控制代码的执行。break会立刻退出循环，强制执行循环后面的语句。而continue虽然也是立刻退出循环，
但只是跳过循环的当前迭代，会重新回到循环体顶部继续执行。

```
  var num = 0;
  
  for(var i = 0;i < 10; i++) {
    if(i == 5) {
      break;
    }
    num++;
    console.log(num) //num输出为4
  }
```

```
  var num = 0;
  
  for(var i = 0; i < 10; i++) {
    if(i == 5) {
      continue;
    }
    num++;
    console.log(num) //num输出为8
  }
```

## 6. lable语句

* 使用lable可以在代码中添加标签，以便将来使用。

```
  var num = 0;
  
  outside: 
  for(var i = 0; i < 10; i++) {
    inside:
    for(var j = 0; j< 10, j++) {
      if(i == 5 && j == 5) {
        break outside
      }
      num++
      console.log(num) //输出55
    }
  }
```

```
  var num = 0;
  
  outside: 
  for(var i = 0; i < 10; i++) {
    inside:
    for(var j = 0; j< 10, j++) {
      if(i == 5 && j == 5) {
        continue outside
      }
      num++
      console.log(num) //输出95
    }
  }
```

outside 和inside 就是标签，配合break和continue在多层循环时使用，可以很好指定退出哪一层的循环。




