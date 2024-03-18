> 11. Functional Programming Systems (FP Systems) 

## 11. 函数式编程系统（FP 系统）

> 11.1 Introduction 

### 11.1 介绍

> In this section we give an informal description of a class of simple applicative programming systems called functional programming (FP) systems, in which "programs" are simply functions without variables. The description is followed by some examples and by a discussion of various properties of FP systems. 

这一部分，我们将非正式地描述一类简单应用型编程系统，称为函数式编程（FP）系统，其程序仅仅是没有任何变量的函数。其细节，我们将在 FP 系统的各种性质的讨论和示例中展开。

> An FP system is founded on the use of a fixed set of combining forms called functional forms. These, plus simple definitions, are the only means of building new functions from existing ones; they use no variables or substitution rules, and they become the operations of an associated algebra of programs. All the functions of an FP system are of one type: they map objects into objects and always take a single argument.

FP 系统建立在使用一套固定的组合形式 (combining forms) 之上，这些形式被称为函数形式 (functional forms)。这些函数形式，加上简单的定义，是构建新函数的唯一方法。没有变量或替换规则，它们就是程序代数相关的运算操作。FP 系统中的所有函数都是一种类型：将一个对象映射为另一个对象，并且总是接受单个参数。

> In contrast, a lambda-calculus based system is founded on the use of the lambda expression, with an associated set of substitution rules for variables, for building new functions. The lambda expression (with its substitution rules) is capable of defining all possible computable functions of all possible types and of any number of arguments. This freedom and power has its disadvantages as well as its obvious advantages. It is analogous to the power of unrestricted control statements in conventional languages: with unrestricted freedom comes chaos. If one constantly invents new combining forms to suit the occasion, as one can in the lambda calculus, one will not become familiar with the style or useful properties of the few combining forms that are adequate for all purposes. Just as structured programming eschews many control statements to obtain programs with simpler structure, better properties, and uniform methods for understanding their behavior, so functional programming eschews the lambda expression, substitution, and multiple function types. It thereby achieves programs built with familiar functional forms with known useful properties. These programs are so structured that their behavior can often be understood and proven by mechanical use of algebraic techniques similar to those used in solving high school algebra problems.

与之相对的，lambda 演算的系统，它通过 lambda 表达式（lambda expression）和相关的变量替换规则来构建新函数。lambda 表达式（连同其替换规则）能够定义所有可能的可计算函数，涵盖所有数据类型和参数个数。这种自由度和强大性的缺点与优点同样明显。如同传统语言中不受限制地控制流语句：过度的自由会导致混乱。如果像 lambda 演算那样，为了满足特定情境而不断发明新的组合形式，程序员将无法熟悉少数能够满足所有需求的组合形式的风格或有用特性。就像结构化编程为了获得结构更简单、性质更好、理解行为方法更统一的程序而避免使用许多控制语句一样，函数式编程也摒弃了 lambda 表达式、替换和多函数类型。通过这种方式，它使用具有已知有用性质的熟悉函数形式来构建程序。这些程序的结构使得人们通常可以通过类似于高中代数问题求解的代数技术，机械地理解和证明其行为。

> Functional forms, unlike most programming constructs, need not be chosen on an ad hoc basis. Since they are the operations of an associated algebra, one chooses only those functional forms that not only provide powerful programming constructs, but that also have attractive algebraic properties: one chooses them to maximize the strength and utility of the algebraic laws that relate them to other functional forms of the system. 

函数形式不像大多数编程结构那样，无需临时决定。考虑到它们是相关代数的运算，选择那些既能提供强大编程结构，又具有吸引人的代数性质的函数形式：以最大化与系统其他函数形式相关的代数定律的强度和效用。

> In the following description we shall be imprecise in not distinguishing between (a) a function symbol or expression and (b) the function it denotes. We shall indicate the symbols and expressions used to denote functions by example and usage. Section 13 describes a formal extension of FP systems (FFP systems); they can serve to clarify any ambiguities about FP systems.

接下来的描述中，我们将不区分 (a) 函数符号或表达式和 (b) 它表示的函数之间的区别。根据示例和使用情况，我们应明白用于表示函数的符号和表达式。第 13 节描述了 FP 系统的正式扩展 (FFP 系统)；它们可以用来澄清 FP 系统的任何歧义。

> 11.2 Description

### 11.2 描述

> An FP system comprises the following: 
> 
> 1) a set $\rm O$ of objects; 
> 
> 2) a set $\rm F$ of functions $f$ that map objects into objects; 
> 
> 3) an operation, application; 
> 
> 4) a set $\bf {F}$ of functional forms; these are used to combine existing functions, or objects, to form new functions in $\rm F$ ; 
> 
> 5) a set $\rm D$ of definitions that define some functions in $\rm F$ and assign a name to each. 

一个 FP 系统构成如下：

1. $\rm O$ 代表对象；
2. $\rm F$ 代表函数 $f$ ，能将一类对象映射为另一类对象；
3. 操作，即应用；
4. $\bf F$ 代表函数形式； 用于组合已有的函数，或对象，成新的函数 $\rm F$ ；
5. $\rm D$ 代表定义，用于定义 $\rm F$ 中函数，并为之命名。

> What follows is an informal description of each of the above entities with examples.

接下来，将结合示例对以上内容进行逐一的非正式描述。

> 11.2.1 Objects, $\rm O$. 

#### 11.2.1 对象， $\rm O$

> An object $x$ is either an atom, a sequence $< x_1, \dots, x_n >$ whose elements $x_i$ are objects, or $\bot$ ("bottom" or "undefined"). Thus the choice of a set $\rm A$ of atoms determines the set of objects. We shall take $\rm A$ to be the set of nonnull strings of capital letters, digits, and special symbols not used by the notation of the FP system. Some of these strings belong to the class of atoms called "numbers." The atom $\phi$ is used to denote the empty sequence and is the only object which is both an atom and a sequence. The atoms $\it T$ and $\it F$ are used to denote "true" and "false." 

一个对象 $x$ 只能是以下三种类型中的一种：

1. 原子（atom）；
2. 序列（sequence）， $< x_1, \dots, x_n >$  ，其中的元素 $x_i$ 都是对象；
3. $\bot$ ， 底部（bottom）或未定义（undefined）。

因此，由 $\rm A$ 代表的原子的选择，决定了对象的集合。我们将 $\rm A$ 视作一组非空字符串，这些字符串可以包含大写字母、数字以及 FP 系统本身的记法中没有使用的特殊符号。部分字符串属于称为 "数字" 的原子类型。空序列记为 $\phi$  ，它是唯一既是原子又是序列的对象。原子 $\it T$ 和 $\it F$ 分别用于表示 “true” 和 “false”。

> There is one important constraint in the construction of objects: if $x$ is a sequence with $\bot$ as an element, then $x = \bot$ . That is, the "sequence constructor" is " $\bot$ -preserving." Thus no proper sequence has $\bot$ as an element.

构建对象时存在一个重要限制：如果序列 $x$ 中包含元素 $\bot$ ，则意味着 $x = \bot$ 。换句话说，序列的构造是“ $\bot$ 保留”的。因此，任何有效的序列都不可能包含元素 $\bot$ 。

> Examples of objects 

对象的例子

$$
\begin{aligned}
  \bot\quad \textit{1.5}\quad \phi\quad \textit{AB3}\quad &< AB,\ \textit{1},\ \textit{2.3} >\\
  < A, < < B >, C >, D >\ &< A,\ \bot > = \bot
\end{aligned}
$$

> 11.2.2 Application

#### 11.2.2 应用

> An FP system has a single operation, application. If $f$ is a function and $x$ is an object, then $f:x$ is an application and denotes the object which is the result of applying $f$ to $x$ . $f$ is the operator of the application and $x$ is the operand. 

FP 系统只有一个运算，称为应用 （application）。如果 $f$ 是一个函数， $x$ 是一个对象，那么 $f:x$ 表示应用运算，它表示将函数 $f$ 作用于对象 $x$ 的结果。其中， $f$ 是应用运算的运算符 （operator）， $x$ 是操作数 （operand）。


> Examples of applications

应用的例子

$$
\begin{aligned}
+:< \textit{1},\ \textit{2} > &= \textit{3} &tl:< A, B, C > &= < B, C >\\
1:< A, B, C > &= A &2:< A, B, C > &= B    
\end{aligned}
$$

> 11.2.3 Function, $\rm F$

#### 11.2.3 函数， $\rm F$

> All functions $f$ in $\rm F$ map objects into objects and are *bottom-preserving*: $f:\bot = \bot$ , for all $f$ in $\rm F$ . Every function in $\rm F$ is either *primitive*, that is, supplied with the system, or it is *defined* (see below), or it is a *functional form* (see below).

所有函数 $f$ 都属于集合 $\rm F$ ，它们将对象映射为对象，并且都满足*底部保留*：对于集合 $\rm F$ 中的任何函数 $f$ ，都成立 $f:\bot = \bot$ 。 $\rm F$ 里的每个函数只可能是 *原生函数*（primitive），由系统直接提供；或是，*定义函数* （defined）；再就是，函数形式（functional form）。

> It is sometimes useful to distinguish between two cases in which $f:x = \bot$ . If the computation for $f:x$ terminates and yields the object $\bot$ , we say $f$ is *undefined* at $x$ , that is, $f$ terminates but has no meaningful value at $x$ . Otherwise we say $f$ is *nonterminating* at $x$ .

在某些情况下，区分函数应用 $f:x = \bot$ 的两种情形会比较有用：

- 如果对函数 $f$ 施加对象 $x$ 的运算会终止并得到结果 $\bot$ ，那么称函数 $f$ 在输入 $x$ 时是 *未定义的*。也就是说，函数运算虽然会终止，但是在输入 $x$ 的情况下没有产生有意义的值。
- 另一种情况，我们称函数 $f$ 在输入 $x$ 时是 *非终止的*（nonterminating）。

> Examples of primitive functions

原生函数的例子

> Our intention is to provide FP systems with widely useful and powerful primitive functions rather than weak ones that could then be used to define useful ones. The following examples define some typical primitive functions, many of which are used in later examples of programs. In the following definitions we use a variant of McCarthy's conditional expressions [^17]; thus we write 

我们打算为 FP 系统提供广泛实用且强大的基本函数，而不是一些较弱的函数让用户再去定义更强大的函数。以下示例定义了一些典型的基本函数，它们中的许多将在后面的程序示例中用到。下面的定义使用了一种 McCarthy 条件表达式的变体 [^17]，因此我们将

[^17]: TODO

$$
p_1 \to e_1; \dots; p_n \to e_n; e_{n+1}
$$

> instead of McCarthy's expression

代替 McCarthy 表达式

$$
(p_1 \to e_1; \dots; p_n \to e_n; T \to e_{n+1})
$$

> The following definitions are to hold for all objects $x , x_i , y , y_i , z , z_i$ : 

下面的定义将包括对象 $x , x_i , y , y_i , z , z_i$ ：

**Selection functions**

$$
\text{1} : x \equiv x = < x_1, \dots , x_n >\ \to \ x_1; \bot
$$

> and for any positive integer $\text{s}$

对任何正整数 $\text{s}$ 有

$$
\text{s} : x \equiv x = < x_1, \dots , x_n > \And\ n \ge s\ \to\ x_s; \bot 
$$

> Thus, for example, $\text{3} :< A,B,C > = C$ and $\text{2} : < A > = \bot$ . Note that the function symbols $\text{1}$ , $\text{2}$ , etc. are distinct from the atoms $\it 1$ , $\it 2$ , etc

由此可得， $\text{3} :< A,B,C > = C$ 和 $\text{2} : < A > = \bot$ 。注意，函数符号 $\text{1}$ 、 $\text{2}$ 等，是有别于原子 $\it 1$ 、 $\it 2$ 等

**Tail**

$$
\begin{aligned}
  \text{tl} : x \equiv x &= < x_1 >\ &&\to \phi;\\
                       x &= < x_1, \dots , x_n > \And\ n \ge \textit{2} &&\to < x_2, \dots , x_n >;
                       \bot   
\end{aligned}
$$

**Identity**

$$
\text{id} : x \equiv x
$$

**Atom**

$$
\text{atom} : x \equiv x\ \text{is an atom} \to T;
                       x \not = \bot \to F;
                       \bot
$$

**Equals**

$$
\text{eq} : x \equiv x = < y, z > \And\ y = z \to T;
              x = < y, z > \And\ y \not = z \to F;
              \bot
$$

**Null**

$$
\text{null} : x \equiv x = \phi \to T;
                       x \not = \bot \to F;
                       \bot
$$

**Reverse**

$$
\begin{aligned}
  \text{reverse} : x \equiv x &= \phi &&\to \phi ;\\
                            x &= < x_1, \dots, x_n > &&\to < x_n, \dots, x_1 > ;
                            \bot
\end{aligned}
$$

**Distribute from left; distribute from right**

$$
\begin{aligned}
  \text{distl} : x \equiv x &= < y, \phi > &&\to \phi;\\
                          x &= < y, < z_1, \dots, z_n > > &&\to < < y, z_1 >, \dots, < y, z_n > >;
                          \bot\\
  \text{distr} : x \equiv x &= < \phi, y > &&\to \phi;\\
                          x &= < < y_1, \dots, y_n >, z > &&\to < < y_1, z >, \dots, < y_n, z > >;
                          \bot
\end{aligned}
$$

**Length**

$$
\text{length} : x \equiv x = < x_1, \dots, x_n >\ \to\ n;
                  x = \phi \to \textit{0};
                  \bot
$$

**Add, substract, multiply, and divide**

$$
\begin{aligned}    
  +: x \equiv x = < y, z > \And\ y,z\ \text{are numbers} \to\ y + z; \bot \\
  -: x \equiv x = < y, z > \And\ y,z\ \text{are numbers} \to\ y - z; \bot \\
  \times : x \equiv x = < y, z > \And\ y,z\ \text{are numbers} \to\ y \times z; \bot \\
  \div : x \equiv x = < y, z > \And\ y,z\ \text{are numbers} \to\ y \div z; \bot \\
  (\text{where}\ y \div \textit{0} = \bot)
\end{aligned}
$$

**Transpose**

$$
\begin{aligned}
  \text{trans} : x \equiv x &= < \phi, \dots, \phi>\ &&\to \phi;\\
                          x &= < x_1, \dots, x_n >\ &&\to < y_1, \dots, y_m>;\bot\\
  \text{where}\\
                        x_i &= < x_{i1}, \dots, x_{im} > &&\text{and}\\
                        y_j &= < x_{1j}, \dots, x_{nj} > &&, \textit{1} \le i \le n, 1 \le j \le m.                      
\end{aligned}
$$

**And, or, not**

$$
\begin{aligned}
  \text{and} : x \equiv x &= < T, T >\ &\to& T;\\
                        x &= < T, F > \lor\ x = < F, T > \lor\ x = < F, F > \ &\to& F;
                        \bot\\
  \text{etc.}
\end{aligned}
$$

**Append left; append right**

$$
\begin{aligned}
  \text{apndl} : x \equiv x &= < y, \phi >\ &\to& < y >;\\
                          x &= < y, < z_1, \dots, z_n > >\ &\to& < y, z_1, \dots, z_n >;\bot\\   
  \text{apndr} : x \equiv x &= < \phi, z >\ &\to& < z >;\\
                          x &= < < y_1, \dots, y_n >, z >\ &\to& < y_1, \dots, y_n, z >;\bot\\   
\end{aligned}
$$

**Right selector; Right tail**

$$
\begin{aligned}
  \text{1r} : x \equiv x &= < x_1, \dots, x_n > &&\to\ x_n;\bot\\  
  \text{2r} : x \equiv x &= < x_1, \dots, x_n > \And\ n \ge \textit{2} \ &&\to\ x_{n-1};\bot\\  
  \text{etc.} \\
  \text{tlr} : x \equiv x &= < x_1 >\ &&\to \phi;\\
                         x &= < x_1, \dots, x_n > \And\ n \ge \textit{2} \ &&\to < x_1, \dots, x_{n-1} >;\bot
\end{aligned}
$$

**Rotate left; rotate right**

$$
\begin{aligned}
  \text{rotl} : x \equiv x &= \phi &&\to \phi;\\
                         x &= < x_1 > &&\to < x_1 >;\\
                         x &= < x_1, \dots, x_n > \And\ n \ge \textit{2} \ &&\to < x_2, \dots, x_n, x_1 >;\bot\\
  \text{etc.}                          
\end{aligned}
$$

> 11.2.4 Functional forms, $\bf F$

#### 11.2.4 函数形式， $\bf F$

> A functional form is an expression denoting a function; that function depends on the functions or objects which are the parameters of the expression. Thus, for example, if $f$ and $g$ are any functions, then $f \circ g$ is a functional form, the composition of $f$ and $g$, $f$ and $g$ are its parameters, and it denotes the function such that, for any object $x$ ,

函数形式是关于函数的表达式，即函数依赖作为表达式参数的其他函数或对象。比如，对任意函数 $f$ 和 $g$ ，则 $f \circ g$ 就是一种函数形式，表示对参数 $f$ 和 $g$ 的复合应用。这样的函数对任意对象 $x$ 而言，都满足：

$$
(f \circ g) : x = f : (g : x)
$$

> Some functional forms may have objects as parameters. For example, for any object $x$ , $\={x}$ is a functional form, the *constant* function of $x$ , so that for any object $y$ 

有一些函数形式会有对象做参数。比如，对任意对象 $x$ ， $\bar{x}$ 则是一个关于 $x$ 的*常量*函数的形式，因此对于任意对象 $y$ 而言， 都满足：

$$
\bar{x} : y \equiv y = \bot \to \bot;x.
$$

> In particular, $\=\bot$ is the everywhere- $\bot$ , function.

一个特例是， $\=\bot$ 是始终返回 $\bot$ 的函数。

> Below we give some functional forms, many of which are used later in this paper. We use $p$ , $f$ , and $g$ with and without subscfipts to denote arbitrary functions; and $x, x_1, \dots x_n, y$ as arbitrary objects. Square brackets $[ \dots ]$ are used to indicate the functional form for construction, which denotes a function, whereas pointed brackets $< \dots >$ denote sequences, which are objects. Parentheses are used both in particular functional forms (e.g., in *condition*) and generally to indicate grouping. 

以下提到的一些函数形式，大都会在后文用到。像 $p$ ， $f$ 和 $g$ 无论是否带下标，都表示任何函数。 $x, x_1, \dots x_n, y$ 表示任意对象。方括号 $[ \dots ]$ 表示构造型的函数形式， 其中都是函数。尖括号 $< \dots >$ 表示序列，其中是对象。圆括号既表示特定的函数形式（例如在条件表达式中），也可以表示分组。

**Composition**

$$
(f \circ g) : x \equiv f : (g : x)
$$

**Construction**

$$
[ f_1, \dots, f_n ] : x \equiv < f_1 : x, \dots, f_n : x >
$$

> (Recall that since $< \dots, \bot, \dots >\ = \bot$ and all functions are $\bot$-preserving, so is $[ f_1, \dots, f_n ]$.) 

正如前文有 $< \dots, \bot, \dots >\ = \bot$ ，同样适用于 $[ f_1, \dots, f_n ]$ 。

**Condition**

$$
\begin{aligned}    
(p \to f; g) : x \equiv\ (p : x) &= T \to f : x;\\
                         (p : x) &= F \to g : x;\bot 
\end{aligned}
$$

> Conditional expressions (used outside of FP systems to describe their functions) and the functional form condition are both identified by " $\to$ ". They are quite different although closely related, as shown in the above definitions. But no confusion should arise, since the elements of a conditional expression all denote values, whereas the elements of the functional form condition all denote functions, never values. When no ambiguity arises we omit right-associated parentheses; we write, for example, $p_1 \to f_1; p_2 \to f_2;g$ for $(p_1 \to f_1; (p_2 \to f_2;g))$.

条件表达式 (用在 FP 系统之外描述其函数) 和函数形式条件都用符号 “ $\to$ ” 表示，虽然密切相关，但从以上定义来看有很大区别 。不要混淆彼此，条件表达式里的元素都是某个值，而函数形式条件中的元素则是某个函数。当不会引起歧义时，可以省略向右关联（right-associated）的括号来简化表示， 如： $p_1 \to f_1; p_2 \to f_2;g$ 是 $(p_1 \to f_1; (p_2 \to f_2;g))$ 的简化表示。

**Constant** 

> (Here $x$ is an object parameter.)

（这里的 $x$ 是一个对象参数。）

$$
\bar{x} : y \equiv y = \bot \to \bot ; x
$$

**Insert**

$$
\begin{aligned}
  /f : x \equiv x &= < x_1 > &&\to x_1 ;\\
                x &= < x_1, \dots, x_n > \And\ n \ge \textit{2} && \to f : < x_1, /f : < x_2, \dots, x_n > > ;\bot
\end{aligned}
$$

> If $f$ has a unique right unit $u_f \not = \bot$ , where $f : < x, u_f >\ \in \set{ x, \bot }$ for all objects $x$ , then the above definition is extended: $/f : \phi = u_f$ . Thus 

当函数 $f$ 存在唯一的右单元（right unit）满足 $u_f \not = \bot$ [^ru]， 且对所有对象 $x$ 满足 $f : < x, u_f >\ \in \set{ x, \bot }$ ，由此可得  $/f : \phi = u_f$ 。具体来说：

$$
\begin{aligned}
&/+ : < \textit{4, 5, 6} > 
  &=&\ + : < \textit{4}, + : < \textit{5}, /+ : < \textit{6} > > > \\
 &&=&\ + : < \textit{4}, + : < \textit{5, 6} > > \\
 &&=&\ + : < \textit{4, 11} > \\ 
 &&=&\ \textit{15} \\
&/+ : \phi = \textit{0}                 
\end{aligned}
$$

[^ru]: TODO

**Apply to all**

$$
\begin{aligned}
\alpha f : x \equiv x &= \phi &&\to \phi; \\
                    x &= < x_1, \dots, x_n > &&\to < f : x_1, \dots, f : x_n >;
                    \bot
\end{aligned}
$$

**Binary to unary**

>( $x$ is an object parameter )

（ $x$ 是一个对象参数 ）

$$
(\text{bu}\ f\ x) : y \equiv f : < x, y >
$$

> Thus

可得

$$
(\text{bu}\ +\ \textit{1}) : x = \textit{1} + x
$$

**While**

$$
\begin{aligned}
  (\text{while}\ p\ f) : x \equiv p : x &= T \to (\text{while}\ p\ f) : (f : x);\\
                                  p : x &= F \to x;
                                  \bot     
\end{aligned}
$$

> The above functional forms provide an effective method for computing the values of the functions they denote (if they terminate) provided one can effectively apply their function parameters.

一个函数能有效的应用其函数参数（且能终止的话），以上函数形式就能提供了一种高效的方法去计算它们。

> 11.2.5 Definitions

#### 11.2.5 定义

> A *definition* in an FP system is an expression of the form

在 FP 系统里，*定义* 是如下形式的表达式

$$
\textbf{Def}\ l \equiv r
$$

> where the left side $l$ is an unused function symbol and the right side $r$ is a functional form (which may depend on $l$ ). It expresses the fact that the symbol $l$ is to denote the function given by $r$ . Thus the definition $\textbf{Def}\ \text{last1} \equiv 1 \circ reverse$ defines the function $\text{last1}$ that produces the last element of a sequence (or $\bot$ ). Similarly, 

左边的 $l$ 是没有用过的函数符号，右边的 $r$ 是函数形式（它可能依赖 $l$ ）。它表达了符号 $l$ 就是由 $r$ 给定的函数。因此，定义 $\textbf{Def}\ \text{last1} \equiv 1 \circ reverse$ [^1f]的意思是，函数 $\text{last1}$ 可以获得一个序列的最后一个元素（或 $\bot$ ）。类似的

$$
\textbf{Def}\ \text{last} \equiv \text{null} \circ \text{tl} \to 1; \text{last} \circ \text{tl}
$$

[^1f]: 这里的 `1` 容易被直觉混淆视听，它不是数值，而是获取第一个元素的选择函数。

> defines the function $\text{last}$, which is the same as $\text{last1}$ . Here in detail is how the definition would be used to compute $\text{last} : < \textit{1, 2} >$ : 

函数 $\text{last}$ 和 $\text{last1}$ 其实是等价的。下面就来看看 $\text{last} : < \textit{1, 2} >$ 的计算过程：

$$
\begin{aligned}
&\text{last} : < \textit{1, 2} >\\
&\text{definition of last }             &\implies& (\text{null} \circ \text{tl} \to 1; \text{last} \circ \text{tl}) : < \textit{1, 2} >\\
&\text{action of the form } (p \to f;g) &\implies& \text{last} \circ \text{tl} : < \textit{1, 2} > \\
&                                       &&\text{since } \text{null} \circ \text{tl} : < \textit{1, 2} > = \text{null} : < \textit{2} > = F\\
&\text{action of the form } f \circ g   &\implies& \text{last} : (\text{tl} : < \textit{1, 2} >)\\
&\text{definition of primitive tail }   &\implies& \text{last} : < \textit{2} >\\
&\text{definition of last }             &\implies& (\text{null} \circ \text{tl} \to 1; \text{last} \circ \text{tl}) : < \textit{2} >\\
&\text{action of the form } (p \to f;g) &\implies& 1 : < \textit{1, 2} >\\
&                                       &&\text{since } \text{null} \circ \text{tl} : < \textit{2} > = \text{null} : \phi = T\\
&\text{definition of selector } 1       &\implies& \textit{2}
\end{aligned}
$$

> The above illustrates the simple rule: to apply a defined symbol, replace it by the right side of its definition. Of course, some definitions may define nonterminating functions. A set $\rm D$ of definitions is well formed if no two left sides are the same. 

上面很好的呈现一条简单的规则，就是将一个定义的符号，替换为定义在它右侧的内容。当然，会有一些定义是非终止的函数。一组良好的定义集是不会有左侧符号相同的存在的。

> 11.2.6 Semantics

#### 11.2.6 语义

> It can be seen from the above that an FP system is determined by choice of the following sets: (a) The set of atoms $\rm A$ (which determines the set of objects). (b) The set of primitive functions $\rm P$ . (c) The set of functional forms $\bf F$ . (d) A well formed set of definitions $\rm D$ . To understand the semantics of such a system one needs to know how to compute $f:x$ for any function $f$ and any object $x$ of the system. There are exactly four possibilities for $f$ : 

基于以上内容可以看出，FP 系统是由以下的几组合集的选择决定：

1. 一组原子的集合 $\rm A$ （也就是一组对象的集合）；
2. 一组原生函数的集合 $\rm P$ ；
3. 一组函数形式的集合 $\bf F$ ；
4. 一组良好定义的集合 $\rm D$ 。
   
要想理解这样一个系统的语义，就必须弄明白对于任意函数 $f$ 和任意对象 $x$ 而言， $f:x$ 是如何计算。 对 $f$ 来说，只有以下四种可能：

> (1) $f$ is a primitive function;
>  
> (2) $f$ is a functional form; 
> 
> (3) there is one definition in $\rm D$ , $\textbf{Def } f \equiv r$ ; and 
> 
> (4) none of the above. 

1. $f$ 是原生函数；
2. $f$ 是函数形式；
3. 存在一种定义 $\rm D$ , $\textbf{Def } f \equiv r$ ；以及
4. 以上均不是。

> If $f$ is a primitive function, then one has its description and knows how to apply it. If $f$ is a functional form, then the description of the form tells how to compute $f:x$ in terms of the parameters of the form, which can be done by further use of these rules. If $f$ is defined, $\textbf{Def } f \equiv r$ , as in (3), then to find $f:x$ one computes $r:x$ , which can be done by further use of these rules. If none of these, then $f:x \equiv \bot$ . Of course, the use of these rules may not terminate for some $f$ and some $x$ , in which case we assign the value $f:x \equiv \bot$ .

1. 若 $f$ 是原生函数，则根据描述应用它；
2. 若 $f$ 是函数形式，则形式的描述交代了如何通过其型参来运算 $f:x$ ，再进一步运用以上规则；
3. 若 $f$ 是 $\textbf{Def } f \equiv r$ ，则将 $f:x$ 以 $r:x$ 进行运算，再进一步运用以上规则；
4. 以上均不是，则表示为 $f:x \equiv \bot$ 。当然，在对一些 $f$ 和 $x$ 应用本规则无法停止时，同样表示为 $f:x \equiv \bot$ 。

> 11.3 Examples of Functional Programs

### 11.3 函数式程序的例子

> The following examples illustrate the functional programming style. Since this style is unfamiliar to most readers, it may cause confusion at first; the important point to remember is that no part of a function definition is a result itself. Instead, each part is a function that must be applied to an argument to obtain a result. 

以下例子很好的说明了函数式编程风格。考虑到这种风格对大多数读者很陌生，一开始会感到困惑。不要紧，只要记住一点，函数定义的任何部分不能是结果本身。换言之，函数的每一个部分都必须对其参数应用且获得一个结果。

> 11.3.1 Factorial

#### 11.3.1 阶乘

$$
\begin{aligned}
  &\textbf{Def } \text{!}    &\equiv&\ \text{eq0} \to \bar{1}; \times \circ [ \text{id}, \text{!} \circ \text{sub1} ]\\
  &\text{where}\\
  &\textbf{Def } \text{eq0}  &\equiv&\ \text{eq} \circ [ \text{id}, \bar{0} ]\\
  &\textbf{Def } \text{sub1} &\equiv&\ - \circ\ [ \text{id}, \bar{1} ]
\end{aligned}
$$

> Here are some of the intermediate expressions an FP system would obtain in evaluating $\text{!} : \textit{2}$:

让我们来以 $\text{!} : \textit{2}$ 为例，推导一下中间的过程[^fac]：

$$
\begin{aligned}
  \text{!} : \textit{2} 
  &\implies (\text{eq0} \to \bar{1}; \times \circ [ \text{id}, \text{!} \circ \text{sub1} ]) : \textit{2}\\
  &\implies \times \circ [ \text{id}, \text{!} \circ \text{sub1} ] : \textit{2}\\
  &\implies \times : < \text{id} : \textit{2}, \text{!} \circ \text{sub1} : \textit{2} >\\
  &\implies \times : < \textit{2}, \text{!} : \textit{1} >\\
  &\implies \times : < \textit{2}, \times : < \textit{1}, \text{!} : \textit{0} > >\\
  &\implies \times : < \textit{2}, \times : < \textit{1}, \bar{1} : 0 > >\\   
  &\implies \times : < \textit{2}, \times : < \textit{1}, \textit{1} > >\\   
  &\implies \times : < \textit{2}, \textit{1} >\\   
  &\implies \textit{2}.
\end{aligned}
$$

[^fac]: 中间过程译者做了一些重新排版和修订，与原文有所出入。

> In Section 12 we shall see how theorems of the algebra of FP programs can be used to prove that $\text{!}$ is the factorial function. 

在第 12 节里，我们会看到如何用 FP 程序的代数定理来证明 $\text{!}$ 是阶乘函数。

> 11.3.2 Inner product

#### 11.3.2 内积

> We have seen earlier how this definition works. 

其实前面已经定义过了。

$$
\textbf{Def } \text{IP} \equiv (/ +) \circ (\alpha \times) \circ \text{trans}
$$

> 11.3.3 Matrix multiply

#### 11.3.3 矩阵乘法

> This matrix multiplication program yields the product of any pair $< m, n >$ of conformable matrices, where each matrix $m$ is represented as the sequence of its rows: 

这个矩阵乘法的程序可求得任何满足 $< m, n >$ 矩阵积[^mm]。其中，每个矩阵的 $m$ 表示其行的序列：

[^mm]: 对矩阵乘法不熟悉的，请结合[这里](https://zh.wikipedia.org/wiki/%E7%9F%A9%E9%99%A3%E4%B9%98%E6%B3%95)一起理解。

$$
\begin{aligned}
  &m = < m_1, \dots, m_r > \\
  &\qquad \text{where } m_i = < m_{i1}, \dots, m_{is}> \text{for } i = \textit{1}, \dots, r.\\
  &\textbf{Def } \text{MM} \equiv (\alpha \alpha \text{IP}) \circ (\alpha \text{distl}) \circ \text{distr} \circ [ 1, \text{trans} \circ 2 ]
\end{aligned}
$$

> The program $\text{MM}$ has four steps, reading from right to left; each is applied in turn, beginning with $[ 1, \text{trans} \circ 2 ]$ , to the result of its predecessor. 
> If the argument is $< m,n >$, then the first step yields $< m, n' > \text{where } n' = \text{trans}:n$. 
> The second step yields $< < m_1, n' >, ..., < m_r, n' > >$, where the $m_i$ are the rows of $m$. 
> The third step, $\alpha \text{distl}$ , yields $< \text{distl} : < m_1, n' >, \dots, \text{distl} : < m_r, n' > > = < p_1, \dots, p_r >$ where $p_i = \text{distl} : < m_1, n' > = < < m_i, n_1' >, \dots, < m_i, n_s' > > \text{for } i = \textit{1}, \dots, r$ and $n_j'$ is the jth column of $n$ ( the jth row of $n'$ ). Thus $p_i$, a sequence of row and column pairs, corresponds to the i-th product row. 
> The operator $\alpha \alpha \text{IP}$ , or $\alpha (\alpha \text{IP})$ , causes $\alpha \text{IP}$ to be applied to each $p_i$ , which in turn causes $\text{IP}$ to be applied to each row and column pair in each $p_i$ . The result of the last step is therefore the sequence of rows comprising the product matrix. 
> If either matrix is not rectangular, or if the length of a row of $m$ differs from that of a column of $n$, or if any element of $m$ or $n$ is not a number, the result is $\bot$ .

$\text{MM}$ 程序有四个步骤，从右往左，以此执行。从 $[ 1, \text{trans} \circ 2 ]$ 开始，得到最初的结果。当参数满足 $< m,n >$ ，则

1. 执行第一步得到 $< m, n' > \text{where } n' = \text{trans}:n$ ；
2. 执行第二步得到 $< < m_1, n' >, ..., < m_r, n' > >$ ， 其中 $m_i$ 是矩阵 $m$ 的一行；
3. 执行第三步， $\alpha \text{distl}$ ，得到 $< \text{distl} : < m_1, n' >, \dots, \text{distl} : < m_r, n' > > = < p_1, \dots, p_r >$ ，其中 $p_i = \text{distl} : < m_1, n' > = < < m_i, n_1' >, \dots, < m_i, n_s' > > \text{for } i = \textit{1}, \dots, r$ ， 且 $n_j'$ 是 $n$ 的第 $j$ 列（也就是 $n'$ 的第 $j$ 行）。 $p_i$ 则是行列对序列对应的第 $i$ 个行积；
4. 最后一步， $\alpha \alpha \text{IP}$ ，或是 $\alpha (\alpha \text{IP})$ ， 即对每个 $p_i$ 应用 $\alpha \text{IP}$ ，也就是对每个 $p_i$ 的行列对应用 $\text{IP}$ 。这样一个由行序列构成其结果就是矩阵积。

如果矩阵不是矩形，又或是 $m$ 的行数对不上 $n$ 的列数，还是二者的任意元素不是数字，其结果都是 $\bot$ 。

> This program $\text{MM}$ does not name its arguments or any intermediate results; contains no variables, no loops, no control statements nor procedure declarations; has no initialization instructions; is not word-at-a-time in nature; is hierarchically constructed from simpler components; uses generally applicable housekeeping forms and operators (e.g., $\alpha f, \text{distl}, \text{distr}, \text{trans}$ ); is perfectly general; yields $\bot$ whenever its argument is inappropriate in any way; does not constrain the order of evaluation unnecessarily (all applications of $\text{IP}$ to row and column pairs can be done in parallel or in any order); and, using algebraic laws (see below), can be transformed into more "efficient" or into more "explanatory" programs (e.g., one that is recursively defined). None of these properties hold for the typical von Neumann matrix multiplication program.

程序 $\text{MM}$ ，没有命名参数，或任何中间结果；它不包含变量，循环，控制语句，以及任何过程声明；它没有初始化指令，甚至天然不是逐字处理的；它由各种小组件有层次的构建而成，像是通用的“收拾”（housekeeping）组合形式和操作（比如， $\alpha f, \text{distl}, \text{distr}, \text{trans}$ ），适用性极强；即便在任何时候，面对任何可能的不恰当的参数，它都会得到 $\bot$ 。它不要求必须按顺序执行（对所有行列对应用 $\text{IP}$ 完全可以是平行或其它任意顺序），并且依据代数定律（见后文）可将其替换成更“高效”，或更“清晰”版本（例如，一个递归风格的版本）。相反，这些性质是一个典型的冯·诺伊曼式矩阵乘法程序所不具备的。

> Although it has an unfamiliar and hence puzzling form, the program $\text{MM}$ describes the essential operations of matrix multiplication without overdetermining the process or obscuring parts of it, as most programs do; hence many straightforward programs for the operation can be obtained from it by formal transformations. It is an inherently inefficient program for von Neumann computers (with regard to the use of space), but efficient ones can be derived from it and realizations of FP systems can be imagined that could execute MM without the prodigal use of space it implies. Efficiency questions are beyond the scope of this paper; let me suggest only that since the language is so simple and does not dictate any binding of lambda-type variables to data, there may be better opportunities for the system to do some kind of "lazy" evaluation [^9] [^10] and to control data management more efficiently than is possible in lambda-calculus based systems.

虽然程序 $\text{MM}$ 的形式可能看起来陌生让人费解，但它却清晰地描述了矩阵乘法的核心运算。不像大多数程序那样，过度限定计算过程或隐藏细节。由此可见，通过形式化变换可以得到许多简洁的程序。虽然，在冯诺依曼计算机上运行时，其效率天生低下，因为它会占用大量的空间；但是，我们可以从中推导高效的版本，可以想象一些 FP 系统的实现能够高效执行，并像程序本身那样浪费空间。关于效率的问题超出了本文的讨论范围，但我必须指出，函数式编程语言如此简单，且避免了 lambda 类型变量和数据的绑定关系，可能为系统带来一些优势。比如，可以采用某种形式的惰性求值 (lazy evaluation) [^9] [^10] ，以及更有效的数据管理，而这些是基于 lambda 演算的系统可能难以实现。

[^9]: TODO
[^10]: TODO

> 11.4 Remarks About FP Systems

### 11.4 FP 系统小结

> 11.4.1 FP systems as programming languages

#### 11.4.1 FP 系统的编程语言

> FP systems are so minimal that some readers may find it difficult to view them as programming languages. Viewed as such, a function $f$ is a program, an object $x$ is the contents of the store, and $f:x$ is the contents of the store after program $f$ is activated with $x$ in the store. The set of definitions is the program library. The primitive functions and the functional forms provided by the system are the basic statements of a particular programming language. Thus, depending on the choice of primitive functions and functional forms, the FP framework provides for a large class of languages with various styles and capabilities. The algebra of programs associated with each of these depends on its particular set of functional forms. The primitive functions, functional forms, and programs given in this paper comprise an effort to develop just one of these possible styles.

对一些读者来说，FP 系统的极简设计可能令人难以将其视为一种编程语言。我们不妨这样来看：

- 函数 $f$ 是一个程序；
- 对象 $x$ 是存储器中的内容；
- $f:x$ 是给定 $x$ 的情况下，执行程序 $f$ 之后得到的存储器中的新内容；
- 定义的集合相当于程序库；
- 系统提供的原生函数和函数形式相当于特定编程语言的基本语句。

因此，通过选择不同的基本函数和函数形式，FP 框架可以支持种类繁多、风格各异的编程语言。每个框架所关联的程序代数都取决于其特定的函数形式集合。本文提供的基本函数、函数形式和程序示例，只是尝试开发其中的一种风格。

> 11.4.2 Limitations of FP systems

#### 11.4.2 FP 系统的局限

> FP systems have a number of limitations. For example, a given FP system is a fixed language; it is not history sensitive: no program can alter the library of programs. It can treat input and output only in the sense that $x$ is an input and $f:x$ is the output. If the set of primitive functions and functional forms is weak, it may not be able to express every computable function.

FP 系统是由一些限制的。例如：一旦定义了 FP 系统，它就变成一种固定语言；不具备前序敏感性；程序本身无法修改程序库的内容。FP 系统只能将初始状态视为输入（记为 $x$ ），将计算结果视为输出（记为 $f:x$ ）。如果 FP 系统提供的基本函数和函数形式不够强大，那么它就可能无法表达所有可计算的函数。
 
> An FP system cannot compute a program since function expressions are not objects. Nor can one define new functional forms within an FP system. (Both of these limitations are removed in formal functional programming (FFP) systems in which objects "represent" functions.) Thus no FP system can have a function, $\text{apply}$ , such that 

FP 系统无法计算程序本身，因为函数表达式并不是对象。也不能在系统内定义新的函数形式。（形式函数编程 (FFP) 系统移除了这两个限制，其中对象可以 “表示” 函数。）为此，没有 FP 系统可以使得函数 $\text{apply}$ 满足

$$
\text{apply} : < x, y > \equiv x : y
$$

> because, on the left, $x$ is an object, and, on the right, $x$ is a function. (Note that we have been careful to keep the set of function symbols and the set of objects distinct: thus $1$ is a function symbol, and $\it 1$ is an object.)

这是因为等式左侧的 $x$ 是一个对象，而右侧的 $x$ 却是一个函数。（注意，我们是严格区分了函数符号和对象集合的，因此 $1$ 是一个函数符号，而 $\it 1$ 是一个对象。）

> The primary limitation of FP systems is that they are not history sensitive. Therefore they must be extended somehow before they can become practically useful. For discussion of such extensions, see the sections on FFP and AST systems (Sections 13 and 14).

FP 系统最主要的局限还是做不到前序敏感。如果想要让 FP 系统更具实用性，就需要进行扩展。文中提到了两种扩展方案，分别是 FFP 和 AST（参见第 13 和 14 节）。


> 11.4.3 Expressive power of FP systems

#### 11.4.3 FP 系统的表达力

> Suppose two FP systems, FP1 and FP2, both have the same set of objects and the same set of primitive functions, but the set of functional forms of FP1 properly includes that of FP2. Suppose also that both systems cart express all computable functions on objects. Nevertheless, we can say that FP1 is more expressive than FP2, since every function expression in FP2 can be duplicated in FP1, but by using a functional form not belonging to FP2, FP1 can express some functions more directly and easily than FP2. 

假设 FP1 和 FP2 拥有相同的对象集合和基本函数集合，但是 FP1 的函数形式集合严格包含 FP2 的函数形式集合。同时假设这两个系统都能够表达所有可计算的函数。尽管如此，我们仍然可以说 FP1 的表达能力比 FP2 强。因为，FP2 中的所有函数表达式在 FP1 中都可以表示。与此同时，FP1 可以更直接、更容易地表示某些函数。

> I believe the above observation could be developed into a theory of the expressive power of languages in which a language A would be more expressive than language B under the following roughly stated conditions. First, form all possible functions of all types in A by applying all existing functions to objects and to each other in all possible ways until no new function of any type can be formed. (The set of objects is a type; the set of continuous functions $[T \to U]$ from type $T$ to type $U$ is a type. If $f \in [T \to U]$ and $t \in T$ , then $ft$ in $U$ can be formed by applying $f$ to $t$ .) Do the same in language B. Next, compare each type in A to the corresponding type in B. If, for every type, A's type includes B's corresponding type, then A is more expressive than B (or equally expressive). If some type of A's functions is incomparable to B's, then A and B are not comparable in expressive power.

我认为之前关于 FP1 和 FP2 的比较可以扩展为一套语言表达能力的理论。根据以下大致的条件，我们可以判断语言 A 比语言 B 更具表达能力。首先，枚举语言 A 中所有类型的所有可能函数。具体方法是，不断地用现有函数作用于对象或其他函数，并重复该过程，直到无法生成任何新的函数为止。更进一步说，

- 对象本身被视为一种类型；
- 从类型 $T$ 到类型 $U$ 的连续函数集合记为 $[T \to U]$，它也是一种类型；
- 当 $f \in [T \to U]$ 且 $t \in T$ ，则通过应用 $f$ 于 $t$ 可得 $ft \in U$ 。

其次，将语言 A 中的每个类型与其在语言 B 中对应的类型进行比较。如果对于所有类型，A 的类型都包含 B 的对应类型，那么 A 就比 B 更具表达力 (或两者表达力相同)。如果 A 中存在某种类型的函数在 B 中找不到对应的类型 (incomparable)，那么 A 和 B 的表达能力就无法直接比较。

> 11.4.4 Advantages of FP systems

#### 11.4.4 FP 系统的优势

> The main reason FP systems are considerably simpler than either conventional languages or lambda-calculus-based languages is that they use only the most elementary fixed naming system (naming a function in a definition) with a simple fixed rule of substituting a function for its name. Thus they avoid the complexities both of the naming systems of conventional languages and of the substitution rules of the lambda calculus. FP systems permit the definition of different naming systems (see Sections 13.3.4 and 14.7) for various purposes. These need not be complex, since many programs can do without them completely. Most importantly, they treat names as functions that can be combined with other functions without special treatment.

FP 系统比传统语言或基于 lambda 演算的语言更简单的主要原因在于，使用一种最基本的固定命名系统（定义中为函数命名），替换也遵循简单固定的规则。从而避免了传统语言复杂冗长的命名系统，以及 lambda 演算中复杂的替换规则。FP 系统允许为不同的目的定义不同的命名系统 (见 13.3.4 和 14.7 节)。它无需多复杂，甚至许多程序甚至完全不需要用到这种特性。最重要的是，FP 系统将名称视为函数，可以与其他函数进行组合，而不需要特殊的处理方式。

> FP systems offer an escape from conventional word-at-a-time programming to a degree greater even than APL [^12] (the most successful attack on the problem to date within the von Neumann framework) because they provide a more powerful set of functional forms within a unified world of expressions. They offer the opportunity to develop higher level techniques for thinking about, manipulating, and writing programs. 

FP 系统比 APL [^12]（冯诺依曼架构下迄今为止最成功的尝试之一）更能摆脱传统逐字编程模式，那是因为它在一个统一的表达式世界中提供了一组更强大的函数形式，并让程序员可以用更抽象的概念来思考、操作和编写程序。
