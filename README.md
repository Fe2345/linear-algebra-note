# 线性代数——个人笔记

## 模板
[一个LaTeX的数学笔记模板](https://zhuanlan.zhihu.com/p/604236564)

用知乎上的模板魔改的，可以用来做我想要的数学笔记。

## 使用

使用`XeLaTeX`编译项目，即可完成构建。

如果使用的是Visual Studio Code的LaTex-Workshop插件，可以将编译配置设置为：
```json
{
"name": "latexmk",
"command": "latexmk",
"args": [
	"-synctex=1",
	"-interaction=nonstopmode",
	"-file-line-error",
	"-pdf",
	"-outdir=%OUTDIR%",
	"%DOC%",
	"-xelatex",
	"-shell-escape"
],
"env": {}
},
```
## 笔记结构

参阅前言和目录

## 网络链接

[知乎专栏](https://www.zhihu.com/column/c_1951744250359288000)

## 贡献

如果你发现了项目的任何漏洞、或者内容上的伪证，欢迎进行Pull Request进行贡献