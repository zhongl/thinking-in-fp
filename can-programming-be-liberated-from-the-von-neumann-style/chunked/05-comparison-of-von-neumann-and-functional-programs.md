> 5. Comparison of von Neumann and Functional Programs 

## 5. 冯·诺伊曼与函数式编程的比较

> To get a more detailed picture of some of the defects of von Neumann languages, let us compare a conventional program for inner product with a functional one written in a simple language to be detailed further on. 

为了更详细地了解冯·诺伊曼语言的缺陷，让我们比较一下传统语言编写的内积程序和一个即将详细讲解的简单函数式语言编写的内积程序。

> 5.1 A von Neumann Program for Inner Product 

### 5.1 冯式内积程序[^von]

[^von]: 冯·诺伊曼式的简称。

```
c := 0
for i := 1 step 1 until n do
    c := c + a[i] x b[i]
```

> Several properties of this program are worth noting: 

这段程序的几个性质总结如下：

> 1. Its statements operate on an invisible "state" according to complex rules. 
> 2. It is not hierarchical. Except for the right side of the assignment statement, it > does not construct complex entities from simpler ones. (Larger programs, however, > often do.) 
> 3. It is dynamic and repetitive. One must mentally execute it to understand it. 
> 4. It computes word-at-a-time by repetition (of the assignment) and by modification (of variable i). 
> 5. Part of the data, n, is in the program; thus it lacks generality and works only for vectors of length n. 
> 6. It names its arguments; it can only be used for vectors a and b. To become general, it requires a procedure declaration. These involve complex issues (e.g., call-by-name versus call-by-value). 
> 7. Its "housekeeping" operations are represented by symbols in scattered places (in the for statement and the subscripts in the assignment). This makes it impossible to consolidate housekeeping operations, the most common of all, into single, powerful, widely useful operators. Thus in programming those operations one must always start again at square one, writing `for i ~ ...` and `for j ~ ...` followed by assignment statements sprinkled with i's and j's.


1. 它的语句遵循复杂规则操作隐式状态[^invi-stat]。
2. 它缺乏层次结构。除了赋值语句的右边部分，程序没有能分解成更小的、可重用的部分，以构建复杂的操作。（大型程序通常会更有层次）
3. 它动态且重复。需要在脑中推演整个过程才能理解其逻辑。
4. 它通过重复（赋值）和修改（变量`i`）来逐字计算。
5. 程序中有数据的部分，`n`， 只能作为向量的长度信息，限制程序的实用性。
6. 它命名的参数，只能使用向量`a`和`b`，要使其变得通用，则需声明过程，这会引入复杂问题（如，是`call-by-name`还是`call-by-value`）。
7. 它那些“收拾”[^hk]操作，以符号形式散落各处（`for`语句里和下标赋值语句里），无法整合为一个通用操作。因而，这样的编程就需要反复使用类似`for i := ...`和`for j := ...`，并伴随满是`i`和`j`相关的赋值语句。

[^invi-stat]: 隐式状态是指`c := c + ...`。
[^hk]: 原文用 Housekeeping，指代处理数据的逻辑操作和步骤。

> 5.2 A Functional Program for Inner Product 

### 5.2 函数式内积程序

$$
\begin{aligned}
  &\text{Def Innerproduct}\\
  &\qquad \equiv (\text{Insert}\ +) \circ (\text{ApplyToAll}\ \times) \circ \text{Transpose} 
\end{aligned}    
$$

> Or, in abbreviated form:

或以缩写形式：

$$
\text{Def IP} \equiv (/ +) \circ (\alpha \times) \circ Trans.
$$

> Composition $(\circ)$, $\text{Insert}\ (/)$, and $\text{ApplyToAll}\ (\alpha)$ are functional forms that combine existing functions to form new ones. Thus $f \circ g$ is the function obtained by applying first $g$ and then $f$, and $\alpha f$ is the function obtained by applying $f$ to every member of the argument. If we write $f:x$ for the result of applying $f$ to the object $x$, then we can explain each step in evaluating Innerproduct applied to the pair of vectors $<<\textit{1, 2, 3}>, <\textit{6, 5, 4}>>$ as follows: 

复合 $(\circ)$， $\text{Insert}\ (/)$ 和 $\text{ApplyToAll}\ (\alpha)$ 都是函数的形式，而函数又可以被组合为新的函数。因而有， $f\circ g$ 代表先应用函数 $g$，后应用函数 $f$ 。 $\alpha f$ 代表函数 $f$ 应用于参数的每个元素。当出现 $f:x$ 则代表对象 $x$ 应用了函数 $f$ 的结果。现在，我们可以逐步解释 $\text{Innerproduct}$ 应用于一对向量 $<<\textit{1, 2, 3}>, <\textit{6, 5, 4}>>$ 计算过程，如下：

$$
\begin{aligned}
    &\text{IP}: <<\textit{1,2,3}>,<\textit{6,5,4}>> && = \\
    &\text{Definition of IP} && \implies (/ +) \circ (\alpha \times) \circ \text{Trans}: <<\textit{1,2,3}>,<\textit{6,5,4}>>\\
    &\text{Effect of composition}, \circ && \implies (/ +) : ((\alpha \times) : (\text{Trans}: <<\textit{1,2,3}>,<\textit{6,5,4}>>))\\
    &\text{Applying Transpose} && \implies (/ +) : ((\alpha \times) : <<\textit{1,6}>,<\textit{2,5}>,<\textit{3,4}>>)\\
    &\text{Effect of ApplyToAll},\alpha && \implies (/+): <\times: <\textit{1,6}>, \times: <\textit{2,5}>, \times: <\textit{3,4}>>\\
    &\text{Applying}\ \times && \implies (/+): <\textit{6,10,12}>\\
    &\text{Effect of Insert},/ && \implies +: <\textit{6},+: <\textit{10,12}>>\\
    &\text{Applying}\ + && \implies +: <\textit{6,22}>\\
    &\text{Applying}\ + \text{again} && \implies \textit{28}
\end{aligned}
$$

> Let us compare the properties of this program with those of the von Neumann program. 

让我们对比一下这两种风格程序的性质。

> 1. It operates only on its arguments. There are no hidden states or complex transition rules. There are only two kinds of rules, one for applying a function to its argument, the other for obtaining the function denoted by a functional form such as composition, $f \circ g$, or $\text{ApplyToAll}$, $\alpha f$, when one knows the functions $f$ and $g$, the parameters of the forms. 
> 2. It is hierarchical, being built from three simpler functions ($+$, $\times$, $\text{Trans}$) and three functional forms $f \circ g$, $\alpha f$, and $/f$. 
> 3. It is static and nonrepetitive, in the sense that its structure is helpful in understanding it without mentally executing it. For example, if one understands the action of the forms $f \circ g$ and $\alpha f$, and of the functions $\times$ and $\text{Trans}$, then one understands the action of $\alpha \times$ and of $(\alpha \times) \circ \text{Trans}$, and so on. 
> 4. It operates on whole conceptual units, not words; it has three steps; no step is repeated. 
> 5. It incorporates no data; it is completely general; it works for any pair of conformable vectors. 
> 6. It does not name its arguments; it can be applied to any pair of vectors without any procedure declaration or complex substitution rules. 
> 7. It employs housekeeping forms and functions that are generally useful in many other programs; in fact, only $+$ and $\times$ are not concerned with housekeeping. These forms and functions can combine with others to create higher level housekeeping operators. 

1. 它只作用于它的参数，没有隐藏状态或复杂转换规则。它只有两种规则，一种是函数应用其参数，另一种是函数可以由其形式获得，如，复合形式 $f \circ g$，或全体应用形式 $\alpha f$，一旦给定 $f$ 和 $g$ 作为其参数形式，即能获得新的函数。
2. 它是分层构建的，三个较小的函数（ $+$、 $\times$ 、 $\text{Trans}$ ），加上三个函数形式 $f \circ g$ 、 $\alpha f$ 、 $/f$。
3. 它是静态且非重复的，意味着其结构易于理解，而无需在脑中推演。比如，只要能够理解 $\alpha f$（全体应用）和 $f \circ g$（复合）形式的作用，便能理解 $\alpha \times$ （全体应用乘法）和 $(\alpha \times) \circ \text{Trans}$ （转置后全体应用乘法）的作用，以此类推。
4. 它操作在完整的概念单元上，而不是字。一共三步，却无一步是重复。
5. 它没有牵扯任何数据，是完全通用的。它可以用于任何一致成对的向量。
6. 它没有命名任何参数，因此可应用于任何成对向量，而无需任何过程声明，或是遵循复杂的替换规则。
7. 它采用“收拾”的函数形式和函数，统统适用于大多其它程序。事实上，只有 $+$ 和 $\times$ 是与“收拾”无关。这些函数形式和函数可以进行其它的组合，以创建更高级的“收拾”。


> Section 14 sketches a kind of system designed to make the above functional style of programming available in a history-sensitive system with a simple framework, but much work remains to be done before the above applicative style can become the basis for elegant and practical programming languages. For the present, the above comparison exhibits a number of serious flaws in von Neumann programming languages and can serve as a starting point in an effort to account for their present fat and flabby condition.

第14节概述了一种系统，旨在将上述函数式编程风格引入到一个具有前序敏感且框架简单的系统中。然而，要使上述应用型风格成为优雅实用编程语言的基础，还有很多工作要做。就目前而言，以上对比揭示了冯·诺伊曼编程语言的一些严重缺陷，可以作为理解其目前臃肿笨拙状态的出发点。
