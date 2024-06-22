---
profileName: Estruswent
postId: "2375"
postType: post
categories:
  - 44
---
# how to start writing in LaTeX

这是一篇简短的笔记，是我在之前的课程中关于辅学lec4-latex的课程收获。

## 一、文章结构

- 文档类型声明  
  `\documentclass{<type>}`  

- 导言区  
  1. title & author & date  
     `\title`代表标题，用法：`\title{<the title of the article>}`  
     `\author`代表作者，用法：`\author{<the author of the work>}`  
     `\date`代表日期，用法：`\date{the date of the work}`  
  2. package  
     `\usepackage`相当于引用第三方库，实现更多元化的拓展功能。  
     用法：`\usepackage{<the package you want to include>}`  
  3. linespread  
     `\linespread`代表全局行距设置，后续在文本中也是无法局部修改的。  
     可以有多种单位，用法：`\linespread{<distance>}`。  

- 正文区  
  将在这里书写文章正文部分，有很多用法将在第二部分写出  

## 二、用法

- 注释  
  使用`%`来进行注释，类似C语言中的`//`。  

- 换行、分段与断页  
  使用`\\`或者`\newline`强制换行，但是不会另起一段。  
  使用`\par`实现分段，就观测来看是有缩进的。  
  使用`\newpage`实现强制断页。  
  使用`\clearpage`不仅会实现强制断页，还会清除浮动体。  

- 字体与字号  
  使用`{\bfseries <text>}` & `\textbf{<text>}`来完成字体与字号的调试，但不要滥用。  
  e.g.1 This is a {\Large large cat} and that is a {\small small cat}.  
  e.g.2 This is \textbf{B} and that is \textit{I}.  
  e.g.1 This is a {\Large large cat} and that is a {\small small cat}.  
  e.g.2 This is **B** and that is *I*.  

- 字符与标点  
  1. 特殊字符转义  
     使用`\`对某些特殊字符转义，因为这些特殊字符可能有别的含义。  
     e.g.1 `\_`、`\%`、`\$`、`\&`、`\{`、`\}` 等。  
     e.g.2 `\~{}`、`\^{}` 带大括号防止将后面的字符理解为参数。  
  2. `- -- ---`  
     使用`-`代表连接号  
     使用`--`代表短破折号  
     使用`---`代表长破折号  
  3. 防止西文连字  
     使用`{}`实现字母的分隔，防止连在一块。  
     e.g. `difficult dif{}f{}icult`  
     e.g. difficult dif{}f{}icult  

- 行距与间距的设置  
  使用`{\linespread{<distance>}\selectfont <text>}`来调整局部的行距。  
  使用`\quad \qquad`分别水平间隔一个m字母和两个m字母的距离。  
  使用`\hspace{<length>}`插入水平的间距。  
  使用`\vspace{<distance>}`插入垂直的间距。