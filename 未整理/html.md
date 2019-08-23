# HTML 超文本编辑语言
HTML良好的代码规范

使用正确的文档类型：
文档类型声明位于HTML文档的第一行：
```html
<!DOCTYPE html>
```

或者跟其他标签一样使用小写：
```html
<!doctype html>
```


使用小写元素名
推荐使用小写字符：
1. 混合了大小写的风格是非常糟糕的。
2. 开发人员通常使用小写（类似XHTML）
3. 小写风看起来更加清爽
4. 小写字符容易编写
推荐：
```html
<section>
    <p>这是一个段落。</p>
</section>
```


关闭所有HTML元素
建议每个元素都要添加关闭标签。

关闭空的HTML元素。
```html
<meta charset="utf-8" />
```


使用小写属性名：
推荐使用小写字母属性名：
1. 同时使用大小写是非常不好的习惯。
2. 开发人员通常使用小写（类似 XHTML）
3. 小写风格看起来更加清爽
4. 小写字母容易编写。
推荐：
```html
<div class="menu">
```


属性值：
属性值推荐使用引号：
1. 如果属性值含有空格需要使用引号
2. 混合风格不推荐，建议统一风格。
3. 属性值使用引号易于阅读。
```html
<table class="table striped">
```


空格和等号：
等号前后可以使用空格，但推荐少用空格：
```html
<link rel="stylesheet" href="styles.css">
```


空格和缩进：
1. 不要无缘无故添加空行。
2. 为每个逻辑功能块添加空行，这样更易于阅读。
3. 缩进使用两个空格，不建议使用tab。
4. 比较短的代码间不要使用不必要的空行和缩进。

元数据：
```html
<title>元素是必须的，标题名描述了页面的主题。
标题和语言可以让搜索引擎很快的了解你的主题。
```


HTML注释：
注释可以写
```html
<!-- 注释 -->
```


样式表：
样式表使用简洁的语法格式（type属性不是必须的）
```html
<link rel="stylesheet" href="styles.css">
```

短的规则可以写成一行:
```css
p.into {font-family: Verdana; font-size: 16em;}
```

长的规则可以写成多行:
```css
body {
  background-color: lightgrey;
  font-family: "Arial Black", Helvetica, sans-serif;
  font-size: 16em;
  color: black;
}
```

将左花括号与选择器放在同一行。
左花括号与选择器间添加一个空格。
使用两个空格来缩进。
冒号与属性值之间添加一个空格。
逗号和符号之后使用一个空格。
每个属性与值结尾都要使用分号。
只有属性值包含空格时才使用引号。
右花括号放在新的一行。
每行最多 80 个字符。
在逗号和冒号后添加空格是常见的一个规则。

在HTML中载入JavaScript
使用简洁的语法来载入外部的脚本文件 ( type 属性不是必须的 ):
```html
<script src="myscript.js">
```


使用JavaScript访问HTML元素
```javascript
var obj = getElementById("demo")
```

HTML中JavaScript尽量使用相同的命名格式。

使用小写文件名：
必须保持统一的风格，建议统一使用小写的文件名。

文件扩展名：
HTML文件后缀可以是.html或.htm
CSS文件后缀是.css
JavaScript文件后缀是.js