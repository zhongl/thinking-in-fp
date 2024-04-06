> 12. The Algebra of Programs for FP Systems 

## 12. FP 系统里的程序代数

> 12.1 Introduction 

### 12.1 介绍

> The algebra of the programs described below is the work of an amateur in algebra, and I want to show that it is a game amateurs can profitably play and enjoy, a game that does not require a deep understanding of logic and mathematics. In spite of its simplicity, it can help one to understand and prove things about programs in a systematic, rather mechanical way. 

以下描述的程序代数可能看起来业余，但我想要表明这对于业余爱好者来说也是一个有趣且有益的探索。它并不需要深厚的逻辑数学功底。尽管形式简单，这种代数方法依然可以帮助我们系统地、近乎机械地理解和证明程序相关的问题。

> So far, proving a program correct requires knowledge of some moderately heavy topics in mathematics and logic: properties of complete partially ordered sets, continuous functions, least fixed points of functionals, the first-order predicate calculus, predicate transformers, weakest preconditions, to mention a few topics in a few approaches to proving programs correct. These topics have been very useful for professionals who make it their business to devise proof techniques; they have published a lot of beautiful work on this subject, starting with the work of McCarthy and Floyd, and, more recently, that of BurstaU, Dijkstra, Manna and his associates, Milner, Morris, Reynolds, and many others. Much of this work is based on the foundations laid down by Dana Scott (denotational semantics) and C. A. R. Hoare (axiomatic semantics). But its theoretical level places it beyond the scope of most amateurs who work outside of this specialized field. 

直到现在，证明程序的正确性需要用到一些相当复杂的数学和逻辑知识：

- 偏序集的性质 (properties of complete partially ordered sets)
- 连续函数 (continuous functions)
- 函数式的最小不动点 (least fixed points of functionals)
- 一阶谓词逻辑 (the first-order predicate calculus)
- 谓词变换器 (predicate transformers)
- 最弱前提条件 (weakest preconditions)

以上这些仅仅是证明程序正确性的一些方法中涉及到的部分主题。这些复杂的知识对于专业人士制定程序证明技术非常有用，像是麦卡锡和弗洛伊德 (McCarthy and Floyd) 的早期工作，到最近伯斯塔尔 (BurstaU)、戴克斯特拉 (Dijkstra)、曼纳 (Manna) 及其同事、米尔纳 (Milner)、莫里斯 (Morris)、雷诺兹 (Reynolds) 等众多学者的研究，都取得了令人赞叹的成就。这些成果大多建立在达纳·斯科特 (Dana Scott，指称语义学) 和 C. A. R. 霍尔 (C. A. R. Hoare，公理语义学) 的基础之上。然而，这些理论的复杂程度让它们超出了大多数非相关领域的业余爱好者的理解范围。

> If the average programmer is to prove his programs correct, he will need much simpler techniques than those the professionals have so far put forward. The algebra of programs below may be one starting point for such a proof discipline and, coupled with current work on algebraic manipulation, it may also help provide a basis for automating some of that discipline.

如果希望普通的程序员也能证明程序的正确性，那么就需要比现有方法更简单易懂的证明技术。本文描述的程序代数可以是这样一个证明方法的起点。结合当下关于代数操作(algebraic manipulation) 的研究成果，它甚至可以帮助实现部分程序正确性证明过程的自动化。 

> One advantage of this algebra over other proof techniques is that the programmer can use his programming language as the language for deriving proofs, rather than having to state proofs in a separate logical system that merely talks about his programs. 

程序代数相比其他证明方法的一大优势是，程序员可以使用熟悉的编程语言进行证明推导，而不是去使用与自己程序无关且独立的逻辑系统来证明。

> At the heart of the algebra of programs are laws and theorems that state that one function expression is the same as another. Thus the law $[f,g] \circ h \equiv [f \circ h, g  \circ h]$ says that the construction of $f$ and $g$ (composed with $h$ ) is the same function as the construction of ( $f$ composed with $h$ ) and ( $g$ composed with $h$ ) no matter what the functions $f$ , $g$ , and $h$ are. Such laws are easy to understand, easy to justify, and easy and powerful to use. However, we also wish to use such laws to solve equations in which an "unknown" function appears on both sides of the equation. The problem is that if $f$ satisfies some such equation, it will often happen that some extension $f'$ of $f$ will also satisfy the same equation. Thus, to give a unique meaning to solutions of such equations, we shall require a foundation for the algebra of programs (which uses Scott's notion of least fixed points of continuous functionals) to assure us that solutions obtained by algebraic manipulation are indeed least, and hence unique, solutions.

程序代数的核心是定义函数表达式相等关系的定律和定理。例如，定律 $[f,g] \circ h \equiv [f \circ h, g  \circ h]$ 表示，由 $f$ 和 $g$ 构成的构造式（construction）与 $h$ 的组合，无论 $f,g,h$ 是什么，都等价于由 $f$ 和 $g$ 分别组合了 $h$ 的结果构成的构造式。这些定律易于理解、证明，并且应用起来既方便又强大。然而，我们还希望利用这些定律来解方程，且方程两边都可能出现未知函数。问题在于，如果函数 $f$ 是某个方程的解，那么往往它的扩展 $f'$ 也可能是该方程的解。因此，为了让方程的解是唯一确定，我们需要程序代数的基础 (该基础运用了 Scott 关于连续函数式的最小不动点的概念) 来确保通过代数运算得到就是最小解，即唯一解。

> Our goal is to develop a foundation for the algebra of programs that disposes of the theoretical issues, so that a programmer can use simple algebraic laws and one or two theorems from the foundations to solve problems and create proofs in the same mechanical style we use to solve high-school algebra problems, and so that he can do so without knowing anything about least fixed points or predicate transformers. 

我们的目标是打造一套程序代数的基础理论，让程序员如同解高中代数题一般，使用简单的代数定律和一两个基础定理来解决问题完成证明，而无需了解最小不动点、谓词变换器等艰深的书序概念。

> One particular foundational problem arises: given equations of the form

一个特别基础的问题借由下面给定形式的等式来展开

$$
f \equiv p_0 \to q_0; \dots; p_i \to q_i; E_i(f) \tag{1}
$$

> where the $p_i$ 's and $q_i$ 's are functions not involving $f$ and $E_i(f)$ is a function expression involving $f$ , the laws of the algebra will often permit the formal "extension" of this equation by one more "clause" by deriving 

其中 $p_i$ 和 $q_i$ 都是不函 $f$ 的函数，而是 $E_i(f)$ 是包含 $f$ 的函数表达式。结合下面另一个“子句”，根据代数的定律，我们可以对等式进行形式化“扩展”

$$
E_i(f) \equiv p_{i+1} \to q_{i+1}; E_{i+1}(f) \tag{2}
$$

> which, by replacing $E_i(f)$ in (1) by the right side of (2), yields

即，将（1）式中 $E_i(f)$ 替换为（2）式右侧的部分，得到

$$
f \equiv p_0 \to q_0; \dots; p_{i+1} \to q_{i+1}; E_{i+1}(f) \tag{3}   
$$

> This formal extension may go on without limit. One question the foundations must then answer is: when can the least $f$ satisfying (1) be represented by the infinite expansion

这样的形式化扩展可以无限制的进行下去。那么，基础理论必须回答一个问题就是：满足（1）式的最小 $f$ 何时能在无限展开式的

$$
f \equiv p_0 \to q_0; \dots; p_n \to q_n; \dots \tag{4}
$$

> in which the final clause involving $f$ has been dropped, so that we now have a solution whose right side is free of $f$ 's? Such solutions are helpful in two ways: first, they give proofs of "termination" in the sense that (4) means that $f: x$ is defined if and only if there is an $n$ such that, for every $i$ less than $n$, $p_i: x = F$ and $p_n : x = T$ and $q_n : x$ is defined. Second, (4) gives a case-by-case description of $f$ that can often clarify its behavior.

子句中消除对 $f$ 引用，从而立即得到右侧无 $f$ 的解呢？这个解会在两方面很有用：

1. 给出“终止”的证明。以（4）式中 $f: x$ 而言，尤其仅有一个 $n$ ，对于每个小于 $n$ 的 $i$ 都有 $p_i: x = F$ 和 $p_n : x = T$ ，从而得到 $q_n : x$ ；
2. 给出每种情况下 $f$ 的描述，以阐明其行为。

> The foundations for the algebra given in a subsequent section are a modest start toward the goal stated above. For a limited class of equations its "linear expansion theorem" gives a useful answer as to when one can go from indefinitely extendable equations like (1) to infinite expansions like (4). For a larger class of equations, a more general "expansion theorem" gives a less helpful answer to similar questions. Hopefully, more powerful theorems covering additional classes of equations can be found. But for the present, one need only know the conclusions of these two simple foundational theorems in order to follow the theorems and examples appearing in this section. 

本文后续部分介绍的程序代数仅仅是实现既定目标的初步尝试。 对于有限的一类方程，该理论中的 “线性展开定理” 提供了实用的解答。这个定理告诉我们，何时可以将像 (1) 式一样无限展开的方程转化成像 (4) 式一样的无限展开式。对于更广泛的一类方程，文中给出了一个更一般的 “展开定理”，但其解答对于类似问题的作用较小。希望未来能找到针对更多类型方程的强大定理。但就目前而言，读者只需要理解这两个简单基础定理的结论，就足以理解本文档后续部分的定理和示例。

> The results of the foundations subsection are summarized in a separate, earlier subsection titled "expansion theorems," without reference to fixed point concepts. The foundations subsection itself is placed later where it can be skipped by readers who do not want to go into that subject.

关于代数基础的结论被单独总结在一个名为 “展开定理” 的靠前子节中，并且没有引用“不动点” (fixed point) 的概念。而代数基础本身则被放置靠后，方便不想深入研究该主题的读者跳过。

> 12.2 Some Laws of the Algebra of Programs

### 12.2 一些程序代数的定律

> In the algebra of programs for an FP system variables range over the set of functions of the system. The "operations" of the algebra are the functional forms of the system. Thus, for example, $[f,g] \circ h$ is an expression of the algebra for the FP system described above, in which $f$ , $g$ , and $h$ are variables denoting arbitrary functions of that system. And 

在 FP 系统的程序代数中，变量的取值范围是系统的所有函数集合。代数的 “运算” 则由该系统的函数式构成。有如， $[f,g] \circ h$ 这样上述提及的 FP 系统的代数表达式， 其中 $f$ 、 $g$ 和 $h$ 都 是变量，表示该系统中的任意函数。则

$$
[f, g] \circ h \equiv [f \circ h, g \circ h]
$$

> is a law of the algebra which says that, whatever functions one chooses for $f$ , $g$ , and $h$ , the function on the left is the same as that on the right. Thus this algebraic law is merely a restatement of the following proposition about any FP system that includes the functional forms $[f, g]$ and $f \circ g$ :

是一个代数定律，表示无论 $f$ 、 $g$ 和 $h$ 是什么函数，上式左右是等价的。这样的代数定律也只是在重声下面的命题，即，对任何 FP 系统，其内的函数式 $[f, g]$ 和 $f \circ g$ ：

> PROPOSITION: For all functions $f$ , $g$ , and $h$ and all objects $x$, $([f,g] \circ h):x \equiv [f \circ h, g \circ h ]:x$ . 
> 
> PROOF:

**命题**：对所有函数 $f$ 、 $g$ 和 $h$ ，以及所有对象 $x$ ，都有 $([f,g] \circ h):x \equiv [f \circ h, g \circ h ]:x$ . 

**证明**：

$$
\begin{align*}    
([f, g] \circ h) : x 
  &= [f, g] : (h : x)                     &\text{ by definition of composition}\\
  &= < f : (h : x), g : (h : x) >         &\text{ by definition of construction}\\
  &= < (f \circ h) : x, (g \circ h) : x > &\text{ by definition of composition}\\
  &= [ f \circ h, g \circ h ] : x         &\text{ by definition of construction}\\
\end{align*}
$$

> Some laws have a domain smaller than the domain of all objects. Thus $1 \circ [f,g] \equiv f$ does not hold for objects $x$ such that $g:x = \bot$. We write

一些定律并非适用于所有对象。像 $1 \circ [f,g] \equiv f$ 对于对象 $x$ 满足 $g:x = \bot$ 就不适用了。此时，我们将其记作

$$
\text{defined} \circ g \to\to 1 \circ [f, g] \equiv f
$$

> to indicate that the law (or theorem) on the right holds within the domain of objects $x$ for which $\text{defined} \circ g:x = T$. Where 

用以说明这个定律（或定理）右侧只有在对象 $x$ 满足 $\text{defined} \circ g:x = T$ 时才成立。其定义

$$
\textbf{Def } \text{defined} \equiv \bar{T}
$$

> i.e. $\text{defined} : x \equiv x = \bot \to \bot; T$. In general we shall write a *qualified functional equation*: 

意指 $\text{defined} : x \equiv x = \bot \to \bot; T$ 可检测对象 $x$ 是否未知。通常，我们会写成一个 *限定函数式方程*：

$$
p \to\to f \equiv g
$$

> to mean that, for any object $x$ , whenever $p:x = T$, then $f:x = g:x$ . 

意思是，对任何对象 $x$ ，当满足 $p:x = T$ ，则 $f:x = g:x$ 。

> Ordinary algebra concerns itself with two operations, addition and multiplication; it needs few laws. The algebra of programs is concerned with more operations (functional forms) and therefore needs more laws.

常规代数只涉及加法和乘法这两种运算，因此只需要少量定律就能描述其基本性质。然而，程序代数则涉及更多的运算 (函数式)，因此需要更多的定律来描述程序的行为和性质。

> Each of the following laws requires a corresponding proposition to validate it. The interested reader will find most proofs of such propositions easy (two are given below). We first define the usual ordering on functions and equivalence in terms of this ordering: 

后续的每个定律都需要一个对应的命题来证明其有效性。对于感兴趣的读者来说，大部分此类命题的证明都比较简单（文章中还会给出两个为示例）。首先，我们就常见函数的排序以及基于排序的等价关系展开定义：

> DEFINITION $f \le g$ iff for all objects $x$ , either $f:x = \bot$ , or $f:x = g:x$ .

**定义** $f \le g$ 有且仅当(iff)[^iff] 所有对象，满足 $f:x = \bot$ ，或 $f:x = g:x$ 。

[^iff]: 是 “if and only if” 的缩写。

> DEFINITION $f \equiv g$ iff $f \le g$ and $g \le f$.

**定义** $f \equiv g$ 有且仅当 $f \le g$ 且 $g \le f$ 。

> It is easy to verify that $\le$ is a partial ordering, that $f \le g$ means $g$ is an extension of $f$ , and that $f \equiv g$ iff $f:x = g:x$ for all objects $x$ . We now give a list of algebraic laws organized by the two principal functional forms in volved.

显而易见， $\le$ 表达了一种偏序关系，即 $f \le g$ 表示函数 $g$ 是函数 $f$ 的一个扩展，而当所有对象 $x$ 都满足 $f:x = g:x$ 时， $f \equiv g$ 自然也是成立的。接下来，文章将提供一系列的代数定律，这些定律将根据程序代数中涉及的两种主要函数式进行组织。

> I Composition and construction

#### I 组合与构造

**I.1** 

$$
[f_1, \dots, f_n] \circ g \equiv [f_1 \circ g, \dots, f_n \circ g]
$$

**I.2**

$$
\alpha f \circ [g_1, \dots, g_n] \equiv [f \circ g_1, \dots, f \circ g_n] 
$$

**I.3**

$$
\begin{align*}
    /f \circ [g_1, \dots, g_n]\\
    &\equiv f \circ [g_1, /f \circ [g_2, \dots, g_n]] &\text{ when } n \ge \textit{2}\\
    &\equiv f \circ [g_1, f \circ [g_2, \dots, f \circ [g_{n-1}, g_n] \dots]] \\
    /f \circ [g] &\equiv g
\end{align*}
$$

**I.4**

$$
f \circ [\bar{x}, g] \equiv (\text{bu } f x) \circ g
$$

**I.5**

$$
\begin{align*}
  1 \circ [f_1, \dots, f_n] &\le f_1 \\
  \text{s} \circ [f_1, \dots, f_s, \dots, f_n] &\le f_s \text{ for any  selector s, } s \le n \\
\text{defined} \circ f_i (\text{for all } i \ne s, \textit{1} \le i \le n) \to\to \text{s} \circ [f_1, \dots, f_n] &\equiv f_s
\end{align*}
$$

**I.5.1**

$$
[f_1 \circ 1, \dots, f_n \circ n] \circ [g_1, \dots, g_n] \equiv [f_1 \circ g_1, \dots f_n \circ g_n]
$$

**I.6**

$$
\begin{align*}
\text{tl} \circ [f_1] &\le \bar{\phi} &\text{ and } \\
\text{tl} \circ [f_1, \dots, f_n] &\le [f_2, \dots, f_n] &\text{ for } n \ge \textit{2} \\
\text{defined} \circ f_1 \to \to \text{tl} \circ [f_1] &\equiv \bar{\phi} &\text{ and } \\
\text{tl} \circ [f_1, \dots, f_n] &\equiv [f_2, \dots, f_n] &\text{ for } n \ge \textit{2}    
\end{align*}
$$

**I.7**

$$
\begin{align*}
  \text{distl} \circ [f, [g_1, \dots, g_n]] &\equiv [[f, g_1], \dots, [f, g_n]] \\
  \text{defined} \circ f \to \to \text{distl} \circ [f, \bar{\phi}] &\equiv \bar{\phi} 
\end{align*}
$$

> The analogous law holds for $\text{distr}$ .

$\text{distr}$ 也是类似的。

**I.8**

$$
\begin{align*}
  \text{apndl} \circ [f, [g_1, \dots, g_n]] &\equiv [f, g_1, \dots, g_n]  \\
  \text{null} \circ g \to \to \text{apndl} \circ [f, g] &\equiv [f]
\end{align*}
$$

> And so on for $\text{apndr, reverse, rotl }$ etc.

$\text{apndr, reverse, rotl }$ 等也是一样的。

**I.9**

$$
[\dots, \bar{\bot}, \dots] \equiv \bar{\bot}
$$

**I.10**

$$
\text{apndl} \circ [f \circ g, \alpha f \circ h] \equiv \alpha f \circ \text{apndl} \circ [g, h]
$$


**I.11**

$$
\begin{align*}
\text{pair} \And \text{not} \circ \text{null} \circ 1 \to \to \\
&\text{apndl} \circ [[1 \circ 1, 2], \text{distr} \circ [\text{tl} \circ 1, 2]] &&\equiv \text{distr} \\
\text{Where} \\
&f \And g &&\equiv \text{and } \circ [f, g];\\
&\text{pair} &&\equiv \text{atom} \to \bar{F}; \text{eq} \circ [\text{length}, \bar{\it 2}]\\
\end{align*}
$$

> II Composition and condition 
> (right associated parentheses omitted)
> (Law II.2 is noted in Manna et al. [^16] p.493.)

#### II 组合与条件

（这里省略右关联的括号）
（定律 II.2 参见曼纳等人的著作[^16]第493页。）

**II.1**

$$
(p \to f; g) \circ h \equiv p \circ h \to f \circ h ; g \circ h
$$

**II.2**

$$
h \circ (p \to f; g) \equiv p \to h \circ f; h \circ g
$$

**II.3**

$$
\begin{align*}
&\text{or} \circ [q, \text{not} \circ q] \to \to \text{and} \circ [p, q] \to f;\\
&\quad\text{and} \circ [p, \text{not} \circ q] \to g; h \equiv p \to (q \to f; g); h    
\end{align*}
$$

**II.3.1**

$$
p \to (p \to f; g); h \equiv p \to f; h
$$

> III Composition and miscellaneous

#### III 组合与杂项

**III.1**

$$
\begin{align*}    
\bar{x} \circ f &\le \bar{x} \\
\text{defined} \circ f \to \to \bar{x} \circ f &\equiv \bar{x}
\end{align*}
$$

**III.1.1**

$$
\bar{\bot} \circ f \equiv f \circ \bar{\bot} \equiv \bar{\bot}
$$

**III.2**

$$
f \circ \text{id} \equiv \text{id} \circ f \equiv f
$$

**III.3**

$$
\begin{align*}    
\text{pair} \to \to &1 \circ \text{distr} &\equiv&\ [1 \circ 1, 2] &\text{ also:} \\
\text{pair} \to \to &1 \circ \text{tl} &\equiv&\ 2 &\text{etc.}
\end{align*}
$$

**III.4**

$$
\alpha (f \circ g) \equiv \alpha f \circ \alpha g
$$

**III.5**

$$
\text{null} \circ g \to \to \alpha f \circ g \equiv \bar{\phi}
$$

> IV Condition and construction

#### IV 条件与构造

**IV.1**

$$
\begin{align*}
  &[f_1, \dots, (p \to g; h), \dots, f_n]\\
  &\qquad \equiv p \to [f_1, \dots, g, \dots, f_n]; [f_1, \dots, h, \dots, f_n]
\end{align*}
$$

**IV.1.1**

$$
\begin{align*}
  &[f_1, \dots, (p_1 \to g_1;\dots;p_n \to g_n; h), \dots, f_m]\\
  &\qquad \equiv p_1 \to [f_1, \dots, g_1, \dots, f_m]; \\
  &\qquad \dots ; p_n \to [f_1, \dots, g_n, \dots, f_m];[f_1, \dots, h, \dots, f_m] 
\end{align*}
$$

> This concludes the present list of algebraic laws; it is by no means exhaustive, there are many others. 

至此，我们列出了部分程序代数定律。需要注意的是，这并不是一个详尽的列表，还有许多其他的定律未被提及。

> Proof of two laws

#### 两个定律的证明

> We give the proofs of validating propositions for laws **I.10** and **I.11**, which are slightly more involved than most of the others.

我们将提供验证 **I.10** 和 **I.11** 定律的命题的证明。这两个定律的证明比大多数其他定律的证明稍微复杂一些。

> PROPOSITION 1

**命题 1**

$$
\text{apndl} \circ [f \circ g, \alpha f \circ h] \equiv \alpha f \circ \text{apndl} \circ [g, h]
$$

> PROOF. We show that, for every object $x$, both of the above functions yield the same result. 

**证明** 对所有对象 $x$ 上面两边的函数结果是一样的。

> CASE 1. $h:x$ is neither a sequence nor $\phi$. 
> Then both sides yield $\bot$ when applied to $x$ .

**情况 1** 当 $h:x$ 既不是序列，也不是 $\phi$ ，则两边应用到 $x$ 就都会得到 $\bot$ 。

> CASE 2. $h:x = \phi$ . Then

**情况 2** 当 $h:x = \phi$ ，则

$$
\begin{align*}
  &\text{apndl} \circ [f \circ g, \alpha f \circ h] : x \\
  &\quad = \text{apndl} : < f \circ g : x, \phi > \\
  &\quad = < f : (g : x) > \\
  \\
  &\alpha f \circ \text{apndl} \circ [g, h] : x \\
  &\quad = \alpha f \circ \text{apndl} : < g : x, \phi > \\
  &\quad = \alpha f : < g : x > \\
  &\quad = < f : (g : x) >
\end{align*}
$$

> CASE 3. $h : x = < y_1, \dots, y_n >$ . Then

**情况 3** 当 $h : x = < y_1, \dots, y_n >$ ，则

$$
\begin{align*}
  &\text{apndl} \circ [f \circ g, \alpha f \circ h] : x \\
  &\quad = \text{apndl} : < f \circ g : x, \alpha f : < y_1, \dots, y_n > > \\
  &\quad = < f : (g : x), f : y_1, \dots, f : y_n > \\
  \\
  &\alpha f \circ \text{apndl} \circ [g, h] : x \\
  &\quad = \alpha f \circ \text{apndl} : < g : x, < y_1, \dots, y_n > > \\
  &\quad = \alpha f : < g : x, y_1, \dots, y_n > \\
  &\quad = < f : (g : x), f : y_1, \dots, f : y_n >
\end{align*}
$$

> PROPOSITION 2

**命题 2**

$$
\begin{align*}
\text{pair} \And \text{not} \circ \text{null} \circ 1 \to \to \\
&\text{apndl} \circ [[1^2, 2], \text{distr} \circ [\text{tl} \circ 1, 2]] \equiv \text{distr} 
\end{align*}
$$

> where $f \And g$ is the function: $\text{and} \circ [f, g]$ , and $f^2 \equiv f \circ f$ .

其中 $f \And g$ 是函数 $\text{and} \circ [f, g]$ ，且 $f^2 \equiv f \circ f$ 。

> PROOF. We show that both sides produce the same result when applied to any $pair <x,y>$ , where $x \ne \phi$ , as per the stated qualification. 

**证明** 限定，对任意 $pair < x, y >$ ，且其中 $x \ne \phi$ 的应用，两边的结果是一致的。

> CASE 1. $x$ is an atom or $\bot$ . Then $\text{distr} : < x, y > = \bot$ , since $x \ne \phi$ . The left side also yields $\bot$ when applied to $< x, y >$ , since $\text{tl} \circ 1 : < x, y > = \bot$ and all functions are $\bot$ -preserving. 

**情况 1** 当 $x \ne \phi$， $x$ 是一个原子，或 $\bot$ 时，则 $\text{distr} : < x, y > = \bot$ 。又因为 $\text{tl} \circ 1 : < x, y > = \bot$ 且所有函数都是 $\bot$ 保留的，所以左边的函数应用 $< x, y >$ 只会的到 $\bot$ 。

> CASE 2. $x = < x_1, \dots, x_n >$. Then 

**情况 2** 当 $x = < x_1, \dots, x_n >$ ，则

$$
\begin{align*}
  &\text{apndl} \circ [[1^2, 2], \text{distr} \circ [\text{tl} \circ 1, 2]] : < x, y >\\
  &\quad = \text{apndl} : << 1 : x, y >, \text{distr} : < \text{tl} : x, y >> \\
  &\quad = \text{apndl} : << x_1, y >, \phi> &&= << x_1, y >> &&\text{if tl} : x = \phi \\
  &\quad = \text{apndl} : << x_1, y >, < x_2, y >, \dots, < x_n, y >> &&= << x_1, y>, \dots, < x_n, y >> &&\text{if tl} : x \ne \phi \\
  &\quad = \text{distr} : < x, y >
\end{align*}
$$

> 12.3 Example: Equivalence of Two Matrix Multiplication Programs

### 12.3 案例：两个矩阵相乘的等价程序

> We have seen earlier the matrix multiplication program: 

之前我们已经讨论过的矩阵乘法程序：

$$
\textbf{Def } \text{MM} \equiv \alpha \alpha \text{IP} \circ \alpha \text{distl} \circ \text{distr} \circ [ 1, \text{trans} \circ 2 ]
$$  

> We shall now show that its initial segment, $\text{MM'}$ , where 

我们将其前面的片段定义为  $\text{MM'}$ ，如

$$
\textbf{Def } \text{MM'} \equiv 
    \alpha \alpha \text{IP} \circ \alpha \text{distl} \circ \text{distr}
$$ 

> can be defined recursively. ( $\text{MM'}$ "multiplies" a pair of matrices after the second matrix has been transposed. Note that $\text{MM'}$, unlike $\text{MM}$, gives $\bot$ for all arguments that are not pairs.) That is, we shall show that $\text{MM'}$ satisfies the following equation which recursively defines the same function (on pairs): 

而它是可以递归定义的。

（ $\text{MM'}$ 是针对一对矩阵，其第二矩阵需要经过转置，的“乘法” 计算。与 $\text{MM}$ 不同的是，若输入的不是矩阵对的话，会得到 $\bot$ 。）

是的， $\text{MM'}$ 确实满足下面这个递归定义的等式（仅限成对的输入）：

$$
f \equiv \text{null} \circ 1 \to \bar{\phi};\text{apndl} \circ [\alpha \text{IP} \circ \text{distl} \circ [1 \circ 1, 2], f \circ [\text{tl} \circ 1, 2]]
$$

> Our proof will take the form of showing that the following function, $\text{R}$, 

如下函数形式， $\text{R}$ 说明了，

$$
\textbf{Def } \text{R} 
    \equiv \text{null} \circ 1 \to \bar{\phi};
    \text{apndl} \circ [
        \alpha \text{IP} \circ \text{distl} \circ [1 \circ 1, 2], 
        \text{MM'} \circ [\text{tl} \circ 1, 2]
    ]
$$

> is, for all pairs $< x, y >$ , the same function as $\text{MM'}$ . $\text{R}$ "multiplies" two matrices, when the first has more than zero rows, by computing the first row of the "product" (with $\alpha \text{IP} \circ \text{distl} \circ [1 \circ 1, 2]$) and adjoining it to the "product" of the tail of the first matrix and the second matrix. Thus the theorem we want is

对所有成对的 $< x, y >$ 而言，是等价于 $\text{MM'}$ 。 $\text{R}$ 的矩阵“乘法，只要第一个矩阵行数不为零，则计算第一行与第二个矩阵的“积”（即 $\alpha \text{IP} \circ \text{distl} \circ [1 \circ 1, 2]$ ），依此类推计算余下的部分的积，并接连起来。这就是我们想要的定理

$$
\text{pair} \to \to \text{MM'} \equiv \text{R}
$$

> from which the following is immediate: 

由此可见：

$$
\text{MM} 
  \equiv \text{MM'} \circ [1, \text{trans} \circ 2] 
  \equiv \text{R} \circ [1, \text{trans} \circ 2]
$$

> where

只要

$$
\textbf{Def } \text{pair} \equiv
    \text{atom} \to \bar{F};
    \text{eq} \circ [\text{length}, \bar{\it 2}]
$$

> THEOREM: 

**定理**

$$
\begin{align*}
\text{pair} \to \to \text{MM'} &\equiv \text{R} \\
\text{where}\\
\textbf{Def } \text{MM'} &\equiv 
    \alpha \alpha \text{IP} \circ \alpha \text{distl} \circ \text{distr}\\
\textbf{Def } \text{R} &\equiv 
    \text{null} \circ 1 \to \bar{\phi};
    \text{apndl} \circ [
        \alpha \text{IP} \circ \text{distl} \circ [1^2, 2], 
        \text{MM'} \circ [\text{tl} \circ 1, 2]
    ]    
\end{align*}
$$

> PROOF.

**证明**

> CASE 1. $\text{pair} \And \text{null} \circ 1 \to \to \text{MM'} \equiv \text{R}$

**情况 1** $\text{pair} \And \text{null} \circ 1 \to \to \text{MM'} \equiv \text{R}$

$$
\begin{align*}
\text{pair} \And \text{null} \circ 1 \to \to \text{R} &\equiv 
    \bar{\phi} &&\text{ by def of R} \\
\text{pair} \And \text{null} \circ 1 \to \to \text{MM'} &\equiv 
    \bar{\phi} \\
\text{since distr} : < \phi, x > &= \phi &&\text{ by def of distr}\\
\text{and } \alpha f : \phi &= \phi &&\text{ by def of Apply to all}
\end{align*}
$$

> And so: $\alpha \alpha \text{IP} \circ \alpha \text{distl} \circ \text{distr} : < \phi, x > = \phi$.

可见 $\alpha \alpha \text{IP} \circ \alpha \text{distl} \circ \text{distr} : < \phi, x > = \phi$ 。

> Thus $\text{pair} \And \text{null} \circ 1 \to \to \text{MM'} \equiv \text{R}$.

因此 $\text{pair} \And \text{null} \circ 1 \to \to \text{MM'} \equiv \text{R}$ 。

> CASE 2. $\text{pair} \And \text{not} \circ \text{null} \circ 1 \to \to \text{MM'} \equiv \text{R}$

**情况 2** $\text{pair} \And \text{not} \circ \text{null} \circ 1 \to \to \text{MM'} \equiv \text{R}$

$$
\tag{1} \text{pair} \And \text{not} \circ \text{null} \circ 1 \to \to \text{R} \equiv \text{R'}  
$$

> by def of $\text{R}$ and $\text{R'}$ , where

由 $\text{R}$ 的定义，对应的 $\text{R'}$ 有

$$
\textbf{Def } \text{R'} \equiv 
    \text{apndl} \circ [
        \alpha \text{IP} \circ \text{distl} \circ [1^2, 2], 
        \text{MM'} \circ [\text{tl} \circ 1, 2]
    ]
$$

> We note that

我们可以改写为

$$
\begin{align*}
  \text{R'} &\equiv \text{apndl} \circ [f \circ g, \alpha f \circ h] \\
  \text{where} \\
  f &\equiv \alpha \text{IP} \circ \text{distl} \\
  g &\equiv [1^2, 2] \\
  h &\equiv \text{distr} \circ [\text{tl} \circ 1, 2]\\
\end{align*}
$$

$$
\alpha f \equiv \alpha (\alpha \text{IP} \circ \text{distl}) 
         \equiv \alpha \alpha \text{IP} \circ \alpha \text{distl} 
         \quad \text{(by III.4)} \tag{2}
$$

> Thus, by **I.10** ,

根据 **I.10** 可得，

$$
\text{R'} \equiv \alpha f \circ \text{apndl} \circ [g, h] \tag{3}
$$

> Now $\text{apndl} \circ [g, h] \equiv \text{apndl} \circ [[1^2, 2], \text{distr} \circ [\text{tl} \circ 1, 2]]$ ,

现在 $\text{apndl} \circ [g, h] \equiv \text{apndl} \circ [[1^2, 2], \text{distr} \circ [\text{tl} \circ 1, 2]]$ ，

> thus, by **I.11**,

又根据 **I.11** 得到，

$$
\text{pair} \And \text{not} \circ \text{null} \circ 1 \to \to \text{apndl} \circ [g, h] \equiv \text{distr} \tag{4}
$$

> And so we have, by (1), (2), (3) and (4),

基于 (1)、(2)、(3) 和 (4)，最后得到，

$$
\begin{align*}
\text{pair} \And \text{not} \circ \text{null} \circ 1 \to \to
\text{R} &\equiv \text{R'} \\
            &\equiv \alpha \circ \text{distr} \\
            &\equiv \alpha \alpha \text{IP} \circ \alpha \text{distl} \circ \text{distr} \\
            &\equiv \text{MM'}
\end{align*}
$$

> Case 1 and Case 2 together prove the theorem.

综合 **情况 1** 和 **情况 2** 可以证明这个定理成立。

> 12.4 Expansion Theorems

### 12.4 展开定理

> In the following subsections we shall be "solving" some simple equations (where by a "solution" we shall mean the "least" function which satisfies an equation). To do so we shall need the following notions and results drawn from the later subsection on foundations of the algebra, where their proofs appear.

后续小节里我们会“求解”一些简单的方程（其“解”指的是满足方程的“最小”的函数）。为此，我们需要用到从后续小节里的代数基础知识和结论，其相关证明也在随后给出。

> 12.4.1 Expansion.

#### 12.4.1 展开

> Suppose we have an equation of the form

假设有如下形式的等式

$$
\tag{E1} f \equiv \text{E}(f)
$$

> where $\text{E}(f)$ is an expression involving $f$ . Suppose further that there is an infinite sequence of functions $f_i$ for $i = 0, 1, 2, \dots$ , each having the following form:

其中， $\text{E}(f)$ 代表一个包含 $f$ 的表达式。再假设存在一个无限函数序列，记为 $f_i$ 且 $i = 0, 1, 2, \dots$ ，并有：

$$
\begin{align*}    
  f_0 &\equiv \bar{\bot} \\
  f_{i+1} &\equiv p_0 \to q_0; \dots; p_i \to q_i; \bar{\bot}
\end{align*}
\tag{E2}
$$

> where the $p_i$ 's and $q_i$ 's are particular functions, so that $\text{E}$ has the property: 

其中 $p_i$ 和 $q_i$ 两类特定的函数，使得表达式 $\text{E}$ 能呈现出（可展开的）性质：

$$
\text{E}(f_i) \equiv f_{i+1} \text{ for } i = 0, 1, 2, \dots \tag{E3}
$$

> Then we say that $\text{E}$ is *expansive* and has the $f_i$ 's *as approximating functions*. 

此时，我们称 $\text{E}$ 是*可展开的*（expansive）的表达式， $f_i$ 是它的*逼近函数*（approximating function）。

> If $\text{E}$ is expansive and has approximating functions as in (E2), and if $f$ is the solution of (E1), then $f$ can be written as the infinite expansion

既然 $\text{E}$ 是可展开的，又有如（E2）中的逼近函数，那么当 $f$ 是（E1）的解，则 $f$ 可无限展开为

$$
f \equiv p_0 \to q_0; \dots; p_n \to q_n; \dots \tag{E4}
$$

> meaning that, for any $x, f : x \ne \bot$ iff there is an $n \ge 0$ such that (a) $p_i:x = F$ for all $i < n$ , and (b) $p_n:x = T$ , and (c) $qn:x \ne \bot$ . When $f:x \ne \bot$, then $f:x = q_n:x$ for this $n$. (The foregoing is a consequence of the "expansion theorem".)

这意味着，对任意 $x, f : x \ne \bot$ 有且仅有一个大于等于零的 $n$ ，使得所有小于 $n$ 的 $i$  ，满足：

1. $p_i:x = F$ ；
2. $p_n:x = T$ ；
3. $q_n:x \ne \bot$ 。

而 $f:x \ne \bot$ ，即 $f:x = q_n:x$ 。

（以上就是“展开定理”的结论。）

> 12.4.2 Linear expansion

#### 12.4.2 线性展开

> A more helpful tool for solving some equations applies when, for any function $h$ ,

对应用任意函数 $h$ 的一些方程，一个求解它们更好用的工具是

$$
\text{E}(h) \equiv p_0 \to q_0; \text{E}_1(h) \tag{LE1}
$$

> and there exist $p_i$ and $q_i$ such that 

这里同样有函数 $p_i$ 和 $q_i$ ，以便

$$
\text{E} _1 (p _i \to q _i;h) \equiv 
    p _{i+1} \to q _{i+1}; \text{E} _1 (h) \text{ for } i = 0, 1, 2, \dots \tag{LE2}
$$

> and

并且

$$
\text{E}_1(\bar{\bot}) \equiv \bar{\bot} \tag{LE3}
$$

> Under the above conditions $\text{E}$ is said to be *linearly expansive*. If so, and $f$ is the solution of

有了以上前提，我们称表达式 $\text{E}$ 是**可线性展开的**。同样，当 $f$ 为

$$
f \equiv \text{E}(f) \tag{LE4}
$$

> then $\text{E}$ is expansive and $f$ can again be written as the infinite expansion

表达式 $\text{E}$ 便是可展开的，那么 $f$ 就可以无限展开为

$$
f \equiv p_0 \to q_0; \dots; p_n \to q_n; \dots \tag{LE5}
$$

> using the $p_i$ 's and $q_i$ 's generated by (LE1) and (LE2). 

使用函数 $p_i$ 和 $q_i$ ，并依据(LE1)和(LE2)而生成。

> Although the $p_i$ 's and $q_i$ 's of (E4) or (LE5) are not unique for a given function, it may be possible to find additional constraints which would make them so, in which case the expansion (LE5) would comprise a canonical form for a function. Even without uniqueness these expansions often permit one to prove the equivalence of two different function expressions, and they often clarify a function's behavior. 

就给定的函数而言，（E4）和（LE5）中的 $p_i$ 和 $q_i$ 并不是唯一的，但在可能的额外约束下使得它们唯一，这就让（LE5）的展开构成了函数的规范形式（canonical form）。即便没有唯一性，这样的展开仍然可以用来证明两个不同的函数表达式是等价的，同时还有助于理解函数的行为。

> 12.5 A Recursion Theorem 

### 12.5 递归定理

> Using three of the above laws and linear expansion, one can prove the following theorem of moderate generality that gives a clarifying expansion for many recursively defined functions.

利用三个之前提到的定律以及线性展开 (linear expansion) 可以证明一个有一定普遍性的定理。该定理为许多递归定义的函数提供了清晰的展开式。

> RECURSION THEOREM: Let $f$ be a solution of 

**递归定理**：设 $f$ 是如下方程的解

$$
f \equiv p \to q; \text{Q}(f) \tag{1}
$$

> where

其中

$$
\text{Q}(k) \equiv h \circ [i , k \circ j] \text{ for any function k} \tag{2}
$$

> and $p, g, h, i, j$ are any given functions, then

并且 $p, g, h, i, j$ 都是任意给定的函数，则

$$
f \equiv p \to g; 
         p \circ j \to \text{Q}(g);
         \dots;
         p \circ j^n \to \text{Q}^n(g); \dots \tag{3}
$$

> (where $\text{Q}^n(g)$ is $h \circ [i, \text{Q}^{n-1}(g) \circ j]$ , and $j^n$ is $j \circ j^{n-1}$ for $n \ge \textit{2}$ ) and

（其中 $\text{Q}^n(g)$ 展开是 $h \circ [i, \text{Q}^{n-1}(g) \circ j]$ ，而 $j^n$ 则是 $j \circ j^{n-1}$ ，且 $n \ge \textit{2}$ ）且

$$
\text{Q}^n(g) \equiv /h \circ [i, i \circ j, \dots, i \circ j^{n-1}, g \circ j^n] \tag{4}
$$

> PROOF. We verify that $p \to g; \text{Q}(f)$ is linearly expansive. Let $p_n$ , $q_n$ and $k$ be any functions. Then

**证明** 表达式 $p \to g; \text{Q}(f)$ 是可线性展开的。令 $p_n$ 、 $q_n$ 和 $k$ 是任意函数，则有

$$
\tag{5}
\begin{align*}
&\text{Q}(p_n \to q_n; k) \\
&\quad \equiv h \circ [i, (p_n \to q_n; k) \circ j] 
    &&\text{by (2)} \\
&\quad \equiv h \circ [i, (p_n \circ j \to q_n \circ j; k \circ j)]    
    &&\text{by II.1} \\
&\quad \equiv h \circ (p_n \circ j \to [i, q_n \circ j]; [i, k \circ j])
    &&\text{by IV.1}  \\
&\quad \equiv p_n \circ j \to h \circ [i, q_n \circ j]; h \circ [i, k \circ j]
    &&\text{by II.2}  \\
&\quad \equiv p_n \circ j \to \text{Q}(q_n); \text{Q}(k)
    &&\text{by (2)}  
\end{align*}
$$

> Thus if $p_0 \equiv p$ and $q_0 \equiv g$ , then (5) gives $p_1 \equiv p \circ j$ and $q_1 \equiv \text{Q}(g)$ and in general gives the following functions satisfying (LE2)

如果说 $p_0 \equiv p$ 和 $q_0 \equiv g$ ，那么由式（5）得到 $p_1 \equiv p \circ j$ 和 $q_1 \equiv \text{Q}(g)$ ，推而广之得到满足（LE2）的方程

$$
\tag{6} p_n \equiv p \circ j^n \text{ and } q_n \equiv \text{Q}^n(g)
$$

> Finally,

最后，

$$
\begin{align*}
  \text{Q}(\bot)
    &\equiv h \circ [i, \bot \circ j] \\
    &\equiv h \circ [i, \bot] &&\text{by III.1.1}\\
    &\equiv h \circ \bot &&\text{by I.9}&\\
    &\equiv \bot &&\text{by III.1.1}
\end{align*}
\tag{7}
$$

> Thus (5) and (6) verify (LE2) and (7) verifies (LE3), with $\text{E}_1 \equiv Q$ . If we let $\text{E}(f) \equiv p \to g; \text{Q}(f)$ , then we have (LE1); thus $\text{E}$ is linearly expansive. Since $f$ is a solution of $f \equiv \text{E}(f)$ , conclusion (3) follows from (6) and (LE5). Now 

把 $\text{Q}$ 替换 $\text{E}_1$ （ $\text{E}_1 \equiv Q$ ）的话，则（5）和（6）验证了（LE2），（7）验证了（LE3）。同理， $\text{E}(f) \equiv p \to g; \text{Q}(f)$ 则验证了（LE1）。从而得到 $\text{E}$ 是可线性展开的。因为 $f$ 是 $f \equiv \text{E}(f)$ 的解，所以从（6）和（LE5）就验证了第一个结论（3）。现在

$$
\begin{align*}
  \text{Q}^n(g) 
    &\equiv h \circ [i, \text{Q}^{n-1}(g) \circ j] \\
    &\equiv h \circ [i, h \circ [i \circ j, \dots, h \circ [i \circ j^{n-1}, g \circ j^n] \dots ]] && \text{by I.1 repeartedly} \\
    &\equiv /h \circ [i, i \circ j, \dots, i \circ j^{n-1}, g \circ j^n] && \text{by I.3}
\end{align*}
\tag{8}
$$

> Result (8) is the second conclusion (4).

（8）这个结果验证了上面第二结论（4）。

> 12.5.1 Example: correctness proof of a recursive factorial function.

#### 12.5.1 示例：证明递归阶乘函数的正确性

> Let $f$ be a solution of

设 $f$ 是这个方程的解

$$
f \equiv \text{eq0} \to \bar{\it 1}; \times \circ [\text{id}, f \circ \text{s}]
$$

> where

其中

$$
\textbf{Def } \text{s} \equiv - \circ [\text{id}, \bar{\it 1}] \quad \text{(subtract 1)}
$$

> Then $f$ satisfies the hypothesis of the recursion theorem with $p \equiv eq0$ , $g \equiv \bar{\it 1}$ , $h \equiv \times$ , $i \equiv \text{id}$ , and $j \equiv \text{s}$ . Therefore

$p \equiv eq0$ 、 $g \equiv \bar{\it 1}$ 、 $h \equiv \times$ 和 $i \equiv \text{id}$ , and $j \equiv \text{s}$ ， $f$ 显然是满足递归定理的假设的。因此

$$
f \equiv 
    \text{eq0} \to \bar{\it 1}; 
    \dots; 
    \text{eq0} \circ \text{s}^n \to \text{Q}^n(\bar{\it 1});
    \dots
$$

> and

且

$$
\text{Q}^n(\bar{\it 1}) \equiv
    /\times \circ [
        \text{id}, 
        \text{id} \circ \text{s}, 
        \dots, 
        \text{id} \circ \text{s}^{n-1}, 
        \bar{\it 1} \circ \text{s}^n
    ]
$$

> Now $\text{id} \circ \text{s}^k \equiv \text{s}^k$ by **III.2** and $\text{eq0} \circ \text{s}^n \to \to \bar{\it 1} \circ \text{s}^n \equiv \bar{\it 1}$ by **III.1**, since $\text{eq0} \circ \text{s}^n : x$ implies $\text{defined} \circ \text{s}^n : x$ and also $\text{eq0} \circ \text{s}^n : x \equiv \text{eq0} : (x - n) \equiv x = n$ . Thus if $\text{eq0} \circ \text{s}^n : x = T$ , then $x = n$ and

现在，据 **III.2** 有 $\text{id} \circ \text{s}^k \equiv \text{s}^k$ ，又据 **III.1** 有 $\text{eq0} \circ \text{s}^n \to \to \bar{\it 1} \circ \text{s}^n \equiv \bar{\it 1}$ ，既然 $\text{eq0} \circ \text{s}^n : x$ 或者说 $\text{defined} \circ \text{s}^n : x$ ，也就是 $\text{eq0} \circ \text{s}^n : x \equiv \text{eq0} : (x - n) \equiv x = n$ 。 因此，当 $\text{eq0} \circ \text{s}^n : x = T$ 时，则 $x = n$ 同时

$$
\text{Q}^n(\bar{\it 1}): n = 
    n \times (n - 1) \times \dots \times (n - (n - 1)) \times (\bar{\it 1}: (n - n)) = n\text{!}
$$

> Using these results for $\bar{\it 1} \circ \text{s}^n$ , $\text{eq0} \circ \text{s}^n$, and $\text{Q}^n(\bar{\it 1})$ in the previous expansion for $f$ , we obtain

将 $\bar{\it 1} \circ \text{s}^n$ 、 $\text{eq0} \circ \text{s}^n$ 和 $\text{Q}^n(\bar{\it 1})$ 的结果应用到之前对 $f$ 的展开中，我们便能得到

$$
f:x \equiv 
    x = 0 \to \textit{1};
    \dots;
    x = n \to n \times (n - 1) \times \dots \times 1 \times;
    \dots
$$

> Thus we have proved that $f$ terminates on precisely the set of nonnegative integers and that it is the factorial function thereon. 

至此，我们证明了 $f$ 只会在非负整数集合上得到一个有效值（即停止），这恰恰就是阶乘函数本身。

> 12.6 An Iteration Theorem 

### 12.6 迭代定理

> This is really a corollary of the recursion theorem. It gives a simple expansion for many iterative programs.

迭代定理实际上是递归定理的一个推论。它为许多迭代程序提供了一个简单的展示式。

> ITERATION THEOREM: Let $f$ be the solution (i.e., the least solution) of

**迭代定理**：设 $f$ 为此方程的解（比如，最小解）

$$
f \equiv p \to g; h \circ f \circ k
$$

> then

则

$$
f \equiv p \to g; 
         p \circ k \to h \circ g \circ k;
         \dots;
         p \circ k^n \to h^n \circ g \circ k^n;
         \dots
$$

> PROOF. Let $h' \equiv h \circ 2, i' \equiv \text{id}, j' \equiv k,$ then

**证明** 令 $h' \equiv h \circ 2, i' \equiv \text{id}, j' \equiv k,$ 那么

$$
f \equiv p \to g; h' \circ [i', f \circ j']
$$

> since $h \circ 2 \circ [\text{id}, f \circ k] \equiv h \circ f \circ k$ by **I.5** ( $\text{id}$ is defined except for $\bot$ , and the equation holds for $\bot$ ). Thus the recursion theorem gives

因为根据定理**I.5**，有 $h \circ 2 \circ [\text{id}, f \circ k] \equiv h \circ f \circ k$（注意， $\text{id}$ 除了 $\bot$ 未定义以外，该等式恒成立）。所以，根据递归定理可得

$$
f \equiv p \to g; \dots; p \circ k^n \to \text{Q}^n(g); \dots
$$

> where

其中

$$
\begin{align*}
    \text{Q}^n(g) 
        &\equiv h \circ 2 \circ [\text{id}, \text{Q}^{n-1}(g) \circ k] \\
        &\equiv h \circ \text{Q}^{n-1}(g) \circ k \qquad\qquad \text{ by I.5}\\
        &\equiv h^n \circ g \circ k^n        
\end{align*}
$$

> 12.6.1 Example: Correctness proof for an iterative factorial function.

#### 12.6.1 示例：证明迭代阶乘函数的正确性

> Let $f$ be the solution of

设 $f$ 为

$$
f \equiv \text{eq0} \circ 1 \to 2; f \circ [\text{s} \circ 1, \times]
$$

> where

其中

$$
\textbf{Def } \text{s} \equiv - \circ [\text{id}, \bar{\it 1}] \quad \text{(subtract 1)}
$$

> We want to prove that $f:< x,\textit{1} > = x\text{!}$ iff $x$ is a nonnegative integer. Let $p \equiv \text{eq0} \circ 1, g \equiv 2, h \equiv \text{id}, k \equiv [\text{s} \circ 1, \times]$ . Then

我们要证明，有且仅当 $x$ 为非负整数时， $f:< x,\textit{1} > = x\text{!}$ 。现设 $p \equiv \text{eq0} \circ 1, g \equiv 2, h \equiv \text{id}, k \equiv [\text{s} \circ 1, \times]$ ，则

$$
f \equiv p \to g; h \circ f \circ k
$$

> and so


$$
f \equiv p \to g; \dots; p \circ k^n \to g \circ k^n; \dots \tag{1}
$$

> by the iteration theorem, since $h^n \equiv \text{id}$ . We want to show that

由于 $h^n \equiv \text{id}$ （即可以省略掉 $h^n$ ），又依据迭代定理可得到上面的展开式。进而，我们希望看到

$$
\text{pair} \to \to k^n \equiv [a_n, b_n] \tag{2}
$$

> holds for every $n \ge \textit{1}$ , where

对所有 $n \ge \textit{1}$ 都成立，其中

$$
a_n \equiv s^n \circ 1 \tag{3} 
$$
$$
b_n \equiv /\times \circ [\text{s}^{n-1} \circ 1, \dots, \text{s} \circ 1, 1, 2] \tag{4}
$$

> Now (2) holds for $n = 1$ by definition of $k$ . We assume it holds for some $n \ge \textit{1}$ and prove it then holds for $n + \textit{1}$ . Now

当 $n = 1$ 时，根据 $k$ 的定义，我们知道式（2）是成立的。要想 $n \ge \textit{1}$ 也是成立的，我们只需要证明在 $n + \textit{1}$ 也是成立的。即

$$
\text{pair} \to \to k^{n+1} \equiv k \circ k^n \equiv [\text{s} \circ 1, \times] \circ [a_n, b_n] \tag{5}
$$

> since (2) holds for $n$ . And so

式（2）本身就是关于 $n$ 的，可替换得到

$$
\text{pair} \to \to k^{n+1} \equiv [\text{s} \circ a_n, \times \circ [a_n, b_n]] \quad \text{by I.1 and I.5} \tag{6}
$$

> To pass form (5) to (6) we must check that whenever $a_n$ or $b_n$ yield $\bot$ in (5), so will the right side of (6). Now

要想从式（5）得到式（6），就需要保证 $a_n$ 或 $b_n$ 不能为 $\bot$ 。继续

$$
\text{s} \circ a_n \equiv s^{n+1} \circ 1 \equiv a_{n+1} \tag{7}
$$
$$
\times \circ [a_n, b_n] 
    \equiv /\times \circ [\text{s}^n \circ 1, \text{s}^{n-1} \circ 1, \dots, \text{s} \circ 1, 1, 2] \equiv b_{n+1} \quad \text{by I.3} \tag{8}
$$

> Combining (6), (7), and (8) gives

结合式（6）、（7）和（8）可得

$$
\text{pair} \to \to k^{n+1} \equiv [a_{n+1}, b_{n+1}] \tag{9}
$$

> Thus (2) holds for $n = 1$ and holds for $n + \textit{1}$ whenever it holds for $n$ , therefore, by induction, it holds for every $n \ge \textit{1}$ . Now (2) gives, for pairs: 

既然 $n = 1$ 和 $n + \textit{1}$ 式（2）均成立，那么，基于归纳法，满足 $n \ge \textit{1}$ 的任意 $n$ ，式（2）是成立的。而由式（2）又可得，对于一对值而言：

$$
\begin{align*}
\text{defined} \circ k^n \to \to p \circ k^n 
    &\equiv \text{eq0} \circ 1 \circ [a_n, b_n] \\
    &\equiv \text{eq0} \circ a_n \\
    &\equiv \text{eq0} \circ \text{s}^n \circ 1
\end{align*}
\tag{10}
$$

$$
\begin{align*}
\text{defined} \circ k^n \to \to g \circ k
    &\equiv 2 \circ [a_n, b_n] \\
    &\equiv /\times \circ [\text{s}^{n-1} \circ 1, \dots, \text{s} \circ 1, 1, 2]
\end{align*}
\tag{11}
$$

> (both use 1.5). Now (1) tells us that $f:<x,\textit{1}>$ is defined iff there is an $n$ such that $p \circ k^i:<x,\textit{1}> = F$ for all $i < n$ , and $p \circ k^n:<x ,\textit{1}> = T$ , that is, by (10), $\text{eq0} \circ \text{s}^n:x = T$ , i.e., $x=n$ ; and $g \circ k^n:<x,\textit{1}>$ is defined, in which case, by (11), 

(上述两式都是应用 **I.5** 得到)。现在，若要其式（1）才是确定，则只要 $n$ ，且 $i < n$ ，存在 $p \circ k^i:<x,\textit{1}> = F$ 和 $p \circ k^n:<x ,\textit{1}> = T$ 。也就是，由式（10）得到， $\text{eq0} \circ \text{s}^n:x = T$ 且 $x=n$ ；再根据式（11） $g \circ k^n:<x,\textit{1}>$ 的定义，便有了

$$
f: < x, \it 1 > = /\times:< 1, 2, \dots, x - 1, x, 1> = n!
$$

> which is what we set out to prove.

以上就是证明全过程。

> 12.6.2 Example: proof of equivalence of two iterative programs.

#### 12.6.2 示例：证明两个迭代程序是等价的

> In this example we want to prove that two iteratively defined programs, $f$ and $g$ , are the same function. Let $f$ be the solution of

这里我们要证明两个迭代定义的程序 $f$ 和 $g$ 是等价的。设 $f$ 为

$$
f \equiv p \circ 1 \to 2; h \circ f \circ [k \circ 1, 2] \tag{1}
$$

> Let $g$ be the solution of

而 $g$ 为

$$
g \equiv p \circ 1 \to 2; g \circ [k \circ 1, h \circ 2] \tag{2}
$$

> Then, by the iteration theorem: 

由迭代定理可得：

$$
f \equiv p_0 \to q_0; \dots, p_n \to q_n; \dots \tag{3}
$$
$$
g \equiv p'_0 \to q'_0; \dots, p'_n \to q'_n; \dots \tag{4}
$$

> where (letting $r^0 \equiv \text{id}$ for any $r$ ), for $n = 0, 1, \dots$

其中（令对任意 $r$ 都满足 $r^0 \equiv \text{id}$ ），对 $n = 0, 1, \dots$ 有

$$
p_n \equiv p \circ 1 \circ [k \circ 1, 2]^n 
    \equiv p \circ 1 \circ [k^n \circ 1, 2] 
    \quad \quad \quad \quad \text{by I.5.1} \tag{5}
$$
$$
q_n \equiv h \circ 2 \circ [k \circ 1, 2]^n 
    \equiv h \circ 2 \circ [k^n \circ 1, 2] 
    \quad \quad \quad \quad\text{by I.5.1} \tag{6}
$$
$$
p'_n \equiv h \circ 1 \circ [k \circ 1, h \circ 2]^n 
     \equiv p \circ 1 \circ [k^n \circ 1, h^n \circ 2] 
     \quad \text{by I.5.1} \tag{7}
$$
$$
q'_n \equiv  2 \circ [k \circ 1, h \circ 2]^n 
     \equiv 2 \circ [k^n \circ 1, h^n \circ 2]
     \quad \quad \quad \quad\text{by I.5.1} \tag{8}
$$

（提示一下， $[k \circ 1, 2]^n \equiv [k \circ 1, \text{id} \circ 2]^n$ ）

> Now, from the above, using **I.5**,

以上，应用 **I.5** 得，

$$
\text{defined} \circ 2 \to \to p_n \equiv p \circ k^n \circ 1 
    \enspace \quad \quad \tag{9}
$$
$$
\text{defined} \circ h^n \circ 2 \to \to p'_n \equiv p \circ k^n \circ 1 
    \enspace \tag{10}
$$
$$
\text{defined} \circ k^n \circ 1 \to \to q_n \equiv q'_n \equiv h^n \circ 1 
    \tag{11}
$$

> Thus

进而

$$
\text{defined} \circ h^n \circ 2 \to \to \text{defined} \circ 2 \equiv \bar{T} 
    \tag{11}
$$
$$
\text{defined} \circ h^n \circ 2 \to \to p_n \equiv p'_n
    \quad \quad \quad \enspace\tag{12}
$$

> and

以及

$$
f \equiv p_0 \to q_0; \dots; p_n \to h^n \circ 2; \dots \tag{14}
$$
$$
g \equiv p'_0 \to q'_0; \dots; p'_n \to h^n \circ 2; \dots \tag{15}
$$

> since $p_n$ and $p'_n$ provide the qualification needed for $q_n \equiv q'_n \equiv h^n \circ 2$ .

即，在 $p_n$ 和 $p'_n$ 的限定条件下， 有 $q_n \equiv q'_n \equiv h^n \circ 2$ 。

> Now suppose there is an $x$ such that $f:x \not \equiv g:x$. Then there is an $n$ such that $p_i:x = p'_i:x = F$ for $i < n$ , and $p_n:x \not \equiv p'_n:x$ . From (12) and (13) this can only happen when $h^n \circ 2:x = \bot$ . But since $h$ is $\bot$ -preserving, $h^m \circ 2:x = \bot$ for all $m \ge n$ . Hence $f:x = g:x = \bot$ by (14) and (15). This contradicts the assumption that there is an $x$ for which $f:x \not \equiv g:x$ . Hence $f \equiv g$ .

现在假设存在一个 $x$ 使得 $f:x \not \equiv g:x$ 成立，那么一定有一个 $n$ ，满足 $p_n:x \not \equiv p'_n:x$，且当  $i < n$ 时，满足 $p_i:x = p'_i:x = F$ 。由（12）和（13）可知，这只有在 $h^n \circ 2:x = \bot$ 才成立。 然而 $h$ 本身是 $\bot$ 保留的，这意味着 $h^m \circ 2:x = \bot$ 只要 $m \ge n$ 。因此，根据（14）和（15）可知， $f:x = g:x = \bot$ 。 这恰恰与前面的假设自相矛盾。由此可见， $f \equiv g$ 成立。

> This example (by J. H. Morris, Jr.) is treated more elegantly in [^16] on p. 498. However, some may find that the above treatment is more constructive, leads one more mechanically to the key questions, and provides more insight into the behavior of the two functions. 

这个（由 J. H. Morris, Jr. 提出的）例子在 [^16] 的 498 页中处理地更为优雅。然而，不排除一些人会认为上面的做法更有建设性一些，按部就班地将其引导至核心问题，并提供更多有关这两个函数的见解。

[^16]: [Manna, Z., Ness, S., and Vuillemin, J. Inductive methods for proving properties of programs. Comm.4 CM 16,8 (Aug. 1973) 491-502.](https://dl.acm.org/doi/abs/10.1145/800235.807070)

> 12.7 Nonlinear Equations 

### 12.7 非线性等式

> The preceding examples have concerned "linear" equations (in which the "unknown" function does not have an argument involving itself). The question of the existence of simple expansions that "solve" "quadratic" and higher order equations remains open.

前面的例子都涉及 "线性" 方程（未知函数的参数不包含它本身）。对于 "二次" 及更高次方程的 "解" 是否存在简单展开形式，这个问题仍然悬而未决。

> The earlier examples concerned solutions of $f \equiv \text{E}(f)$ , where $\text{E}$ is linearly expansive. The following example involves an $\text{E}(f)$ that is quadratic and expansive (but not linearly expansive).

之前讨论的例子涉及求解 $f \equiv \text{E}(f)$ 的形式，其中 $\text{E}$ 是线性展开的。而下面例子中的 $\text{E}$ 则是二次（非线性）展开式。

> 12.7.1 Example: proof of idempotency[^16] 

#### 12.7.1 示例：证明幂等性[^16]

> Let $f$ be the solution of

设 $f$ 为

$$
f \equiv E(f) \equiv p \to id; f^2 \circ h \tag{1}
$$

> We wish to prove that $f \equiv f^2$ . We verify that $\text{E}$ is expansive (Section 12.4.1) with the following approximating functions: 

要证明 $f \equiv f^2$ ，我们需要验证 $\text{E}$ 是以如下逼近函数展开的（回忆一下 12.4.1）:

$$
f_0 \equiv \bar{\bot} \tag{2a}
\qquad \qquad \qquad \qquad \qquad \qquad \qquad \qquad \quad
$$

$$
f_n \equiv p \to \text{id}; \dots; p \circ h^{n-1} \to h^{n-1}; \bar{\bot} \text{ for } n \gt 0 \tag{2b}
$$

> First we note that $p \to \to f_n \equiv \text{id}$ and so

首先，我们可以将其记为 $p \to \to f_n \equiv \text{id}$ ，可得

$$
p \circ h^i \to \to f_n \circ h^i \equiv h^i \tag{3}
\qquad
$$
$$
\text{E}(f_0) \equiv p \to \text{id}; \bar{\bot}^2 \circ h \equiv f_1 \tag{4}
$$

> and

以及

$$
\begin{align*}
\text{E}(f_n) \\
  &\equiv p \to \text{id}; f_n \circ (p \to \text{id}; \dots; p \circ h^{n-1} \to h^{n-1}; \bar{\bot}) \circ h \\
  &\equiv p \to \text{id}; f_n \circ (p \circ h \to h; \dots; p \circ h^n \to h^n; \bar{\bot} \circ h) \\
  &\equiv p \to \text{id}; p \circ h \to f_n \circ h; \dots; p \circ h^n \to f_n \circ h^n; f_n \circ \bar{\bot}  \\
  &\equiv p \to \text{id}; p \circ h \to  h; \dots; p \circ h^n \to h^n; \bar{\bot} &\text{ by (3)} \\
  &\equiv f_{n+1}
\end{align*}
\tag{5}
$$

> Thus $\text{E}$ is expansive by (4) and (5); so by (2) and Section 12.4.1 (E4)

基于（4）和（5）可以展开 $\text{E}$ ；而根据（2）和 12.4.1 的（E4）可得无限展开式

$$
f \equiv p \to \text{id}; \dots; p \circ h^n \to h^n; \dots \tag{6}
$$

> But (6), by the iteration theorem, gives 

（6）又结合迭代定理，可得

$$
f \equiv p \to \text{id}; f \circ h \tag{7}
$$

> Now, if $p:x = T$ , then $f.x = x = f^2:x$, by (1). If $p:x = F$ , then

此时，当 $p:x = T$ ，基于（1）则 $f.x = x = f^2:x$ 。而当 $p:x = F$ ，则

$$
\begin{align*}
f:x 
  &= f^2 \circ h: x &\text{by (1)} \\
  &= f:(f \circ h:x) \\
  &= f:(f:x)        &\text{by (7)}\\
  &= f^2:x
\end{align*}
$$

> If $p:x$ is neither $T$ nor $F$ , then $f:x = \bot =f^2:x$. Thus $f \equiv f^2$. 

若是 $p:x$ 既不是 $T$ ，也不是 $F$ ，那么 $f:x = \bot =f^2:x$ 。总之， $f \equiv f^2$ 是成立的。

> 12.8 Foundations for the Algebra of Programs

### 12.8 程序代数的基石

> Our purpose in this section is to establish the validity of the results stated in Section 12.4. Subsequent sections do not depend on this one, hence it can be skipped by readers who wish to do so. We use the standard concepts and results from [^16], but the notation used for objects and functions, etc., will be that of this paper. 

本节的目的是确立 12.4 节的结果的有效性，后续章节不依赖于此，因此读者可以选择跳过本节。我们将使用来自参考[^16] 的标准概念和结果，但是对象、函数等使用的符号会遵循本文的约定。

> We take as the domain (and range) for all functions the set $\rm O$ of objects (which includes $\bot$ ) of a given FP system. We take $\rm F$ to be the set of functions, and $\bf F$ to be the set of functional forms of that FP system. We write $\text{E}(f)$ for any function expression involving functional forms, primitive and defined functions, and the function symbol $f$ ; and we regard $\rm E$ as a functional that maps a function $f$ into the corresponding function $\text{E}(f)$ . We assume that all $f \in \text{F}$ are $\bot$ -preserving and that all functional forms in $\bf F$ correspond to continuous functionals in every variable (e.g., $[f, g]$ is continuous in both $f$ and $g$ ). (All primitive functions of the FP system given earlier are $\bot$ -preserving, and all its functional forms are continuous.) 

就给定的 FP 系统而言，

- 所有函数应用的域（domain）（和范围（range））为对象集合 $\rm O$ （包括 $\bot$ ）；
- 所有函数的集合为 $\rm F$ ，所有函数式的集合为 $\bf F$ ；
- 任何包含函数式、原生函数、定义函数以及函数符号 $f$ 的表达式记为 $\text{E}(f)$ ，其中 $\rm E$ 被视作是将函数 $f$ 映射为 $\text{E}(f)$ 的函数式（functional）；
- 假定所有函数（ $f \in \text{F}$ ）都是 $\bot$ 保留的，且所有函数式（ $\bf F$ ）对应于每个变量的连续函数式（continuous functionals）（早前给定的 FP 系统的所有原声函数就是 $\bot$ 保留的，所有的函数式也是连续的）。

> DEFINITIONS. Let $\text{E}(f)$ be a function expression. Let

**定义** 设 $\text{E}(f)$ 是一个函数表达式，且有

$$
\begin{align*}
f_0 &\equiv \bar{\bot} \\
f_{i+1} &\equiv p_0 \to q_0; \dots; p_i \to q_i; \bar{\bot} &\text{for } i = 0, 1, \dots
\end{align*}
$$

> where $p_i, q_i \in \rm F$. Let $\rm E$ have the property that

其中满足 $p_i, q_i \in \rm F$ 。设 $\rm E$ 具有性质

$$
\text{E}(f_i) \equiv f_{i+1} \quad \text{for } i = 0, 1, \dots
$$

> Then $\rm E$ is said to be *expansive* with the *approximating functions* $f$ . We write 

那 $\rm E$ 可用*逼近函数* $f$ 进行*展开*。我们记作

$$
f \equiv p_0 \to q_0; \dots; p_n \to q_n; \dots
$$

> to mean that $f \equiv \lim_i\{f_i\}$, where the $f$ have the form above. We call the right side an *infinite expansion* of $f$. We take $f:x$ to be defined iff there is an $n \ge 0$ such that (a) $p_i:x = F$ for all $i < n$ , and (b) $p_n:x = T$, and (c) $q_n:x$ is defined, in which case $f:x = q_n:x$ .

其意味着 $f \equiv \lim_i\{f_i\}$ ，里面的 $f$ 是上面的形式。我们也称右边为 $f$ 的*无限展开式*。有且仅当 $n \ge 0$ ，并满足

1. $p_i:x = F$ 且 $i < n$ ；
2. $p_n:x = T$ ；
3. $q_n:x$ 是确定的；

我们便确定了 $f:x$ ， 即 $f:x = q_n:x$ 。

> EXPANSION THEOREM: Let $\text{E}(f)$ be expansive with *approximating functions* as above. Let $f$ be the least function satisfying

**展开定理**：设 $\text{E}(f)$ 是上述逼近函数的展开式， 其 $f$ 满足方程的最小函数

$$
f \equiv \text{E}(f)
$$

> Then

那么

$$
f \equiv p_0 \to q_0; \dots; p_n \to q_n; \dots
$$

> PROOF. Since $\rm E$ is the composition of continuous functionals (from $\bf F$) involving only monotonic functions ($\bot$ -preserving functions from $\rm F$) as constant terms, $\rm E$ is continuous ([^16] p. 493). Therefore its least fixed point $f$ is $\lim_i\{\text{E}^i(\bar{\bot})\} \equiv \lim_i\{f_i\}$ ([^16] p. 494), which by definition is the above infinite expansion for $f$ . 

**证明** 因为 $\rm E$ 是（来自函数式 $\bf F$ ）连续函数式的复合，并且只包含单调函数（来自 $\rm F$ 的 $\bot$ 保留的函数）作为常量项，所以 $\rm E$ 也是连续的（资料[^16]第493页）。进而，最小不动点 $f$ 满足 $\lim_i\{\text{E}^i(\bar{\bot})\} \equiv \lim_i\{f_i\}$ ，这也是被上面  $f$ 的无限展开式所定义的。

> DEFINITION. Let $text{E}(f)$ be a function expression satisfying the following:

**定义** 设 函数表达式 $\text{E}(f)$ 满足

$$
\text{E}(h) \equiv p_0 \to q_0; \text{E}_1(h) \quad \text{for all } h \in \text{F} \tag{LE1}
$$

> where $p_i \in \rm F$ and $q_i \in \rm F$ exist such that

其中存在 $p_i \in \rm F$ 和 $q_i \in \rm F$ 满足

$$
\text{E} _ 1(p_i \to q_i; h) \equiv p _ {i+1} \to q _ {i+1}; \text{E} _ 1(h) \quad \text{for all } h \in \text{F} \text{ and } i = 0, 1, \dots \tag{LE2}
$$

> and

并且

$$
\text{E}_1(\bar{\bot}) \equiv \bar{\bot} \tag{LE3}
$$

> Then $\rm E$ is said to be linearly expansive with respect to these $p_i$ 's and $q_i$ 's.

由此可见， $\rm E$ 是基于 $p_i$ 和 $q_i$ 的*线性展开式*。

> LINEAR EXPANSION THEOREM: Let $\rm E$ be linearly expansive with respect to $p_i$ and $q_i$, $i = 0, 1, \dots$ Then $\rm E$ is expansive with approximating functions 

**线性展开定理**：设 $\rm E$ 是基于 $p_i$ 和 $q_i$ 的线性展开式，且 $i = 0, 1, \dots$ ，那么 $\rm E$ 用逼近函数展开得到

$$
f_0 \equiv \bar{\bot} \tag{1} \qquad\qquad\qquad\qquad
$$

$$
f_{i+1} \equiv p_0 \to q_0; \dots; p_i \to q_i; \bar{\bot} \tag{2}
$$

> PROOF. We want to show that $\text{E}(f_i) \equiv f_{i+1}$ for any $i \ge 0$. Now 

**证明** 对任意 $i \ge 0$ ，有 $\text{E}(f_i) \equiv f_{i+1}$ 。现在

$$
\begin{align*}
\text{E}(f_0) 
  &\equiv p_0 \to q_0; \text{E}_1(\bar{\bot}) \\
  &\equiv p_0 \to q_0; \bar{\bot} \\
  &\equiv f_1   &\text{by (LE1) (LE3) (1)}
\end{align*}
\tag{3}
$$

> Let $i > 0$ be fixed and let 

设 $i > 0$ 且是定值，并有

$$
f_i \equiv p_0 \to q_0; w_1 \tag{4a}
$$

$$
w_1 \equiv p_1 \to q_1; w_2 \tag{4b}
$$

> etc.

依此类推

$$
w_{i-1} \equiv p_{i1} \to q_{i-1}; \bar{\bot} \tag{4-}
$$

> Then, for this $i > 0$

那么，对于这个 $i > 0$ 有

$$
\begin{align*}
\text{E}(f_i) &\equiv p_0 \to q_0; \text{E}_1(f_i) && \text{by (LE1)} \\
\text{E}_1(f_i) &\equiv p_1 \to q_1; \text{E}_1(w_1) && \text{by (LE2) and (4a)} \\
\text{E}_1(w_1) &\equiv p_2 \to q_2; \text{E}_1(w_2) && \text{by (LE2) and (4b)} \\
\end{align*}
$$

> etc.

依此类推

$$
\begin{align*}
\text{E}_ 1(w_ {i-1})
  &\equiv p_i \to q_i; \text{E} _ 1(\bar{\bot}) && \text{by (LE2) and (4-)}\\
  &\equiv p_i \to q_i; \bar{\bot} && \text{by (LE3)}
\end{align*}
$$

> Combining the above gives

综上所得

$$
\text{E}(f_i) \equiv f_{i+1} \quad \text{for arbitrary } i > 0, \text{ by (2)} \tag{5}
$$

> By (3), (5) also holds for $i = 0$; thus it holds for all $i \ge 0$. Therefore $\rm E$ is expansive and has the required approximating functions.

根据（3），（5）在 $i = 0$ 时也是成立的；也就是在所有 $i \ge 0$ 情况下都成立。因此， $\rm E$ 是可展开的，且有其必要的逼近函数。

> COROLLARY. If $\rm E$ is linearly expansive with respect to $p_i$ and $q_i$ , $i = 0, 1, \dots$ and $f$ is the least function satisfying

**推论** 如果 $\rm E$ 是基于 $p_i$ 和 $q_i$ 的线性展开的，且 $i = 0, 1, \dots$ ，且 $f$ 是令其成立的最小函数

$$
f \equiv \text{E}(f) \tag{LE4}
$$

> then

那么

$$
f \equiv p_0 \to q_0; \dots; p_n \to q_n; \dots \tag{LE5}
$$

> 12.9 The Algebra of Programs for the Lambda Calculus and for Combinators

### 12.9 基于Lambda演算和组合子的程序代数

> Because Church's lambda calculus [^5] and the system of combinators developed by Schönfinkel and Curry [^6] are the primary mathematical systems for representing the notion of application of functions, and because they are more powerful than FP systems, it is natural to enquire what an algebra of programs based on those systems would look like.

Church 的 lambda 演算 [^5] 和 Schönfinkel 和 Curry 开发的组合子系统 [^6] 是表示函数应用概念的主要数学系统，同时它们比 FP 系统更强大，自然而然让人去想，基于这些系统的程序代数会是什么样子。

[^5]: [Church, A. The Calculi of Lambda-Conversion. Princeton U. Press, Princeton, N.J., 1941.](https://dl.acm.org/doi/10.5555/1096495)
[^6]: [Curry, H.B., and Feys, R. Combinatory Logic, Vol. 1. North-Holland Pub. Co., Amsterdam, 1958.](http://scholar.google.com/scholar?hl=en&q=Curry%2C+H.B.%2C+and+Feys%2C+R.+Combinatory+Logic%2C+Vol.+1.+North-+Holland+Pub.+Co.%2C+Amsterdam%2C+1958.)


> The lambda calculus and combinator equivalents of FP composition, $f \circ g$, are

在 lambda 演算和组合子中，与 FP 组合 $f \circ g$ 等价的是

$$
\lambda fgx.(f(gx)) \equiv \text{B}
$$

> where $\rm B$ is a simple combinator defined by Curry. There is no direct equivalent for the FP object $< x, y >$ in the Church or Curry systems proper; however, following Landin [^14] and Burge [^4], one can use the primitive functions prefix, head, tail, null, and atomic to introduce the notion of list structures that correspond to FP sequences. Then, using FP notation for lists, the lambda calculus equivalent for construction is $\lambda fgx.<fx,gx>$. A combinatory equivalent is an expression involving prefix, the null list, and two or more basic combinators. It is so complex that I shall not attempt to give it.

其中 $\rm B$ 是由 Curry 定义的一个简单组合子。在 Church 或 Curry 系统本身中，没有直接等价于 FP 对象 < x, y > 的表示；然而，遵循 Landin [^14] 和 Burge [^4] 的方法，可以使用原始函数 prefix、head、tail、null 和 atomic 来引入与 FP 序列相对应的列表结构概念。也就是说，使用 FP 的列表表示法，lambda 演算中用于构造的等价形式是 $\lambda fgx.<fx,gx>$ 。组合子等价物是一个包含前缀、空列表和两个或更多个基本组合子的表达式。这个过于复杂，在这儿就不尝试给出了。

[^14]: [Landin, P.J. The mechanical evaluation of expressions. Computer J. 6, 4 (1964), 308-320.](http://scholar.google.com/scholar?hl=en&q=Landin%2C+P.J.+The+mechanical+evaluation+of+expressions.+Computer+J.+6%2C+4+%281964%29%2C+308-320.)
[^4]: [Burge, W.H. Recursive Programming Techniques. Addison-Wesley, Reading, Mass., 1975](http://scholar.google.com/scholar?hl=en&q=Burge%2C+W.H.+Recursive+Programming+Techniques.+Addison-+Wesley%2C+Reading%2C+Mass.%2C+1975.)

> If one uses the lambda calculus or combinatory expressions for the functional forms $f \circ g$ and $[f, g]$ to express the law **I.1** in the FP algebra, $[f,g] \circ h \equiv [f \circ h, g \circ h]$ , the result is an expression so complex that the sense of the law is obscured. The only way to make that sense clear in either system is to name the two functionals: composition $\equiv \text{B}$ , and construction $\equiv \text{A}$ , so that $\text{B}fg \equiv f \circ g$, and $\text{A}fg \equiv [f, g]$ . Then **I.1** becomes 

像函数式 $f \circ g$ 和 $[f, g]$ ，若要以 lambda 演算或组合子表达式的形式来表达 FP 代数里的定律 **I.1**，即 $[f,g] \circ h \equiv [f \circ h, g \circ h]$ ，其呈现的结果会过于复杂，令定律显得晦涩难懂。要想清晰表达的唯一方法是，在这两个系统里命名两个函数式：组合 $\equiv \text{B}$ 和 构建 $\equiv \text{A}$ ， 也就是 $\text{B}fg \equiv f \circ g$ ， $\text{A}fg \equiv [f, g]$ 。因此， 定律 **I.1** 则变成

$$
\text{B}(\text{A}fg)h \equiv \text{A}(\text{B}fh)(\text{B}gh)
$$

> which is still not as perspicuous as the FP law.

即便如此，这也依然不如 FP 定律表达得明了。

> The point of the above is that if one wishes to state clear laws like those of the FP algebra in either Church's or Curry's system, one finds it necessary to select certain functionals (e.g., composition and construction) as the basic operations of the algebra and to either give them short names or, preferably, represent them by some special notation as in FP. If one does this and provides primitives, objects, lists, etc., the result is an FP-like system in which the usual lambda expressions or combinators do not appear. Even then these Church or Curry versions of FP systems, being less restricted, have some problems that FP systems do not have:

正如前文提及的，若想要在 Church 或 Curry 系统中，像 FP 代数一般清晰地呈现定律，就必须选择特定的函数式（例如，复合和构造）作为代数的基本运算，并为它们取简短的名称，或者最好像 FP 一样用特殊符号表示它们。要是这样做了，还提供原始函数、对象、列表等，那么结果只会是一个类似于 FP 的系统，其中不会出现通常意义上的 lambda 演算和组合子。尽管基于 Church 或 Curry 的 FP 系统版本限制很少，但也会存在一些 FP 系统没有的问题：

> a) The Church and Curry versions accommodate functions of many types and can define functions that do not exist in FP systems. Thus, $\text{B}f$ is a function that has no counterpart in FP systems. This added power carries with it problems of type compatibility. For example, in $f \circ g$ , is the range of $g$ included in the domain of $f$ ? In FP systems all functions have the same domain and range. 
> 
> b) The semantics of Church's lambda calculus depends on substitution rules that are simply stated but whose implications are very difficult to fully comprehend. The true complexity of these rules is not widely recognized but is evidenced by the succession of able logicians who have published "proofs" of the Church-Rosser theorem that failed to account for one or another of these complexities. (The Church-Rosser theorem, or Scott's proof of the existence of a model [^22], is required to show that the lambda calculus has a consistent seman- tics.) The definition of pure Lisp contained a related error for a considerable period (the "funarg" problem). Analogous problems attach to Curry's system as well. 

1. Church 和 Curry 版本里允许多种类型的函数，并且可以定义 FP 系统中不存在的函数。例如， $\text{B}f$ 是一个在 FP 系统中没有对应表达的函数。可是，这种额外的功能带来了类型兼容性问题。具体到 $f \circ g$ 来说， $g$ 的输出值范围 (range) 是否包含在 $f$ 的输入值范围 (domain) 内呢？在 FP 系统里，所有函数都具有相同的输入值范围和输出值范围，这个问题是不存在的。
2. Church 的 lambda 演算的语义定义依赖于替换规则，虽然规则本身看起来简单，但是理解其所有影响和细节却非常困难。这些规则的真正复杂性并未被广泛认知，无视它们，即便是才华横溢的逻辑学家，也会导致证明 Church-Rosser 定理的失败。（Church-Rosser 定理，或 Scott 的模型存在性证明[^22]，是体现 lambda 演算具有一致性语义的关键。）纯 Lisp 的定义在相当长一段时间内也包含了一个与之关联的错误 (“funarg” 问题)。类似的问题也存在于 Curry 系统中。

[^22]: [Scott, D. Lattice-theoretic models for various type-free calculi. Proc. Fourth Int. Congress for Logic, Methodology, and the Philosophy of Science, Bucharest, 1972.](http://scholar.google.com/scholar?hl=en&q=Scott%2C+D.+Lattice-theoretic+models+for+various+type-free+calculi.+Proc.+Fourth+Int.+Congress+for+Logic%2C+Methodology%2C+and+the+Philosophy+of+Science%2C+Bucharest%2C+1972.)

> In contrast, the formal (FFP) version of FP systems (described in the next section) has no variables and only an elementary substitution rule (a function for its name), and it can be shown to have a consistent semantics by a relatively simple fixed-point argument along the lines developed by Dana Scott and by Manna et al [^16]. For such a proof see McJones [^18]. 

相比之下，FP 系统的形式化（FFP）版本 (将在下一节描述)没有变量，并且只有一个基本的替换规则（即函数替换其名）。它可以通过 Dana Scott 和 Manna 等人 [^16] 开发的相对简单的固定点论证来证明它具有一致性的语义。

[^18]: [Me Jones, P. A Church-Rosser property of closed applicative languages. Rep. RJ 1589, IBM Res. Lab., San Jose, Calif., May 1975.](http://scholar.google.com/scholar?hl=en&q=Me+Jones%2C+P.+A+Church-Rosser+property+of+closed+applicative+languages.+Rep.+RJ+1589%2C+IBM+Res.+Lab.%2C+San+Jose%2C+Calif.%2C+May+1975.)

> 12.10 Remarks

### 12.10 小结

The algebra of programs outlined above needs much work to provide expansions for larger classes of equations and to extend its laws and theorems beyond the elementary ones given here. It would be interesting to explore the algebra for an FP-like system whose sequence constructor is not $\bot$ -preserving (law **I.5** is strengthened, but **IV.1** is lost). Other interesting problems are: (a) Find rules that make expansions unique, giving canonical forms for functions; (b) find algorithms for expanding and analyzing the behavior of functions for various classes of arguments; and (c) explore ways of using the laws and theorems of the algebra as the basic rules either of a formal, preexecution "lazy evaluation" scheme [^9] [^10], or of one which operates during execution. Such schemes would, for example, make use of the law $1 \circ [f, g] \le f$ to avoid evaluating $g:x$ . 

上面概述的程序代数还需要大量工作才能为更复杂（larger classes）的方程提供展开式，并扩展其基础定律和定理，以应对到更多以外的情况。一个有趣的拓展方向是，探索一个类似 FP 的系统，其序列构造器不是 $\bot$ 保留的（即定律 **I.5** 被加强，而定律 **IV.1** 会消失）。其他有趣的问题包括：

1. 找到唯一化展开的规则，为函数提供规范形式；
2. 找到用于展开和分析函数在各类参数下行为的算法；
3. 探索使用代数定律和定理的方法，作为基础的规则以便形式化，执行前或执行中的“延迟求值”方案[^9] [^10]。比如，避免定律 $1 \circ [f, g] \le f$ 在 $g:x$ 上的求值计算。

[^9]: [Friedman, D.P., and Wise, D.S. CONS should not evaluate its arguments. In Automata, Languages and Programming, S. Michaelson and R. Milner, Eds., Edinburgh U. Press, Edinburgh, 1976, pp. 257-284.](http://scholar.google.com/scholar?hl=en&q=Friedman%2C+D.P.%2C+and+Wise%2C+D.S.+CONS+should+not+evaluate+its+arguments.+In+Automata%2C+Languages+and+Programming%2C+S.+Michaelson+and+R.+Milner%2C+Eds.%2C+Edinburgh+U.+Press%2C+Edinburgh%2C+1976%2C+pp.+257-284.)
[^10]: [Henderson, P., and Morris, J.H. Jr. A lazy evaluator. Conf. Record Third ACM Symp. on Principles of Programming Languages, Atlanta, Ga., Jan. 1976, pp. 95-103.](https://dl.acm.org/doi/10.1145/800168.811543)
