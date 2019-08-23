# MarkDown 
> Markdown 是一种轻量级标记语言。它是一种标准、一种语言，而非特定的软件。

## 支持 Markdown 的编辑器
#### Windows
- [Sublime Text 3](https://www.sublimetext.com/3), 强大优雅的编辑器。
- [MarkdownPad](http://markdownpad.com/)，一款可以直接预览排版效果的编辑器。
#### Mac
- [Ulysess](https://ulysses.app/)，专注写作的编辑器，功能强大，体验一流。
- [Macdown](https://macdown.uranusjr.com/)，可以预览排版效果。
#### Linux
- [VIM](https://www.vim.org/)，编辑器之神。
- [Emacs](https://www.gnu.org/software/emacs/), 神的编辑器。
- [ReText](https://sourceforge.net/projects/retext/)，可以预览。

---
## Markdown 语法
```text
注意：
1. 另起一段时，需要多敲一次回车键，来在段落之间添加一个空行。
```

#### 标题
```text
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题
```

#### 无序列表
```text
加号“+”或减号“-”都可以作为列表标记，后面要跟一个空格
```
例：
+ 2 
- 4 

#### 有序列表
```text
使用数字、一个英文句号和一个空格即可
```
例： 
1. A
2. B

#### 图片
```text
感叹号、方括号和圆括号
![Alt text](/path/to/img.jpg)
```

#### 链接
```text
方括号写下链接文字，圆括号写下网址。
[text](http://xxx)

```
#### 引用
```text
使用">" 标记来引用其他人的言论、书籍或报纸的内容。

引用可以嵌套，只要根据层次的不同，加上不同数量的 > 即可：

> 这是第一级引用。

>> 这是第二级引用。

> 现在回到第一级引用。

```

#### 斜体
```text
使用 * 和 _ 来表示斜体和加粗。

**的**
_的_

```

#### 分割线
```text
连续三个减号"-"
```

#### 表格
```text
在表头下方的分隔线标记中加入 :，
即可标记下方单元格内容的对齐方式：
:--- 代表左对齐
:--: 代表居中对齐
---: 代表右对齐

header 1 | header 2
---|---
row 1 col 1 | row 1 col 2
row 2 col 1 | row 2 col 2

```
例： 

dog | bird | cat
----|------|----
foo | foo  | foo
bar | bar  | bar
baz | baz  | baz


#### 待办清单
```text
- [x] 已完成项目1
  - [x] 已完成事项
  - [ ] 代办事项
- [ ] 代办项目2
- [ ] 代办项目3

```
例：
- [x] 已完成项目1
  - [x] 已完成事项
  - [ ] 代办事项
- [ ] 代办项目2
- [ ] 代办项目3

#### 上标
```text
<sup>xxx</sup>
```
例：
1. A<sup>xxx</sup>
2. n<sup>2</sup>=n+1

#### 下标
```text
<sub>xxx</sub>
```
例：
1. a=log<sub>2</sub>b

#### 注册商标的符号
```text
&reg;
```
例： &reg;

#### function符号
```text
&fnof;
```
例： &fnof;(x)=x+1

#### 根号
```text
&radic;
```
例： &radic;5

#### 角度符号
```text
&deg;
```
例： 30&deg;

#### 空格
```text
&nbsp;
```

## 其他

[Markdown 语法说明](http://www.markdown.cn/)
