> 14 . Applicative State Transition Systems (AST Systems)

## 14. 应用型状态转换系统 （AST 系统）

> 14.1 Introduction

### 14.1 介绍

> This section sketches a class of systems mentioned earlier as alternatives to von Neumann systems. It must be emphasized again that these applicative state transition systems are put forward not as practical programming systems in their present form, but as examples of a class in which applicative style programming is made available in a history sensitive, but non-von Neumann system. These systems are loosely coupled to states and depend on an underlying applicative system for both their programming language and the description of their state transitions. The underlying applicative system of the AST system described below is an FFP system, but other applicative systems could also be used. 

本节将概述之前提到的替代冯·诺伊曼系统的另一类系统。需要再次强调的是，这些应用型状态转换系统并不是以其当前形式作为实用的编程系统提出的，而是作为一类前序敏感（history sensitive）的非冯·诺伊曼系统中实现应用型风格编程的示例。这样的系统在编程语言和状态转换的描述上，均是状态松耦合的，并且依赖于底层的应用型系统。尽管下面描述的 AST 系统的底层应用型系统是一个 FFP 系统，但同样适用于其他应用型系统。

> To understand the reasons for the structure of AST systems, it is helpful first to review the basic structure of a von Neumann system, Algol, observe its limitations, and compare it with the structure of AST systems. After that review a minimal AST system is described; a small, top-down, self-protecting system program for file maintenance and running user programs is given, with directions for installing it in the AST system and for running an example user program. The system program uses "name functions" instead of conventional names and the user may do so too. The section concludes with subsections discussing variants of AST systems, their general properties, and naming systems.

为了理解 AST 系统结构的成因，我们首先需要回顾冯·诺伊曼系统 (例如 Algol) 的基本结构，了解其局限性，并将其与 AST 系统的结构进行比较。然后，我们将描述一个最小的 AST 系统，并提供一个用于维护文件和运行用户程序的小型自顶向下的自我保护系统程序，以及在 AST 系统中安装该程序和运行示例用户程序的说明。该系统程序使用“命名函数”代替传统名称，用户也可以这样做。本节最后将通过子节讨论 AST 系统的变体、它们的通用属性以及命名系统。

> 14.2 The Structure of Algol Compared to That of AST Systems

### 14.2 Algol 与 AST 系统的结构对比

> An Algol program is a sequence of statements, each representing a transformation of the Algol state, which is a complex repository of information about the status of various stacks, pointers, and variable mappings of identifiers onto values, etc. Each statement communicates with this constantly changing state by means of complicated protocols peculiar to itself and even to its different parts (e.g., the protocol associated with the variable $x$ depends on its occurrence on the left or right of an assignment, in a declaration, as a parameter, etc.).

Algol 程序由一系列语句组成，每个语句都代表了对 Algol 状态的转换。Algol 状态是一个复杂的存储库，包含了各种栈、指针、标识符到值的变量映射等信息的状态。每个语句都通过与其自身甚至其不同部分相关的复杂协议与此不断变化的状态进行通信。（例如，与变量 $x$ 相关的协议取决于它出现在赋值的左边还是右边，是在声明中，还是作为参数等）。

> It is as if the Algol state were a complex "store" that communicates with the Algol program through an enormous "cable" of many specialized wires. The complex communications protocols of this cable are fixed and include those for every statement type. The "meaning" of an Algol program must be given in terms of the total effect of a vast number of communications with the state via the cable and its protocols (plus a means for identifying the output and inserting the input into the state). By comparison with this massive cable to the Algol state/store, the cable that is the von Neumann bottleneck of a computer is a simple, elegant concept.


可以将 Algol 状态想象成一个复杂的“存储器”，它通过一根由许多专用电线组成的庞大“电缆”与 Algol 程序进行通信。这条电缆的复杂通信协议是固定的，并且涵盖了所有语句类型。Algol 程序的“含义”必须通过电缆及其协议与状态进行大量通信的全部效果来定义 (还要加上识别输出和将输入插入状态的方法)。与连接 Algol 状态/存储器的这条巨大电缆相比，被视为冯·诺伊曼机瓶颈的小电缆则是一个简单而优雅的概念。

> Thus Algol statements are not expressions representing state-to-state functions that are built up by the use of orderly combining forms from simpler state-to-state functions. Instead they are complex *messages* with context-dependent parts that nibble away at the state. Each part transmits information to and from the state over the cable by its own protocols. There is no provision for applying general functions to the *whole* state and thereby making large changes in it. The possibility of large, powerful transformations of the state $\rm S$ by function application, $\text{S} \to f:\rm S$, is in fact inconceivable in the von Neumann--cable and protocol--context: there could be no assurance that the new state $f:\rm S$ would match the cable and its fixed protocols unless $f$ is restricted to the tiny changes allowed by the cable in the first place. 

可见，Algol 语句不是状态到状态的函数表达式，更不要说这些函数是通过使用有序的组合形式从更简单的状态转换函数构建出来的。相反，它们是复杂的 *消息*，包含依赖于上下文的片段，一点一点地改变状态。每个片段都以自己专属的协议经由电缆与状态进行信息传递。Algol 没有提供任何机制，使得通用函数能够应用于 *整个* 状态，从而对其进行大的更改。在冯·诺依曼架构（电缆和协议）下，通过函数应用实现对状态 $\rm S$ 的大范围、强有力的转换（ $\text{S} \to f:\rm S$ ）实际上是不可想象的：除非 $f$ 从一开始就受到电缆限制，仅允许微小更改，否则无法保证新状态 $f:\rm S$ 与电缆及其固定协议匹配。

> We want a computing system whose semantics does not depend on a host of baroque protocols for communicating with the state, and we want to be able to make large transformations in the state by the application of general functions. AST systems provide one way of achieving these goals. Their semantics has two protocols for getting information from the state: (1) get from it the definition of a function to be applied, and (2) get the whole state itself. There is one protocol for changing the state: compute the new state by function application. Besides these communications with the state, AST semantics is applicative (i.e. FFP). It does not depend on state changes because the state does not change at all during a computation. Instead, the result of a computation is output and a new state. The structure of an AST state is slightly restricted by one of its protocols: It must be possible to identify a definition (i.e. cell) in it. Its structure--it is a sequence--is far simpler than that of the Algol state.

我们需要一个计算系统，它的语义不依赖于与状态通信的繁琐（baroque）协议，并且我们希望能够通过应用通用函数对状态进行大规模转换。AST 系统就提供了实现这些目标的方法。语义上，有两个获取状态信息的协议：（1）应用一个定义了从状态中获取的函数，（2）获取整个状态本身。一个改变状态信息的协议：应用函数计算出新状态。除了这些与状态的通信之外，AST 语义是应用型的 (如 FFP)。它不依赖于状态改变，因为在计算过程中状态根本不会改变。相反，计算的结果是输出和一个新的状态。AST 状态的结构受到其中一个协议的轻微限制：必须能够识别其中的定义 (即单元格)。这样的状态结构就是一个序列，比 Algol 状态的结构简单得多。

> Thus the structure of AST systems avoids the complexity and restrictions of the von Neumann state (with its communications protocols) while achieving greater power and freedom in a radically different and simpler framework.

因此，AST 系统的结构避免了冯·诺伊曼状态（及其通信协议）的复杂性和限制，同时在一种截然不同且更简单的框架中实现了更强大的功能和自由度。

> 14.3 Structure of an AST System 

### 14.3 AST 系统的结构

> An AST system is made up of three elements: 

AST 系统由三部分组成：

> 1) An applicative subsystem (such as an FFP system). 
> 2) A state $\rm D$ that is the set of definitions of the applicative subsystem. 
> 3) A set of transition rules that describe how inputs are transformed into outputs and how the state $\rm D$ is changed. 

1. 一个应用型子系统（比如 FFP 系统）；
2. 一个状态 $\rm D$ ，即应用型子系统的定义集；
3. 一个转换规则集，描述了输入如何变成输出，以及状态 $\rm D$ 如何改变。

> The programming language of an AST system is just that of its applicative subsystem. (From here on we shall assume that the latter is an FFP system.) Thus AST systems can use the FP programming style we have discussed. The applicative subsystem cannot change the state $\rm D$ and it does not change during the evaluation of an expression. A new state is computed along with output and replaces the old state when output is issued. (Recall that a set of definitions $\rm D$ is a sequence of cells; a cell name is the name of a defined function and its contents is the defining expression. Here, however, some cells may name data rather than functions; a data name $n$ will be used in $\uparrow n$ (fetch $n$) whereas a function name will be used as an operator itself.) 

AST 系统的编程语言也就是应用型子系统的编程语言。（以下我们假设应用型子系统就是一个 FFP 系统。）因此，AST 系统可以使用我们之前讨论过的 FP 编程风格。应用型子系统不能改变状态 $\rm D$ ，尤其是在表达式求值过程中。一个新的状态只能是与输出一并计算得到的，并在输出后替换就旧的状态。（回想一下，定义集 D 是一个单元格序列；单元格名称是已定义函数的名称，其内容是定义表达式。但是，在这里，一些单元格会命名数据而不是函数；数据名称 $n$ 将用于 $\uparrow n$ （获取 $n$），而函数名称本身将用作运算符。）

> We give below the transition rules for the elementary AST system we shall use for examples of programs. These are perhaps the simplest of many possible transition rules that could determine the behavior of a great variety of AST systems. 

下面我们将给出用于示例程序的初级 AST 系统的转换规则。在决定各种 AST 系统的行为里，这些规则或许会是众多可能性中最简单的。

> 14.3.1 Transition rules for an elementary AST system.

#### 14.3.1 初级 AST 系统的转换规则

> When the system receives an input $x$, it forms the application ( $SYSTEM:x$ ) and then proceeds to obtain its meaning in the FFP subsystem, using the current state $\rm D$ as the set of definitions. $SYSTEM$ is the distinguished name of a function defined in $\rm D$ (i.e. it is the "system program"). Normally the result is a pair

当系统接受到输入 $x$ ，会被形式化为应用（ $SYSTEM:x$ ），接着在 FFP 子系统里，结合作为定义集的当前状态 $\rm D$ ，处理并得到其意义。 $SYSTEM$ 是定义集 $\rm D$ 已经存在的函数名（比如，“system program”）。通常结果会是一个二元组

$$
\mu(SYSTEM : x) = < o, d >
$$

> where $o$ is the system output that results from input $x$ and $d$ becomes the new state $\rm D$ for the system's next input. Usually $d$ will be a copy or partly changed copy of the old state. If $\mu(SYSTEM:x)$ is not a pair, the output is an error message and the state remains unchanged.

其中 $o$ 表示系统从输入 $x$ 得到的结果（输出）， $d$ 则是系统下次输入的新状态 $\rm D$ 。通常， $d$ 会是旧状态的副本或部分变化的副本。若 $\mu(SYSTEM:x)$ 不是一个二元组，则输出会是一个错误消息，且状态保持不变。

> 14.3.2 Transition rules: exception conditions and startup.

#### 14.3.2 转换规则：异常条件和启动

> Once an input has been accepted, our system will not accept another (except $< RESET, x >$, see below) until an output has been issued and the new state, if any, installed. The system will accept the input $< RESET, x >$ at any time. There are two cases: (a) If $SYSTEM$ is defined in the current state $\rm D$, then the system aborts its current computation without altering $\rm D$ and treats $x$ as a new normal input; (b) if $SYSTEM$ is not defined in $\rm D$, then $x$ is appended to $\rm D$ as its first element. (This ends the complete description of the transition rules for our elementary AST system.)

一旦输入被接受，系统就拒绝其它的（ $< RESET, x >$ 除外，见后文）直到输出和新状态产生，如果有的话。系统在任何时候都接受输入 $< RESET, x >$ ，这会有两种情况：

1. 若当前状态 $\rm D$ 中定义了 $SYSTEM$ ，则系统中止当前计算，保持 $\rm D$ 不变，并把 $x$ 视作新的常规输入；
2. 若当前状态 $\rm D$ 中未定义 $SYSTEM$ ，则将 $x$ 追加到 $\rm D$ 作为第一个元素。（我们初级 AST 系统的转换规则至此已全部描述完成。）

> If $SYSTEM$ is defined in $\rm D$ it can always prevent any change in its own definition. If it is not defined, an ordinary input $x$ will produce $\mu(SYSTEM:x) = \bot$ and the transition rules yield an error message and an unchanged state; on the other hand, the input $< RESET, < CELL, SYSTEM, s > >$ will define $SYSTEM$ to be $s$. 

若 $\rm D$ 中定义了 $SYSTEM$ ，则其定义不会发生任何变化。反之，若未定义，一个普通的输入 $x$ 将产生 $\mu(SYSTEM:x) = \bot$ ，并且转换规则会返回一个错误消息和一个未变化的状态。另一方面，输入 $< RESET, < CELL, SYSTEM, s > >$ 会把 $SYSTEM$ 定义为 $x$ 。

> 14.3.3 Program access to the state; the function $\rho DEFS$

#### 14.3.3 程序访问状态之函数 $\rho DEFS$

> Our FFP subsystem is required to have one new primitive function, $\rm defs$ , named $DEFS$ such that for any object $x \ne \bot$, 

我们的 FFP 子系统必须要有一个新的原生函数， $\rm defs$ ，命名为 $DEFS$ ，且对任意满足 $x \ne \bot$ 的对象有，

$$
defs:x = \rho DEFS:x = \text{D}
$$

> where $\rm D$ is the current state and set of definitions of the AST system. This function allows programs access to the whole state for any purpose, including the essential one of computing the successor state.

其中 $\rm D$ 是当前状态和 AST 系统的定义集。这个函数允许程序出于任何目的访问整个状态，其中一个重要目的是计算后继状态。

> 14.4 An Example of a System Program

### 14.4 一个系统程序的示例

> The above description of our elementary AST system, plus the FFP subsystem and the FP primitives and functional forms of earlier sections, specify a complete history-sensitive computing system. Its input and output behavior is limited by its simple transition rules, but otherwise it is a powerful system once it is equipped with a suitable set of definitions. As an example of its use we shall describe a small system program, its installation, and operation.

有了上面初级 AST 系统的描述，再加上 FFP 系统、FP 原生函数以及前面章节的函数式，现在我们可以指定一个完整的前序敏感（history-sensitive）的计算系统了。尽管系统的输入和输出行为受到前面简单转换规则的限制，可以一旦具备了合适的定义集，它将是一个强大无匹的系统。我们将描述一个小巧的系统程序，包含它的安装和操作，作为这个系统的示例。

> Our example system program will handle queries and updates for a file it maintains, evaluate FFP expressions, run general user programs that do not damage the file or the state, and allow authorized users to change the set of definitions and the system program itself. All inputs it accepts will be of the form $< key, input >$ where $key$ is a code that determines both the input class (*system-change*, *expression*, *program*, *query*, *update*) and also the identity of the user and his authority to  use the system for the given input class. We shall not specify a format for $key$. $Input$ is the input itself, of the class given by $key$.

我们的示例系统程序将处理其维护的文件的查询和更新，计算 FFP 表达式，运行不会损坏文件或状态的通用用户程序，并允许授权用户更改定义集和系统程序本身。它接受的所有输入都将采用 $< key, input >$ 的形式，其中：

- $key$ 是一个代码，用于确定输入类别（系统变动、表达式、程序、查询或更新），以及用户的身份和他对给定输入类别使用系统的权限。我们不会限定 $key$ 的格式；
- $input$ 是输入本身，其类别由 $key$ 指定。

> 14.4.1 General plan of the system program

#### 14.4.1 系统程序的通用计划

> The state $\rm D$ of our AST system will contain the definitions of all nonprimitive functions needed for the system program and for users' programs. (Each definition is in a cell of the sequence $\rm D$.) In addition, there will be a cell in $\rm D$ named $FILE$ with contents $file$, which the system maintains. We shall give FP definitions of functions and later show how to get them into the system in their FFP form. The transition rules make the input the operand of $SYSTEM$, but our plan is to use name-functions to refer to data, so the first thing we shall do with the input is to create two cells named $KEY$ and $INPUT$ with contents $key$ and $input$ and append these to $\rm D$. This sequence of cells has one each for $key$, $input$, and $file$; it will be the operand of our main function called $\text{subsystem}$. Subsystem can then obtain $key$ by applying $\uparrow KEY$ to its operand, etc. Thus the definition 

我们 AST 系统的状态 $\rm D$ 将包含系统程序和用户程序所需的所有非原生函数的定义。（每个定义都在序列 $\rm D$ 的一个单元格中。）此外， $\rm D$ 中还会有一个名为 $FILE$ 的单元格，其内容为系统维护的 $file$ 。我们将给出函数的 FP 定义，稍后会展示如何将它们以 FFP 形式放入系统中。转换规则将输入设为 $SYSTEM$ 的操作数，但我们的计划是使用命名函数引用它们，因此首先，我们将输入创建为两个名为 $KEY$ 和 $INPUT$ 的单元格，它们的内容分别为 $key$ 和 $input$，然后将它们追加到 $\rm D$ 中。这个单元格序列就分别包含 $key$ 、 $input$ 和 $file$ ，并作为名为 $\text{subsystem}$ 的主函数的操作数。这样， $\text{subsystem}$ 便可通过应用 $\uparrow KEY$ 来获取 $key$ 的内容。 其定义如下

$$
\textbf{Def } \text{system} \equiv 
  pair \to \text{subsystem} \circ f; [\overline{NONPAIR}, \text{defs}]
$$

> where 

其中

$$
f \equiv \downarrow INPUT \circ [2, \downarrow KEY \circ [1, \text{defs}]]
$$

> cause the system to output $NONPAIR$ and leave the state unchanged if the input is not a  pair. Otherwise, if it is $< key, input >$, then

当输入不是二元组是，系统则会输出 $NONPAIR$ 和未变化的状态。反之，如果是 $< key, input >$ ， 那么

$$
f:< key, input > = << CELL, INPUT, input >, < CELL, KEY, key >, d_1, \dots, d_n >
$$

> where $\text{D} = < d_1, \dots, d_n >$. (We might have constructed a different operand than the one above, one with just three cells, for $key$, $input$, and $file$. We did not do so because real programs, unlike $\rm subsystem$, would contain many name functions referring to data in the state, and this "standard" construction of the operand would suffice then as well.) 

其中 $\text{D} = < d_1, \dots, d_n >$ 。（我们可以构建一个不同与上面的操作数，它会有三个单元格，分别对应于 $key$ 、 $input$ 和 $file$ 。不这么做的原因在于，真实的程序，不像 $\rm subsystem$ ，会在包含许多命名函数来引用状态中数据，而这种“标准”的操作数构建方式在这里已经够用了。）

> 14.4.2 The " $\rm subsystem$ " function

#### 14.4.2 函数 “ $\rm subsystem$ ”

> We now give the FP definition of the function $\rm subsystem$, followed by brief explanations of its six cases and auxiliary functions. 

现在我们给出函数 $\rm subsystem$ 的 FP 定义，以下包含其六种情况的简要解释和辅助函数。

$$
\begin{align*}
\textbf{Def } \text{subsystem} \equiv \qquad\qquad\qquad \\
  \text{is-system-change} \ \circ \uparrow KEY \to
    &\ [\text{report-change}, \text{apply}] \circ [\uparrow INPUT, \text{defs}]; \\
  \text{is-expression} \ \circ \uparrow KEY \to
    &\ [\uparrow INPUT, \text{defs}]; \\
  \text{is-program} \ \circ \uparrow KEY \to
    &\ \text{system-check} \circ \text{apply} \circ [\uparrow INPUT, \text{defs}]; \\
  \text{is-query} \ \circ \uparrow KEY \to
    &\ [\text{query-response} \circ [\uparrow INPUT, \uparrow FILE], \text{defs}]; \\
  \text{is-update} \ \circ \uparrow KEY \to
    &\ [\text{report-update}, \downarrow FILE \circ [\text{update}, \text{defs}]] \circ [\uparrow INPUT, \uparrow FILE]; \\
    &\ [\text{report-error} \circ [\uparrow KEY, \uparrow INPUT], \text{defs}]
\end{align*}
$$

> This $\rm subsystem$ has five " $p \to f;$ " clauses and a final default function, for a  total of six classes of inputs; the treatment of each class is given below. Recall that the $operand$ of $\rm subsystem$ is a sequence of cells containing $key$, $input$, and $file$ as well as all the defined functions of $\rm D$, and that $\text{subsystem}:operand = < output, newstate >$. 

$\rm subsystem$ 有五条“ $p \to f;$ ” 的子句和一个最终的默认函数，以应对六类输入；每类输入的处理后面会给出。回忆一下，$\rm subsystem$ 的 $operand$ 是一个单元格的序列，其中包含了 $key$ 、 $input$ 和 $file$ ，还有定义集 $\rm D$ 里的所有函数，即 $\text{subsystem}:operand = < output, newstate >$ 。

> **System-change inputs**. When $\text{is-system-change} \ \circ \uparrow KEY: operand = \text{is-system-change}: key = T$ , $key$ specifies that the user is authorized to make a system change and that $input = \uparrow INPUT:operand$ represents a function $f$ that is to be applied to $\rm D$ to produce the new state $f:\rm D$. (Of course $f:\rm D$ can be a useless new state; no constraints are placed on it.) The output is a report, namely $\text{report-change}: < input,\rm D >$. 

**系统变动输入** 

当 $\text{is-system-change} \ \circ \uparrow KEY: operand = \text{is-system-change}: key = T$ 成立时， $key$ 指明了用户被授权进行系统改动， $input = \uparrow INPUT:operand$ 表示一个函数 $f$ ，会被作用于 $\rm D$ ，以产生一个新的状态 $f:\rm D$ 。（当然， $f:\rm D$ 新的状态可能毫无用处，这点没有任何限制。）其输出是一个报告，即 $\text{report-change}: < input,\rm D >$。

> **Expression inputs**. When $\text{is-expression}:key = T$, the system understands that the output is to be the meaning of the FFP expression $input$; $\uparrow INPUT:operand$ produces it and it is evaluated, as are all expressions. The state is unchanged. 

**表达式输入**

当 $\text{is-expression}:key = T$ 成立时，系统的输出则是 FFP 表达式 $input$ 的意义； 由 $\uparrow INPUT:operand$ 得到并计算这个表达式，如同所有表达式一样。此时，状态并未改变。

> **Program inputs and system self-protection**. When $\text{is-program}:key = T$, both the output and new state are given by $(\rho input): \text{D} = <output,newstate>$. If $newstate$ contains $file$ in suitable condition and the definitions of system and other protected functions, then $\text{system-check}: <output,newstate> =<output, newstate>$. Otherwise, $\text{system-check}: <output,newstate> = <\text{error-report}, D>$. 

**程序输入和系统自我保护**

当 $\text{is-program}:key = T$ 成立时， $(\rho input): \text{D} = <output,newstate>$ 会给出输出和新的状态。若 $newstate$ 包含 $file$ 条件合适，且满足系统定义和其它保护函数，则 $\text{system-check}: <output,newstate> =<output, newstate>$ ；反之， $\text{system-check}: <output,newstate> = <\text{error-report}, D>$ 。

> Although $program$ inputs can make major, possibly disastrous changes in the state when it produces $newstate$, $\text{system-check}$ can use any criteria to either allow it to become the actual new state or to keep the old. A more sophisticated $\text{system-check}$ might correct only prohibited changes in the state. Functions of this sort are possible because they can always access the old state for comparison with the new state-to-be and control what state transition will finally be allowed.

尽管 $program$ 的输入在产生 $newstate$ 时可能会对系统状态造成重大甚至灾难性的改变，但是 $\text{system-check}$ 可以根据任何标准来决定是允许它成为真正的新的系统状态还是保留旧的状态。更复杂的 $\text{system-check}$ 可能会只纠正那些被禁止的的状态改变。之所以能够实现这样的功能，是因为系统检查总是可以访问旧的系统状态，以便与即将成为的新状态进行比较，并控制最终允许的状态转换。

> **File query inputs**. If $\text{is-query}:key = T$, the function $\text{query-response}$ is designed to produce the output $=$ answer to the query $input$ from its operand $< input,file >$. 

**文件查询输入**

当 $\text{is-query}:key = T$ 成立时，函数 $\text{query-response}$ 被设计用来产生的输出就是，从操作数 $< input,file >$ 中查询 $input$ 的结果。

> **File update inputs**. If $\text{is-update}:key = T$, $input$ specifies a file transaction understood by the function $\text{update}$, which computes $updated\text{-}file = \text{update}: <input,file>$. Thus $\downarrow FILE$ has $< updated\text{-}file, \rm D >$ as its operand and thus stores the updated file in the cell $FILE$ in the new state. The rest of the state is unchanged. The function $\text{report-update}$ generates the output from its operand $< input,file >$. 

**文件更新输入**

当 $\text{is-update}:key = T$ 成立时，函数 $\text{update}$ 会理解 $input$ 指定的文件处理方式，并计算 $updated\text{-}file = \text{update}: <input,file>$ 。而后 $\downarrow FILE$ 作用于操作数 $< updated\text{-}file, \rm D >$ ，并将更新的文件存储到新状态的单元格 $FILE$ 中，但状态其余的部分和之前一样（保持不变）。最后，函数 $\text{report-update}$ 作用于操作数 $< input,file >$ 得到输出。

> 14.4.3 Installing the system program.

#### 14.4.3 安装系统程序

> We have described the function called $\rm system$ by some FP definitions (using auxiliary functions whose behavior is only indicated). Let us suppose that we have FP definitions for all the nonprimitive functions required. Then each definition can be converted to give the name and contents of a cell in $\rm D$ (of course this conversion itself would be done by a better system). The conversion is accomplished by changing each FP function name to its equivalent atom (e.g., $\rm update$ becomes $UPDATE$) and by replacing functional forms by sequences whose first member is the controlling function for the particular form. Thus , $\downarrow FILE \circ [\rm update, defs]$ is converted to 


我们之前使用了一些 FP 定义 (用到的辅助函数仅是示意) 来描述名为 $\rm system$ 的函数。假设我们已经拥有所有必需的非原始函数的 FP 定义，其中每个定义都变成了 $\rm D$ 中给定名字和内容的单元格（当然，转换本身将由一个更高级的系统完成）。变换方法是将每个 FP 函数名替换为其等价的原子（如 $\rm update$ 变为 $UPDATE$ ），并将函数式替换为序列，序列的首元素是该特定形式的控制函数。由此， $\downarrow FILE \circ [\rm update, defs]$ 则会变为

$$
< COMP, < STORE, FILE >, < CONS, UPDATE, DEFS > >
$$

> and the FP function is the same as that represented by the FFP object, provided that $\text{update} \equiv \rho UPDATE$ and $COMP$, $STORE$, and $CONS$ represent the controlling functions for composition, store, and construction. 

这个 FP 函数与 FFP 对象表示是一样的，像是其中的 $\text{update} \equiv \rho UPDATE$ ， $COMP$ 、 $STORE$ 和 $CONS$  这些控制函数分别对应着组合，存储和构建。

> All FP definitions needed for our system can be converted to cells as indicated above, giving a sequence Do. We assume that the AST system has an empty state to start with, hence $SYSTEM$ is not defined. We want to define $SYSTEM$ initially so that it will install its next input as the state; having done so we can then input $\rm D_0$ and all our definitions will be installed, including our program-- $\rm system$ --itself. To accomplish this we enter our first input


系统中所需的所有 FP 定义都能变为如上序列形式的单元格。假定 AST 系统初始的状态为空，也就说 $SYSTEM$ 是没有定义的。要想初始地定义 $SYSTEM$ ，则需要将它视为状态作为下一步的输入。这样一来，我们便能在安装了所有的定义（包括我们程序 $\rm system$ 本身）之后，输入 $\rm D_0$ 。为了做到这点，我们第一个输入是

$$
< RESET, < CELL, SYSTEM, loader > > \text{ where }\\
loader \equiv < CONS, < CONST, DONE >, ID >
$$

> Then, by the transition rule for $RESET$ when $SYSTEM$ is undefined in $\rm D$ , the cell in our intput is put at the head of $\rm D = \phi$ , thus defining $\rho SYSTEM \equiv \rho loader \equiv [\overline{DONE}, \rm id]$ . Our second input is $\rm D_0$, the set of definitions we wish to become the state. The regular transition rule causes the AST system to evaluate $\mu(SYSTEM:\text{D}_0) = [\overline{DONE}, \text{id}]:\text{D}_0 = < DONE, \text{D}_0 >$ . Thus the output from our second input is $DONE$, the new state $\rm D_0$, and $\rho SYSTEM$ is now our system program (which only accepts inputs of the from $< key, input >$).

根据 $RESET$ 的转换规则，当 $\rm D$ 中没有定义 $SYSTEM$ 时，输入的单元格会放置在状态的首位（ $\rm D = \phi$ ），即 $\rho SYSTEM \equiv \rho loader \equiv [\overline{DONE}, \rm id]$ 。第二个输入是  $\rm D_0$ ，我们希望作为状态的定义集。又根据通常的转换规则，AST 系统会解释得到 $\mu(SYSTEM:\text{D}_0) = [\overline{DONE}, \text{id}]:\text{D}_0 = < DONE, \text{D}_0 >$ ，即第二输入后的输出是 $DONE$ ，新的状态为 $\rm D_0$ ，此时的 $\rho SYSTEM$ 就是我们的系统程序（只接受 $< key, input >$ 的输入）。

> Our next task is to load the file (we are given an initial value $file$ ). To load it we input a *program* into the newly installed system that contains $file$ as a constant and stores it in the state; the input is 

下一步就是载入文件（我们这里给一个初始值 $file$ ）。为了载入它，我们需要给新安装的系统输入一个 *程序* ，即包含常量 $file$ ，并将它存储到状态里。这个程序如下

$$
< \textit{program-key}, [\overline{DONE}, \textit{store-file}] > \text{ where} \\
\rho \textit{store-file} \equiv \downarrow FILE \circ [\overline{file}, \text{id}]
$$

> $\textit{Program-key}$ identifies $[\overline{DONE}, \textit{store-file}]$ as a program to be applied to the state $\rm D_0$ to give the output and new state $\rm D_1$, which is:

$\textit{program-key}$ 表示将 $[\overline{DONE}, \textit{store-file}]$ 作为程序作用于状态 $\rm D_0$ ，然后得到输出和新状态 $\rm D_1$ ，即

$$
\rho \textit{store-file}:\text{D}_0 = \downarrow FILE \circ [\overline{file}, \text{id}]: \text{D}_0
$$

> or $\rm D_0$ with a cell containing $file$ at its head. The output is $\overline{DONE}:\text{D}_0 = DONE$. We assume that $\text{system-check}$ will pass $< DONE, \text{D}_1 >$ unchanged. FP expressions have been used in the above in place of the FFP objects the denote, e.g. $\overline{DONE}$ for $< CONST, DONE >$.

也可以认为是 $\rm D_0$ 前增加了一个包含了 $file$ 的单元格。它的输出则是 $\overline{DONE}:\text{D}_0 = DONE$ 。假定函数 $\text{system-check}$ 不做任何改变，上面的返回就是 $< DONE, \text{D}_1 >$ 。上面用到的 FP 表达式就是对应 FFP 对象表示的替换，比如 $\overline{DONE}$ 替换的是 $< CONST, DONE >$ 。

> 14.4.4 Using the system

#### 14.4.4 使用系统

> We have not said how the system's file, queries or updates are structured, so we cannot give a detailed example of file operations. However, the structure of subsystem shows clearly how the system's response to queries and updates depends on the functions $\text{query-response}$ , $\text{update}$ , and $\text{report-update}$.

由于我们不曾说明文件、查询和更新是什么结构，因此无法在这里给出文件操作的具体示例细节。不过，子系统的结构已经清晰地表明系统对于查询和更新响应是依赖函数 $\text{query-response}$ 、 $\text{update}$ 和 $\text{report-update}$ 的。

> Let us suppose that matrices $m$, $n$ named $M$, and $N$ are stored in $\rm D$ and that the function $MM$ described earlier is definded in $\rm D$. Then the input

让我们假定有两个矩阵 $m$ 和 $n$ ，分别命名为 $M$ 和 $N$ 都存储在 $\rm D$ ， 早先定义的函数 $MM$ 也在 $\rm D$ 中。 然后， 输入

$$
< \textit{expression-key}, (MM \circ [\uparrow M, \uparrow N] \circ DEFS: \\\#)>
$$

> would give the product of the two matrices as output and unchanged state. $\textit{Expression-key}$ identifies the application as an expression to be evaluated and since $\text{defs}:$ $\\#$ $= \rm D$ and $[\uparrow M, \uparrow N]: \text{D} = < m, n >$, the value of the expression is the result $MM:< m, n >$, which is the output.

则会输出两个矩阵的积，且状态不变。 $\textit{expression-key}$ 表示其后的应用作为表达式进行解释，正如 $\text{defs}:$ $\\#$ $= \rm D$ ，而 $[\uparrow M, \uparrow N]: \text{D} = < m, n >$ ，那么表达式的值就是 $MM:< m, n >$ 的结果，也就是最后的输出。

> Our miniature system program has no provision for giving control to a user's program to process many inputs, but it world not be difficult to give it that capability while still monitoring the user's program with option of taking control back.

当前的迷你系统程序并不允许用户程序连续处理多个输入。但是，为用户程序加入处理多输入的功能并且仍然保持系统监控用户程序的能力也并不是很难实现的。

> 14.5 Variants of AST Systems

### 14.5 AST 系统的变体

> A major extension of the AST systems suggested above would provide combining forms, "system forms", for building a new AST system from simpler , component AST systems. That is, a system form would take AST systems as parameters and generate a new AST system, just as a functional form takes functions. These system forms would have properties like those of functional forms and would become the "operations" of a useful "algebra of systems" in much the same way that functional forms are the "operations" of the algebra of programs. However, the problem of finding useful system forms is much more difficult, since they must handle $RESETS$, match inputs and outputs, and combine history-sensitive systems rather than fixed functions.

对于之前提到的 AST 系统，一个重要的扩展是提供组合形式，“系统式（system forms）”，用于从更简单的组件 AST 系统构建新的 AST 系统。也就是说，就像函数式接受函数作为参数一样，系统式将把 AST 系统作为参数并生成一个新的 AST 系统。这些系统式将具有类似于函数式的性质，并且会成为一个有用的“系统代数”的“运算”，就像函数式是程序代数的“运算”一样。然而，找到有用的系统式比函数式困难得多，因为它们需要处理“重置（RESETS）”、匹配输入和输出，以及组合前序敏感的系统，而不是固定的函数。

> Moreover, the usefulness or need for system forms is less clear than that for functional forms. The latter are essential for building a great variety of functions from an initial primitive set, whereas, even without system forms, the facilities for building AST systems are already so rich that one could build virtually any system (with the general input and output properties allowed by the given AST scheme). Perhaps system forms would be useful for building systems with complex input and output arrangements.

此外，系统式的实用性或必要性不如函数式清晰。函数式对于用初始的原始函数集构建各种各样的函数是必不可少的，而即使没有系统形式，构建 AST 系统的工具也已经如此丰富，人们几乎可以构建任何系统（仅限于给定 AST 方案允许通用输入和输出的性质）。也许系统式对于构建需要编排复杂输入和输出的系统会很有用。

> 14.6 Remarks About AST Systems

### 14.6 AST 系统小结

> As I have tried to indicate above, there can be innumerable variations in the ingredients of an AST system--how it operates, how it deals with input and output, how and when it produces new states, and so on. In any case, a number of remarks apply to any reasonable AST system:

正如我上面试图指出的那样，AST 系统的组成可以有无数种变化 —— 它如何运行、如何处理输入和输出、如何以及何时生成新状态等等。无论如何，以下几点适用于任何合理的 AST 系统：

> 1) A state transition occurs once per major computation and can have useful mathematical properties. State transitions are not involved in the tiniest details of a computation as in conventional languages; thus the linguistic von Neumann bottleneck has been eliminated. No complex "cable" or protocols are needed to communicate with the state. 
> 2) Programs are written in an applicative language that can accommodate a great range of changeable parts, parts whose power and flexibility exceed that of any von Neumann language so far. The word-at-a-time style is replaced by an applicative style; there is no division of programming into a world of expressions and a world of statements. Programs can be analyzed and optimized by an algebra of programs. 
> 3)  Since the state cannot change during the computation of $\text{system}:x$, there are no side effects. Thus independent applications can be evaluated in parallel. 
> 4)  By defining appropriate functions one can, I believe, introduce major new features at any time, using the same framework. Such features must be built into the framework of a von Neumann language. I have in mind such features as: "stores" with a great variety of naming systems, types and type checking, communicating parallel processes, nondeterminacy and Dijkstra's "guarded command" constructs [^8], and improved methods for structured programming. 
> 5)  The framework of an AST system comprises the syntax and semantics of the underlying applicative system plus the system framework sketched above. By current standards, this is a tiny framework for a language and is the only fixed part of the system. 


[^8]: [Dijkstra, E.W. ,4 Discipline of Programming. Prentice-Hall, Englewood Cliffs, N.J., 1976.](https://dl.acm.org/doi/10.5555/550359)

1. 每次主要计算发生一次状态转换，该转换可以具有有用的数学性质。与传统语言不同，状态转换不会涉及计算的细枝末节；因此，消除了语言学上的冯·诺伊曼瓶颈，也无需复杂的“电缆”或协议与状态通信；
2. 程序使用应用型语言编写，该语言可以容纳各种可变部分，这些部分的强大和灵活性超过了迄今为止任何冯·诺伊曼语言。 应用型风格取代逐字风格，编程不在被分割成表达式和语句两个世界。程序可以通过程序代数进行分析和优化；
3. 由于在计算 $\text{system}:x$ 期间状态不会改变，因此不存在副作用。也就是说，独立的应用可以并行解释；
4. 我相信，通过定义适当的函数，使用相同的框架，可以在任何时候引入大的新特性。对比之下，对于冯·诺伊曼语言，这些大的特性必须内置于框架中。我想到的一些特性包括：具有各种命名系统、类型和类型检查的“存储器”、并行进程间通信、非确定性以及 Dijkstra 的“警戒命令”结构 [^8]，还有结构编程的改进方法；
5. AST 系统的框架包括底层应用型系统的语法和语义，以及上面概述的系统框架。按照当前标准，这对于一种语言来说是一个非常小的框架，并且是系统唯一固定的部分。

> 14.7 Naming Systems in AST and von Neumann Models

### 14.7 AST 系统里的命名与冯·诺伊曼模型

> In an AST system, naming is accomplished by functions as indicated in Section 13.3.3. Many useful functions for altering and accessing a store can be defined (e.g. push, pop, purge, typed fetch, etc.). All these definitions and their associated naming systems can be introduced without altering the AST framework. Different kinds of "stores" (e.g., with "typed cells") with individual naming systems can be used in one program. A cell in one store may contain another entire store. 

在 AST 系统中，命名由函数完成，正如 13.3.3 节所述。还可以定义许多用于更改和访问存储的有用函数（例如压栈、出栈、清除、带类型提取等）。所有这些定义及其相关的命名系统都可以引入，而无需更改 AST 框架。程序中可以使用不同类型的“存储”（例如具有“类型单元格”的存储器），且每个存储都有独立的命名系统。一个存储中的单元格也可能包含另一个整个存储。

> The important point about AST naming systems is that they utilize the functional nature of names (Reynolds' GEDANKEN [^19] also does so to some extent within a von Neumann framework). Thus name functions can be composed and combined with other functions by functional forms. In contrast, functions and names in von Neumann languages are usually disjoint concepts and the function-like nature of names is almost totally concealed and useless, because 
> 1) names cannot be applied as functions;
> 2) there are no general means to combine names with other names and functions; 
> 3) the objects to which name functions apply (stores) are not accessible as objects. 

[^19]: [Reynolds, J.C. GEDANKEN--a simple typeless language based on the principle of completeness and the reference concept. Comm. ACM 13, 5 (May 1970), 308-318.](https://dl.acm.org/doi/10.1145/362349.362364)

AST 命名系统的重要之处在于利用了名称的函数性质（雷诺兹的 GEDANKEN [^19] 也在一定程度上在冯·诺伊曼框架内这样做）。因此，名称函数可以通过函数式与其他函数进行组合和结合。相比之下，冯·诺伊曼语言中的函数和名称通常是分离的概念，名称的类函数本质几乎被完全隐藏且无用，因为

1. 名称不能作为函数应用；
2. 没有通用方法将名称与其他名称和函数结合；
3. 名称函数应用的对象（存储）无法作为对象访问。

> The failure of von Neumann languages to treat names as functions may be one of their more important weaknesses. In any case, the ability to use names as functions and stores as objects may turn out to be a useful and important programming concept, one which should be thoroughly explored.

冯·诺伊曼语言未能将名称视为函数可能是其更重要的弱点之一。无论如何，能够将名称用作函数，将存储用作对象，可能是一个有用且重要的编程概念，值得深入探索。