---
title: Markdown学习笔记
date: 2019-08-29 23:25:52
categroies: log
thumbnail: /gallery/thumbnail/markdown.png
tags: 
- 博客建设 
- Markdown
---
## Introduction
>接下来我将会以简单明了的方式介绍Markdown的语法，介绍的过程也是我学习实践的过程，这也是我第一次全文用*Markdown*语法书写文章，还很生疏，有些语法可能也还不太了解，所以会有翻车的现象。

`Markdown` 由 John Gruber 在2004年创建，至今已经是12年的时间。这门语言的宗旨是**易读易写**，而它的语法也确实如此，简单强大！接下来开始学习！
<!--more-->
## 基本写作
### 1. 标题
标题分为6级，如下
>#一级标题<br>
##二级标题<br>
###三级标题<br>
####四级标题<br>
#####五级标题<br>
######六级标题<br>

效果如下

# 一级标题<br>
## 二级标题<br>
### 三级标题<br>
#### 四级标题<br>
##### 五级标题<br>
###### 六级标题<br>
***
### 2.强调
>*斜体*---包括在两个 ‘*’或‘_’ 之间的字符<br>
**黑体**---包括在两个‘**’或‘__’之间的字符<br>
~~删除线~~---包括在两个‘~~'之间的字符<br>
*全部复合*使用（有待补充）

### 3.列表
>无序列表
* 苹果
* 香蕉
>有序列表
1. 苹果
2. 香蕉
### 4.引用
引用如下
>这里面是引用的内容，通过在段前添加‘>’符号开始引用段落，在此段后空一行即结束引用，在段落间使用
>>这是嵌套引用
>>>这也是
### 5.代码
>`print 'Hello world'`
>>在两个反引号‘`’之间为行内代码

```
def function(x):
    return x^2
```
>在连用三个反引号‘`’之间的符号为代码区块，如上所示
### 6.分割线
>如下（连续三个或以上‘*’），即表示分割线
***
>或者如下（空一行，连续三个或以上‘-’）

---
### 7.表格
通过如下方式可以渲染出表格
```
|table|head|here|
|:-----|:-----:|-----:|
|content1|content2|content3|
|content1|content2|content3|
|content1|content2|content3|
```
>效果如下

|table|head|here|
|:-----|:-----:|-----:|
|content1|content2|content3|
|content1|content2|content3|
|content1|content2|content3|
### 8.图片
![Von Gogh](./Markdown简易教程/Von_Gogh.jpg)
`![Von Gogh](./Markdown简易教程/Von_Gogh.jpg)`
>就是上面这段格式的代码就是引用了这张梵高的图片了，注意的是其中的图片的地址，这个是同级目录下的直接引用，属于相对目录，也可以用绝对路径，不管相对还是绝对，路径一定要准确，这样才能定位到需要引用的图片上，才能展示出来
### 9.链接
>链接就是比上面的图片的引用少了前面的‘！’，去掉这个感叹号后，再把需要的链接URL放在后面的括号里就可以了<br>
`[My github page site](https://genening.github.io)`

[My github page site](https://genening.github.io)
或者[百度首页](http://www.baidu.com )
### 10.公式
>公式的展示是采用LaTeX的语法，通过[这个网站](https://www.codecogs.com/latex/eqneditor.php)
可以把公式对应的LaTeX的写法转换出来

如下为行内公式
>`$E=mc^2$`对应 $E=mc^2$ 有待尝试

如下为公式块

```
$$
e^{i\theta} = \cos \theta +i\sin \theta \
e^z = 1 + \frac{z}{1!} + \frac{z^2}{2!} + \frac{z^3}{3!} + \cdots = \sum_{n=0}^{\infty}\frac{z^n}{n!}
$$
```
>效果出不来，比较尴尬

### 11.反斜线
>如果想插入一些特殊字符的话需要转义符号反斜线‘\’，引入这个反斜线后，就可以使用上面的那些特殊的字符了，这样不会触发对应的渲染效果
>>\反斜线<br>
\`反引号<br>
\*星号<br>
\_底线<br>
\{}花括号<br>
如上符号等等

### 12.脚注
脚注可以用于编辑参考文献
>1. `在文中使用[^1]的方式标记脚注`<br>
>2. `在文末使用[^1]:加入参考文献，注意要使用英文冒号，后面有无空格均可`

效果如此[^1]，或者是参考文献[^1]:
>此处尝试又出bug了，接着完善
## 结语
*Markdown*是所谓的**轻量标记语言**(lightweight markup language)，它可以让我们在写文章的时候专注于写作本身，而不用费心于排版，这种思想和*LaTeX*的思想不谋而合。现在很多网站都支持*Markdown*，也有很多相应的编辑软件，例如`Typora`，这是个很好用的*Markdown*的编辑软件。<br>
另外，让*Markdown*更强大的是，*Markdown*支持直接插入**HTML**的语法，也能插入**LaTeX**的语法，这样的扩展能力，让*Markdown*即满足了轻便易用的基础上，进一步增强了能力，这也是*Markdown*现在炙手可热的原因之一。
