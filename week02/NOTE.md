

# 编程语言通识

首先，我们来了解一下为什么要学习编译原理？



相信在看这篇文章的朋友都已经学了 JavaScript 了吧，但是我想问一下大家真的懂 JavaScript 吗？能描述出 JavaScript 的语法规则吗？ 能理解语法的逻辑结构吗？知道 JavaScript 是如何解析的和执行的吗？所以，大家整的懂 JavaScript 吗？反正我是至今都没有底气说自己仅"精通" JavaScript。



现在计算机的技术变化的很快，目前我们使用的那些很流行的框架与工具可能几年内就会变成过时的东西。但是，计算机科学的整体思维不会变，在学习中我们更应该注重思维能力的培养、如何清晰表达自己的能力、如何高效的解决问题的能力。这些方面的能力在我看来是具有持久的价值的。而学好编程语言基础可以提升我们的思维能力。



## 什么是语言？



关于什么是语言这个问题，大家可能会想,语言，我们每天说的汉语、英语，甚至我们计算机常用的编程语言不都是语言么？在当今的世界上，编程语言可能达到了几千种，他们的语言规则都千差万别，但是他们总体来看都是有一个共同的特点，都是**由一个字符集（有限字母表上的字母的集合所）组成的**，也就是说我们是可以用一种统一的抽象方法来进行讨论，研究编程语言的。形式语言是对编程语言的形式化描述，这里边我们可以引申出两种重要的方向：



- 研究产生语言的形式规则 —— **文法（G****rammar****）**
- 识别语言的装置 —— **机器**



## 文法类型分类（乔姆斯基谱系）



| **文法** | **语言**       | **自动机**           | **产生式规则**        |
| -------- | -------------- | -------------------- | --------------------- |
| 0-型     | 递归可枚举语言 | 图灵机               | 无限制                |
| 1-型     | 上下文相关语言 | 线性有界非确定图灵机 | α*A*β -> αγβ          |
| 2-型     | 上下文无关语言 | 非确定下推自动机     | *A* -> γ              |
| 3-型     | 正则语言       | 有限状态自动机       | *A* -> *aB**A* -> *a* |



形式文法是形式语言中字符串的一套**产生式规则**。这些规则描述了如何用语言的**字母表**生产符合语法的规则的字符串。**文法不描述字符串的含义，也不描述在任何上下文中可以用他们做什么——只描述他们的形式。**为了让你更好的理解形式文法，接下来我们用**产生式 (BNF)**来帮助我们理解：



## 产生式（BNF）



巴克斯范式（Backus Normal Form），是一种用于表示上下文无关文法的语言，上下文无关文法描述了形式语言。



### 规则

- 用尖括号括起来的名称来表示语法结果名
- 语法结构分成基础结构和需要用其他语法结构定义的复合结构

- - 基础结构称终结符
  - 复合结构称非终结符

- 引号和中间的字符表示终结符
- 可以有括号
- \* 表示重复多次
- | 表示或
- \+ 表示至少一次



### 举个例子（用BNF编写带括号的四则运算）：

```
<Number> ="0" | "1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9" 
  <DecimalNumber> = "0" | (("0" | "1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9" ) <Number>+ )
    <MultiplicationAndDivisionExpression> = <DecimalNumber> ("*" <DecimalNumber>)*  ("/" <DecimalNumber>)*
      <AdditionAndSubtractionExpression> = <MultiplicationAndDivisionExpression> ("+" <MultiplicationAndDivisionExpression>)* ("-" <MultiplicationAndDivisionExpression>)*
        <LogicalExpression> = <AdditionAndSubtractionExpression>  ("||" <AdditionAndSubtractionExpression>)*("&&" <AdditionAndSubtractionExpression>)*
          <PrimaryExpression> = <LogicalExpression> | "("<LogicalExpression>")"
   
```

从上面例子可以得出，上下文无关文法的规则是 **A** **-> γ 。**



## 图灵完备性



- 图灵完备性

- - 命令式——图灵机

- - - `goto`
    - `if` 和 `while`

- - 声明式——lambda

- - - 递归





## **动态与静态**





- 动态：

- - 在用户的设备 / 在线服务器上
  - 产品实际运行时
  - Runtime

- 静态：

- - 在程序员的设备上
  - 产品开发时
  - Compiletime



## 类型系统



- 动态类型系统与静态类型系统
- 强类型与弱类型

- - 是否可隐式转换

- 复合类型

- - 结构体
  - 函数签名

- 子类型

- - 逆变 / 协变





# 词法

词法规定了语言的最小语义单元：**token**（可以翻译成“标记”或者“词”，这里统一把 token 翻译成词）。从字符到词的整个过程是没有结构的，只要符合词的规则，就构成词，一般来说，词法设计不会包含冲突。

## 概述



我们先来看一看 JavaScript 的词法定义。JavaScript 源代码中的输入可以这样分类：



- **WhiteSpace** 空白字符
- **LineTerminator** 换行符
- **Comment** 注释
- **ToKen** 词

- - **IdentifierName** 标识符名称，典型案例是我们使用的变量名，关键字也包含在内。
  - **Puctiator** 符号，我们使用的运算符合大括号等。
  - **NumericLiteral**  数字字面量，就是我们写的数字
  - **StringLiteral** 字符串字面量，就是我们用引号或者双引号引起来的字面量
  - **Template** 字符串模板，用反引号 ` 括起来的字面量



### 注意：



这个设计符合比较通用的编程语言设计方式，不过，JavaScript 中有一些特别之处，我下面就来讲讲特别在哪里。



首先是**除法和正则表达式冲突问题**。我们都知道，JavaScript 不但支持除法运算符“ / ”和“ /= ”，还支持用斜杠括起来的正则表达式“ /abc/ ”。



但是，这时候对词法分析来说，其实是没有办法处理的，所以 JavaScript 的解决方案是定义两组词法，然后靠语法分析传一个标志给词法分析器，让它来决定使用哪一套词法。



JavaScript 词法的另一个特别设计是**字符串模板**，模板语法大概是这样的：``Hello, ${name}`` 。理论上，`${ } ` 内部可以放任何 JavaScript 表达式代码，而这些代码是以“ } ” 结尾的，也就是说，这部分词法不允许出现“ } ”运算符。



是否允许“ } ”的两种情况，与除法和正则表达式的两种情况相乘就是四种词法定义，所以你在 JavaScript 标准中，可以看到四种定义：



- InputElementDiv;
- InputElementRegExp;
- InputElementRegExpOrTemplateTail;
- InputElementTemplateTail;



为了解决这两个问题，标准中还不得不把除法、正则表达式字面量和“ } ”从 token 中单独抽出来，用词上，也把原本的 Token 改为 CommonToken。



但是，从理解的角度上出发，不应该受到影响，所以我们依然把它们归类到 token 来理解。



## WhiteSpace 空白字符



空白符号用于提高源文本的可读性，并将标记(不可分割的词法单位)彼此分开，但在其他方面无关紧要



| **Code Point** | **Name**                  | **Abbreviation** | **String** | **描述**       |
| -------------- | ------------------------- | ---------------- | ---------- | -------------- |
| U+0009         | CHARACTER TABULATION      | <TAB>            | \t         | 缩进TAB符      |
| U+000B         | LINE TABULATION           | <VT>             |            | 垂直Tab符      |
| U+000C         | FORM FEED (FF)            | <FF>             | \f         | 分页符         |
| U+0020         | SPACE                     | <SP>             | \s         | 普通空格       |
| U+00A0         | NO-BREAK SPACE            | <NBSP>           |            | 非断行空格     |
| U+FEFF         | ZERO WIDTH NO-BREAK SPACE | <ZWNBSP>         |            | 零宽非断行空格 |



- **<FF>** 分页符，现代已经很少有打印源程序的事情发生了，所以这个字符在 JavaScript 源代码中很少用到。
- **<NBSP>** 非断行空格，它是 SP 的一个变体，在文字排版中，可以避免因为空格在此处发生断行，其它方面和普通空格完全一样。多数的 JavaScript 编辑环境都会把它当做普通空格（因为一般源代码编辑环境根本就不会自动折行……）。HTML 中，很多人喜欢用的   最后生成的就是它了。
- **<ZWNBSP>** 是 ES5 新加入的空白符，是 Unicode 中的零宽非断行空格，在以 UTF 格式编码的文件中，常常在文件首插入一个额外的 U+FEFF，解析 UTF 文件的程序可以根据 U+FEFF 的表示方法猜测文件采用哪种 UTF 编码方式。这个字符也叫做“bit order mark”。



> 很多公司的编码规范要求 JavaScript 源代码控制在 ASCII 范围内，那么，就只有五种空白可用了。



## LineTerminator 换行符



JavaScript 中只提供了 4 种字符作为换行符。

| **Code Point** | **Name**             | **Abbreviation** | **String** | **描述**               |
| -------------- | -------------------- | ---------------- | ---------- | ---------------------- |
| U+000A         | LINE FEED (LF)       | <LF>             | \n         | 最正常换行符           |
| U+000D         | CARRIAGE RETURN (CR) | <CR>             | \r\n       | 回车                   |
| U+2028         | LINE SEPARATOR       | <LS>             |            | Unicode 中的行分隔符   |
| U+2029         | PARAGRAPH SEPARATOR  | <PS>             |            | Unicode 中的段落分隔符 |



## Comment 注释



注释可以是单行的，也可以是多行的。多行注释不能嵌套。



```
/* MultiLineCommentChars */ 
// SingleLineCommentChars
```



多行注释中允许自由地出现MultiLineNotAsteriskChar，也就是除了`*`之外的所有字符。而每一个*之后，不能出现正斜杠符` /`。



除了四种 LineTerminator 之外，所有字符都可以作为单行注释。



我们需要注意，多行注释中是否包含换行符号，会对 JavaScript 语法产生影响，对于“no line terminator”规则来说，带换行的多行注释与换行符是等效的。





## IdentifierName 标识符名称 



IdentifierName可以以美元符 `$` 、下划线 `_` 或者 **Unicode 字母**开始，除了开始字符以外，IdentifierName中还可以使用 Unicode 中的连接标记、数字、以及连接符号。



IdentifierName的任意字符可以使用 JavaScript 的 **Unicode 转义写法**，使用 Unicode 转义写法时，没有任何字符限制。



IdentifierName可以是**Identifier、NullLiteral、BooleanLiteral**或者**keyword**，在**ObjectLiteral**中，IdentifierName还**可以被直接当做属性名称使用**。



仅当不是保留字的时候，IdentifierName会被解析为Identifier。



在 JavaScript 中，保留关键字有：



| abstract | arguments | boolean    | break     | byte         |
| -------- | --------- | ---------- | --------- | ------------ |
| case     | catch     | char       | class*    | const        |
| continue | debugger  | default    | delete    | do           |
| double   | else      | enum*      | eval      | export*      |
| extends* | false     | final      | finally   | float        |
| for      | function  | goto       | if        | implements   |
| import*  | in        | instanceof | int       | interface    |
| let      | long      | native     | new       | null         |
| package  | private   | protected  | public    | return       |
| short    | static    | super*     | switch    | synchronized |
| this     | throw     | throws     | transient | true         |
| try      | typeof    | var        | void      | volatile     |
| while    | with      | yield      |           |              |



## Punctuator 符号



因为前面提到的除法和正则问题, / 和 /= 两个运算符被拆分为 DivPunctuator，因为前面提到的字符串模板问题，}也被独立拆分。加在一起，所有符号为：

 

| {    | （)  | !=   | .    | ...  |
| ---- | ---- | ---- | ---- | ---- |
| ;    | ,    | <    | >    | <=   |
| >=   | ==   | ===  | !==  | +    |
| -    | *    | %    | **   | ++   |
| --   | <<   | >>   | >>>  | &    |
| \|   | ^    | !    | ~    | &&   |
| \|\| | ?    | :    | =    | +=   |
| -=   | *=   | %=   | **=  | <<=  |

##  

## NumbericLiteral 数字字面量



JavaScript 规范中规定的数字字面量可以支持四种写法：十进制数、二进制整数、八进制整数和十六进制整数。



十进制的 Number 可以带小数，小数点前后部分都可以省略，但是不能同时省略，我们看几个例子：



```
.01
12.
12.01
```



这都是合法的数字直面量。这里就有一个问题，也是我们标题提出的问题，我们看一段代码：



```
12.toString()
```



这时候12. 会被当做省略了小数点后面部分的数字而看成一个整体，所以我们要想让点单独成为一个 token，就要加入空格，这样写：



```
12 .toString()
```



数字直面量还支持科学计数法，例如：



```
10.24E+2
10.24e-2
10.24e2
```



这里 e 后面的部分，只允许使用整数。当以0x 0b 或者0o 开头时，表示特定进制的整数：



```
0xFA
0o73
0b10000
```



上面这几种进制都不支持小数，也不支持科学计数法。



## StringLiteral 字符串字面量



JavaScript 中的 StringLiteral 支持单引号和双引号两种写法。

```
" DoubleStringCharacters "
' SingleStringCharacters '
```



单双引号的区别仅仅在于写法，在双引号字符串直面量中，双引号必须转义，在单引号字符串直面量中，单引号必须转义。字符串中其他必须转义的字符是 `\` 和所有换行符。



JavaScript 中支持四种转义形式，还有一种虽然标准没有定义，但是大部分实现都支持的八进制转义。



第一种是单字符转义。 即一个反斜杠 `\` 后面跟一个字符这种形式。



有特别意义的字符包括有SingleEscapeCharacter所定义的 9 种，见下表：

| **转义字符** | **转义Unicode** | **产生字符** |
| ------------ | --------------- | ------------ |
| '            | U+0022          | "            |
| "            | U+0027          | '            |
| \            | U+005C          | \            |
| b            | U+0008          | <BS>         |
| f            | U+000C          | <FF>         |
| n            | U+000A          | <LF>         |
| r            | U+000D          | <CR>         |
| t            | U+0009          | <HT>         |
| v            | U+000B          | <VT>         |

除了这 9 种字符、数字、x 和 u 以及所有的换行符之外，其它字符经过 `\` 转义后都是自身。



## RegularExpressionLiteral 正则表达式字面量



正则表达式由 Body 和 Flags 两部分组成，例如：



```
/RegularExpressionBody/g
```



其中 Body 部分至少有一个字符，第一个字符不能是 *（因为 /* 跟多行注释有词法冲突）。



正则表达式有自己的语法规则，在词法阶段，仅会对它做简单解析。



正则表达式并非机械地见到 `/` 就停止，在正则表达式`[ ]`中的 `/` 就会被认为是普通字符。我们可以看一个例子：

```
/[/]/.test("/");
```

除了`\`、`/` 和`[` 三个字符之外，JavaScript 正则表达式中的字符都是普通字符。



用`\`和一个非换行符可以组成一个转义，`[ ]`中也支持转义。正则表达式中的 flag 在词法阶段不会限制字符。



虽然只有 ig 几个是有效的，但是任何 IdentifierPart（Identifier 中合法的字符）序列在词法阶段都会被认为是合法的。



## Template 字符串模板



从语法结构上，Template 是个整体，其中的 `${ }` 是并列关系。



但是实际上，在 JavaScript 词法中，包含` ${ }` 的 Template，是被拆开分析的，如：

```
`a${b}c${d}e`
```



它被拆成了五个部分：



- ``a${ ` 这个被称为模板头
- `}c${` 被称为模板中段
- `}e`` 被称为模板尾
- `b` 和 `d` 都是普通标识符



实际上，这里的词法分析过程已经跟语法分析深度耦合了。



不过我们学习的时候，大可不必按照标准和引擎工程师这样去理解，可以认为模板就是一个由反引号括起来的、可以在中间插入代码的字符串。



模板支持添加处理函数的写法，这时模板的各段会被拆开，传递给函数当参数：

```
function f(){ 
  console.log(arguments);
}

var a = "world"
f`Hello ${a}!`;// [["Hello", "!"], world]
```



模板字符串不需要关心大多数字符的转义，但是至少 `${` 和 `` `还是需要处理的。



模板中的转义跟字符串几乎完全一样，都是使用 `\`。





## 作业：

- 写一个正则 匹配所有Number字面量

```
let reg = /^[+-]?(((0|([1-9]\d*))(\.\d*)?(e[+-]?\d+)?)|(0[Oo][0-7]+)|(0[Xx][0-9a-fA-F]+)|(0[Bb][01]+))$/g
```

- 完成 UTF8__Encoding 的函数

```javascript

```

- 写一个正则表达式来匹配字符串

```
let reg = /^['"]['"]$/
```