# LaTeX 笔记

!!! TODO
	好久没折腾LaTeX了，以后找机会一定重新学一下。

安装和VSCode配置参考了 [【TeXLive+VSCode LaTeX中文环境配置教程】](https://www.bilibili.com/video/BV1Gt4y117VD?vd_source=fb70993df833421086ba8589f9bd3ed1) 和视频中推荐的[知乎文章](https://zhuanlan.zhihu.com/p/38178015)。

!!! info "说明"
    以下内容均采用XeLaTeX编译。

### 最基础内容

```latex
\documentclass[UTF8]{ctexart}
% 百分号后面是注释
% 这里是导言区
\title{标题}
\author{作者}
\date{\today}

\begin{document}
% 这里开始是正文
\maketitle
\tableofcontents %目录
\section{Section}
\subsection{Subsection}
\subsubsection{Subsubsection}
\paragraph{before a paragraph}Text in a paragraph.
\end{document}
```

### 插入图片

导言区添加

```latex
\usepackage{graphicx} % 图片支持
\usepackage{float} % 图片强制放置，不然总是乱跑
\usepackage{caption} % 取消图片编号
```

在插入图片的地方放置

```latex
\begin{figure}[H]
	\centering
	\includegraphics[width=0.25\linewidth]{img/1.png}
	\caption*{对元件和输入图标进行重命名的方法} % 这个星号可以取消说明部分的编号
\end{figure}
```

### 插入代码块

最常用的方法应该是「minted」，但我嫌麻烦。导言区添加

```latex
\usepackage{listings} % 代码支持
```

导言区放一个`\lstset{}`用于调整代码风格，实现细节见附录。

正文引用代码处放置

```latex
\begin{lstlisting}
	Your Code Here
\end{lstlisting}
```

### 插入行内代码

```latex
\verb|Your Code Here|
```

### 页眉页脚

导言区

```latex
\pagestyle{empty}%取消页眉页脚
\pagestyle{plain} %无页眉，页脚为居中页码
```

参见[这里](https://www.latexstudio.net/archives/7985.html)

如果想要更复杂的效果，可以采用`fancyhdr` 宏包

### 小节标题靠左

导言区

```latex
\usepackage{titlesec}
\titleformat*{\section}{\Large\bfseries\raggedright}
```

### 行间距调整

导言区放置

```latex
\usepackage{setspace}
\linespread{1.5} % 行距调整
```

### 段间距调整

导言区放置如下内容，增加0.4em

```latex
\addtolength{\parskip}{.4em}
```

### 列表

正文插入有序列表：

```latex
\begin{enumerate}
	\item A
	\item B
\end{enumerate}
```

正文插入无序列表：

```latex
\begin{itemize}
	\item A
	\item B
\end{itemize}
```

### 加粗与斜体

```latex
\textbf{内容} % 加粗
\emph{内容} % 斜体
```

### 标红

导言区放置

```latex
\usepackage{color}
```

文本：

```latex
\textcolor{red}{文本}
```

### 公式

符号列表可以参考：[https://www.cmor-faculty.rice.edu/~heinken/latex/symbols.pdf](https://www.cmor-faculty.rice.edu/~heinken/latex/symbols.pdf)

引用公式块可采用如下两种方法，注意星号表示取消编号。

```latex
行内：$a^2+b^2=c^2$
多行：
\begin{equation *}
	a^2+b^2=c^2
\end{equation}
```

多行公式对齐：
```latex
\begin{align}
	A &= B \\
	&=C
\end{align}
```

### 图片转公式

免费但需要复杂的注册：[https://simpletex.cn/](https://simpletex.cn/)

### 公式转图片

这个公式转图片方式看起来还可以：[https://www.latexlive.com/](https://www.latexlive.com/)

### 表格

这个网站待尝试：[https://tablesgenerator.com/](https://tablesgenerator.com/)

#### Excel2LaTeX插件

[Excel2LaTeX插件](https://blog.csdn.net/qq_16763983/article/details/122912373)

[表线与单元格距离太近](https://www.zhihu.com/question/288695777/answer/3156283040)

[表格内文字换行](https://blog.csdn.net/weixin_47062807/article/details/127702779)





---

## 附录1：旧版内容

原先只放这些链接，后来发现不做笔记不行。

!!! info "注"
    从别处整理而来。只放来源链接。

快速上手使用 [简短教程](https://liam.page/2014/09/08/latex-introduction/) 和 [Overleaf的教程（英文）](https://www.overleaf.com/learn/latex/Free_online_introduction_to_LaTeX_(part_1))

#### 具体功能

[伪代码](https://zhuanlan.zhihu.com/p/166418214)，<font size=2> 注：这个方法的伪代码不能换页。</font>

[将不编号的章节列入目录](https://www.jianshu.com/p/9fda4ac51524)，<font size=2>注：思路一保存不生效，点击右上角Build Project才生效</font>

[Excel2LaTeX插件](https://blog.csdn.net/qq_16763983/article/details/122912373)

[表线与单元格距离太近](https://www.zhihu.com/question/288695777/answer/3156283040)

[表格内文字换行](https://blog.csdn.net/weixin_47062807/article/details/127702779)

[关于代码块](https://zhuanlan.zhihu.com/p/495840495) <font size=2>注：我采用的是第二种方法</font>

[代码块的设置](https://blog.csdn.net/qq_44885695/article/details/124258901) <font size=2>注：我用不了\lstset，只能写在\begin{lstlisting}后面的中括号里</font>

[listings宏包美化代码](https://zhuanlan.zhihu.com/p/464141424)

[绘制树图](https://blog.csdn.net/qq_33919450/article/details/127638969)

[添加脚注](https://blog.csdn.net/xovee/article/details/127563209)

---

## 附录2：我最常用的模板

我用得最多的是大二上学期的数逻课的模板。

```latex
\documentclass[UTF8]{ctexart}
\usepackage{geometry}%页边距调整
\usepackage{setspace}%行距调整
\usepackage{graphicx}%图片支持
\usepackage{xcolor} %代码着色
\usepackage{listings}%代码支持
\usepackage{float}%图片强制放置
\usepackage{underscore}%下划线支持
\usepackage{titlesec}%小节标题靠左
\usepackage{caption}%取消图片编号
\geometry{
	a4paper,
	left=3.18cm,
	right=3.18cm,
	top=2.54cm,
	bottom=2.54cm
}%页边距调整
%代码调整
\definecolor{mygreen}{rgb}{0,0.7,0}
\definecolor{mygray}{rgb}{0.5,0.5,0.5}
\definecolor{mymauve}{rgb}{0.58,0,0.82}
\linespread{1.5}%行距调整
\lstset{%代码风格
	backgroundcolor=\color{white},   % choose the background color
	basicstyle=\footnotesize, % size of fonts used for the code或改成\small\monaco稍大
	numbers=none,                        
	columns=flexible,
	breaklines=true,                 % automatic line breaking only at whitespace
	captionpos=b,                    % sets the caption-position to bottom
	tabsize=4,                       % 把tab扩展为4个空格，默认是8个太长
	commentstyle=\color{mygreen},    % 设置注释颜色
	keywordstyle=\color{blue},       % 设置keyword颜色
	stringstyle=\color{mymauve},     % string literal style
	emph={\enspace},
	emphstyle=\color{white},
	frame=single,                        % 设置有边框
	rulesepcolor=\color{red!20!green!20!blue!20},
	identifierstyle=\color{black},
	language = verilog,
}
\pagestyle{empty}%取消页眉页脚
\titleformat*{\section}{\Large\bfseries\raggedright}%小标题靠左
\begin{document}
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%封面部分，如不需要则直接注释掉
	\newgeometry{
		top=4cm,
	}
	\begin{figure}[H]
		\centering
		\includegraphics[scale=1.6]{img/logol}
	\end{figure}
	$ $%间隔
	\begin{center}
		\textbf{\Large 本科实验报告}
		
		\vspace{10ex}
		\Large
		课程名称：\underline{\hbox to 8cm{\hfill 数字逻辑设计\hfill}}\\
		\vspace{1ex}
		姓\qquad 名：\underline{\hbox to 8cm{\hfill  \hfill}}\\
		\vspace{1ex}
		学\qquad 院：\underline{\hbox to 8cm{\hfill 计算机科学与技术学院 \hfill}}\\
		\vspace{1ex}
		专\qquad 业：\underline{\hbox to 8cm{\hfill 计算机科学与技术 \hfill}}\\
		\vspace{1ex}
		学\qquad 号：\underline{\hbox to 8cm{\hfill  \hfill}}\\
		\vspace{1ex}
		邮\qquad 箱：\underline{\hbox to 8cm{\hfill  \hfill}}\\
		\vspace{1ex}
		电\qquad 话：\underline{\hbox to 8cm{\hfill  \hfill}}\\
		\vspace{1ex}
		指导教师：\underline{\hbox to 8cm{\hfill  \hfill}}\\
		\vspace{1ex}
		报告日期：\underline{\hbox to 8cm{\hfill 2023年11月23日 \hfill}}\\		
	\end{center}
	
	\restoregeometry
	
	\clearpage

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%开始正文部分

	\begin{center}
		\textbf{\Large 浙江大学实验报告}
		\vspace{5ex}
	\end{center}
	\parbox{\linewidth}{
		\begin{spacing}{2}
			课程名称： \underline{\hbox to 5cm{\hfill 数字逻辑设计\hfill}}\quad 实验类型： \underline{\hbox to 5cm{\hfill 综合\hfill}}
			
			实验项目名称：\underline{\hbox to 11.5cm{\hfill 变量译码器的设计与应用 \hfill}}
			
			学生姓名：\underline{\hbox to 3cm{\hfill  \hfill}}专业：\underline{\hbox to 3.6cm{\hfill 计算机科学与技术  \hfill}}学号：\underline{\hbox to 3.2cm{\hfill  \hfill}}
			
			实验地点： \underline{\hbox to 3.7cm{\hfill 紫金港东4-509室 \hfill}}实验日期：\underline{\hbox to 2cm{\hfill 2023 \hfill}}年\underline{\hbox to 1.5cm{\hfill 10 \hfill}}月\underline{\hbox to 1.5cm{\hfill 24 \hfill}}日\\
		\end{spacing}	
		\vspace{6ex}
	}
	
\section*{一、操作方法与实验步骤}
\subsection*{（一）原理图设计实现74LS138译码器模块}
\paragraph{1. }新建工程，工程名称用D_74LS138_SCH。

\section*{二、实验结果与分析}
\section*{三、讨论与心得}

\end{document}

%插入图片方法
% \begin{figure}[H]
% 	\centering
% 	\includegraphics[width=0.25\linewidth]{img/1.png}
% 	\includegraphics[width=0.65\linewidth]{img/2.png}
% 	\caption*{对元件和输入图标进行重命名的方法}
% \end{figure}

%插入代码方法
% \begin{lstlisting}
% 	`timescale 1ns / 1ps
% 	module D_74LS138_D_74LS138_sch_tb();
% 	endmodule
% \end{lstlisting}
```

