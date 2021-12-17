## typora使用教程

### 一、简介

相比较world这种文档编辑器而言，Typora更适合写一些程序相关的博客，因为可以用代码+快捷键的方式，方便的对文章内容进行处理，不用在担心排版和样式变形的问题了，在编辑的过程中，就能预览到效果。

------



### 二、下载

进入Typora官网下载，[点击进入](https://www.oschina.net/action/GoToLink?url=https%3A%2F%2Ftypora.io%2F)。

------



### 三、常用快捷键

- 加粗： <kbd>Ctrl</kbd> + <kbd>B</kbd>
- 替换： <kbd>Ctrl</kbd> + <kbd>H</kbd>
- 撤销： <kbd>Ctrl</kbd> + <kbd>Z</kbd>
- 插入链接：<kbd>Ctrl</kbd> + <kbd>K</kbd>
- 插入图片：<kbd>Ctrl</kbd> + <kbd>ShifIt</kbd> + <kbd>I</kbd>
- 插代码块：<kbd>Ctrl</kbd> + <kbd>ShifIt</kbd> + <kbd>K</kbd>
- 显示大纲：<kbd>Ctrl</kbd> + <kbd>ShifIt</kbd> + <kbd>L</kbd>
- 切换源代码：<kbd>Ctrl</kbd> + <kbd>/</kbd>

------



### 四、块元素



#### 4.1 标题级别

<kbd>#</kbd> 一级标题， 快捷键为 <kbd>Ctrl</kbd> + <kbd>1</kbd>

<kbd>#</kbd><kbd>#</kbd> 二级标题，快捷键为 <kbd>Ctrl</kbd> + <kbd>2</kbd>

<kbd>#</kbd><kbd>#</kbd><kbd>#</kbd><kbd>#</kbd><kbd>#</kbd><kbd>#</kbd> 六级标题，快捷键为 <kbd>Ctrl</kbd> + <kbd>6</kbd>

注意：回车下行自动排序。

------



#### 4.2 引用文字

<kbd>></kbd> + <kbd>spacebar</kbd>



#### 4.3 列表

- 无序列表： <kbd>+</kbd> 或 <kbd>-</kbd> + <kbd>spacebar</kbd>
- 有序列表：<kbd>1</kbd><kbd>.</kbd> + <kbd>spacebar</kbd>

注意：回车下行自动排序。

------



#### 4.4 代码块

快捷键：<kbd>Ctrl</kbd> + <kbd>ShifIt</kbd> + <kbd>K</kbd>

语法：<kbd>~</kbd><kbd>~</kbd><kbd>~</kbd> + <kbd>Enter</kbd> 在后面选择一个语言名称可语法高亮。

------



#### 4.5 数学表达式

语法：`$` `$` + <kbd>Enter</kbd>

效果：

V1×V2=∣∣ijk ∂X∂u∂Y∂u0 ∂X∂v∂Y∂v0 ∣∣$$tep1V1×V2=|ijk ∂X∂u∂Y∂u0 ∂X∂v∂Y∂v0 |$$tep1



------



#### 4.6 表格

语法：`| 1 | 2 |` + <kbd>Enter</kbd>，即可将创建一个两行两列的表，表格左上右上角有扩展功能。

注意：插入表格需要顶头写，不然显示不出来。

效果：

| 标题1 | 标题2 |
| ----- | ----- |
| 内容1 | 内容2 |

------



#### 4.7 目录

语法：<kbd>toc</kbd> + <kbd>Enter</kbd>标题内容自动更新。

------



#### 4.8 代码标记

快捷键：<kbd>Shift</kbd> + <kbd>Alt</kbd> + <kbd>`</kbd>

语法：双<kbd>`</kbd>引起来。

------



### 五、链接

跨度元素即图片，网址，视频等，在Typora中输入后，会立即载入并呈现。



#### 5.1 超链接

快捷键：<kbd>Ctrl</kbd> + <kbd>K</kbd>

这是一个带有标题属性的链接：`[链接说明](http://example.com/ "标题")`

这是一个没有标题属性的链接：`[链接说明](http://example.net/)`

------



#### 5.2 图片

快捷键：<kbd>Ctrl</kbd> + <kbd>ShifIt</kbd> + <kbd>L</kbd>

`![显示的文字](/path/to/img.jpg)` `![显示的文字](/path/to/img.jpg "图片标题")`

------



#### 5.3 视频

`< video src=”xxx.mp4” />`

------



### 六、文字符号



#### 6.1 倾斜

快捷键：<kbd>Ctrl</kbd> + <kbd>I</kbd>

语法：`* `内容 `*`

效果：*单个星号*

------



#### 6.2 加粗

快捷键：<kbd>Ctrl</kbd> + <kbd>B</kbd>

语法：`**` 内容 `**`

效果：**两个星号**

------



#### 6.3 删除线

快捷键：<kbd>ShifIt</kbd> + <kbd>Alt</kbd> + <kbd>5</kbd>

语法：`~~`内容`~~`

效果：删除线

------



#### 6.4 下划线

快捷键：<kbd>Ctrl</kbd> + <kbd>U</kbd>

语法：`<u>`内容`</u>`

效果：<u>下划线</u>

------



#### 6.5 分割线

语法：`*** `或 `---` + <kbd>Enter</kbd>

------



#### 6.6 表情符号

typora 会在你键入 <kbd>:</kbd> 的时候根据你输入的单词匹配表情。

输入：`:happy:` 、`:cry:` 、`:smile:` 等等就能获得相应的表情。

效果：:happy: :cry: :sweat_smile:

------



#### 6.7 上下标，高亮显示

注意：需要在设置中打开

上标：X2 方法：`字母+^+数字+^`

下标：H2O 方法：`字母+~字母~+字母`

高亮：高亮 方法：`==文字==`

------



#### 6.8 脚注

- 脚注：`[^1]`
- 注释内容：`[^1]:`

注意：脚注标识是1，标识可以为字母数字下划线，不支持中文。脚注内容可为任意字符，包括中文。

------



### 七、支持的 HTML 元素



#### 7.1 文本居中

语法：`<center>` 内容 `</center>`

效果：

<center>这是要居中的内容</center>

------



#### 7.2 快捷键显示

语法：`<kbd> `内容 `</kbd>`

效果：<kbd>Ctrl</kbd><kbd>Enter</kbd><kbd>123</kbd>

------



#### 7.3 加粗

语法：`<b>` 加粗`</b>`

效果：<b>粗了</b>

------



#### 7.4 倾斜

语法：`<i>` 倾斜 `</i>`

效果：<i> 斜了 </i>

------



#### 7.5 上下标

语法：`<sup>`123hi你好`</sup>`

语法：`<sub>`321hi你好`</sub>`

效果：<sup>123hi你好</sup> / <sub>321hi你好



- 转自 https://my.oschina.net/u/4302665/blog/3313248?hmsr=kaifa_aladdin

### 