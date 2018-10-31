# alecthomas/chroma [![explain]][source] [![translate-svg]][translate-list]

<!-- [![size-img]][size] -->

[explain]: http://llever.com/explain.svg
[source]: https://github.com/chinanf-boy/Source-Explain
[translate-svg]: http://llever.com/translate.svg
[translate-list]: https://github.com/chinanf-boy/chinese-translate-list
[size-img]: https://packagephobia.now.sh/badge?p=Name
[size]: https://packagephobia.now.sh/result?p=Name

「 纯Go中的通用语法高亮显示器 」

[中文](./readme.md) | [english](https://github.com/alecthomas/chroma)

---

## 校对 🀄️

<!-- doc-templite START generated -->
<!-- repo = 'alecthomas/chroma' -->
<!-- commit = '5a473179cfe450c6d80407452c241428de387f6b' -->
<!-- time = '2018-10-21' -->

| 翻译的原文 | 与日期        | 最新更新 | 更多                       |
| ---------- | ------------- | -------- | -------------------------- |
| [commit]   | ⏰ 2018-10-21 | ![last]  | [中文翻译][translate-list] |

[last]: https://img.shields.io/github/last-commit/alecthomas/chroma.svg
[commit]: https://github.com/alecthomas/chroma/tree/5a473179cfe450c6d80407452c241428de387f6b

<!-- doc-templite END generated -->

### 贡献

欢迎 👏 勘误/校对/更新贡献 😊 [具体贡献请看](https://github.com/chinanf-boy/chinese-translate-list#贡献)

## 生活

[help me live , live need money 💰](https://github.com/chinanf-boy/live-need-money)

---

### 目录

<!-- START doctoc -->
<!-- END doctoc -->

# Chroma  - 纯Go中的通用语法高亮显示器[![](https://godoc.org/github.com/alecthomas/chroma?status.svg)](http://godoc.org/github.com/alecthomas/chroma) [![Build Status](https://travis-ci.org/alecthomas/chroma.png)](https://travis-ci.org/alecthomas/chroma) [![Gitter chat](https://badges.gitter.im/alecthomas.png)](https://gitter.im/alecthomas/Lobby)

> **注意:**由于Chroma刚刚发布,其API仍在不断变化.也就是说,高级接口不应该发生显着变化.

Chroma采用源代码和其他结构化文本,并将其转换为语法高亮HTML,ANSI色文本等.

色度很大程度上依赖于[Pygments来做](http://pygments.org/),包括Pygments词法分析器和样式的翻译.

## 目录

<!-- MarkdownTOC -->

1.  [支持的语言](#supported-languages)
2.  [使用库](#using-the-library)
    1.  [快速开始](#quick-start)
    2.  [识别语言](#identifying-the-language)
    3.  [格式化输出](#formatting-the-output)
    4.  [HTML格式化程序](#the-html-formatter)
3.  [更多详情](#more-detail)
    1.  [词法分析器](#lexers)
    2.  [格式化程序](#formatters)
    3.  [样式](#styles)
4.  [命令行界面](#command-line-interface)
5.  [与Pygments相比有什么缺失?](#whats-missing-compared-to-pygments)

<!-- /MarkdownTOC -->

## 支持的语言

| 字首 | 语言 |
| :-: | --- |
| 一个 | ABNF,ActionScript,ActionScript 3,Ada,Angular2,ANTLR,ApacheConf,APL,AppleScript,Awk |
| 乙 | 芭蕾舞女演员,Base Makefile,Bash,Batchfile,BlitzBasic,BNF,Brainfuck |
| C | C,C#,C ++,Cassandra CQL,CFEngine3,cfstatement / ColdFusion,CMake,COBOL,CSS,Cap'n Proto,Ceylon,ChaiScript,Cheetah,Clojure,CoffeeScript,Common Lisp,Coq,Crystal,Cython |
| D | Dart,Diff,Django / Jinja,Docker,DTD |
| Ë | EBNF,Elixir,Elm,EmacsLisp,Erlang |
| F | Factor,Fish,Forth,Fortran,FSharp |
| G | GAS,GDScript,GLSL,Genshi,Genshi HTML,Genshi Text,Gnuplot,Go,Go HTML模板,Go Text Template,Groovy |
| H | 把手,Haskell,Haxe,Hexdump,HTML,HTTP,Hy |
| 一世 | 伊德里斯,INI,Io |
| Ĵ | Java,JavaScript,JSON,Jsx,Julia,Jungle |
| ķ | 科特林 |
| 大号 | Lighttpd配置文件,LLVM,Lua |
| 中号 | Mako,Markdown,Mason,Mathematica,MiniZinc,Modula-2,MonkeyC,MorrowindScript,Myghty,MySQL |
| ñ | NASM,Newspeak,Nginx配置文件,Nim,Nix |
| Ø | Objective-C,OCaml,Octave,OpenSCAD,组织模式 |
| P | PacmanConf,Perl,PHP,Pig,PkgConfig,Plaintext,PL / pgSQL,PostgreSQL SQL方言,PostScript,POVRay,PowerShell,Prolog,协议缓冲区,Puppet,Python,Python 3 |
| Q | QBasic中 |
| \[R | R,Racket,Ragel,reg,reStructuredText,Rexx,Ruby,Rust |
| 小号 | Sass,Scala,Scheme,Scilab,SCSS,Smalltalk,Smarty,Snobol,Solidity,SPARQL,SQL,SquidConf,Swift,systemd,Systemverilog |
| Ť | TASM,Tcl,Tcsh,Termcap,Terminfo,Terraform,TeX,Thrift,TOML,TradingView,Transact-SQL,Turtle,Twig,TypeScript,TypoScript,TypoScriptCssData,TypoScriptHtmlData |
| V | verilog,VHDL,VimL |
| w ^ | WDTE |
| X | XML,Xorg |
| ÿ | YAML |

*我将尝试使此部分保持最新,但可以显示权威列表`chroma --list`.*

## 使用库

与Pygments一样,Chroma具有以下概念[词法分析器](https://github.com/alecthomas/chroma/tree/master/lexers),[格式化](https://github.com/alecthomas/chroma/tree/master/formatters)和[款式](https://github.com/alecthomas/chroma/tree/master/styles).

Lexers将源文本转换为标记流,样式指定标记类型如何映射到颜色,格式化程序将标记和样式转换为格式化输出.

每个包都有一个包,包含一个全局包`Registry`所有已注册实现的变量.还有一些辅助函数可以在每个包中使用注册表,例如按名称查找词法分析器或匹配文件名等.

在所有情况下,如果无法确定词法分析器,格式化程序或样式,`nil`将被退回.在这种情况下,您可能希望默认为`Fallback`每个包中的值,提供合理的默认值.

### 快速开始

存在一个便利功能,可以用来简单地格式化一些源文本,而不需要任何努力:

```go
err := quick.Highlight(os.Stdout, someSourceCode, "go", "html", "monokai")
```

### 识别语言

要突出显示代码,首先必须确定编写代码的语言.有三种主要方法:

1.  从文件名中检测语言.

    ```go
    lexer := lexers.Match("foo.go")
    ```

2.  通过其Chroma语法ID明确指定语言(可从中获取完整列表)`lexers.Names()`).

    ```go
    lexer := lexers.Get("go")
    ```

3.  从其内容中检测语言.

    ```go
    lexer := lexers.Analyse("package main\n\nfunc main()\n{\n}\n")
    ```

在所有情况下,`nil`如果语言无法识别,将被退回.

```go
if lexer == nil {
  lexer = lexers.Fallback
}
```

在这一点上,应该指出一些词法分析者可能非常健谈.为了缓解这种情况,您可以使用合并词法分析器将相同令牌类型的运行合并到一个令牌中:

```go
lexer = chroma.Coalesce(lexer)
```

### 格式化输出

识别语言后,您需要选择格式化程序和样式(主题).

```go
style := styles.Get("swapoff")
if style == nil {
  style = styles.Fallback
}
formatter := formatters.Get("html")
if formatter == nil {
  formatter = formatters.Fallback
}
```

然后获取令牌上的迭代器:

```go
contents, err := ioutil.ReadAll(r)
iterator, err := lexer.Tokenise(nil, string(contents))
```

最后,从迭代器格式化标记:

```go
err := formatter.Format(w, style, iterator)
```

### HTML格式化程序

默认情况下`html`注册格式化程序生成带有嵌入式CSS的独立HTML.通过更多的灵活性可以获得`formatters/html`包.

首先,可以使用以下构造函数选项自定义格式化程序生成的输出:

-   `Standalone()`- 使用嵌入式CSS生成独立HTML.
-   `WithClasses()`- 使用类而不是内联样式属性.
-   `ClassPrefix(prefix)`- 为每个生成的CSS类添加前缀.
-   `TabWidth(width)`- 以字符为单位设置渲染的标签宽度.
-   `WithLineNumbers()`- 渲染行号(样式与`LineNumbers`).
-   `HighlightLines(ranges)`- 突出显示这些范围内的线条`LineHighlight`).
-   `LineNumbersInTable()`- 使用表格来格式化行号和代码,而不是跨度.

如果`WithClasses()`使用时,可以从格式化程序中获取相应的CSS:

```go
formatter := html.New(html.WithClasses())
err := formatter.WriteCSS(w, style)
```

## 更多详情

### 词法分析器

见[Pygments文档](http://pygments.org/docs/lexerdevelopment/)有关实施词法分析器的详细信息.大多数概念直接适用于Chroma,但请参阅现有的lexer实现以获取实际示例.

在许多情况下,可以使用附带的Python 3脚本直接从Pygments自动转换词法分析器`pygments2chroma.py`.我用的东西如下:

```
python3 ~/Projects/chroma/_tools/pygments2chroma.py \
  pygments.lexers.jvm.KotlinLexer \
  > ~/Projects/chroma/lexers/kotlin.go \
  && gofmt -s -w ~/Projects/chroma/lexers/*.go
```

见附注[Pygments来做,lexers.go](https://github.com/alecthomas/chroma/blob/master/pygments-lexers.txt)有关词法分析器的列表,以及有关导入它们的一些问题的说明.

### 格式化程序

Chroma支持HTML输出,以及8色,256色和真彩色的终端输出.

一个`noop`包含仅输出令牌文本的格式化程序,以及a`tokens`formatter输出原始令牌.后者对调试词法分析器非常有用.

### 样式

色度风格使用[相同的语法](http://pygments.org/docs/styles/)作为Pygments.

所有Pygments样式都已使用.转换为Chroma`_tools/style.py`脚本.

有关可用样式及其外观的快速概述,请查看[色度风格画廊](https://xyproto.github.io/splash/docs/).

## 命令行界面

包括Chroma的命令行界面.它可以安装:

```
go get -u github.com/alecthomas/chroma/cmd/chroma
```

## 与Pygments相比有什么缺失?

-   由于各种原因(欢迎提出请求),有相当多的词法分子:
    -   复杂语言的Pygments词法分析器通常包含处理某些方面的自定义代码,例如Perl6在正则表达式中嵌套代码的能力.这需要时间和精力来转换.
    -   我大多只转换我听过的语言,以降低移植成本.
-   为简单起见,省略了Pygments的一些更深奥的特征.
-   虽然Chroma API支持内容检测,但很少有语言支持它们.我计划在某个时候实施统计分析仪,但时间不够.
