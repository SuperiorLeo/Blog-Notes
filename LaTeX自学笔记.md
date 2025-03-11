@[TOC](LaTeX学习)
## 最基本结构
```latex
%导言区
\documentclass{article}

\usepackage{ctex}

%正文区
\begin{document}
	
\end{document}
```



## 源文件的基本结构

1. 导言区---文档格式的设置：article, book, report, letter；标题、作者、日期的设置
2. 正文区
   1. 如果上面有标题这些设置，在正文区要加上maketitle
   2. 一个空行代表换行
   3. $$一个符号中间输出的是行内数学公式
   4. $$$$两个符号中间输出的是行间数学公式
3. 例子

```latex
%导言区
\documentclass{article} %article,book, report, letter

\title{My First Document}
\author{Leo Superior}
\date{\today}

%正文区(文稿区)
\begin{document}
	\maketitle	%为了使上面的标题、作者和日期正常显示
	
	Hello World!
	
	% $$中间输出的是数学公式，没在里面输出的是文本模式
	% 其中一个$包围的是行内公式，两个$$则是行间公式
	Let $f(x)$ be difined by the formula.
	$f(x)=3x^2+4x+3$.
	$$f(x)=3x^2+4x+3$$ which is a polynomial of degree 2.
	
\end{document}
```



## 中文处理方法

1. 要引入中文的宏包，第一种方法：

   ```latex
   \documentclass{article} %article,book, report, letter
   %中文的话要引入ctex的宏包
   \usepackage{ctex}
   ```

   1. ctex宏包地址：C:\texlive\2020\texmf-dist\doc\latex\ctex\ctex.pdf
   2. 也可以用cmd texdoc ctex进行调出
   3. 利用texdoc 可以调出很多文件，比如一个简短的tex说明：lshort-zh-cn

2. 第二种方法

   ```latex
   \documentclass{ctexart} %ctexbook, ctexrep(对应的是report)
   ```

```latex
%导言区
\documentclass{ctexart} %article,book, report, letter
%中文的话要引入ctex的宏包
%\usepackage{ctex}

%对下文出现的degree符号进行定义
\newcommand\degree{^\circ}

\title{\heiti 杂谈勾股定理}
\author{\kaishu 冷奕泓}
\date{\today}

%正文区(文稿区)
\begin{document}
	\maketitle	%为了使上面的标题、作者和日期正常显示
	
	勾股定理可以用现代语言表诉如下：
	
	直角三角形斜边的平方等于两腰的平方和。
	
	%注意这里的angle和C之间要有空格，否则会出错
	可以用符号语言表诉为：设直角三角形$ABC$，其中$\angle C=90\degree$，则有：
	%下面的插入方式可以输出带有编号的行间公式
	\begin{equation}
		AB^2 = BC^2 + AC^2.
	\end{equation}
\end{document}
```



## LaTeX的字体设置
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/c37f564d2b75fdddc645257eb2a803c9.png)


1. 字体族设置(罗马字体、无衬线字体、打字机字体)

   1. 两种设置方法：字体命令、字体声明

   2. ```latex
      %字体族设置（罗马字体、无衬线字体、打字机字体）
      	%第一种是使用字体命令，括号里就是具体内容
      	\textrm{Roman Family} \textsf{Sans Serif Family} \texttt{Typewriter Family}
      	
      	%第二种是使用字体声明，用于声明后面的字体为罗马字体，大括号用于分组，限定字体限制的范围
      	\rmfamily Roman Family {\sffamily Sans Serif Family} {\ttfamily Typewriter Family}
      ```

      

2. 字体系列设置（粗细、宽度）

   1. ```latex
      %字体系列设置（粗细、宽度）
      	\textmd{Medium Series} \textbf{Boldface Series}
      	
      	{\mdseries Medium Series} {\bfseries Boldface Series}
      ```

3. 字体形状设置（直立、斜体、伪斜体、小型大写）

   1. ```latex
      %字体形状设置（直立、斜体、伪斜体、小型大写）
      	\textup{Upright Shape} \textit{Italic Shape} \textsl{Slanted Shape} \textsc{Small Caps Shape}
      	
      	{\upshape Upright Shape} {\itshape Italic Shape} {\slshape Slanted Shape} {\scshape Small Caps Shape}
      ```

4. 中文字体的设置

   1. ```latex
      	%中文字体
         	{\songti 宋体} {\heiti 黑体} {\fangsong 仿宋} {\kaishu 楷书}
         	
         	%中文字体的粗细和斜体,注意粗体使用黑体表示，斜体使用楷书表示
         	中文字体的\textbf{粗体} \textit{斜体}
      ```

5. 字体大小

   1. ```latex
      %字体大小,都是相对于normal size进行的变化，而normal size在最开始设置,\documentclass[10pt]{article}
      	{\tiny Hello}\\
      	{\scriptsize Hello}\\
      	{\footnotesize Hello}\\
      	{\small Hello}\\
      	{\normalsize Hello}\\
      	{\large Hello}\\
      	{\Large Hello}\\
      	{\LARGE Hello}\\
      	{\huge Hello}\\
      	{\Huge Hello}\\
      	
      	%中文字号设置命令
      	\zihao{4} 你好！
      ```

      

## LaTeX的篇章结构

### 提纲建立

1.![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/71105fe139aac935faeba2e6c6a2cf1b.png) 
2. 用sub代表上一节下面附属的小节![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/0caa482bc2209697c6a73162add76008.png)

### 换行和新的段落

1. 一个空行或者多个连续空行代表着前后内容是两段，会产生缩进。
2. double \也可以表示换行，但只是换行，不会产生缩进。
3. 也可以用\par进行产生新的段落
4. 一般是用插入空行来实现分段，为保证源文件的清晰

### 对原来的设置进行更改

1. 在最开始documentclass{ctexart}，会默认标题居中

2. 对section和subsection的设置

   ```latex
   \ctexset{
   	section = {
   		format+ = \zihao{-4} \heiti \raggedright, name = {,、},
   		number = \chinese{section},
   		%说明这里的大标题是以中文形式，一、
   		beforeskip = 1.0ex plus 0.2ex minus .2ex,
   		afterskip = 1.0ex plus 0.2ex minus .2ex,
   		aftername = \hspace{0pt}	
   },
   	subsection = {
   		format+ = \zihao{5} \heiti \raggedright, name = {,、},
   		number = \arabic{section},
   		beforeskip = 1.0ex plus 0.2ex minus .2ex,
   		afterskip = 1.0ex plus 0.2ex minus .2ex,
   		aftername = \hspace{0pt}
   	}	
   }
   ```

### 产生带章节的大纲

1. 每一个章节有不同的页面

2. 相当于书籍，所以最上边是ctexbook的说明

3. ```latex
   %导言区
   \documentclass{ctexbook}
   
   %\usepackage{ctex}
   
   \ctexset{
   	section = {
   		format+ = \zihao{-4} \heiti \raggedright, name = {,、},
   		number = \chinese{section},
   		beforeskip = 1.0ex plus 0.2ex minus .2ex,
   		afterskip = 1.0ex plus 0.2ex minus .2ex,
   		aftername = \hspace{0pt}	
   	},
   	subsection = {
   		format+ = \zihao{5} \heiti \raggedright, name = {,、},
   		number = \arabic{section},
   		beforeskip = 1.0ex plus 0.2ex minus .2ex,
   		afterskip = 1.0ex plus 0.2ex minus .2ex,
   		aftername = \hspace{0pt}
   	}	
   }
   
   %正文区
   \begin{document}
   	%构建提纲
   	\chapter{绪论}
   	\section{研究的目的和意义}
   	\section{国内外研究现状}
   	\subsection{国外研究现状}
   	\subsection{国内研究现状}
   	\section{研究内容}
   	\section{研究方法和技术路线}
   	\subsection{研究方法}
   	\subsection{研究路线}
   	\chapter{实验与结果分析}	
   	\section{引言}
   	\section{实验方法}
   	\section{实验结果}
   	\subsection{数据}
   	\subsection{图表}
   	\subsubsection{实验条件}
   	\subsubsection{实验过程}
   	\subsection{结果分析}
   	\section{结论}
   	\section{致谢}
   \end{document}
   ```

   4. 此时的sub-section命令不起作用

   5. 引入目录

      ```latex
      	\tableofcontents
      ```

      

   6. ![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/ed2299ad22ddc65de17ce438e75d9ac2.png)

## LaTeX中的特殊字符

1. ```latex
   %导言区
   \documentclass{article}
   
   \usepackage{ctex}
   
   %正文区
   \begin{document}
   	\section{空白符号}
   	%空行分段，多个空行等同于1个
   	%自动缩进，绝对不能用空格代替
   	%英文中多个空格处理为一个空格，中文的空格将被忽略
   	%汉字与其他字符的间距是由自动处理
   	%禁止使用中文全角空格
   	
   	%常用的空格命令	
   	a\quad b
   	a\ b
   	\section{\LaTeX 控制符}
   	%为输入一些特殊的符号，通常是反斜杠\加上对应的符号，而反斜杠本省则用textbackslash输出
   	\# \$ \% \{ \} \~{} \^{} \textbackslash \&
   	\section{排版符号}
   	\S \P \dag \ddag \copyright \pounds
   	\section{\TeX 标志符号}
   	%基本符号
   	\TeX{} \LaTeX{} \LaTeXe{}
   	\section{引号}
   	%分为单引号，双引号，左右引号的区分
   	%1左边的键表示左引号，单引号表示右引号
   	` ' `` ''
   	
   	`我的' ``你好''
   	\section{连字符}
   	%短中长
   	- -- ---
   	\section{非英文字符}
   	\section{重音符号(以o为例)}
   	\`o \'o \^o
   \end{document}
   ```

   2. 敲重点
      1. 空格的表示
      2. 特殊符号的输出\ 特殊符号
      3. 引号`' `` 
      4. 连字符- -- --- 
   3. 对应结果展示
   4. ![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/58c12adccafe67c53bdb45338de0c076.png)

## LaTeX中的插图

```latex
%导言区
\documentclass{ctexart}

%\usepackage{ctex}

%导言区：\usepackage{grapicx}
%语法：\includegraphic[<选项>]{<文件名>}
%格式：EPS、PDF,PNG,JPEG,BMP

\usepackage{graphicx}
\graphicspath{{figures/},{pics/}} %图片在当前目录下的figures目录下

%正文区
\begin{document}
	\LaTeX{}中的插图：
	
	\includegraphics{example1}
	\includegraphics{exa2}
	\includegraphics{exa3}
	
	%会出现图片太大装不下的情况，因此可以设置图片大小
	\includegraphics[scale=0.3]{example1}\quad
	\includegraphics[width=2cm]{exa2}\quad
	\includegraphics[height=2cm]{exa3}
\end{document}
	


```

1. 首先要知道如何引用图片【养成在所属文件夹建立图片文件夹的习惯】
2. 其次如何对图片大小和样式进行设置

## LaTeX中的表格

### 简单表格

```latex
%导言区
\documentclass{article}

\usepackage{ctex}

%正文区
\begin{document}
	%表格的制作以及排版
	%l：左对齐 c：居中对齐 r：右对齐(均指的是表格内文字)
	%|表示竖直的表格线，\hline表示水平的表格线
	%p{1.5cm}用于设置指定宽度的列，内容超过后自动换行
	% texdoc booktab(longtab tabu)查看更复杂的表格的制作
	\begin{tabular}{|l|c|c|c|p{1.5cm}|}
		\hline
		姓名 & 语文 & 数学 & 外语 & 备注 \\
		\hline
		张三 & 87 & 100 & 93 & 优秀\\
		\hline
		李四 & 75 & 64 & 52 & 补考另行通知\\
		\hline
		王二 & 80 & 82 & 78 & \\
		\hline
	\end{tabular}
	
\end{document}
```

### 常见三线表
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/6c257d068db93dcc552339f86bada8e2.png)

```latex
%导言区
\documentclass{article}

\usepackage{ctex}

\usepackage{tabularx}

%正文区
\begin{document}
	%三线表的画法
	\begin{table}
		\caption{设置宽度}
		\begin{tabularx}{12cm}{lXl}
			\hline
			Start & End  & Character Block Name \\
			\hline
			3400  & 4DB5 & CJK Unified Ideographs Extension A \\
			4E00  & 9FFF & CJK Unified Ideographs \\
			\hline
		\end{tabularx}
	\end{table}
\end{document}

```

### 更多表格

> <https://blog.csdn.net/golden1314521/article/details/40891515?utm_medium=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.compare&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.compare>

## LaTeX中的浮动体设置

1. 一般是指对图片或者表格的排版、命名、标签和交叉使用

2. figure、table大的标签下面去写小的图片或者表格

3. ctrl+T ctrl+U分别为注释和取消注释

4. ```latex
   %导言区
   \documentclass{article}
   
   \usepackage{ctex}
   \usepackage{graphicx}
   \graphicspath{{figures/},{pics/}}
   
   %正文区
   \begin{document}
   	\LaTeX{}中的\TeX example1见图\ref{fig-example1}。
   	%实现对图形和表格的管理，也就是浮动体设置
   	\begin{figure}[htbp]
   		\centering		%使得figure中的内容居中显示
   		\includegraphics[scale=0.3]{example1}
   		\caption{\TeX example1}		%设置图片的标题
   		\label{fig-example1}	%给图片设置标签，并利用ref实现交叉引用
   	\end{figure}
   	
   	在\LaTeX{}中的表格如下表\ref{table-1}。
   	\begin{table}[htbp]
   		\centering
   		\caption{考试成绩单}
   		\label{table-1}
   			\begin{tabular}{|l|c|c|c|p{1.5cm}|}
   			\hline
   			姓名 & 语文 & 数学 & 外语 & 备注 \\
   			\hline
   			张三 & 87 & 100 & 93 & 优秀\\
   			\hline
   			李四 & 75 & 64 & 52 & 补考另行通知\\
   			\hline
   			王二 & 80 & 82 & 78 & \\
   			\hline
   		\end{tabular}
   	\end{table}
   
   \end{document}
   ```

   5. 效果图如下![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/124a0572c2afbc59c7647bd326881871.png)

   6. 实现灵活分页、给图标添加标题并自动编号、交叉引用

   7. ```latex
      figure环境(table与之类似)
      \begin{figure}[<允许位置>]
      	< 任意内容 >
      \end{figure}
      
      <允许位置的选项>
      h,here-代码所在上下文位置
      t,top-代码所在页面或者之后页面的顶部
      b,bottom-代码所在页面或之后页面的底部
      p,page-独立一页，浮动页面
      ```

## LaTeX中的数学公式

### 导包

```latex
\usepackage{amsmath}
```

### 行内公式

1. single $ + 公式

2. 小括号+公式

3. math的环境

4. ```latex
   	\section{行内公式}
      	%行内公式的三种表示方式，美元符号或者小括号方便一点
      	\subsection{美元符号}
      	交换律是$a+b=b+a$,如$1+2=2+1=3$。
      	\subsection{小括号}
      	交换律是\(a+b=b+a\),如\(1+2=2+1=3\)。	
      	\subsection{math环境}
      	交换律是\begin{math}
      		a+b=b+a
      	\end{math},如
      	\begin{math}
      		1+2=2+1=3
      	\end{math}。
   ```

   

### 上下标

1. 上标用^，下标用_

2. 当上下标超过一个字符时，用{}进行分组

3. ```latex
   	\section{上下标}
      	\subsection{上标}
      	%上标是通过^符号实现
      	$3x^2 - x + 2 = 0$
      	
      	%有时复杂的上边需要用大括号进行分组
      	$3x^{20} - x + 2 = 0$
      	
      	$3x^{3y+2} - x + 2 = 0$
      	\subsection{下标}
      	%下标是通过_下划线来实现
      	%分组组要是当上下标超过一个字符就要用大括号
      	$a_0,a_1,a_x,a_{xy},a_{100}$
   ```

   

### 希腊字母

1. \加上希腊字母的英文即可

2. ```latex
   	\section{希腊字母}
      	%引用希腊字幕，用命令加其英文名称即可
      	$\alpha$
      	$\beta$
      	$\gamma$
      	$\epsilon$
      	$\pi$
      	$\omega$
      	
      	%大写
      	$\Gamma$
      	$\Delta$
      	$\Theta$
      	$\Pi$
      	$\Omega$
      	
      	$\alpha^2 + \beta - \gamma^{23} = 0$
   ```

   

### 数学函数

1. \数学函数的英文表示即可

2. 注意命令和后面加空格

3. 注意加指数和对数函数的表示方法

4. ```latex
   	\section{数学函数}
      	%对数、指数、三角函数
      	$\log$
      	$\ln$
      	$\sin$
      	$\cos$
      	$\tan$
      	$\arccos$
      	$\arcsin$
      	$\arccos$
      
      	%利用其构成公式
      	$\sin^2 x+\cos^2 x=1$	
      	
      	$y=\log_3 x$
      	
      	$z=\arccos^2 x+\ln y$
   ```

   

### 根式

1. \sqrt命令

2. 可以自己制定开方次数

3. ```latex
   	\section{根式}
      	$\sqrt{2}$
      	$\sqrt{x^2+y^2}$
      	$\sqrt{2+\sqrt{x}}$	
      	%制定开发的次数
      	$\sqrt[4]{x}$
   ```

   

### 分式fraction

1. ```latex
   	\section{分式}
      	可以直接使用/进行，如：$3/4$
      	
      	也可以通过frac命令进行，如：$\frac{x_1+y_1^2}{\sqrt{x^2+y^2}}$
      	
      	上下标，复杂公式以及根式的结合，如：$\sqrt{\frac{\arccos^x 2}{\log_x y}}$
   ```

   

### 行间公式

1. ```latex
   	%行间公式用的是double$符号进行阐述，下面是行间公式的几种方法
      	\subsection{双美元符号}
      	交换律是 $$a+b=b+a$$
      	如$$1+2=2+1=3$$
      	\subsection{方括号}
      	交换律是：
      	\[a+b=b+a\]
      	如
      	\[1+2=2+1=3\]
      	\subsection{displaymath环境}
      	交换律是：
      	\begin{displaymath}
      		a+b=b+a
      	\end{displaymath}
      	如：
      	\begin{displaymath}
      		1+2=2+1=3
      	\end{displaymath}
   ```

   

### 行间公式的自动编号与不自动编号

1. 自动编号，公式放置在equation的环境下

2. 不自动编号，公式放置在equation*

3. 默认是行间公式

4. label和ref的相互调用，方便删除和添加公式时的编号可以自动切换

5. ```latex
   	\subsection{自动编号公式equation环境}
      	%将需要排序的公式置于equation环境中
      	%可以用label和ref命令实现交叉引用
      	交换律见式\ref{commutative}
      	\begin{equation}
      		a+b=b+a \label{commutative}
      	\end{equation}
      
      	\begin{equation}
      		\frac{\sqrt{x+y}}{\frac{1}{x}+1}
      	\end{equation}
      	\subsection{不自动编号equation*环境}
      	\begin{equation*}
      		\frac{\sqrt{x+y}}{\frac{1}{x}+1}
      	\end{equation*}
      
      	公示的编号与交叉引用也是自动实现的，要尽量养成用自动形成的习惯。方便当进行公式的删除和添加时可以全文自动修改编号，不用单独修改。
   ```

## LaTeX数学公式的矩阵

### 简单说明

1. 矩阵的表示是在大环境公式下面的

2. 注意导入环境

   ```latex
   \usepackage{amsmath}
   \usepackage{mathdots} %用于省略号左下到右上
   ```

3.![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/8d1db746d219a9b2c03a9debb89118dc.png) 

4. ![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/b7f09a745027f622e027d5e5e5a33431.png)

### 简单矩阵表示方法

1. 无括号、小括号、大括号、中括号、单双竖线

2.![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/47c2de12ac260092807ae2151540a4f8.png) 

3. ```latex
   \section{简单矩阵表示方式}
   	%矩阵环境，用&分割列，\\分割行，注意命令与文字间要用空格隔开
   	%matrix环境，同时用的是行间公式,注意下面这些环境命令都要在大的公式环境下
   	%这里是在中括号行间公式的命令下面
   	%matrix环境是没有任何括号的矩阵
   	\[
   	\begin{matrix}
   		0 & 1 \\
   		1 & 2
   	\end{matrix} \qquad
   	%pmatrix环境，小括号环境	
   	\begin{pmatrix}
   		i & 0 \\
   		0 & -i
   	\end{pmatrix} \qquad
   	%bmatrix环境，方括号环境
   	\begin{bmatrix}
   		i & 0 \\
   		0 & -i	
   	\end{bmatrix} \qquad
   	%Bmatrix环境，大括号环境
   	\begin{Bmatrix}
   		i & 0 \\
   		0 & -i
   	\end{Bmatrix} \qquad
   	%vmtrix环境，单竖线环境
   	\begin{vmatrix}
   		a & b \\
   		c & d
   	\end{vmatrix} \qquad
   	%Vmatrix环境，双竖线模式
   	\begin{Vmatrix}
   		a & b \\
   		c & d
   	\end{Vmatrix}
   	\]
   ```

   

### 上下标

1. ```latex
   \section{上下标}
   %可以在矩阵中使用上下标
   \[
   A = \begin{pmatrix}
   	a_{11}^2 & a_{12}^2 & a_{13}^2 \\
   	0 & a_{22} & a_{23} \\
   	a_{31} & 0 & a_{33}
   \end{pmatrix}
   \]
   ```

### 不同方向省略号

1. 水平、竖直、左右、右左

2. ```latex
   \section{省略号的表示}
   %矩阵中经常使用的省略号可以用:水平：\dots 竖直：\vdots 左上到右下\ddots
   %矩阵下标表示,\times命令排版✖
   %左下到右上的省略号，在导入mathdots的情况下，用\iddots
   \[
   A = \begin{bmatrix}
   	a_{11} & a_{12} & \dots & a_{1n} \\
   	0 & a_{22} & \dots & a_{2n} \\
   	\vdots & \vdots & \ddots & \vdots \\
   	0 & 0 & 0 & 0
   \end{bmatrix}_{n \times n}	\qquad
   B = \begin{pmatrix}
   	a_{11}^2 & a_{12}^2 & a_{13}^2 \\
   	0 & \iddots & a_{23} \\
   	a_{31} & 0 & a_{33}
   \end{pmatrix}_{3 \times 3}
   \]
   ```

### 分块矩阵

1. ```latex
   \section{分块矩阵}
   %分块矩阵（矩阵嵌套）
   %在数学公式中\Large 0和\text{\Large 0}表示的不一样
   \[
   \begin{pmatrix}
   	\begin{matrix}
   		1&0 \\
   		0&1
   	\end{matrix} & \Large 0 \\
   	\text{\Large 0} & \begin{matrix}
   		1&0 \\
   		0&1
   	\end{matrix}
   \end{pmatrix}
   \]
   ```

### 三角矩阵

1. ```latex
   \section{三角矩阵}
   %三角矩阵
   %\multicolumn{cols}{pos}{text}合并多列
   %\raisebox调整高度
   \[
   \begin{pmatrix}
   	a_{11} & a_{12} & \cdots & a){1n}] \\
   	& a_{22} & \cdots & a_{2n} \\
   	& & \ddots & \vdots \\
   	\multicolumn{2}{c}{\raisebox{1.3ex}[0pt]{\Huge 0}}&   &a_{nn}
   \end{pmatrix}
   \]
   ```

### 跨列省略号

1. ```latex
   \section{跨列省略号}
   %跨列的省略号：\hdotsfor{列数}
   \[
   \begin{pmatrix}
   	1 & \frac 12 & \dots & \frac 1n \\
   	\hdotsfor{4} \\
   	m & \frac m2 & \dots & \frac mn
   	\end{pmatrix}
   \]
   ```

### 行内小矩阵

1. 需要注意手动加括号

2. ```latex
   \section{行内小矩阵}
   %行内小矩阵（smallmatrix）环境
   复数 $z = (x,y)$ 也可以用矩阵
   \begin{math}
   	\left(%需要手动加上左括号
   	\begin{smallmatrix}
   		x & -y \\ y & x
   	\end{smallmatrix}
   	\right)%需要手动加上右括号
   \end{math}来表示。
   ```

### array环境

1. 与tabular环境类似，可以用于特别复杂的矩阵表示

2. ```latex
   %array环境(类似于表格环境tabular)
   	%引入array矩阵可以插入更为复杂的矩阵
   	\[
   	\begin{array}{r|r}
   		\frac 12 & 0 \\
   		\hline
   		0 & -\frac a{bc} \\
   	\end{array}
   	\]
   ```

## LaTeX中的多行数学公式

### 注意和整体图

1. 导入宏包

   ```latex
   \documentclass{ctexart}
   
   %\usepackage{ctex}
   \usepackage{amsmath}
   \usepackage{amssymb}	%输出花体字符,\mathbb
   ```

   

2. 整体图：![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/4c1717a7f7f19ef8aec131337afae76c.png)

3. \text{}表示在公式环境下输出文本模式

### gather环境

1. 实现多个公式居中排版

2. gather都编号、gather*都不编号、gather下\notag制定某一行不编号

3. ```latex
   %gather环境，不仅实现多行公式的排版，而且可以自动编号
   \begin{gather}
   	a + b = b + a \\
   	ab = ba
   \end{gather}
   %gather*环境，不带编号的多行公式排版
   \begin{gather*}
   	a + b = b + a \\
   	ab = ba
   \end{gather*}
   %也可以在某一行换行之前使用\notag命令，取消这一行公示的编号
   \begin{gather}
   	a + b = b + a \\
   	ab = ba \notag \\
   	2 \times 3 = 3 \times 2 = 6
   \end{gather}
   ```

### align环境

1. align环境用于多个公式之间的对齐排版

2. &指定对其的位置

3. ```latex
   %实现公式之间的对齐，可以使用align和align*(用&指定对齐位置)
   %带编号
   \begin{align}
   	x &= t + \cos t +1 \\
   	y &= 2\sin t
   \end{align}
   %不代编号以及多个公式分别对齐
   %如等号对齐，每个开头对齐
   \begin{align*}
   	x &= t & x &= \cos t & x &=t \\
   	y &=2t & y &= \sin (t+1) & y &= \sin t
   \end{align*}
   ```

4. ![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/08001c515779c9d50888c185a96ff258.png)

### split环境

1. 该环境是在大的equation环境下，实现居中编号

2. 适用于连等公式，&确定对齐位置

3. ```latex
   %split环境（对齐采用align环境的方式，编号在中间,主要适用于连等符号，也就是一个公式多行排版）
   %在equation环境下
   \begin{equation}
   	\begin{split}
   		\cos 2x &= \cos^2 x - \sin^2 x \\
   		&= 2\cos^2 x - 1
   	\end{split}
   \end{equation}
   ```

4. ![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/6bdfb87a73510edf4d60b389aa8b5d95.png)

### cases环境

1. 用于分段函数的表示，也是在equation环境下

2. ```latex
   %cases 环境,用于分段函数的表示
   %每行公式中使用&分隔符为连各个部分
   %通常表示值和后面的条件
   %在equation环境下
   %\in表示的是属于符号，\text{}表示在公式环境下输出文本
   \begin{equation}
   	D(x) = \begin{cases}
   		1, & \text{如果 } x \in \mathbb{Q}; \\
   		0, & \text{如果 } x \in \mathbb{R} \setminus\mathbb{Q}.
   	\end{cases}
   \end{equation}
   ```

3. [外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-pHfio5yy-1593783983685)(C:\Users\lyh010108\AppData\Roaming\Typora\typora-user-images\1593746397862.png)]

## LaTeX中的参考文献BibTex

### 普通引用

1. 普通引用需要将文献条目打在tex文件里面，过于复杂

2. 具体引用方式如下：

   ```latex
   %	一次管理，一次使用
   %	参考文献的格式：
   %	\begin{thebibliogaraphy}{编号样本}
   %		\bibitem[记号]{引用标志}文献条目1
   %		\bibitem[记号]{引用标志}文献条目1
   %		......
   %	\end{thebibliogaraphy}
   %	其中文献条目包括：作业，题目，出版社，年代，版本，页码等
   %	引用时候要可以采用：\cite{引用标志1,引用标志2，....}
   ```

   

3. 代码如下：

```latex
\bibliographystyle{plain}

	引用一篇文章\cite{article1}
	
	引用一本书\cite{book1}
	
	
\begin{document}	
	\begin{thebibliography}{99}
		\bibitem{article1}陈立辉，苏伟，蔡川，陈小云. \emph{基于LaTeX的Web数据公式提取方法研究}[J]. 计算机科学. 2014(06)
		\bibitem{book1}William H. Press,Saul A. Teukolsky, William T. Vertterling,Brian P. Flannery, \emph{Numerical Recipes 3rd Edition:The Art of Scientific Computing} Cambridge University Press, New York,2007.
	\end{thebibliography}
	
\end{document}
```



### 自动导入参考文献

1. 参考网站

   [https://www.latexstudio.net/archives/7131]: 

   

   [https://blog.csdn.net/qq_21391921/article/details/78138139]: 

2. zotero结合知网批量导出

### 通过用BibTex的方式

1. 百度学术![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/4ba307a3e43ba36f46ad22b9935adefc.png)

2. 必应学术![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/a88c49cf66d73596c491ece38c634b39.png)

3. 百度学术和必应学术都是选择引用-导入链接-BibTex复制，然后复制到论文目录下的bib文件下

4. 其中表示如下：

   ```latex
   %导言区
   \documentclass{article}
   
   \usepackage{ctex}
   
   \bibliographystyle{plain}
   
   %正文区
   \begin{document}
   	
   	这是一个参考文献的引用：\cite{mittelbach2004}
   	
   	这是一个百度学术的引用：\cite{article3}
   	
   	这是一个必应学术的引用：\cite{coronavirus}
   	
   	\bibliography{book}
   
   \end{document}
   ```

### 利用zotero和知网导出条目

1. 知网中选择目标文献，导入zotero
2. 在zotero中导出为bib文件
3. 将bib文件放置论文目录下或者同一个bib里面
4. ![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/aa955ba101ad76e4f03fa837630c0ba1.png)

![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/0b9f29201345c5e7573f179c439133a5.png)

### 具体引用方式

1. 每次通过工具-清理辅助文件

2. 代码用：

   ```latex
   	
   	这是一个参考文献的引用：\cite{mittelbach2004}
   	
   	这是一个百度学术的引用：\cite{article3}
   	
   	这是一个必应学术的引用：\cite{coronavirus}
   	
   	这是一个知网的引用：\cite{__nodate-1}
   	
   	%显示未引用的但是在bib文件里面的条目用：
   	\nocite{*}
   	\bibliography{book,cnki}
   ```

### 参考文献样式

参考文献标准样式可选项为：

```latex
前面需要导入的包：
\bibliographystyle{plain}
```

> plain：按字母的顺序排列，比较次序为作者、年度和标题；
> unsrt：样式同plain，只是按照引用的先后排序；
> alpha：用作者名首字母+年份后两位作标号，以字母顺序排序；
> abbrv：类似plain，将月份全拼改为缩写，更显紧凑；
> ieeetr：国际电气电子工程师协会期刊样式；
> acm：美国计算机学会期刊样式；
> siam：美国工业和应用数学学会期刊样式；
> apalike：美国心理学学会期刊样式。

## LaTeX的自定义命令和环境

1. 实现内容与格式基本分离的思想

### 新定义命令

1. ```latex
   %\newcommand-定义命令
   %命令只能由字母组成，不能以\end开头
   %\newcommand{命令}[参数个数][首参数默认值]{具体定义}
   
   %\newcommand可以是简单的字符串替换，例如：
   %使用\PRC 相当于 People's Republic of \emph{China}
   
   \newcommand{\PRC}{People's Republic of \emph{China}}
   ```

   

### 带参数的命令

1. ```latex
   %\newcommand也可以使用参数
   %参数个数可以从1到9，使用时用#1,#2，#3，，，#9表示,分别表示不同的参数
   \newcommand\loves[2]{#1 喜欢 #2}
   \newcommand\hateby [2] {#2 不受 #1 喜欢}
   
   %\newcommand{cmd}{def}的参数也可以有默认值
   %指定参数个数的同时制定了首个参数的默认值，那么这个命令的第一个参数就成为了可选参%数，要用中括号指定
   \newcommand\love[3][喜欢]{#2#1#3}
   ```

   

### 重定义命令

1. ```latex
   %\renewcommand-重新定义命令
   %只用于已有的命令
   %\renewcommand{命令}[参数个数][首参数默认值]{具体定义}
   \renewcommand\abstractname{简介}%\renewcommand-重新定义命令
   %只用于已有的命令
   %\renewcommand{命令}[参数个数][首参数默认值]{具体定义}
   \renewcommand\abstractname{简介}
   ```

   

### 新定义环境

1. ```latex
   %也可以用同样的方法定义或者重定义环境
   %\newenvironment{<环境名称>}[<参数个数>][<首参数默认值>]
   %				{<环境前定义>}
   %				{<环境后定义>}
   %\renewenvironment{<环境名称>}[<参数个数>][<首参数默认值>]
   %				{<环境前定义>}
   %				{<环境后定义>}
   \newenvironment{myabstract}[1][摘要]
   {\small
   	\begin{center}
   		\bfseries #1
   	\end{center}
   	}{\begin{equation}
   	\end{equation}}
   ```

   

### 具体使用

1. 代码

   ```latex
   %正文区
   \begin{document}
   	\PRC
   	
   	\loves{猫儿}{鱼}
   	
   	\hateby{猫儿}{鱼}
   	
   	\love{猫儿}{鱼}
   	
   	\love{最爱}{猫儿}{鱼}
   	
   	\begin{abstract}
   		这是一段摘要...
   	\end{abstract}
   
   	\begin{myabstract}
   		这是一段自定义的摘要....
   	\end{myabstract}
   \end{document}
   ```

d\loves[2]{#1 喜欢 #2}
   \newcommand\hateby [2] {#2 不受 #1 喜欢}
   
   %\newcommand{cmd}{def}的参数也可以有默认值
   %指定参数个数的同时制定了首个参数的默认值，那么这个命令的第一个参数就成为了可选参%数，要用中括号指定
   \newcommand\love[3][喜欢]{#2#1#3}
   ```

   

### 重定义命令

1. ```latex
   %\renewcommand-重新定义命令
   %只用于已有的命令
   %\renewcommand{命令}[参数个数][首参数默认值]{具体定义}
   \renewcommand\abstractname{简介}%\renewcommand-重新定义命令
   %只用于已有的命令
   %\renewcommand{命令}[参数个数][首参数默认值]{具体定义}
   \renewcommand\abstractname{简介}
   ```

   

### 新定义环境

1. ```latex
   %也可以用同样的方法定义或者重定义环境
   %\newenvironment{<环境名称>}[<参数个数>][<首参数默认值>]
   %				{<环境前定义>}
   %				{<环境后定义>}
   %\renewenvironment{<环境名称>}[<参数个数>][<首参数默认值>]
   %				{<环境前定义>}
   %				{<环境后定义>}
   \newenvironment{myabstract}[1][摘要]
   {\small
   	\begin{center}
   		\bfseries #1
   	\end{center}
   	}{\begin{equation}
   	\end{equation}}
   ```

   

### 具体使用

1. 代码

   ```latex
   %正文区
   \begin{document}
   	\PRC
   	
   	\loves{猫儿}{鱼}
   	
   	\hateby{猫儿}{鱼}
   	
   	\love{猫儿}{鱼}
   	
   	\love{最爱}{猫儿}{鱼}
   	
   	\begin{abstract}
   		这是一段摘要...
   	\end{abstract}
   
   	\begin{myabstract}
   		这是一段自定义的摘要....
   	\end{myabstract}
   \end{document}
   ```

2. 效果图![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/25f9c8d26e6689886e803994f494c739.png)
