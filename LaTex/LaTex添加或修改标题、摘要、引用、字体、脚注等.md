## LaTex添加或修改标题、摘要、引用、字体、脚注等

### 为文章添加标题、作者、时间

```latex
\documentclass{article} %文档
\usepackage{ctex} %使用包，ctex指支持显示汉字
\title{文章标题} %文章标题
\author{作者名称} %作者名称
\data{\today} %今天的日期

%设置页面，例如A4纸大小，左右上下边距的信息
\usepackage[a4paper, left=10mm, right=10mm, top=15mm, bottom=15mm]{geometry}
\begin{document}
\maketitle %添加这句才能显示标题、作者等信息

正文

\end{document}
```

### 添加摘要

需要在`\maketitle`下添加内容，如下：

```latex
\maketitle
%摘要开始部分
\begin{abstract}
摘要内容
\end{abstract}
```

### 添加标题、段落、目录

* 正文的**标题**设置：一级标题`\section{}`，二级标题`\subsection{}`，三级标题`\subsubsection{}`；
* 正文的**段落**设置：在一段的最后添加`\par`表示一段的结束，而不是单纯地使用`\\`进行换行操作；
* 正文的目录设置：在`\begin{document}`内容中添加：`\tableofcontents`

```latex
\begin{document}
\maketitle
\renewcommand{\contentsname} %将content转为目录
\tableofcontents

\section{一级标题1}
段落1\par
段落2
\subsection{二级标题}
\subsubsection{三级标题}
\section{一级标题2}
\end{document}
```

### 改变文本字体、添加引用环境、脚注

* 使用脚注：在需要添加脚注的文字后添加`\footnote{脚注内容}`即可；
* 使用引用：`begin{quote}`即可；
* 改变字体：例如使用`{\fangsong}`，则是改变为仿宋字体；

```latex
\section{标题}
西游记\footnote{中国古典四大名著之一}小说开头写道：
\begin{quote}
{\kaishu 东胜神洲有一花果山，山顶一石，受日月精华，生出一石猴。之后因为成功闯入水帘洞，被花果山诸猴拜为“美猴王”。}
\end{quote}
```





















