# JS 对象基本用法

## 申明对象的两种语法

* 标准语法

```
  var obj = new Object()
```

* 简洁语法

```
  var obj = {}
```

## 如何删除对象的属性

* 使用关键字 delete 删除对象的属性

```
  var obj = {name: 'hs', age: 25}
  
  delete obj.age  //删除成功，返回true
  
  console.log(obj.age) // undefined
```

## 如何查看对象的属性

* 查看对象属性名 -- 使用Object.keys()，遍历对象所有自身属性。

```
  var obj = {name: 'hs', age: '25'}
  
  Object.keys(obj) // 输出 ["name", "age"]
```

* 查看对象属性的值 -- 使用Object.values()，遍历对象所有自身属性的值。

```
  var obj = {name: 'hs', age: '25'} 
  
  Object.values(obj) // 输出 ["hs", "25"]
```

* 查看对象属性名与属性值 -- 使用Object.entries()，遍历对象所有自身属性名与属性值。

```
  var obj = {name: 'hs', age: '25'} 
  
  Object.entries(obj) // 输出 [["name", "hs"], ["age", "25"]]
```

## 如何修改或增加对象的属性

* 给对象某个属性赋值，对象已存在该属性则为修改，不存在该属性即为添加该属性。

```
  var obj = {}
  
  obj['name'] = 'hs'
  
  obj.age = '25'
```

* 大量修改对象的属性使用Object.assign()，第一个参数为要修改的对象，第二个参数为要修改的属性，原对象不存在对应属性即为添加属性，否则会覆盖掉原对象的原有属性。

```
  var obj = {name: 'hs', age: '25', sex: 'male'}
  
  Object.assign(obj, {name: 'md', age: '18', sex: 'male', hobby: 'music'})
  // obj被修改为obj = {name: 'md', age: '18', sex: 'male', hobby: 'music'}
```

## 'name' in obj和obj.hasOwnProperty('name') 的区别

* in 操作符和obj.hasOwnProperty()方法都可以判断某个属性是否存在与某个对象之中。

```
  var obj = {name: 'hs', age: '25'}
  
  'name' in obj // 返回true
  
  obj.hasOwnProperty('name') //返回true
```

* in 操作符不能判断属性是否是对象的自身属性

```
  var obj = {name: 'hs', age: '25'}
  
  'toString' in obj //返回true，（原型链上的属性）
```

* obj.hasOwnProperty()方法可以精确判断属性是否是对象的自身属性

```
  var obj = {name: 'hs', age: '25'}
  
  obj.hasOwnProperty('name') //返回true
  
  obj.hasOwnProperty('toString') //返回false
```
