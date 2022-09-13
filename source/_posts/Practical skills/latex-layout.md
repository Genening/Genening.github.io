---
title: latex_layout
author: Genening
# thumbnail: /gallery/thumbnail/
date: 2019-12-01 00:21:17
updated: 2019-12-01 00:21:17
categories: Practical skills
tags: latex-layout
---

前言：最近参加比赛，要求是LaTeX排版，所以顺便学习了一下。在毕业论文排版的时候也能够用得上，也算是有点作用，在此记录一下学习笔记的模板，这里只记录代码了，至于效果暂时不展示了。

## 完整论文框架代码

<!--more-->

### 第一部分：全局格式初始化设置
```
%!TEX program = xelatex 

%第一部分：全局格式初始化设置
\documentclass[10pt,onecolumn,a4paper]{article}
%格式初始化，字号10pt；纸张A4；内容类型article


\usepackage{ctex} % 支持中文
	\songti  %设置字体为宋体
%	\zihao{-7}   %设置字号，0对应初号

\usepackage{fontspec}
	\setmonofont[Mapping={}]{DejaVu Sans Mono} %英文引号之类的正常显示，相当于设置英文字体，windows下用Consolas字体，Linux下用DejaVu Sans Mono字体
	\setmonofont{DejaVu Sans Mono}
%	\setmainfont{Consolas} %设置文章主体部分的英文字体

% 页面设置
\usepackage{geometry} % 设置页边距
\geometry{left = 2.2cm, right=2.2cm, top = 2.5cm, bottom=2.5cm}

\usepackage{fancyhdr} % 添加页眉页脚
	% 设置 plain style 的属性
	\fancypagestyle{plain}
	\fancyhf{} % 清空当前设置

	% 设置页眉 (head)   备注，底下这三个设置的顺序不能随便调，结果不可预测
	\renewcommand{\headrulewidth}{0.5pt} % 页眉与正文之间的水平线粗细
	\fancyhead[]{\centering Latex学习笔记} %中间显示
	\fancyhead[LO]{页眉左边} % 出现在页眉左边
	\fancyhead[RO]{页眉右边}% 出现在页眉右边

	%设置页脚（foot）
	\fancyfoot[RO]{\it Typesetting with \LaTeX}	% 页脚右侧斜体显示书名
	\renewcommand{\footrulewidth}{0pt}
	\pagestyle{fancy} % 选用 fancy style
	\cfoot{\thepage} % 页脚中央显示页码

 %章节字体
\usepackage{titlesec}
	\titleformat*{\section}{\centering\bf\large} %设置章节字体
\usepackage{indentfirst} % 首行缩进
	\setlength{\parindent}{2em} % 设置首行缩进两字符

%对齐方式
\makeatletter %使\section中的内容左对齐
\renewcommand{\section}{\@startsection{section}{1}{0mm}
	{-\baselineskip}{0.5\baselineskip}{\bf\leftline}}

\makeatother  %节标题左对齐，默认居中


% 引入文章内容编辑的宏
\usepackage{amssymb} % symbol 符号
\usepackage{amsthm} % proof
\usepackage{courier} % 代码字体
\usepackage{graphicx,subfigure} % figures图片
\usepackage{xcolor,mdframed} % mdframed代码
\usepackage{amsmath} %数学公式
\usepackage{enumerate} % 项目编号
\usepackage{listings} % 项目列表
\usepackage{url} %引入超链接的包
\setcounter{tocdepth}{2} % 设置目录深度
\definecolor{mycolor}{RGB}{207, 226, 243} % 自定义颜色，可以设置代码背景

\usepackage{breqn}
	\renewcommand\d{\mathop{}\!\mathrm{d}}
\usepackage{multirow}
	\newtheorem{theorem}{Theorem}
	\renewcommand{\proofname}{\emph{\textbf{Proof}}}
```

### 第二部分：文章内容排版
```
%第二部分：文章内容排版
\begin{document}	
	% 文章标题
	\title{\LaTeX {} study notes}
	\author{Geneningz}
%	\today
	\maketitle
	% 文章摘要
	\begin{onecolabstract}		
		 \noindent\textbf{摘要：}这篇文档的主要目的是学习LaTeX的基本排版方式，类比于Word的排版，排版需要考虑的因素如下：（1）纸张设置：纸张类型、页边距、页眉、页脚（2）内容设置：字号、字体、段间距、行间距、对齐方式、内容排列方式（一版、两版）（3）文章排版设置：标题、作者、摘要、关键字、一级标题、二级标题、三级标题、目录、加粗、斜体、引用、图片、公式、参考文献、附录\par   % 摘要内容，\noindent要求在“摘要”二字之前不缩进
		\noindent\textbf{关键字: } LaTeX; 论文排版; 格式设置%“\par在段首，表示另起一行，“\textbf{}”,花括号内的内容加粗显示
	\end{onecolabstract}
% 文章目录
\tableofcontents
% 从新页开始
\newpage


% 章节内容
\section{概述}
\par Latex的排版类似于HTML和Markdown的排版，都是通过标签进行排版，在需要排版的内容之前打上不同标签就可以渲染出不同的效果。在LaTeX中的基本标签是begin{}和end{}标签，这两个是一组标签，展示如下：
	\begin{mdframed}[backgroundcolor=mycolor,hidealllines=true]
		\begin{verbatim}
		\begin{mdframed}[backgroundcolor=mycolor,hidealllines=true]
		\begin{verbatim}
		content...
		\ end{verbatim}
		\end{mdframed}
		\end{verbatim}
	\end{mdframed}


\section{初始化设置}
\subsection{纸张}
\par 在文章的纸张类型中，对于学术论文，纸张为A4纸，至于其他类型的排版，可以根据实际的需求进行选择，比如书籍的排版可选择更大或者更小的纸张。
\subsubsection{学术论文}
\subsubsection{书籍}
\subsubsection{杂志}
\subsection{纸内设置}
\par 纸内的设置包括页边距、页脚、页眉、栏数，而这些设置都在文章开始前的初始化进行了声明，声明方式主要是\ usepackage{package}，这些设置可以如下：
\begin{mdframed}[backgroundcolor=mycolor,hidealllines=true]
	\begin{verbatim}
	\usepackage{geometry} % 设置页边距
	\geometry{left = 2.2cm, right=2.2cm, top = 2.5cm, bottom=2.5cm}
	
	\usepackage{amssymb} % symbol
	\usepackage{amsthm} % proof
	\usepackage{courier} % 代码字体
	\usepackage{graphicx,subfigure} % figures
	\usepackage{xcolor,mdframed} % mdframed
	\usepackage{amsmath}
	\usepackage{fancyhdr} % 添加页眉页脚
	\usepackage{titlesec}
	\titleformat*{\section}{\centering\bf\large} %设置章节字体
	
	\usepackage{indentfirst} % 首行缩进
	\setlength{\parindent}{2em} % 设置首行缩进两字符
	\end{verbatim}
\end{mdframed}


\section{文章内容框架}
\subsection{题目、作者、时间}
\par 作为一篇学术论文，论文题目、作者、写作时间（发表时间）这些都是基本的信息，是文章的第一部分内容，这是必需的。没有这些内容，论文就是不完整的。代码如下：
	\begin{mdframed}[backgroundcolor=mycolor,hidealllines=true]
		\begin{verbatim}
		\title{content...}
		\author{names}
		\today
		\maketitle  %这一句是为了以上的设置运行，真正显示出来
		\end{verbatim}
	\end{mdframed}
\subsection{摘要、关键词}
\par 在LaTeX中也有直接的标签是设置这两个的，直接设置时会显示默认格式，也就是会出现“摘要”二字居中，这种格式是偏向于英文论文的习惯，但是对于中文学术论文的排版习惯会像这篇笔记的开始的摘要排版格式，这种设置的方式如下：
	\begin{mdframed}[backgroundcolor=mycolor,hidealllines=true]
		\begin{verbatim}
		%1. 中文论文习惯
		\begin{onecolabstract}		
		\noindent\textbf{摘要：}摘要内容   
		% 摘要内容，\noindent要求在“摘要”二字之前不缩进
		\noindent\textbf{关键字: } LaTeX; 论文排版; 格式设置
		%“\par在段首，表示另起一行，“\textbf{}”,花括号内的内容加粗显示
		\end{onecolabstract}
		%2. 英文习惯
		\begin{abstract}		
		摘要内容  
		\noindent\textbf{关键字: } LaTeX; 论文排版; 格式设置
		%“\par在段首，表示另起一行，“\textbf{}”,花括号内的内容加粗显示
		\end{abstract}
		\end{verbatim}
	\end{mdframed}
\subsection{标题}
\par 文章的标题分为好几个级别，在LaTeX中采用\ section表示标题，这里是默认一级标题，二级标题及三级标题分别在前面累加sub即可，代码如下：
	\begin{mdframed}[backgroundcolor=mycolor,hidealllines=true]
		\begin{verbatim}
		\section %一级标题
		\subsection %二级标题
		\subsubsection %三级标题
		\end{verbatim}
	\end{mdframed}
\subsection{目录}
\par 在LaTeX中引入目录非常简单，在书写文章的时候，我们采用了section来标记标题，在标记完毕后，我们只需要在任意位置添加tableofcontents就可以插入目录了，代码如下：
	\begin{mdframed}[backgroundcolor=mycolor,hidealllines=true]
		\begin{verbatim}
		\tableofcontents
		\end{verbatim}
	\end{mdframed}


\section{书写内容}
\subsection{文本段落}
\par 插入文本的标签如下，在此标签后的内容就是段落内容，以及还有其他，如下：
	\begin{mdframed}[backgroundcolor=mycolor,hidealllines=true]
		\begin{verbatim}
		\par  %表示段落
		\newpage  %从新的一页开始
		\end{verbatim}
	\end{mdframed}
\subsection{代码插入}
\par 在写一些比如数学建模比赛的论文时，有时候我们需要插入一些必要的代码进行展示，在LaTeX中有很好的支持，可以很完美的插入代码，代码如下：
		\begin{mdframed}[backgroundcolor=mycolor,hidealllines=true]
		\begin{verbatim}
		\begin{mdframed}[backgroundcolor=mycolor,hidealllines=true]
			%backgroundcolor设置的是代码栏的颜色，mycolor参数在全局设置的时候进行了设置，
			%全局设置\definecolor{mycolor}{RGB}{207, 226, 243}，
			%hidealllines=true表示无边框
			\begin{verbatim}
			需要插入的代码内容
			\ end{verbatim}
		\end{mdframed}
		\end{verbatim}
	\end{mdframed}
\subsection{列表插入}
\par 列表应该是在博客中经常使用的一种排版方式，或者出现在杂志中，但是对于学术论文来说，应该是不规范的。所以在学术论文中不应使用。
	\begin{itemize}
		\item[-] good morning...
		\item[-] good morning....
	\end{itemize}
	\begin{enumerate}
		\item good morning
		\item good morning
	\end{enumerate}
\par 代码如下：
	\begin{mdframed}[backgroundcolor=mycolor,hidealllines=true]
		\begin{verbatim}
		\begin{itemize}
		\item[-] good morning...
		\item[-] good morning....
		\end{itemize}
		\begin{enumerate}
		\item good morning
		\item good morning
		\end{enumerate}
		\end{verbatim}
	\end{mdframed}
\subsection{图片}
\par 不管是在学术论文中还是普通博客中，图片是非常常见的数据展示形式，因此掌握插入图片是排版的基本要求。
\subsubsection{单张图片}
\par 单张图片：
	\begin{figure}[h]%%图
		\centering  %插入的图片居中表示
		\includegraphics[width=0.9\linewidth]{figures/test1}  %插入的图，包括JPG,PNG,PDF,EPS等，放在源文件目录下
		\caption{this is a figure.}  %图片的名称
		\label{fig:test1}   %标签，用作引用
	\end{figure}
\par 代码如下：
	\begin{mdframed}[backgroundcolor=mycolor,hidealllines=true]
		\begin{verbatim}
		\begin{figure}[h]%%图
		\centering  %插入的图片居中表示
		\includegraphics[width=0.9\linewidth]{figures/test1} 
		 %插入的图，包括JPG,PNG,PDF,EPS等，放在源文件目录下，width是指插入图片的大小
		\caption{this is a figure.}  %图片的名称
		\label{fig:test1}   %标签，用作引用
		\end{figure}
		\end{verbatim}
	\end{mdframed}
\subsubsection{两栏图片}
\par 两栏图片：
	\begin{figure}[h]
	\begin{minipage}[t]{0.4\linewidth}%并排放两张图片，每张占行的0.4，下同 
		\centering     %插入的图片居中表示
		\includegraphics[width=1.2\textwidth]{figures/test1}
		\caption{this is a figure3.}%图片的名称
		\label{fig:liuchengtu1}%标签，用作
	\end{minipage} 
	\hfill
	\begin{minipage}[t]{0.4\linewidth}
		\centering
		\includegraphics[width=1.2\textwidth]{figures/test1}
		\caption{this is a figure4.}%图片的名称
		\label{fig:liuchengtu2}
	\end{minipage}
	\end{figure}
\par 代码如下：
	\begin{mdframed}[backgroundcolor=mycolor,hidealllines=true]
		\begin{verbatim}
			\begin{figure}[h]
		\begin{minipage}[t]{0.4\linewidth}
		%并排放两张图片，每张占行的0.4，下同 
		\centering     %插入的图片居中表示
		\includegraphics[width=1.2\textwidth]{figures/test1}
		\caption{this is a figure3.}%图片的名称
		\label{fig:liuchengtu1}%标签，用作
		\end{minipage} 
		\hfill
		\begin{minipage}[t]{0.4\linewidth}
		\centering
		\includegraphics[width=1.2\textwidth]{figures/test1}
		\caption{this is a figure4.}%图片的名称
		\label{fig:liuchengtu2}
		\end{minipage}
		\end{figure}
		\end{verbatim}
	\end{mdframed}

\subsection{表格}
\par 在文章中加入表格是非常常规的操作，一般需要展示符号、数据时使用。这里坑很大，不明白为什么在这里好端端的表格会浮上去，不和这一段一起，这是非常奇怪的，需要查找资料找出原因。最终原因是：LaTeX插入表格和图片是默认是会浮动的，这就导致我们排版完成后，图片和表格却不一定在我们想要的位置上，所以很烦恼，但是，我们可以通过begin{table}[h]中的h参数取消浮动，这样表格和图片就不会乱跑了。表格示例如下：
\begin{table}[h]  % 这里的h应该是取消浮动的意思，太恶心了，找了很久
	\centering
	\caption{basic structure}
	\vspace{20pt}
	\begin{tabular}{p{2cm}p{3cm}p{2.5cm}p{2.5cm}p{2.5cm}p{2.5cm}}
		\hline
		Gene name & Gene accession No. & CDS length (bp) & Protein size (aa) & Protein MW (kDa) \\
		\hline
		001  & 01g009860.2   & 819             & 272               & 31.34            \\
		002  & 01g021730.2   & 798             & 265               & 30.37            \\
		003  & 01g094490.2   & 630             & 209               & 24.58            \\
		004  & 01g102740.2   & 1242            & 413               & 46.94            \\
		005  & 01g104900.2   & 597             & 198               & 22.85            \\
		006  & 02g036430.1   & 1698            & 565               & 64.88            \\
		007  & 02g061780.2   & 735             & 244               & 28.23            \\
		008  & 02g061870.1   & 660             & 219               & 25.21            \\
		009  & 02g061900.1   & 915             & 304               & 34.61            \\
		010  & 02g061910.1   & 795             & 264               & 29.92 \\    
		\hline       
	\end{tabular}
	\label{bs2}
\end{table}
\par 代码如下：
	\begin{mdframed}[backgroundcolor=mycolor,hidealllines=true]
		\begin{verbatim}
		\begin{table}[h]  % 这里的h应该是取消浮动的意思，太恶心了，找了很久
		\centering
		\caption{basic structure}
		\vspace{20pt}
		\begin{tabular}{p{2cm}p{3cm}p{2.5cm}p{2.5cm}p{2.5cm}p{2.5cm}}
		\hline
		Gene name & Gene accession No. & CDS length (bp)
		 & Protein size (aa) & Protein MW (kDa) \\
		\hline
		001  & 01g009860.2   & 819             & 272               & 31.34 \\
		002  & 01g021730.2   & 798             & 265               & 30.37 \\
		003  & 01g094490.2   & 630             & 209               & 24.58 \\
		004  & 01g102740.2   & 1242            & 413               & 46.94 \\
		005  & 01g104900.2   & 597             & 198               & 22.85 \\
		006  & 02g036430.1   & 1698            & 565               & 64.88 \\
		007  & 02g061780.2   & 735             & 244               & 28.23 \\
		008  & 02g061870.1   & 660             & 219               & 25.21 \\
		009  & 02g061900.1   & 915             & 304               & 34.61 \\
		010  & 02g061910.1   & 795             & 264               & 29.92 \\    
		\hline       
		\end{tabular}
		\label{bs2}
		\end{table}
		\end{verbatim}
	\end{mdframed}

\subsection{数学公式}
\par 论文里的公式以及相关符号是非常常见的，而latex对于数学公式的支持是非常高的，latex渲染的数学公式的美感是声名在外的，所以非常值得学习。
\begin{enumerate}
	\item 行内插入
	\item 独立一行
\end{enumerate}
\par 示例1：$x=\sum_i^ny_i$
\par 示例2：

$$
y=\lim_xy_i+\frac{1+5y}{2-y_i}
$$

\par 示例3：
\begin{equation}
	y=\lim_xy_i+\frac{1+5y}{2-y_i}
\end{equation}
\subsection{链接}
\par 链接在论文书写中并不常用，但是对于博客来说很常用，但是一般我们在博客中也不采用latex写作，所以其实不是非常有必要学习这个，纯当是了解就好，代码如下：
	\begin{mdframed}[backgroundcolor=mycolor,hidealllines=true]
		\begin{verbatim}
		\usepackage{url}  %首先在开头引入包
		\url{https://genening.github.io/}
		\end{verbatim}
	\end{mdframed}
\par 超链接效果如此：\url{https://genening.github.io/}


\section{参考文献}
\par 当论文写完后，千万别忘了写上参考文献，否则会被认为引用他人文献而不声明，即盗窃，是学术不端，所以一定要罗列，效果如下：
\begin{thebibliography}{99}
	\bibitem{ref1}Zheng L, Wang S, Tian L, et al., Query-adaptive late fusion for image search and person re-identification, Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition, 2015: 1741-1750.
	\bibitem{ref2}Arandjelović R, Zisserman A, Three things everyone should know to improve object retrieval, Computer Vision and Pattern Recognition (CVPR), 2012 IEEE Conference on, IEEE, 2012: 2911-2918.
	\bibitem{ref3}Lowe D G. Distinctive image features from scale-invariant keypoints, International journal of computer vision, 2004, 60(2): 91-110.
	\bibitem{ref4}Philbin J, Chum O, Isard M, et al. Lost in quantization: Improving particular object retrieval in large scale image databases, Computer Vision and Pattern Recognition, 2008. CVPR 2008, IEEE Conference on, IEEE, 2008: 1-8.
\end{thebibliography}
\par 代码如下：
	\begin{mdframed}[backgroundcolor=mycolor,hidealllines=true]
		\begin{verbatim}
		\begin{thebibliography}{99}
		\bibitem{ref1}参考文献1
		\bibitem{ref2}参考文献2
		\bibitem{ref3}参考文献3
		\bibitem{ref4}参考文献4
		\end{thebibliography}
		\end{verbatim}
	\end{mdframed}
\end{document}


```
