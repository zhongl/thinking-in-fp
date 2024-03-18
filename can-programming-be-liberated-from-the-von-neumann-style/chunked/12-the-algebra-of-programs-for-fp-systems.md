> 12. The Algebra of Programs for FP Systems 

## 12. 用于 FP 系统的程序代数

> 12.1 Introduction 

### 12.1 介绍

> The algebra of the programs described below is the work of an amateur in algebra, and I want to show that it is a game amateurs can profitably play and enjoy, a game that does not require a deep understanding of logic and mathematics. In spite of its simplicity, it can help one to understand and prove things about programs in a systematic, rather mechanical way. 

以下描述的程序代数可能看起来业余，但我想要表明这对于业余爱好者来说也是一个有趣且有益的探索。它并不需要深厚的逻辑数学功底。尽管形式简单，这种代数方法依然可以帮助我们系统地、近乎机械地理解和证明程序相关的问题。

> So far, proving a program correct requires knowledge of some moderately heavy topics in mathematics and logic: properties of complete partially ordered sets, continuous functions, least fixed points of functionals, the first-order predicate calculus, predicate transformers, weakest preconditions, to mention a few topics in a few approaches to proving programs correct. These topics have been very useful for professionals who make it their business to devise proof techniques; they have published a lot of beautiful work on this subject, starting with the work of McCarthy and Floyd, and, more recently, that of BurstaU, Dijkstra, Manna and his associates, Milner, Morris, Reynolds, and many others. Much of this work is based on the foundations laid down by Dana Scott (denotational semantics) and C. A. R. Hoare (axiomatic semantics). But its theoretical level places it beyond the scope of most amateurs who work outside of this specialized field. 

直到现在，证明程序的正确性需要用到一些相当复杂的数学和逻辑知识：

- 偏序集的性质 (properties of complete partially ordered sets)
- 连续函数 (continuous functions)
- 泛函的最小不动点 (least fixed points of functionals)
- 一阶谓词逻辑 (the first-order predicate calculus)
- 谓词变换器 (predicate transformers)
- 最弱前提条件 (weakest preconditions)

以上这些仅仅是证明程序正确性的一些方法中涉及到的部分主题。这些复杂的知识对于专业人士制定程序证明技术非常有用，像是麦卡锡和弗洛伊德 (McCarthy and Floyd) 的早期工作，到最近伯斯塔尔 (BurstaU)、戴克斯特拉 (Dijkstra)、曼纳 (Manna) 及其同事、米尔纳 (Milner)、莫里斯 (Morris)、雷诺兹 (Reynolds) 等众多学者的研究，都取得了令人赞叹的成就。这些成果大多建立在达纳·斯科特 (Dana Scott，指称语义学) 和 C. A. R. 霍尔 (C. A. R. Hoare，公理语义学) 的基础之上。然而，这些理论的复杂程度让它们超出了大多数非相关领域的业余爱好者的理解范围。

> If the average programmer is to prove his programs correct, he will need much simpler techniques than those the professionals have so far put forward. The algebra of programs below may be one starting point for such a proof discipline and, coupled with current work on algebraic manipulation, it may also help provide a basis for automating some of that discipline.

如果希望普通的程序员也能证明程序的正确性，那么就需要比现有方法更简单易懂的证明技术。本文描述的程序代数可以是这样一个证明方法的起点。结合当下关于代数操作(algebraic manipulation) 的研究成果，它甚至可以帮助实现部分程序正确性证明过程的自动化。 

> One advantage of this algebra over other proof techniques is that the programmer can use his programming language as the language for deriving proofs, rather than having to state proofs in a separate logical system that merely talks about his programs. 

程序代数相比其他证明方法的一大优势是，程序员可以使用熟悉的编程语言进行证明推导，而不是去使用与自己程序无关且独立的逻辑系统来证明。

> At the heart of the algebra of programs are laws and theorems that state that one function expression is the same as another. Thus the law $[f,g] \circ h \equiv [f \circ h, g  \circ h]$ says that the construction of $f$ and $g$ (composed with $h$ ) is the same function as the construction of ( $f$ composed with $h$ ) and ( $g$ composed with $h$ ) no matter what the functions $f$ , $g$ , and $h$ are. Such laws are easy to understand, easy to justify, and easy and powerful to use. However, we also wish to use such laws to solve equations in which an "unknown" function appears on both sides of the equation. The problem is that if $f$ satisfies some such equation, it will often happen that some extension $f'$ of $f$ will also satisfy the same equation. Thus, to give a unique meaning to solutions of such equations, we shall require a foundation for the algebra of programs (which uses Scott's notion of least fixed points of continuous functionals) to assure us that solutions obtained by algebraic manipulation are indeed least, and hence unique, solutions.

程序代数的核心是定义函数表达式相等关系的定律和定理。例如，定律 $[f,g] \circ h \equiv [f \circ h, g  \circ h]$ 表示，由 $f$ 和 $g$ 构成的构造式（construction）与 $h$ 的组合，无论 $f,g,h$ 是什么，都等价于由 $f$ 和 $g$ 分别组合了 $h$ 的结果构成的构造式。这些定律易于理解、证明，并且应用起来既方便又强大。然而，我们还希望利用这些定律来解方程，且方程两边都可能出现未知函数。问题在于，如果函数 $f$ 是某个方程的解，那么往往它的扩展 $f'$ 也可能是该方程的解。因此，为了让方程的解是唯一确定，我们需要程序代数的基础 (该基础运用了 Scott 关于连续泛函的最小不动点的概念) 来确保通过代数运算得到就是最小解，即唯一解。

> Our goal is to develop a foundation for the algebra of programs that disposes of the theoretical issues, so that a programmer can use simple algebraic laws and one or two theorems from the foundations to solve problems and create proofs in the same mechanical style we use to solve high-school algebra problems, and so that he can do so without knowing anything about least fixed points or predicate transformers. 

我们的目标是打造一套程序代数的基础理论，让程序员如同解高中代数题一般，使用简单的代数定律和一两个基础定理来解决问题完成证明，而无需了解最小不动点、谓词变换器等艰深的书序概念。

> One particular foundational problem arises: given equations of the form

一个特别基础的问题借由下面给定形式的等式来展开

$$
\begin{align}
f \equiv p_0 \to q_0; \dots; p_i \to q_i; E_i(f),    
\end{align}
$$

> where the $p_i$ 's and $q_i$ 's are functions not involving $f$ and $E_i(f)$ is a function expression involving $f$ , the laws of the algebra will often permit the formal "extension" of this equation by one more "clause" by deriving 

其中 $p_i$ 和 $q_i$ 都是不函 $f$ 的函数，而是 $E_i(f)$ 是包含 $f$ 的函数表达式。结合下面另一个“子句”，根据代数的定律，我们可以对等式进行形式化“扩展”

$$
\begin{align}
E_i(f) \equiv p_{i+1} \to q_{i+1}; E_{i+1}(f)
\end{align}
$$

> which, by replacing $E_i(f)$ in (1) by the right side of (2), yields

即，将（1）式中 $E_i(f)$ 替换为（2）式右侧的部分，得到

$$
\begin{align}
f \equiv p_0 \to q_0; \dots; p_{i+1} \to q_{i+1}; E_{i+1}(f).    
\end{align}
$$

> This formal extension may go on without limit. One question the foundations must then answer is: when can the least $f$ satisfying (1) be represented by the infinite expansion

这样的形式化扩展可以无限制的进行下去。那么，基础理论必须回答一个问题就是：满足（1）式的最小 $f$ 何时能在无限展开式的

$$
\begin{align}
f \equiv p_0 \to q_0; \dots; p_n \to q_n; \dots
\end{align}
$$

> in which the final clause involving $f$ has been dropped, so that we now have a solution whose right side is free of $f$ 's? Such solutions are helpful in two ways: first, they give proofs of "termination" in the sense that (4) means that $f: x$ is defined if and only if there is an $n$ such that, for every $i$ less than $n$, $p_i: x = F$ and $p_n : x = T$ and $q_n : x$ is defined. Second, (4) gives a case-by-case description of $f$ that can often clarify its behavior.

子句中消除对 $f$ 引用，从而立即得到右侧无 $f$ 的解呢？这个解会在两方面很有用：

1. 给出“终止”的证明。以（4）式中 $f: x$ 而言，尤其仅有一个 $n$ ，对于每个小于 $n$ 的 $i$ 都有 $p_i: x = F$ 和 $p_n : x = T$ ，从而得到 $q_n : x$ ；
2. 给出每种情况下 $f$ 的描述，以阐明其行为。

> The foundations for the algebra given in a subsequent section are a modest start toward the goal stated above. For a limited class of equations its "linear expansion theorem" gives a useful answer as to when one can go from indefinitely extendable equations like (1) to infinite expansions like (4). For a larger class of equations, a more general "expansion theorem" gives a less helpful answer to similar questions. Hopefully, more powerful theorems covering additional classes of equations can be found. But for the present, one need only know the conclusions of these two simple foundational theorems in order to follow the theorems and examples appearing in this section. 

本文后续部分介绍的程序代数仅仅是实现既定目标的初步尝试。 对于有限的一类方程，该理论中的 “线性延拓定理” 提供了实用的解答。这个定理告诉我们，何时可以将像 (1) 式一样无限延拓的方程转化成像 (4) 式一样的无限展开式。对于更广泛的一类方程，文中给出了一个更一般的 “延拓定理”，但其解答对于类似问题的作用较小。希望未来能找到针对更多类型方程的强大定理。但就目前而言，读者只需要理解这两个简单基础定理的结论，就足以理解本文档后续部分的定理和示例。

> The results of the foundations subsection are summarized in a separate, earlier subsection titled "expansion theorems," without reference to fixed point concepts. The foundations subsection itself is placed later where it can be skipped by readers who do not want to go into that subject.

关于代数基础的结论被单独总结在一个名为 “延拓定理” 的靠前子节中，并且没有引用“不动点” (fixed point) 的概念。而代数基础本身则被放置靠后，方便不想深入研究该主题的读者跳过。

> 12.2 Some Laws of the Algebra of Programs

### 12.2 一些程序代数的定律

> In the algebra of programs for an FP system variables range over the set of functions of the system. The "operations" of the algebra are the functional forms of the system. Thus, for example, $[f,g] \circ h$ is an expression of the algebra for the FP system described above, in which $f$ , $g$ , and $h$ are variables denoting arbitrary functions of that system. And 

在 FP 系统的程序代数中，变量的取值范围是系统的所有函数集合。代数的 “运算” 则由该系统的函数形式构成。有如， $[f,g] \circ h$ 这样上述提及的 FP 系统的代数表达式， 其中 $f$ 、 $g$ 和 $h$ 都 是变量，表示该系统中的任意函数。则

$$
[f, g] \circ h \equiv [f \circ h, g \circ h]
$$

> is a law of the algebra which says that, whatever functions one chooses for $f$ , $g$ , and $h$ , the function on the left is the same as that on the right. Thus this algebraic law is merely a restatement of the following proposition about any FP system that includes the functional forms $[f, g]$ and $f \circ g$ :

是一个代数定律，表示无论 $f$ 、 $g$ 和 $h$ 是什么函数，上式左右是等价的。这样的代数定律也只是在重声下面的命题，即，对任何 FP 系统，其内的函数形式 $[f, g]$ 和 $f \circ g$ ：

> PROPOSITION: For all functions $f$ , $g$ , and $h$ and all objects $x$, $([f,g] \circ h):x \equiv [f \circ h, g \circ h ]:x$ . 
> 
> PROOF:

**命题**：对所有函数 $f$ 、 $g$ 和 $h$ ，以及所有对象 $x$ ，都有 $([f,g] \circ h):x \equiv [f \circ h, g \circ h ]:x$ . 

**证明**：

$$
\begin{aligned}    
([f, g] \circ h) : x 
  &= [f, g] : (h : x)                     &\text{ by definition of composition}\\
  &= < f : (h : x), g : (h : x) >         &\text{ by definition of construction}\\
  &= < (f \circ h) : x, (g \circ h) : x > &\text{ by definition of composition}\\
  &= [ f \circ h, g \circ h ] : x         &\text{ by definition of construction}\\
\end{aligned}
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

意指 $\text{defined} : x \equiv x = \bot \to \bot; T$ 可检测对象 $x$ 是否未知。通常，我们会写成一个 *限定函数方程*：

$$
p \to\to f \equiv g
$$

> to mean that, for any object $x$ , whenever $p:x = T$, then $f:x = g:x$ . 

意思是，对任何对象 $x$ ，当满足 $p:x = T$ ，则 $f:x = g:x$ 。

> Ordinary algebra concerns itself with two operations, addition and multiplication; it needs few laws. The algebra of programs is concerned with more operations (functional forms) and therefore needs more laws.

常规代数只涉及加法和乘法这两种运算，因此只需要少量定律就能描述其基本性质。然而，程序代数则涉及更多的运算 (函数形式)，因此需要更多的定律来描述程序的行为和性质。

> Each of the following laws requires a corresponding proposition to validate it. The interested reader will find most proofs of such propositions easy (two are given below). We first define the usual ordering on functions and equivalence in terms of this ordering: 

后续的每个定律都需要一个对应的命题来证明其有效性。对于感兴趣的读者来说，大部分此类命题的证明都比较简单（文章中还会给出两个为示例）。首先，我们就常见函数的排序以及基于排序的等价关系展开定义：

> DEFINITION $f \le g$ iff[^iff] for all objects $x$ , either $f:x = \bot$ , or $f:x = g:x$ .

[^iff]: 是 “if and only if” 的缩写。

**定义** $f \le g$ 有且仅当(iff) 所有对象，满足 $f:x = \bot$ ，或 $f:x = g:x$ 。

> DEFINITION $f \equiv g$ iff $f \le g$ and $g \le f$.

**定义** $f \equiv g$ 有且仅当 $f \le g$ 且 $g \le f$ 。

> It is easy to verify that $\le$ is a partial ordering, that $f \le g$ means $g$ is an extension of $f$ , and that $f \equiv g$ iff $f:x = g:x$ for all objects $x$ . We now give a list of algebraic laws organized by the two principal functional forms in volved.

显而易见，$\le$ 表达了一种偏序关系，即 $f \le g$ 表示函数 $g$ 是函数 $f$ 的一个扩展，而当所有对象 $x$ 都满足 $f:x = g:x$ 时， $f \equiv g$ 自然也是成立的。接下来，文章将提供一系列的代数定律，这些定律将根据程序代数中涉及的两种主要函数形式进行组织。

> I Composition and construction

#### I 组合与构造

**I.1** 

$$
[f_1, \dots, f_n] \circ g \equiv [f_1 \circ, \dots, f_n \circ g]
$$

**I.2**

$$
\alpha f \circ [g_1, \dots, g_n] \equiv [f \circ g_1, \dots, f \circ g_n] 
$$

**I.3**

$$
\begin{alignedat}{3}
    /f \circ [g_1, \dots, g_n]\\
    &\equiv f \circ [g_1, /f \circ [g_2, \dots, g_n]] &\text{ when } n \ge \textit{2}\\
    &\equiv f \circ [g_1, f \circ [g_2, \dots, f \circ [g_{n-1}, g_n] \dots]] \\
    /f \circ [g] &\equiv g
\end{alignedat}
$$

**I.4**

$$
f \circ [\bar{x}, g] \equiv (\text{bu } f x) \circ g
$$

**I.5**

$$
\begin{alignedat}{2}
  1 \circ [f_1, \dots, f_n] &\le f_1 \\
  \text{s} \circ [f_1, \dots, f_s, \dots, f_n] &\le f_s \text{ for any  selector s, } s \le n \\
\text{defined} \circ f_i (\text{for all } i \not = s, \textit{1} \le i \le n) \to\to \text{s} \circ [f_1, \dots, f_n] &\equiv f_s
\end{alignedat}
$$

**I.5.1**

$$
[f_1 \circ 1, \dots, f_n \circ n] \circ [g_1, \dots, g_n] \equiv [f_1 \circ g_1, \dots f_n \circ g_n]
$$

**I.6**

$$
\begin{alignedat}{3}
\text{tl} \circ [f_1] &\le \bar{\phi} &\text{ and } \\
\text{tl} \circ [f_1, \dots, f_n] &\le [f_2, \dots, f_n] &\text{ for } n \ge \textit{2} \\
\text{defined} \circ f_1 \to \to \text{tl} \circ [f_1] &\equiv \bar{\phi} &\text{ and } \\
\text{tl} \circ [f_1, \dots, f_n] &\equiv [f_2, \dots, f_n] &\text{ for } n \ge \textit{2}    
\end{alignedat}
$$

**I.7**

$$
\begin{alignedat}{2}
  \text{distl} \circ [f, [g_1, \dots, g_n]] &\equiv [[f, g_1], \dots, [f, g_n]] \\
  \text{defined} \circ f \to \to \text{distl} \circ [f, \bar{\phi}] &\equiv \bar{\phi} 
\end{alignedat}
$$

> The analogous law holds for $\text{distr}$ .

$\text{distr}$ 也是类似的。

**I.8**

$$
\begin{alignedat}{2}
  \text{apndl} \circ [f, [g_1, \dots, g_n]] &\equiv [f, g_1, \dots, g_n]  \\
  \text{null} \circ g \to \to \text{apndl} \circ [f, g] &\equiv [f]
\end{alignedat}
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
\begin{alignedat}{3}
\text{pair} \And \text{not} \circ \text{null} \circ 1 \to \to \\
&\text{apndl} \circ [[1 \circ 1, 2], \text{distr} \circ [\text{tl} \circ 1, 2]] &&\equiv \text{distr} \\
\text{Where} \\
&f \And g &&\equiv \text{and } \circ [f, g];\\
&\text{pair} &&\equiv \text{atom} \to \bar{F}; \text{eq} \circ [\text{length}, \bar{\it 2}]\\
\end{alignedat}
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
\begin{aligned}
&\text{or} \circ [q, \text{not} \circ q] \to \to \text{and} \circ [p, q] \to f;\\
&\quad\text{and} \circ [p, \text{not} \circ q] \to g; h \equiv p \to (q \to f; g); h    
\end{aligned}
$$

**II.3.1**

$$
p \to (p \to f; g); h \equiv p \to f; h
$$

> III Composition and miscellaneous

#### III 组合与杂项

**III.1**

$$
\begin{aligned}    
\bar{x} \circ f &\le \bar{x} \\
\text{defined} \circ f \to \to \bar{x} \circ f &\equiv \bar{x}
\end{aligned}
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
\begin{aligned}    
\text{pair} \to \to &1 \circ \text{distr} &\equiv&\ [1 \circ 1, 2] &\text{ also:} \\
\text{pair} \to \to &1 \circ \text{tl} &\equiv&\ 2 &\text{etc.}
\end{aligned}
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
\begin{aligned}
  &[f_1, \dots, (p \to g; h), \dots, f_n]\\
  &\qquad \equiv p \to [f_1, \dots, g, \dots, f_n]; [f_1, \dots, h, \dots, f_n]
\end{aligned}
$$

**IV.1.1**

$$
\begin{aligned}
  &[f_1, \dots, (p_1 \to g_1;\dots;p_n \to g_n; h), \dots, f_m]\\
  &\qquad \equiv p_1 \to [f_1, \dots, g_1, \dots, f_m]; \\
  &\qquad \dots ; p_n \to [f_1, \dots, g_n, \dots, f_m];[f_1, \dots, h, \dots, f_m] 
\end{aligned}
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
\begin{aligned}
  &\text{apndl} \circ [f \circ g, \alpha f \circ h] : x \\
  &\quad = \text{apndl} : < f \circ g : x, \phi > \\
  &\quad = < f : (g : x) > \\
  \\
  &\alpha f \circ \text{apndl} \circ [g, h] : x \\
  &\quad = \alpha f \circ \text{apndl} : < g : x, \phi > \\
  &\quad = \alpha f : < g : x > \\
  &\quad = < f : (g : x) >
\end{aligned}
$$

> CASE 3. $h : x = < y_1, \dots, y_n >$ . Then

**情况 3** 当 $h : x = < y_1, \dots, y_n >$ ，则

$$
\begin{aligned}
  &\text{apndl} \circ [f \circ g, \alpha f \circ h] : x \\
  &\quad = \text{apndl} : < f \circ g : x, \alpha f : < y_1, \dots, y_n > > \\
  &\quad = < f : (g : x), f : y_1, \dots, f : y_n > \\
  \\
  &\alpha f \circ \text{apndl} \circ [g, h] : x \\
  &\quad = \alpha f \circ \text{apndl} : < g : x, < y_1, \dots, y_n > > \\
  &\quad = \alpha f : < g : x, y_1, \dots, y_n > \\
  &\quad = < f : (g : x), f : y_1, \dots, f : y_n >
\end{aligned}
$$

> PROPOSITION 2

**命题 2**

$$
\begin{aligned}
\text{pair} \And \text{not} \circ \text{null} \circ 1 \to \to \\
&\text{apndl} \circ [[1^2, 2], \text{distr} \circ [\text{tl} \circ 1, 2]] \equiv \text{distr} 
\end{aligned}
$$

> where $f \And g$ is the function: $\text{and} \circ [f, g]$ , and $f^2 \equiv f \circ f$ .

其中 $f \And g$ 是函数 $\text{and} \circ [f, g]$ ，且 $f^2 \equiv f \circ f$ 。

> PROOF. We show that both sides produce the same result when applied to any $pair <x,y>$ , where $x \not = \phi$ , as per the stated qualification. 

**证明** 限定，对任意 $pair < x, y >$ ，且其中 $x \not = \phi$ 的应用，两边的结果是一致的。

> CASE 1. $x$ is an atom or $\bot$ . Then $\text{distr} : < x, y > = \bot$ , since $x \not = \phi$ . The left side also yields $\bot$ when applied to $< x, y >$ , since $\text{tl} \circ 1 : < x, y > = \bot$ and all functions are $\bot$ -preserving. 

**情况 1** 当 $x \not = \phi$， $x$ 是一个原子，或 $\bot$ 时，则 $\text{distr} : < x, y > = \bot$ 。又因为 $\text{tl} \circ 1 : < x, y > = \bot$ 且所有函数都是 $\bot$ 保留的，所以左边的函数应用 $< x, y >$ 只会的到 $\bot$ 。

> CASE 2. $x = < x_1, \dots, x_n >$. Then 

**情况 2** 当 $x = < x_1, \dots, x_n >$ ，则

$$
\begin{aligned}
  &\text{apndl} \circ [[1^2, 2], \text{distr} \circ [\text{tl} \circ 1, 2]] : < x, y >\\
  &\quad = \text{apndl} : << 1 : x, y >, \text{distr} : < \text{tl} : x, y >> \\
  &\quad = \text{apndl} : << x_1, y >, \phi> &&= << x_1, y >> &&\text{if tl} : x = \phi \\
  &\quad = \text{apndl} : << x_1, y >, < x_2, y >, \dots, < x_n, y >> &&= << x_1, y>, \dots, < x_n, y >> &&\text{if tl} : x \not = \phi \\
  &\quad = \text{distr} : < x, y >
\end{aligned}
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

（$\text{MM'}$ 是针对一对矩阵，其第二矩阵需要经过转置，的“乘法” 计算。与 $\text{MM}$ 不同的是，若输入的不是矩阵对的话，会得到 $\bot$ 。）

是的， $\text{MM'}$ 确实满足下面这个递归定义的等式（仅限成对的输入）：

$$
f \equiv \text{null} \circ 1 \to \bar{\phi};\text{apndl} \circ [\alpha \text{IP} \circ \text{distl} \circ [1 \circ 1, 2], f \circ [\text{tl} \circ 1, 2]]
$$

> Our proof will take the form of showing that the following function, $\text{R}$, 

如下函数形式，$\text{R}$ 说明了，

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
\begin{aligned}
&\text{pair} \to \to \text{MM'} \equiv \text{R} \\
&\text{where}\\
&\textbf{Def } \text{MM'} \equiv 
    \alpha \alpha \text{IP} \circ \alpha \text{distl} \circ \text{distr}\\
&\textbf{Def } \text{R} 
    \equiv \text{null} \circ 1 \to \bar{\phi};
    \text{apndl} \circ [
        \alpha \text{IP} \circ \text{distl} \circ [1 \circ 1, 2], 
        \text{MM'} \circ [\text{tl} \circ 1, 2]
    ]    
\end{aligned}
$$

> PROOF.

**证明**

> CASE 1. $\text{pair} \And \text{null} \circ 1 \to \to \text{MM'} \equiv \text{R}$

**情况 1** $\text{pair} \And \text{null} \circ 1 \to \to \text{MM'} \equiv \text{R}$

$$
\begin{aligned}
&\text{pair} \And \text{null} \circ 1 \to \to
    \text{R} &\equiv \bar{\phi} &\text{ by def of R} \\
&\text{pair} \And \text{null} \circ 1 \to \to
    \text{MM'} &\equiv \bar{\phi} \\
&\quad \text{since distr} : < \phi, x > &= \phi &\text{ by def of distr}\\
&\qquad \text{and } \alpha f : \phi &= \phi &\text{ by def of Apply to all}
\end{aligned}
$$

> And so: $\alpha \alpha \text{IP} \circ \alpha \text{distl} \circ \text{distr} : < \phi, x > = \phi$.

可见 $\alpha \alpha \text{IP} \circ \alpha \text{distl} \circ \text{distr} : < \phi, x > = \phi$ 。

> Thus $\text{pair} \And \text{null} \circ 1 \to \to \text{MM'} \equiv \text{R}$.

因此 $\text{pair} \And \text{null} \circ 1 \to \to \text{MM'} \equiv \text{R}$ 。

> CASE 2. 
