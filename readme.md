# alecthomas/chroma [![explain]][source] [![translate-svg]][translate-list]

<!-- [![size-img]][size] -->

[explain]: http://llever.com/explain.svg
[source]: https://github.com/chinanf-boy/Source-Explain
[translate-svg]: http://llever.com/translate.svg
[translate-list]: https://github.com/chinanf-boy/chinese-translate-list
[size-img]: https://packagephobia.now.sh/badge?p=Name
[size]: https://packagephobia.now.sh/result?p=Name

「 纯 Go 中的通用语法高亮显示器 」

[中文](./readme.md) | [english](https://github.com/alecthomas/chroma)

---

## 校对 ✅

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

- [ ] [加个chroma的使用例子，==]

### 贡献

欢迎 👏 勘误/校对/更新贡献 😊 [具体贡献请看](https://github.com/chinanf-boy/chinese-translate-list#贡献)

## 生活

[help me live , live need money 💰](https://github.com/chinanf-boy/live-need-money)

---

# Chroma - 纯 Go 中的通用语法高亮显示器[![](https://godoc.org/github.com/alecthomas/chroma?status.svg)](http://godoc.org/github.com/alecthomas/chroma) [![Build Status](https://travis-ci.org/alecthomas/chroma.png)](https://travis-ci.org/alecthomas/chroma) [![Gitter chat](https://badges.gitter.im/alecthomas.png)](https://gitter.im/alecthomas/Lobby)

> **注意:**由于 Chroma 刚刚发布,其 API 仍在不断变化.也就是说,高级接口应该不会发生太大变化.

Chroma 采用源码和其他结构的文本,将其转换为语法高亮的 HTML,ANSI 色彩文本等.

Chroma 很大程度上依赖于[Pygments :python](http://pygments.org/),包括 Pygments 的`词法分析器-lexers`和`样式-styles`的转移.

## 目录

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
<!-- END doctoc -->

- [支持的语言](#%E6%94%AF%E6%8C%81%E7%9A%84%E8%AF%AD%E8%A8%80)
- [使用库](#%E4%BD%BF%E7%94%A8%E5%BA%93)
  - [让我们快速开始](#%E8%AE%A9%E6%88%91%E4%BB%AC%E5%BF%AB%E9%80%9F%E5%BC%80%E5%A7%8B)
  - [识别语言](#%E8%AF%86%E5%88%AB%E8%AF%AD%E8%A8%80)
  - [格式化输出](#%E6%A0%BC%E5%BC%8F%E5%8C%96%E8%BE%93%E5%87%BA)
  - [HTML 格式化程序](#html-%E6%A0%BC%E5%BC%8F%E5%8C%96%E7%A8%8B%E5%BA%8F)
- [更多详情](#%E6%9B%B4%E5%A4%9A%E8%AF%A6%E6%83%85)
  - [Lexers-词法分析器](#lexers-%E8%AF%8D%E6%B3%95%E5%88%86%E6%9E%90%E5%99%A8)
  - [格式化程序](#%E6%A0%BC%E5%BC%8F%E5%8C%96%E7%A8%8B%E5%BA%8F)
  - [样式](#%E6%A0%B7%E5%BC%8F)
- [命令行界面](#%E5%91%BD%E4%BB%A4%E8%A1%8C%E7%95%8C%E9%9D%A2)
- [与 Pygments 相比有什么缺失?](#%E4%B8%8E-pygments-%E7%9B%B8%E6%AF%94%E6%9C%89%E4%BB%80%E4%B9%88%E7%BC%BA%E5%A4%B1)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## 支持的语言

| 字首 | 语言                                                                                                                                                                                |
| ---- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| A    | ABNF, ActionScript, ActionScript 3, Ada, Angular2, ANTLR, ApacheConf, APL, AppleScript, Awk                                                                                         |
| B    | Ballerina, Base Makefile, Bash, Batchfile, BlitzBasic, BNF, Brainfuck                                                                                                               |
| C    | C, C#, C++, Cassandra CQL, CFEngine3, cfstatement/ColdFusion, CMake, COBOL, CSS, Cap'n Proto, Ceylon, ChaiScript, Cheetah, Clojure, CoffeeScript, Common Lisp, Coq, Crystal, Cython |
| D    | Dart, Diff, Django/Jinja, Docker, DTD                                                                                                                                               |
| E    | EBNF, Elixir, Elm, EmacsLisp, Erlang                                                                                                                                                |
| F    | Factor, Fish, Forth, Fortran, FSharp                                                                                                                                                |
| G    | GAS, GDScript, GLSL, Genshi, Genshi HTML, Genshi Text, Gnuplot, Go, Go HTML Template, Go Text Template, Groovy                                                                      |
| H    | Handlebars, Haskell, Haxe, Hexdump, HTML, HTTP, Hy                                                                                                                                  |
| I    | Idris, INI, Io                                                                                                                                                                      |
| J    | Java, JavaScript, JSON, Jsx, Julia, Jungle                                                                                                                                          |
| K    | Kotlin                                                                                                                                                                              |
| L    | Lighttpd configuration file, LLVM, Lua                                                                                                                                              |
| M    | Mako, Markdown, Mason, Mathematica, MiniZinc, Modula-2, MonkeyC, MorrowindScript, Myghty, MySQL                                                                                     |
| N    | NASM, Newspeak, Nginx configuration file, Nim, Nix                                                                                                                                  |
| O    | Objective-C, OCaml, Octave, OpenSCAD, Org Mode                                                                                                                                      |
| P    | PacmanConf, Perl, PHP, Pig, PkgConfig, Plaintext, PL/pgSQL, PostgreSQL SQL dialect, PostScript, POVRay, PowerShell, Prolog, Protocol Buffer, Puppet, Python, Python 3               |
| Q    | QBasic                                                                                                                                                                              |
| R    | R, Racket, Ragel, reg, reStructuredText, Rexx, Ruby, Rust                                                                                                                           |
| S    | Sass, Scala, Scheme, Scilab, SCSS, Smalltalk, Smarty, Snobol, Solidity, SPARQL, SQL, SquidConf, Swift, systemd, Systemverilog                                                       |
| T    | TASM, Tcl, Tcsh, Termcap, Terminfo, Terraform, TeX, Thrift, TOML, TradingView, Transact-SQL, Turtle, Twig, TypeScript, TypoScript, TypoScriptCssData, TypoScriptHtmlData            |
| V    | verilog, VHDL, VimL                                                                                                                                                                 |
| W    | WDTE                                                                                                                                                                                |
| X    | XML, Xorg                                                                                                                                                                           |
| Y    | YAML                                                                                                                                                                                |

_我将保持此部分的更新,但更及时与权威的列表在`chroma --list`._

## 使用库

与 Pygments 一样,Chroma 具有以下概念[词法分析器-lexers](https://github.com/alecthomas/chroma/tree/master/lexers),[格式化-formatters](https://github.com/alecthomas/chroma/tree/master/formatters)和[款式-styles](https://github.com/alecthomas/chroma/tree/master/styles).

Lexers 将源文本转换为标记流数据,styles 指定相应的标记类型如何映射到颜色,格式化程序将标记和 styles 转换为格式化输出.

每个概念都有一个包,包含一个全局包`Registry`，其中具有所有已注册实现的变量。还有一些辅助函数可以让每个包都能使用注册表,例如按名称查找词法分析器，或匹配文件名等.

在所有情况下,如果无法确定词法分析器,格式化程序或样式,`nil`将返回。在这种情况下,您可能希望默认为每个包中的`Fallback`值，此提供合理的默认值.

### 让我们快速开始

存在一个便利功能,可以用来简单格式一些源文本,而不需要任何努力:

```go
err := quick.Highlight(os.Stdout, someSourceCode, "go", "html", "monokai")
```

### 识别语言

要高亮代码,首先必须确定编写代码的语言.有三种主要方法:

1.  从文件名中检测语言.

    ```go
    lexer := lexers.Match("foo.go")
    ```

2.  通过其 Chroma 语法 ID 明确指定语言(可从`lexers.Names()`中获取完整列表).

    ```go
    lexer := lexers.Get("go")
    ```

3.  从其内容中，分析语言.

    ```go
    lexer := lexers.Analyse("package main\n\nfunc main()\n{\n}\n")
    ```

在所有情况下,如果语言无法识别，返回一个`nil`.

```go
if lexer == nil {
  lexer = lexers.Fallback
}
```

在这一点上,应该指出一些词法分析者可能不尽如人意。为了缓解这种情况,您可以使用合并词法分析器，将相同标记类型的运行合并到一个标记中:

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

然后获取**Token-标记**上的迭代器:

```go
contents, err := ioutil.ReadAll(r)
iterator, err := lexer.Tokenise(nil, string(contents))
```

最后,从迭代器格式化标记:

```go
err := formatter.Format(w, style, iterator)
```

### HTML 格式化程序

默认情况下，已注册的`html`格式化程序会生成带有嵌入式 CSS 的独立 HTML。更多的灵活性可以试试`formatters/html`包.

首先,可以使用以下构造函数选项，自定义格式化程序生成的输出:

-   `Standalone()`- 使用嵌入式 CSS 生成独立 HTML.
-   `WithClasses()`- 使用类，而不是内联样式属性.
-   `ClassPrefix(prefix)`- 为每个生成的 CSS 类添加前缀.
-   `TabWidth(width)`- 以字符为单位设置渲染的标签宽度.
-   `WithLineNumbers()`- 渲染行号(`LineNumbers`样式).
-   `HighlightLines(ranges)`- 突出显示这些范围内的线条(`LineHighlight`样式).
-   `LineNumbersInTable()`- 使用table,来格式化行号和代码,而不是 span.

如果是使用`WithClasses()`,可以从格式化程序中，获取相应的 CSS:

```go
formatter := html.New(html.WithClasses())
err := formatter.WriteCSS(w, style)
```

## 更多详情

### Lexers-词法分析器

见[Pygments 文档](http://pygments.org/docs/lexerdevelopment/)有关实施词法分析器的详细信息.大多数概念直接适用于 Chroma,但请参阅现有的 lexer 实现，以获取实际示例.

在许多情况下,可以使用附带的 Python 3 脚本`pygments2chroma.py`直接从 Pygments 那里，自动转换词法分析器。如下:

```
python3 ~/Projects/chroma/_tools/pygments2chroma.py \
  pygments.lexers.jvm.KotlinLexer \
  > ~/Projects/chroma/lexers/kotlin.go \
  && gofmt -s -w ~/Projects/chroma/lexers/*.go
```

见[pygments-lexers.go](https://github.com/alecthomas/chroma/blob/master/pygments-lexers.txt)的笔记，其记录了有关词法分析器的列表,以及有关导入它们的一些问题的说明.

### 格式化程序

Chroma 支持 HTML 输出,以及 8 色,256 色和真彩色的终端输出.

一个`noop`仅包含，输出标记文本的格式化程序,以及 一个`tokens`formatter 输出原始标记。后者对调试词法分析器非常有用.

### 样式

Chroma styles使用与Pygments[相同的语法](http://pygments.org/docs/styles/).

所有 Pygments 样式都被`_tools/style.py`脚本转换为 Chroma的了.

有关可用样式，及其外观的简易概述,请查看[Chroma 主题画廊](https://xyproto.github.io/splash/docs/).

## 命令行界面

包括 Chroma 的命令行界面.它可以安装:

```
go get -u github.com/alecthomas/chroma/cmd/chroma
```

## 与 Pygments 相比有什么缺失?

-   由于各种原因(欢迎提出请求),其中相当多的lexers:
    -    Pygments对 复杂语言的词法分析器，通常包含处理某些方面的自定义代码,例如 Perl6 在正则表达式中嵌套代码的能力。这需要时间和精力来转换.
    -   我大多只转换我听过的语言,以降低移植成本.
-   为简单起见,省略了 Pygments 的一些太深奥的功能.
-   虽然 Chroma API 支持内容检测,但仅有少有语言支持。我计划在哪个时候实现一个统计分析仪,但时间不够.
