> 9. Von Neumann Languages Lack Useful Mathematical Properties 

## 9. 冯·诺伊曼语言缺乏有用的数学性质

> So far we have discussed the gross size and inflexibility of von Neumann languages; another important defect is their lack of useful mathematical properties and the obstacles they present to reasoning about programs. Although a great amount of excellent work has been published on proving facts about programs, von Neumann languages have almost no properties that are helpful in this direction and have many properties that are obstacles (e.g., side effects, aliasing).

我们已经讨论了冯·诺伊曼语言的庞大和缺乏灵活性；另一个重要缺陷是它们不仅缺乏用于程序推理的有用数学性质，还对推理造成阻碍。尽管已经发表了许多关于证明程序事实的优秀著作，然而冯·诺伊曼语言几乎没有利于该方向的性质，反倒是拥有许多障碍特性（例如，副作用、别名）。

> Denotational semantics [^23] and its foundations [^20] [^21] provide an extremely helpful mathematical understanding of the domain and function spaces implicit in programs. When applied to an applicative language (such as that of the "recursive programs" of [^16]), its foundations provide powerful tools for describing the language and for proving properties of programs. When applied to a von Neumann language, on the other hand, it provides a precise semantic description and is helpful in identifying trouble spots in the language. But the complexity of the language is mirrored in the complexity of the description, which is a bewildering collection of productions, domains, functions, and equations that is only slightly more helpful in proving facts about programs than the reference manual of the language, since it is less ambiguous. 

指称语义学 [^23] 及其基础 [^20] [^21] 提供了一种非常有用的数学方法，可以理解程序中隐含的域 (domain) 和函数空间。当应用于应用型语言（例如引用文献[^16] 中的“递归程序”）时，它的基础为描述语言和证明程序性质提供了强大的工具。另一方面，当应用于冯·诺伊曼语言时，它可以提供精确的语义描述，并有助于识别语言中的问题所在。但是，语言的复杂性会体现在描述的复杂性上，它由一系列令人困惑的产生式（Production）、域、函数和方程组成，在证明程序事实方面仅比语言的参考手册略有帮助，因为它是更少歧义的。

[^16]: [Manna, Z., Ness, S., and Vuillemin, J. Inductive methods for proving properties of programs. Comm.4 CM 16,8 (Aug. 1973) 491-502.](https://dl.acm.org/doi/abs/10.1145/800235.807070)
[^20]: [Reynolds, J.C. Notes on a lattice-theoretic approach to the theory of computation. Dept. Syst. and Inform. Sci., Syracuse U., Syracuse, N.Y., 1972](http://scholar.google.com/scholar?hl=en&q=Reynolds%2C+J.C.+Notes+on+a+lattice-theoretic+approach+to+the+theory+of+computation.+Dept.+Syst.+and+Inform.+Sci.%2C+Syracuse+U.%2C+Syracuse%2C+N.Y.%2C+1972.)
[^21]: [Scott, D. Outline of a mathematical theory of computation. Proc. 4th Princeton Conf. on Inform. Sci. and Syst., 1970.](http://scholar.google.com/scholar?hl=en&q=Scott%2C+D.+Outline+of+a+mathematical+theory+of+computation.+Proc.+4th+Princeton+Conf.+on+Inform.+Sci.+and+Syst.%2C+1970.)
[^23]: [Scott, D., and Strachey, C. Towards a mathematical semantics for computer languages. Proc. Symp. on Comptrs. and Automata, Polytechnic Inst. of Brooklyn, 1971.](http://scholar.google.com/scholar?hl=en&q=Scott%2C+D.%2C+and+Strachey%2C+C.+Towards+a+mathematical+semantics+for+computer+languages.+Proc.+Symp.+on+Comptrs.+and+Automata%2C+Polytechnic+Inst.+of+Brooklyn%2C+1971.)

> Axiomatic semantics [^11] precisely restates the inelegant properties of von Neumann programs (i.e., transformations on states) as transformations on predicates. The word-at-a-time, repetitive game is not thereby changed, merely the playing field. The complexity of this axiomatic game of proving facts about von Neumann programs makes the successes of its practitioners all the more admirable. Their success rests on two factors in addition to their ingenuity: First, the game is restricted to small, weak subsets of full von Neumann languages that have states vastly simpler than real ones. Second, the new playing field (predicates and their transformations) is richer, more orderly and effective than the old (states and their transformations). But restricting the game and transferring it to a more effective domain does not enable it to handle real programs (with the necessary complexities of procedure calls and aliasing), nor does it eliminate the clumsy properties of the basic von Neumann style. As axiomatic semantics is extended to cover more of a typical von Neumann language, it begins to lose its effectiveness with the increasing complexity that is required. 

公理语义学[^11]将冯·诺伊曼程序 (通过状态转换) 的非优雅性质精确地重新表述为谓词 (predicate) 的转换。逐字处理、重复的游戏并没有因此改变，只是改变了赛场。证明冯·诺伊曼程序事实的公理游戏非常复杂，这使得实践者的成功更加令人钦佩。他们的成功除了才智之外，还依赖于两个因素：首先，游戏仅限于冯·诺伊曼语言的较小、较弱的子集，这些子集的状态比现实世界的状态简单得多。其次，新的赛场（谓词及其转换）比旧的赛场（状态及其转换）更丰富、更有序、更有效。但是，限制游戏范围并转移到更有效的领域并不能处理真实程序（具有必要的过程调用和别名复杂性），也不能消除冯诺·伊曼风格的基本笨拙特性。随着公理语义学扩展到涵盖更多典型的冯诺伊曼语言，其有效性会随着所需复杂性的增加而丧失。

[^11]: [Hoare, C.A.R. An axiomatic basis for computer programming. Comm. ,4CM 12, 10 (Oct. 1969), 576-583.](https://dl.acm.org/doi/10.1145/363235.363259)

> Thus denotational and axiomatic semantics are descriptive formalisms whose foundations embody elegant and powerful concepts; but using them to describe a von Neumann language can not produce an elegant and powerful language any more than the use of elegant and modem machines to build an Edsel can produce an elegant and modem car.

因此，指称语义学和公理语义学都是描述性的形式论，其基础包含着优雅而强大的概念。但是，用它们来描述冯诺伊曼语言并不能创造出优雅强大的语言，就像即便使用先进的机器制造 Edsel [^edsel] 也造不出优雅现代的汽车一样。

[^edsel]: <https://en.wikipedia.org/wiki/Edsel>

> In any case, proofs about programs use the language of logic, not the language of programming. Proofs talk about programs but cannot involve them directly since the axioms of von Neumann languages are so unusable. In contrast, many ordinary proofs are derived by algebraic methods. These methods require a language that has certain algebraic properties. Algebraic laws can then be used in a rather mechanical way to transform a problem into its solution. For example, to solve the equation 

无论如何，程序的证明使用的是逻辑语言，而不是编程语言。证明可以讨论程序，但由于冯·诺伊曼语言的公理如此难以使用，所以不能直接涉及程序本身。相比之下，许多普通的证明都由代数方法得出的。这些方法需要一种具有某些代数性质的语言。然后可以用代数定律以一种相当机械的方式将问题求解。比如，求解如下方程

$$
ax + bx = a + b
$$

> for $x$ (given that $a+b \not = \textit{0}$ ), we mechanically apply the distributive, identity, and cancellation laws, in succession, to obtain

对于 $x$ （假设 $a+b \not = \textit{0}$ ），我们依次使用分配律、幺元律和消去律，机械地将其变形得到

$$
\begin{aligned}
(a + b) x &= a + b\\
(a + b) x &= (a + b) \textit{1}\\
x &= \textit{1}
\end{aligned}
$$

> Thus we have proved that $x = \textit{1}$ without leaving the "language" of algebra. Von Neumann languages, with their grotesque syntax, offer few such possibilities for transforming programs.

因此，我们完全使用代数的“语言”证明了 $x = \textit{1}$ 。冯·诺伊曼语言由于其怪异的语法，无法像代数那样方便地进行程序变换。

As we shall see later, programs can be expressed in a language that has an associated algebra. This algebra can be used to transform programs and to solve some equations whose "unknowns" are programs, in much the same way one solves equations in high school algebra. Algebraic transformations and proofs use the language of the programs themselves, rather than the language of logic, which talks about programs.

正如我们稍后将看到的，程序可以用一种具有相关代数的语言来表达。这种代数可以用来变换程序，并解决一些未知数是程序的方程，就像高中代数解方程一样。代数变换和证明使用程序本身的语言，而不是谈论程序的逻辑语言。
