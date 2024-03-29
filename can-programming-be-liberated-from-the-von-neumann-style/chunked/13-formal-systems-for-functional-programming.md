> 13 . Formal Systems for Functional Programming (FFP Systems)

## 13. 函数式编程的形式化系统（FFP）

> 13.1 Introduction 

### 13.1 介绍

> As we have seen, an FP system has a set of functions that depends on its set of primitive functions, its set of functional forms, and its set of definitions. In particular, its set of functional forms is fixed once and for all, and this set determines the power of the system in a major way. For example, if its set of functional forms is empty, then its entire set of functions is just the set of primitive functions. In FFP systems one can create new functional forms. Functional forms are represented by object sequences; the first element of a sequence determines which form it represents, while the remaining elements are the parameters of the form.

正如我们所见，FP 系统的函数集合取决于其原生函数的集合、函数式的集合以及定义的集合。尤其是，其函数式的集合是一旦确定就不会变的，且在很大程度上决定了系统的强大程度。具体来说，如果没有函数式的集合，那么整个 FP 系统就只剩下原生函数的集合了。与此不同的是，在 FFP 系统中是可以创建新的函数式的。这样的函数式由对象序列表示；序列的第一个元素决定它代表哪个形式，其余元素代表其参数。

> The ability to define new functional forms in FFP systems is one consequence of the principal difference between them and FP systems: in FFP systems objects are used to "represent" functions in a systematic way. Otherwise FFP systems mirror FP systems closely. They are similar to, but simpler than, the Reduction (Red) languages of an earlier paper [^2]. 

FFP 系统可以定义新的函数式，这是它们与 FP 系统的主要区别之一。也就是说，在 FFP 系统中，对象被用来以一种系统的方式“表示”函数。除此之外，FFP 系统与 FP 系统几乎一样。它们很像我早期论文 [^2] 中的 Reduction (Red) 语言，但要更简单。

[^2]: [Backus, J. Programming language semantics and closed applicative languages. Conf. Record ACM Symp. on Principles of Programming Languages, Boston, Oct. 1973, 71-86.](https://dl.acm.org/doi/10.1145/512927.512934)

> We shall first give the simple syntax of FFP systems, then discuss their semantics informally, giving examples, and finally give their formal semantics.

我们将首先介绍 FFP 系统的简单语法，然后通过例子非正式地讨论它们的语义，最后给出它们的正式语义。

> 13.2 Syntax

### 13.2 语法

> We describe the set $\rm O$ of objects and the set $\rm E$ of expressions of an FFP system. These depend on the choice of some set $\rm A$ of *atoms*, which we take as given. We assume that $T$ (true), $F$ (false), $\phi$ (the empty sequence), and $\\#$ (default) belong to $\rm A$, as well as "numbers" of various kinds, etc.

FFP 系统里，对象集合是 $\rm O$ ，表达式集合是 $\rm E$ 。它们由我们给定的*原子*(atom)集合 $\rm A$ 决定。集合 $\rm A$ 又包括有： $T$ （真）、 $F$ （假）、 $\phi$ （空序列）、 $\\#$ （默认值）以及各类“数字”等。

> 1) Bottom, $\bot$ , is an object but not an atom. 
> 2) Every atom is an object. 
> 3) Every object is an expression. 
> 4) If $x_1, \dots, x_n$ are objects [expressions], then $< x_1, \dots, x_n >$ is an object [resp., expression] called a sequence (of *length* n) for $n \ge 1$ . The object [expression] $x _ i$ for $1 \le i \le n$ , is the ith *element* of the sequence $< x_1, \dots, x_i, \dots, x_n >$ . ( $\phi$ is both a sequence and an atom; its length is 0.) 
> 5) If $x$ and $y$ are expressions, then $(x:y)$ is an expression called  an application, $x$ is its operator and $y$ is its operand. Both are elements of the expression.  
> 6) If $x = < x_1, \dots, x_n >$ and if one of the elements of $x$ is $\bot$ ,then $x = \bot$ .That is, $<\dots, \bot, \dots> = \bot$ . 
> 7) All objects and expressions are formed by finite use of the above rules. 

1. 底，即 $\bot$ ，是一个对象，但不是原子；
2. 每个原子都是一个对象；
3. 每个对象都是一个表达式；
4. 若 $x_1, \dots, x_n$ 表示若干表达式对象，则 $< x_1, \dots, x_n >$ 表示一个表达式组的对象，又叫序列（长度是n），且 $n \ge 1$ 。这个表达式组的对象中，$x_i$ （ $1 \le i \le n$ ）代表 $< x_1, \dots, x_i, \dots, x_n >$ 序列的第 $i$ 个*元素*。（ $\phi$ 既是序列，也是原子，但长度为零。）
5. 若 $x$ 和 $y$ 都是表达式，则 $x:y$ 是一个*应用*（application）的*表达式*。其中 $x$ 是操作符， $y$ 是操作数。它们都是表达式的元素；
6. 若 $x = < x_1, \dots, x_n >$ ，且其中有一个元素 $x$ 是 $\bot$ ，即 $x = \bot$ ，则 $<\dots, \bot, \dots> = \bot$ ；
7. 所有对象和表达式都是以上规则的有限情况的组合形式。

> A *subexpression* of an expression $x$ is either $x$ itself or a subexpression of an element of $x$. An FFP object is an expression that has no application as a subexpression. Given the same set of atoms, FFP and FP objects are the same. 

一个表达式 $x$ 的子表达式可以是 $x$ 本身，也可以是 $x$ 中某个元素的子表达式。一个 FFP 对象作为一个没有应用的表达式，可以被当作子表达式。给定同样的原子集合，FFP 和 FP 的对象是一样的。

> 13.3 Informal Remarks About FFP Semantics

### 13.3 有关 FFP 语义的非正式小结

> 13.3.1 The meaning of expressions; the semantic function $\mu$.

#### 13.3.1 表达式的意义（meaning）之语义函数 $\mu$

> Every FFP expression $e$ has a *meaning*, $\mu e$ , which is always an object; $\mu e$ is found by repeatedly replacing each innermost application in $e$ by its meaning. If this process is nonterminating, the meaning of $e$ is $\bot$ . The meaning of an innermost application $(x:y)$ (since it is innermost, $x$ and $y$ must be objects) is the result of applying the function represented by $x$ to $y$ , just as in FP systems, except that in FFP systems functions are represented by objects, rather than by function expressions, with atoms (instead of function symbols) representing primitive and defined functions, and with sequences representing the FP functions denoted by functional forms.

每個 FFP 表达式 $e$ 都有一個意义（ $\mu e$ ），它始终是一个对象。找到意义（ $\mu e$ ）方法是反复替换表达式 $e$ 最内层（innermost）应用的意义。如果替换过程一直进行下去没有终止，那么表达式 $e$ 的意义就是 $\bot$ 。而一个最内层应用 $(x:y)$ （因为是最内层，所以 $x$ 和 $y$ 都必须是对象 ）的意义是，将 $x$ 表示的函数作用于 $y$ 的结果。这与 FP 系统类似，但区别在于 FFP 系统中， 函数由对象表示，而不是函数表达式；原子（替代了函数符号）表示原生函数和定义函数；序列表示由函数式定义的 FP 函数。

> The association between objects and the functions they represent is given by the *representation function*, $\rho$ , of the FFP system. (Both $\rho$ and $\mu$ belong to the description of the system, not the system itself.) Thus if the atom $NULL$ represents the FP function $\rm null$, then $\rho NULL = \rm null$ and the meaning of $(NULL:A)$ is $\mu(NULL:A) = (\rho NULL):A = \text{null}:A = F$. From here on, as above, we use the colon in two senses. When it is between two objects, as in $(NULL:A)$ , it identifies an FFP application that denotes only itself; when it comes between a function and an object, as in $(\rho NULL):A$ or $\text{null}:A$ , it identifies an FP-like application that denotes the result of applying the function to the object.

在 FFP 系统中，对象与函数间的关系是由 表示函数 (representation function) $\rho$ 来定义的。（注意 $\rho$ 和 $\mu$ 都属于对系统的描述，而不是系统本身。）举例来讲，如果系统中的原子 $NULL$ 代表 FP 函数 $\rm null$ ，那么 $\rho NULL = \rm null$ ，而 $(NULL:A)$ 的意义则是 $\mu(NULL:A) = (\rho NULL):A = \text{null}:A = F$ 。至此，其中的分号会有两种用法。当它位于两个对象之间时，如 $(NULL:A)$ ，表示为一个 FFP 的应用本身；而当它位于函数和对象之间时，如 $(\rho NULL):A$ 或 $\text{null}:A$ ，则表示类似于 FP 的应用，计算函数作用于对象的结果。

> The fact that FFP operators are objects makes possible a function, $\rm apply$ , which is meaningless in FP systems:

事实是，FFP 的操作符是对象，使得它能成为一个函数，即 $\rm apply$ ，而这在 FP 系统里是毫无意义的：

$$
\text{apply}:< x, y > = (x:y)
$$

> The result of $\text{apply}:< x, y >$ , namely $(x:y)$ , is meaningless in FP systems on two levels. First, $(x:y)$ is not itself an object; it illustrates another difference between FP and FFP systems: some FFP functions, like $\rm apply$ , map objects into expressions, not directly into objects as FP functions do. However, the meaning of $\text{apply}:< x, y >$ is an object (see below). Second, $(x:y)$ could not be even an intermediate result in an FP system; it is meaningless in FP systems since $x$ is an object, not a function and FP systems do not associate functions with objects. Now if $APPLY$ represents $\rm apply$, then the meaning of $(APPLY:< NULL, A >)$ is

$\text{apply}:< x, y >$ 的结果，就是 $(x:y)$ ，这在 FP 系统的无意义有两层。第一层， $(x:y)$ 本身并不是一个对象。这说明了 FFP 与 FP 系统的另一个区别是，一些 FFP 的函数（例如 $\rm apply$ ）会将对象映射成表达式，而不是像 FP 的函数那样直接映射成对象。然而， $\text{apply}:< x, y >$ 的意义却是一个对象 (见下文解释)。第二层，在 FP 系统里 $(x:y)$ 甚至都不能作为一个中间结果，其无意义的原因在于 $x$ 是一个对象而不是函数，并且 FP 系统也无法将函数与对象对应上。现在，若用 $APPLY$ 表示 $\rm apply$ ，那么 $(APPLY:< NULL,A >)$ 的意义会是

$$
\begin{align*}
\mu(APPLY:< NULL, A >) 
  &= \mu((\rho APPLY):< NULL,A >) \\
  &= \mu(\text{apply}:< NULL,A >) \\
  &= \mu(< NULL,A >) \\
  &= \mu((\rho NULL):A) \\
  &= \mu(\text{null}:A) \\
  &= \mu(F) \\
  &= F \\
\end{align*}
$$

> The last step follows from the fact that every object is its own meaning. Since the meaning function $\mu$ eventually evaluates all applications, one can think of $\text{apply}:< NULL,A >$ as yielding $F$ even though the actual result is $(NULL:A)$ .

依照每个对象自身的意义反复替换可得最后的结果。正如意义函数 $\mu$ 最终会计算所有的应用，使得 $\text{apply}:< NULL,A >$ 可以被视作是计算得到了 $F$ ，而实际的结果是 $(NULL:A)$ 。

> 13.3.2 How objects represent functions; the representation function $\rho$ .

#### 13.3.2 对象如何表示函数之表示函数 $\rho$

> As we have seen, some atoms (primitive atoms) will represent the primitive functions of the system. Other atoms can represent defined functions just as symbols can in FP systems. If an atom is neither primitive nor defined, it represents $\bot$ , the function which is $\bot$ everywhere.

如你所见，一些原子（原生原子）将表示系统原生函数。其它原则可以表示定义函数，类似 FP 系统里的函数符号。若是一个原子既不表示原生函数，🈶不表示定义函数，那它就表示 $\bar{\bot}$ ，即这样的函数无论输入什么都会得到 $\bot$ 。

> Sequences also represent functions and are analogous to the functional forms of FP. The function represented by a sequence is given (recursively) by the following rule. 

序列也能表示函数，这点很像 FP 里的函数式。 由一个（递归）给定的序列表示的函数会遵循以下规则。

> Metacomposition rule 

**元构规则**

$$
(\rho < x_1, \dots, x_n >) : y = (\rho x_1) : << x_1, \dots, x_n >, y >
$$

> where the $x_i$ 's and $y$ are objects. Here $\rho x_1$ determines what functional form $< x_1, \dots, x_n >$ represents, and $< x_2, \dots, x_n >$ , are the parameters of the form (in FFP, $x_1$ itself can also serve as a parameter). Thus, for example, let $\textbf{Def } \rho CONST \equiv 2 \circ 1$; then $< CONST, x >$ in FFP represents the FP functional form $\bar{x}$, since, by the metacomposition rule, if $y \ne \bot$ , 

其中 $x_i$ 和 $y$ 都是对象。这里的 $\rho x_1$ 决定了  $< x_1, \dots, x_n >$ 所表示的函数式，而 $< x_2, \dots, x_n >$ 是函数式的参数（在 FFP 里，$x_1$ 也可作为一个参数）。举例而言，设 $\textbf{Def } \rho CONST \equiv 2 \circ 1$ ，那么 $< CONST, x >$ 在 FFP 里表示的就是 FP 里的函数式 $\bar{x}$ 。那是因为，根据元构规则，只要 $y \ne \bot$ ，

$$
\begin{align*}
(\rho< CONST, x >) : y
  &= (\rho CONST) : << CONST, x >, y > \\
  &= 2 \circ 1 : << CONST, x >, y > \\
  &= x
\end{align*}
$$

> Here we can see that the first, controlling, operator of a sequence or form, $CONST$ in this case, always has as its operand, after metacomposition, a pair whose first element is the sequence itself and whose second element is the original operand of the sequence, $y$ in this case. The controlling operator can then rearrange and reapply the elements of the sequence and original operand in a great variety of ways. The significant point about metacomposition is that it permits the definition of new functional forms, in effect, merely by defining new functions. It also permits one to write recursive functions without a definition.

这里我们能看到最开头的，序列或函数式的控制操作符， $CONST$ ，始终是有其操作数（这里的 $x$ ）的。元构之后，新序列的第一个元素是之前函数式序列，第二个元素则是函数式原本的操作数 $y$ 。换言之，控制操作符能够以多种多样的方式重新调整和应用序列的元素以及原本的操作数。元构的关键在于，用定义新函数的方式来达到定义新的函数式的效果。甚至，能在无需定义的情况下，写出递归函数。

> We give one more example of a controlling function for a functional form: $\textbf{Def } \rho CONS \equiv \alpha \text{apply} \circ \text{tl} \circ \text{distr}$. This definition results in $< CONS,f_1, \dots, f_n >$ -- where the $f_i$ are objects -- representing the same function as $[\rho f_1, \dots, \rho f_n]$. The following shows this.

我们再来看一个函数式控制函数的例子： $\textbf{Def } \rho CONS \equiv \alpha \text{apply} \circ \text{tl} \circ \text{distr}$ 。这个定义会使得 $< CONS,f_1, \dots, f_n >$ （其中 $f_i$ 是对象）的结果与函数 $[\rho f_1, \dots, \rho f_n]$ 是一样的。如下证明过程：

$$
\begin{align*}
(\rho < CONS, f_1, \dots, f_n >) : x 
  &= (\rho CONS) : << CONS, f_1, \dots, f_n >, x > &&\text{by metacomposition} \\
  &= \alpha \text{apply} \circ \text{tl} \circ \text{distr} : << CONS, f_1, \dots, f_n >, x > &&\text{by def of } \rho CONS\\
  &= \alpha \text{apply}: << f_1, x >, \dots, < f_n, x >> &&\text{by def of tl and distr and } \circ \\
  &= < \text{apply}:< f_1, x >, \dots, \text{apply}:< f_n, x >> &&\text{by def of } \alpha \\
  &= < (f_1:x), \dots, (f_n:x) > &&\text{by def of apply}
\end{align*}
$$

> In evaluating the last expression, the meaning function $\mu$ will produce the meaning of each application, giving $\rho f_i:x$ as the ith element. 

在最后的表示求值中，意义函数 $\mu$ 将产生各个应用的意义，即给出 $\rho f_i:x$ 作为结果序列的第 $i$ 个元素。

> Usually, in describing the function represented by a sequence, we shall give its overall effect rather than show how its controlling operator achieves that effect. Thus we would simply write

一般在对序列表示的函数的描述中，我们会给出最后的结果，而不呈现控制操作符是如何达成的过程。因此，我们会简单记为

$$
(\rho < CONS, f_1, \dots, f_n >) : x = < (f_1:x), \dots, (f_n:x) >
$$

> instead of the more detailed account above. 

以替代上面更多的过程细节。

> We need a controlling operator, $COMP$ , to give us sequences representing the functional form composition. We take $\rho COMP$ to be a primitive function such that, for all objects $x$,


一个我们会用到的控制操作符， $COMP$  ，将给定的序列表示为组合的函数式。 我们将 $\rho COMP$ 作为一个原生函数，他对所有对象 $x$ 有

$$
(\rho < COMP, f_1, \dots, f_n >) : x = (f_1 : (f_2 : (\dots : (f_n:x)))) \quad \text{for } n \ge 1
$$

> (I am indebted to Paul McJones for his observation that ordinary composition could be achieved by this primitive function rather than by using two composition rules in the basic semantics, as was done in an earlier paper [^2].)

（得益于 Paul McJones 的观察，普通组合（ordinary composition）可由这个原生函数实现，避免在基础语义上应用两两组合的规则，如同我早期论文里做的[^2]。）

Although FFP systems permit the definition and investigation of new functional forms, it is to be expected that most programming would use a fixed set of forms (whose controlling operators are primitives), as in FP, so that the algebraic laws for those forms could be employed, and so that a structured programming style could be used based on those forms.

尽管 FFP 系统允许定义和研究新的函数形式，但可以预见的是，大多数编程会像 FP 语言一样使用一组固定的函数式（其控制操作符均为原语），以便利用这些函数式的代数定律，并以此为基础采用一种结构化的编程风格。

> In addition to its use in defining functional forms, metacomposition can be used to create recursive functions directly without the use of recursive definitions of the form $\textbf{Def } f \equiv E(f)$. For example, if $\rho MLAST \equiv null \circ \text{tl} \circ 2 \to 1 \circ 2; \text{apply} \circ [1, \text{tl} \circ 2]$, then $\rho< MLAST > \equiv \text{last}$, where $\text{last}:x \equiv x = < x_1, \dots, x_n > \to x_n; \bot$. Thus the operator $< MLAST >$ works as follows:

除了定义函数式以外，元构可以用来直接创建递归函数，无需以 $\textbf{Def } f \equiv E(f)$ 的形式递归定义。例如，若 $\rho MLAST \equiv null \circ \text{tl} \circ 2 \to 1 \circ 2; \text{apply} \circ [1, \text{tl} \circ 2]$ ，则 $\rho< MLAST > \equiv \text{last}$ ，也就是 
$\text{last}:x \equiv x = < x_1, \dots, x_n > \to x_n; \bot$ 。 操作符  $< MLAST >$ 的细节如下：

$$
\begin{align*}
\mu (< MLAST > : < A, B >)
  &= \mu (\rho MLAST : << MLAST >, < A, B >>) &&\text{by metacomposition} \\
  &= \mu (\text{apply} \circ [1, \text{tl} \circ 2] : << MLAST >, < A, B >>) \\
  &= \mu (\text{apply} : << MLAST >, < B >>) \\
  &= \mu (<< MLAST >, < B >>) \\
  &= \mu (\rho MLAST : << MLAST >, < B >>) \\
  &= \mu (1 \circ 2 : << MLAST >, < B >>) \\
  &= B
\end{align*}
$$

> 13.3.3 Summary of the properties of $\rho$ and $\mu$.

#### 13.3.3 $\rho$ 和 $\mu$ 的性质总结

> So far we have shown how $\rho$ maps atoms and sequences into functions and how those functions map objects into expressions. Actually, $\rho$ and all FFP functions can be extended so that they are defined for all expressions. With such extensions the properties of $\rho$ and $\mu$ can be summarized as follows: 

到目前为止，我们已经展示了如何将原子和序列通过 $\rho$ 函数映射成函数，以及这些函数如何将对象映射成表达式。实际上，$\rho$ 函数以及所有 FFP 函数都可以进行扩展，使其可以对所有表达式进行定义。通过这样的扩展，$\rho$ 和 $\mu$ 的性质可以概括如下：

> 1) $\mu \in [\rm expressions \to objects]$.
> 2) If $x$ is an object, $\mu x = x$.
> 3) If $e$ is an expression and $e = < e_1, \dots, e_n >$ , then $\mu e = < \mu e_1, \dots, \mu e_n >$ .
> 4) $\rho \in [\rm expressions \to [expressions \to expressions]]$.
> 5) For any expression $e$, $\rho e = \rho(\mu e)$.
> 6) If $x$ is an object and $e$ an expression, then $\rho x:e = \rho x : (\mu e)$.
> 7) If $x$ and $y$ are objects, then $\mu (x:y) = \mu(\rho x:y)$. In words: the meaning of an FFP application $(x:y)$ is found by applying $\rho x$, the function represented by $x$, to $y$ and then finding the meaning of the resulting expression (which is usually an object and is then its own meaning). 

1. $\mu \in [\rm expressions \to objects]$ ；
2. 若 $x$ 是一个对象，则 $\mu x = x$ ；
3. 若 $e$ 是一个表达式，且 $e = < e_1, \dots, e_n >$ ，则 $\mu e = < \mu e_1, \dots, \mu e_n >$ ；
4. $\rho \in [\rm expressions \to [expressions \to expressions]]$ ；
5. 对任何表达式 $e$ ，都满足 $\rho e = \rho(\mu e)$ ；
6. 若 $x$ 是一个对象， $e$ 是一个表达式， 则 $\rho x:e = \rho x : (\mu e)$ ；
7. 若 $x$ 和 $y$ 都是对象， 则  $\mu (x:y) = \mu(\rho x:y)$ 。简言之，一个 FFP 的应用 $(x:y)$ 的意义是通过 $\rho x$ 找到的，即由 $x$ 表示的函数作用于 $y$ ，进而找到起结果表达式的意义（这通常是一个对象，其意义就是它本身）。

> 13.3.4 Cells, fetching, and storing.

#### 13.3.4 单元格，获取与存储

> For a number of reasons it is convenient to create functions which serve as names. In particular, we shall need this facility in describing the semantics of definition in FFP systems. To introduce naming functions, that is, the ability to fetch the contents of a cell with a given name from a store (a sequence of cells) and to store a cell with given name and contents in such a sequence, we introduce objects called cells and two new functional forms, $fetch$ and $store$. 

为了方便起见，创建一些名称函数是非常实用的。尤其是在描述 FFP 系统中的定义语义时，我们将需要这种功能。而引入名称函数，即从存储（一个单元格序列）中用名称获取（ $fetch$ ）和存储（ $store$ ）对应单元格内容，我们就需要引入称为单元格（ $cells$ ）的对象和两种新的函数式： 获取（ $fetch$ ） 和 存储（ $store$ ）。

> Cells

**单元格**

> A cell is a triple $< CELL, name, contents >$. We use this form instead of the pair $< name, contents >$ so that cells can be distinguished from ordinary pairs. 

单元格是一个三元组 $< CELL, name, contents >$ ，之所以不用 $< name, contents >$ ，是为了让单元格和普通二元组（pairs）区分开来。

> Fetch 

**获取**

> The functional form $fetch$ takes an object $n$ as its parameter ($n$ is customarily an atom serving as a name); it is written $\uparrow n$ (read "fetch $n$"). Its definition for objects $n$ and $x$ is 

函数式 $fetch$ 接受一个对象 $n$ 作为参数（通常 $n$ 是一个原子用作名称）；我们记作  $\uparrow n$ （读作“获取 $n$ ”）。就对象 $n$ 和 $x$ ，其定义如下

$$
\begin{align*}
\uparrow n:x \equiv\
  &x = \phi &&\to \\\# ; \\
  &\text{atom}:x &&\to \bot; \\
  &(1:x) = < CELL, n, c > &&\to c;
  \uparrow n \circ \text{tl}:x
\end{align*}
$$

> where $\\#$ is the atom "default." Thus $\uparrow n$ (fetch $n$) applied to a sequence gives the contents of the first cell in the sequence whose name is $n$; If there is no cell named $n$, the result is default, $\\#$. Thus $\uparrow n$ is the name function for the name $n$. (We assume that $\rho FETCH$ is the primitive function such that $\rho <FETCH, n> \equiv\ \uparrow n$. Note that $\uparrow n$ simply passes over elements in its operand that are not cells.) 

其中 $\\#$ 是“默认值”（原子）。  $\uparrow n$ （获取 $n$ ）作用于一个序列，获取第一个名字为 $n$ 单元格的内容。若没有名为 $n$ 的单元格，则结果是默认值（ $\\#$ ）。至此， $\uparrow n$ 就是一个以 $n$ 为名的名称函数。（假定 $\rho FETCH$ 是原生函数，则 $\rho <FETCH, n> \equiv\ \uparrow n$ 。需要注意的是， $\uparrow n$ 会跳过操作数中非单元格的元素。）

> Store and push, pop, purge 

**存储，入栈，出栈和清除**

> Like fetch, store takes an object $n$ as its parameter; it is written $\downarrow n$ ("store $n$ "). When applied to a pair $< x,y >$, where $y$ is a sequence, $\downarrow n$ removes the first cell named $n$ from $y$, if any, then creates a new cell named $n$ with contents $x$ and appends it to $y$. Before defining $\downarrow n$ (store $n$) we shall specify four auxiliary functional forms. (These can be used in combination with fetch $n$ and store $n$ to obtain multiple, named, LIFO stacks within a storage sequence.) Two of these auxiliary forms are specified by recursive functional equations; each takes an object $n$ as its parameter.

与获取类似，存储也接受一个对象 $n$ 作为参数，记为 $\downarrow n$ （读作“存储 $n$ ”）。当作用于二元组 $< x, y >$ （其中 $y$ 是一个序列）时， $\downarrow n$ 先是删除 $y$ 中第一个名为 $n$ 的单元格（若有的话），然后创建一个新的单元格（名为 $n$ ，内容为 $x$），将其追加到 $y$ 的末尾。在定义 $\downarrow n$ （存储 $n$ ）之前，我们还需要定义四个辅助函数式。（它们可与存取结合使用，从而在存储序列上实现多个命名的 LIFO 栈。）其中两个辅助函数式定义为了递归函数式方程，它们同样接受一个对象 $n$ 作为参数。

$$
\begin{align*}
(\text{cellname } n) \equiv\space 
  &atom &&\to \bar{F}; \\
  &eq \circ [length, \bar{\it 3}] &&\to eq \circ [[\bar{CELL}, \bar{n}], [1, 2]]; \bar{F} \\
(\text{push } n) \equiv\space 
  &pair &&\to \text{apndl} \circ[[\bar{CELL}, \bar{n}, 1],2]; \bot \\
(\text{pop } n) \equiv\space
  &null &&\to \bar{\phi};\\
  &(\text{cellname } n) \circ 1 &&\to \text{tl}; 
  \text{apndl} \circ [1, (\text{pop } n) \circ \text{tl}] \\
(\text{purge } n) \equiv\space
  &null &&\to \bar{\phi}; \\
  &(\text{cellname } n) \circ 1 &&\to (\text{purge } n) \circ \text{tl};
  \text{apndl} \circ [1, (\text{purge } n) \circ \text{tl}] \\
\downarrow n \equiv\space
  &pair &&\to (\text{push } n) \circ [1, (\text{pop } n) \circ 2]; \bot
\end{align*}
$$

> The above functional forms work as follows. For $x \ne \bot$ , $(\text{cellname} n):x$ is $T$ if $x$ is a cell named $n$, otherwise it is $F$. $(\text{pop } n):y$ removes the first cell named $n$ from a sequence $y$; $(\text{purge }n):y$ removes all cells named $n$ from $y$. $(\text{push }n):<x,y>$ puts a cell named $n$ with contents $x$ at the head of sequence $y$; $\downarrow n:<x,y>$ is $(\text{push }n):< x, (\text{pop }n):y >$. 

上述的功能形式的工作原理如下：

- 对于 $x \ne \bot$ 的情况，若 $x$ 是名为 $n$ 的单元格，则 $(\text{cellname} n):x$ 为 $T$ ，否则为 $F$ ； 
- $(\text{pop } n):y$ 从序列 $y$ 中删除第一个名为 $n$ 的单元格；
- $(\text{purge }n):y$ 从序列 $y$ 中删除所有名称为 $n$ 的单元格；
- $(\text{push }n):<x,y>$ 将一个名为 $n$ 的单元格（内容为 $x$）置于序列 $y$ 的头部；
- $\downarrow n:<x,y>$ 等于 $(\text{push }n):< x, (\text{pop }n):y >$

> (Thus $(\text{push }n):< x,y > = y'$ pushes $x$ onto the top of a "stack" named $n$ in $y'$; $x$ can be read by $\uparrow n:y'= x$ and can be removed by $(\text{pop }n):y'$; thus $\uparrow n \circ (\text{pop }n):y'$ is the element below $x$ in the stack $n$, provided there is more than one cell named $n$ in $y'$.) 

（也就是说， 
- $(\text{push }n):< x,y > = y'$ 在序列 $y'$ 中将 $x$ 置于一个名为 $n$ 的“栈”顶； 
- $\uparrow n:y'= x$ 可以读取到 $x$ ，而 $(\text{pop }n):y'$ 会删除它；
- 因此，若 $y'$ 中有多个名为 $n$ 的单元格，则 $\uparrow n \circ (\text{pop }n):y'$ 会得到栈 $n$ 中位于 $x$ 下方的元素。）

> 13.3.5 Definitions in FFP systems.

#### 13.3.5 FFP 系统里的定义

> The semantics of an FFP system depends on a fixed set of definitions $\rm D$ (a sequence of cells), just as an FP system depends on its informally given set of definitions. Thus the semantic function $\mu$ depends on $\rm D$; altering $\rm D$ gives a new $\mu'$ that reflects the altered definitions. We have represented $\rm D$ as an object because in AST systems (Section 14) we shall want to transform $\rm D$ by applying functions to it and to fetch data from it--in addition to using it as the source of function definitions in FFP semantics.

FFP 系统的语义依赖于一组固定定义集 $\rm D$ （一个单元格序列），就像 FP 系统依赖于其非正式给定的定义集一样。因此，语义函数 $\mu$ 取决于 $\rm D$ ，改变 $\rm D$ 会得到一个新的 $\mu'$ ， 它反映了改变后的定义。我们把 $\rm D$ 表示为一个对象，因为在 AST 系统（第 14 节）中，我们不仅要将它用作 FFP 语义中的函数定义源，还需要通过应用函数来转换 $\rm D$ 并从中提取数据。

> If $< CELL,n,c >$ is the first cell named $n$ in the sequence $\rm D$ (and $n$ is an atom) then it has the same effect as the FP definition $\textbf{Def } n \equiv \rho c$, that is, the meaning of $(n:x)$ will be the same as that of $\rho c:x$. Thus for example, if $< CELL, CONST,< COMP,2,1 > >$ is the first cell in $\rm D$ named $CONST$, then it has the same effect as $\textbf{Def } CONST \equiv 2 \circ 1$, and the FFP system with that $\rm D$ would find 

如果序列 $\rm D$ 中的第一个名为 $\rm D$ 的单元格是 $< CELL,n,c >$ （并且 $n$ 是一个原子），那么它与 FP 里定义 $\textbf{Def } n \equiv \rho c$ 具有相同的效果，即 $(n:x)$ 的含义将与 $\rho c:x$ 的含义相同。又如 $< CELL, CONST,< COMP,2,1 > >$ 是 $\rm D$ 中第一个名为 $CONST$ 的单元格，它就相当于 $\textbf{Def } CONST \equiv 2 \circ 1$ ，在有了这样定义 $\rm D$ 在 FFP 系统里会得到

$$
\mu(CONST : < < x, y >, z >) = y
$$

> and consequently

和

$$
\mu(< CONST, A > : B) = A
$$

> In general, in an FFP system with definitions $\rm D$, the meaning of an application of the form $(atom:x)$ is dependent on $\rm D$; if $\uparrow atom:D \ne$ $\\#$ (that is, $atom$ is defined in $\rm D$) then its meaning is $\mu(c:x)$, where $c = \uparrow atom: \rm D$, the contents of the first cell in $\rm D$ named $atom$. If $\uparrow\rm atom:D =$ $\\#$, then $atom$ is not defined in $\rm D$ and either $atom$ is primitive, i.e. the system knows how to compute $\rho atom:x$, and $\mu(atom:x) = \mu(\rho atom:x)$, otherwise $\mu(atom:x) = \bot$ .

在具有定义集 $\rm D$ 的 FFP 系统中，表达式 $(atom:x)$ 应用的含义通常依赖于 $\rm D$ 。具体来说：

- 如果 $\uparrow atom:D \ne$ $\\#$ （即，原子 $atom$ 在 $\rm D$ 中被定义），那么其含义为 $\mu(c:x)$ ，其中 $c = \uparrow atom: \rm D$ ，即 $\rm D$ 中第一个名为 $atom$ 的单元格的内容；
- 如果 $\uparrow\rm atom:D =$ $\\#$ （即，原子 $atom$ 不在 $\rm D$ 中被定义），则又分两种情况：
  - 如果 $atom$ 是系统原生的 (primitive)，即系统知道如何计算 $\rho atom:x$ ，那么 $\mu(atom:x) = \mu(\rho atom:x)$；
  - 反之， $\mu(atom:x) = \bot$ 。

> 13.4 Formal Semantics for FFP Systems 

### 13.4 FFP 系统的形式化语义

> We assume that a set $\rm A$ of atoms, a set $\rm D$ of definitions, a set $P \subset A$ of primitive atoms and the primitive functions they represent have all been chosen. We assume that $\rho a$ is the primitive function represented by $a$ if $a$ belongs to $\rm P$, and that $\rho a = \bot$ if $a$ belongs to $\rm Q$, the set of atoms in $A-P$ that are not defined in $\rm D$. Although $\rho$ is defined for all expressions (see 13.3.3), the formal semantics uses its definition only on $\rm P$ and $\rm Q$. The functions that $\rho$ assigns to other expressions $x$ are implicitly determined and applied in the following semantic rules for evaluating $\mu(x:y)$. The above choices of $\rm A$ and $\rm D$, and of $\rm P$ and the associated primitive functions determine the objects, expressions, and the semantic function $\mu \rm D$ for an FFP system. (We regard $\rm D$ as fixed and write $\mu$ for $\mu \rm D$.) We assume $\rm D$ is a sequence and that $\uparrow y:D$ can be computed (by the function $\uparrow y$ as given in Section 13.3.4) for any atom $y$. With these assumptions we define $\mu$ as the least fixed point of the functional $\tau$, where the function $\tau \mu$ is defined as follows for any function $\mu$ (for all expressions $x$, $x_i$, $y$, $y_i$, $z$, and $w$): 

假设原子集合 $\rm A$ 、定义集合 $\rm D$ 、原生原子的子集 $\rm P$ （包含原生原子及其代表的原始函数）。当 $a$ 属于 $\rm P$ 时， $\rho a$ 则是由 $a$ 代表的原生函数；而 $a$ 属于 $\rm Q$ （ $\rm A-P$ 的集合）且不在 $\rm D$ 中定义，则 $\rho a = \bot$ 。尽管 $\rho$ 可以定义所有表达式 (参见 13.3.3 节)，形式语义只会在 $\rm P$ 和 $\rm Q$ 上使用其定义。分配给其他表达式 $x$ 的函数由 $\rho$ 隐式确定，并在以下用于估算 $\mu(x:y)$ 的语义规则中应用。上述对 $\rm A$ 和 $\rm D$ 以及对 $\rm P$ 和相关原始函数的选择决定了一个 FFP 系统的对象、表达式和语义函数 $\mu \rm D$ ​（我们认为 $\rm D$ 是固定的，用 $\mu$ 代替 $\mu \rm D$​ ）。假设 $\rm D$ 是一个序列，并且（可以使用第 13.3.4 节给出的函数 $\uparrow y$ ）对任何原子 $y$ 计算 $\uparrow y: \rm D$ 的值。基于这些假设，我们将 $\mu$ 定义为函数式 $\tau$ 的最小不动点，其中函数 $\tau \mu$ 针对任何函数 $\mu$ (适用于所有表达式 $x$ 、 $x_i$ 、 $y$ 、 $y_i$ 、 $z$ 和 $w$) 的定义如下：

$$
\begin{align*}
(\tau\mu)x \equiv\space 
  &x \in \text{A} &&\to x; \\
  &x = < x_1, \dots, x_n > &&\to < \mu x_1, \dots, \mu x_n >;\\
  &x = (y:z) &&\to (\\
  &\qquad y \in \text{A}\ \And\ (\uparrow y: \text{D}) = \\\# &&\to \mu((\rho y)(\mu z)); \\
  &\qquad y \in \text{A}\ \And\ (\uparrow y: \text{D}) = w &&\to \mu(w:z);\\
  &\qquad y = < y_1, \dots, y_n > &&\to \mu(y_1 : < y, z >); \mu(\mu y:z)\\
  &);\bot
\end{align*}
$$

> The above description of $\mu$ expands the operator of an application by definitions and by metacomposition before evaluating the operand. It is assumed that predicates like " $x \in \rm A$ " in the above definition of $\tau\mu$ are $\bot$ -preserving (e.g., " $\bot \in A$ " has the value $\bot$ ) and that the conditional expression itself is also $\bot$ -preserving. Thus $(\tau\mu)\bot \equiv \bot$ and $(\tau\mu)(\bot:z) \equiv \bot$. This concludes the semantics of FFP systems. 

之前对 $\mu$ 的描述扩展了操作符的功能，使其可以在估算操作数之前根据定义和元构 (metacomposition) 进行操作。假设上述 $\tau\mu$ 定义中使用的谓词（像“ $x \in \rm A$ ”）都是 $\bot$ 保留的（比如，“ $\bot \in A$ ”的值为 $\bot$ ），且条件表达式本身也是 $\bot$ 保留的，那么 $(\tau\mu)\bot \equiv \bot$ 和 $(\tau\mu)(\bot:z) \equiv \bot$ 都得以成立。以上就是 FFP 系统的全部语义了。