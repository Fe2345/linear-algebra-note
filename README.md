# [一个LaTeX的数学笔记模板](https://zhuanlan.zhihu.com/p/604236564)

用知乎上的模板魔改的，可以用来做我想要的数学笔记。

## 使用

### `main.tex` 主文件

```latex
\def\allfiles{}
\documentclass[12pt, a4paper, oneside, UTF8]{ctexbook}
\def\path{./config}
\input{config/_config}
\begin{document}
\include{config/cover}

\include{chap0/chap}
% \include{chap1/chap}
% \include{chap2/chap}
% ...通过上述方式引入对应章节

\end{document}
```

### `config/_config.tex` 配置文件

```latex
% 包以及配置【有需要添加其他包以及配置，添加在 package.tex 文件中】
\input{\path/package.tex}

% 定理环境，内置两种定理环境以及中英文版本，可通过修改引入文件改变
% theorem1.tex 及 theorem1_zh.tex / theorem0.tex 以 theorem0_zh.tex
\input{\path/theorem1.tex}

% 自定义命令【自定义命令，添加在 custom.tex 文件中】
\input{\path/custom.tex}

% 封面，可选 0 -> 3 四种， 0 为默认封面，无需引入其他文件
\def\myIndex{0}
% 不为 0 时，需引入下方的封面配置文件，取消注释即可
% \input{\path/cover_package_\myIndex.tex}

% ######################## 模板配置信息 ##########################

% #标题
\def\myTitle{一份 \LaTeX 的笔记模板}

% #作者名称
\def\myAuthor{Guo}

% #封面页面显示日期
\def\myDateCover{\today}

% #前言页面显示日期
\def\myDateForeword{2023 年 1 月 28 日}

% #前言标题
\def\myForeword{前言}

% 前言内容
\def\myForewordText{
    这里写前言内容

    第二行
}

% 副标题
\def\mySubheading{格物致知，慎思明辨}
```

### `config/custom.tex` 自定义命令

```latex
% 微分符号
\def\d{\mathrm{d}}

% 实数集
\def\R{\mathbb{R}}

% 加粗
\newcommand{\bs}[1]{\boldsymbol{#1}}

% 向量
\newcommand{\ora}[1]{\overrightarrow{#1}}

% 空行
\newcommand{\myspace}[1]{\par\vspace{#1\baselineskip}}

% 依赖 \usepackage{stackengine} 调整表格高度
\newcommand{\xrowht}[2][0]{\addstackgap[.5\dimexpr#2\relax]{\vphantom{#1}}}

% 自定义行高的 cases 和 vmatrix 环境
\newenvironment{ca}[1][1]{\linespread{#1} \selectfont \begin{cases}}{\end{cases}}
\newenvironment{vx}[1][1]{\linespread{#1} \selectfont \begin{vmatrix}}{\end{vmatrix}}

% 表格内长内容换行
\newcommand{\tabincell}[2]{\begin{tabular}{@{}#1@{}}#2\end{tabular}}

% 平行符号 //
\newcommand{\pll}{\kern 0.56em/\kern -0.8em /\kern 0.56em}

% 散度 旋度
\newcommand{\dive}[1][F]{\mathrm{div}\;\bs{#1}}
\newcommand{\rotn}[1][A]{\mathrm{rot}\;\bs{#1}}
```

### `chap[number]/chap.tex` 章节文件

```latex
\ifx\allfiles\undefined
\documentclass[12pt, a4paper, oneside, UTF8]{ctexbook}
\def\path{../config}
\input{../config/_config}
\begin{document}
% \input{../config/cover}        % 注释与否决定单独编译时，是否编译封面
\else
\fi
%  正文
%  正文
%  正文
\ifx\allfiles\undefined
\end{document}
\fi
```

## 魔改部分

新环境：para

创建一个层次段落，其中可以用\point创建一个小标题

```tex
\begin{para}{0}
			\point{定义}
			\begin{defn}{伯努利数的级数定义}{}
				符合以下级数展开的数列称为伯努利数：
				\begin{equation}
					\frac{z}{e^z -1} = \sum_{n=0}^{\infty}\frac{B_n}{n!}z^n
				\end{equation}
			\end{defn}
			以上的定义十分简洁，但是难以计算。但是显然，借助Taylor级数我们可以推导出等价的递归定义：
			\begin{defn}{伯努利数的递归定义}{}
				\begin{equation}
					B_0=1,B_n=-\frac{1}{n+1}\sum\limits_{k=1}^{n}\binom{n+1}{k+1}B_{n-k}
				\end{equation}
			\end{defn}
			\begin{proof}
				利用级数定义中的展开式反推：
				
				\because $\left(e^z-1\right)\left(\frac{z}{e^z-1}\right)=z$
				
				\therefore $z\left[\frac{1}{1!}+\frac{1}{2!}z+...\cdots+\frac{1}{(n+1)!}z^n+R_1(z)\right]\left[B_0+B_1 z+\cdots+\frac{B_n}{n!}z^n+R_2(z)\right]=z$
				
				对比常数项可知：$B_0=1$
				
			\end{proof}
			\begin{them}{欧拉-麦克劳林公式}{}
				假设$f(x)$无穷阶可导，那么：
				\begin{equation}
					\sum\limits_{a\leq n<b}f(n) = \int_{a}^{b}f(x)\d x+\sum\limits_{k=1}^{\infty}\frac{B_k}{k!}f^{(k-1)}(x)\big|_{a}^{b}+{(-1)}^{m}\int_{a}^{b}\frac{B_m({x})}{m!}f^{(m)}(x)\d x
				\end{equation}
				
			\end{them}
		\end{para}
```

参数：0为1.2.3.这样，1为①②③这样，2为(i)(ii)(iii)这样，其他值当作0处理

\point的参数就是标题内容，不需要写编号，可以自动编号