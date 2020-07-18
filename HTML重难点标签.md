# 1. a标签

## 作用

* 跳转到外部页面
* 跳转到内部锚点
* 跳转到邮箱或者电话等

## 属性

### href 

##### 1. 网址

* https://xxx.com
* http://xxx.com
* //xxx.com

##### 2. 路径

* 绝对路径
* 相对路径

##### 3. 伪协议

* javascript:(0);
* mailto: email address
* tel: phone number

##### 4. id

* href = #id

### target

##### 1. 内置的名字

* _blank -- 在新标签页打开
* _top -- 在顶部窗口打开 
* _parent -- 在父级窗口打开
* _self -- 在本身的窗口打开

##### 2. 程序员命名

* window的name
* iframe的name

### download

作用：是下载页面，而不是打开页面。（不是所有浏览器都支持，特别是手机浏览器）

### rel = noopener

暂不做介绍

# 2. img标签

## 作用

* 发送get请求，展示一张图片

## 属性

### alt 

* 对图片的描述，当图片加载失败时的可替换文本。

### height

* 设置图片的高估

### width

* 设置图片的宽度

### src

* 图片的文件路径（可以是绝对路径，也可是相对路径）

## 事件

### onload

* 图片加载成功时的触发该事件 `onoload = () => {}`

### onerror

* 图片加载失败时的触发该事件 `onerror = () => {}`

## 响应式

* `max-width: 100%;`

## 可替换元素

* 准备一张备用图片（404.png）当原图正常成功，就没404.png什么卵事了。当原图无法正常失败，就加载404.png。

```
onload = () => {
    console.log('加载成功')
}

onerror = () => {
    console.log('加载失败')
    src = '404.png'
}
```

# 3. table标签

## 相关的标签

* table
* thead
* tbody
* tfoot
* tr
* td
* th

## 相关的样式

* table-layout
* border-collapse
* border-spacing

# 4. form标签

## 作用

* 发送get/post请求，然后刷新页面。

## 属性

### action

* 处理表单提交的URL

### autocomplete

* 自动完成属性（通常，值来自用户输入的过去值）

### method 

##### get

* 表单数据会附加在action属性的URL中，并以 '?' 作为分隔符，没有副作用时使用这个方法。

##### post

* 指的是HTTP POST方法；表单数据会包含在表单体内然后发送给服务器。

##### dialog

* 如果表单在`<dialog>`元素中，提交时关闭对话框。

### target

* _self -- 在本窗口响应信息
* _blank -- 在新标签页响应信息
* _parent -- 在父级窗口响应信息
* _top -- 在顶层窗口响应信息

## 事件

### onsubmit

* 点击提交按钮时触发该事件 `onsubmit = () => {}`

# 5. input标签

## 作用

* 让用户输入内容

## 属性

### type

* button
* checkbox
* radio
* email
* file 
* hidden
* number
* password
* search
* submit
* tel
* text

### 其他

* name
* autofocus
* checked
* disabled
* maxlength
* pattern
* value
* placeholder

## 事件

### onchange

* 当用户提交对元素值的更改时触发 `onchange = () => {}`

### onfocus

* 当元素获取焦点时触发 `onfocus = () => {}`

### onblur

* 当元素失去焦点时触发 `onblur = () => {}`

## 验证器

* 为input元素添加 required属性（HTML5新增功能）

# 6. 其他输入标签

## 标签

* select + option
* textarea
* label

## 注意事项

* 一般不监听input的click事件
* form里面的input要有name
* form里面要存在一个元素包含属性type = 'submit'才能触发submit事件

# 7. 其他标签

## 标签

* video
* audio
* canvas
* svg
* ...

## 注意事项

* 有些元素会存在兼容性问题，随用随查

