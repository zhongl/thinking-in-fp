> 2. Models of Computing Systems

## 2. 计算系统的模型

> Underlying every programming language is a model of a computing system that its programs control. Some models are pure abstractions, some are represented by hardware, and others by compiling or interpretive programs. Before we examine conventional languages more closely, it is useful to make a brief survey of existing models as an introduction to the current universe of alternatives. Existing models may be crudely classified by the criteria outlined below.

每种编程语言的底层都包含着一个计算系统的模型，程序可以控制这个模型。有些模型是纯粹的抽象概念，有些由硬件表示，还有一些由编译器或解释器程序表示。在更仔细研究传统语言之前，为了让我们了解当前可替代方案的范围，对现有模型进行简要概述会很有帮助。我们可以根据以下标准粗略地对现有模型进行分类。

> 2.1 Criteria for Models 

### 2.1 模型标准

> 2.1.1 Foundations

#### 2.1.1 基础

> Is there an elegant and concise mathematical description of the model? Is it useful in proving helpful facts about the behavior of the model? Or is the model so complex that its description is bulky and of little mathematical use? 

对于模型是否存在优雅且简洁的数学描述？ 该描述是否有助于证明模型行为有效的事实？或者，该模型是否过于复杂，以至于其描述庞大且数学用途有限呢？

> 2.1.2 History sensitivity

#### 2.1.2 前序敏感性（History sensitivity）

> Does the model include a notion of storage, so that one program can save information that can affect the behavior of a later program? That is, is the model history sensitive? 

模型是否具有存储的概念，以便程序能保存影响后序程序行为的信息？也就是，模型是否是前序敏感的？

> 2.1.3 Type of semantics

#### 2.1.3 语义类型

> Does a program successively transform states (which are not programs) until a terminal state is reached (state-transition semantics)? Are states simple or complex? Or can a "program" be successively reduced to simpler "programs" to yield a final "normal form program," which is the result (reduction semantics)?

程序能否连续变换状态（，状态不是程序），直到结束（即**状态变化语义**）？状态是简单还是复杂，或者说，“程序”能否连续简化为更简单的“程序”，以产生最终的“规范形式程序”（normal form program），是哪种（即**归约语义**）？

> 2.1.4 Clarity and conceptual usefulness of programs

#### 2.1.4 程序的清晰性和概念性

> Are programs of the model clear expressions of a process or computation? Do they embody concepts that help us to formulate and reason about processes?

模型的程序能否清楚地表达过程或计算？ 该表达能否体现出有助于过程的形式化及推导的概念？


> 2.2 Classification of Models 

### 2.2 模型分类

> Using the above criteria we can crudely characterize three classes of models for computing systems--simple operational models, applicative models, and von Neumann models. 

根据上述标准，我们可以粗略地将计算系统的模型分为三类：简单操作模型，应用型模型和冯·诺伊曼模型。

> 2.2.1 Simple operational models 

#### 2.2.1 简单的操作模型

> Examples
> :	Turing machines, various automata.

例如
:	图灵机，各种自动机。
 
> Foundations
> :	concise and useful.

基础
:	简洁而有用。

> History sensitivity
> :	have storage, are history sensitive.

前序敏感性
:	拥有存储，前序敏感。

> Semantics
> :	state transition with very simple states.

语义
:	在极简状态间变换。

> Program clarity
> :	programs unclear and conceptually not helpful.

程序清晰度
:	程序不清晰，在概念上没有用。


> 2.2.2 Applicative models 

#### 2.2.2 应用型模型

> Examples
> :	Church's lambda calculus[^5], Curry's system of combinators[^6], pure Lisp[^17], functional programming systems described in this paper.

例如
:	邱奇的Lambda演算[^5]，Curry的组合系统[^6]，纯LISP[^17]，本文提到的函数式编程系统。

> Foundations
> :	concise and useful.

基础
:	简洁而有用。

> History sensitivity
> :	no storage, not history sensitive.

前序敏感性
:	没有存储，前序不敏感。

> Semantics
> :	reduction semantics, no states.

语义
:	归约语义，无状态。

> Program clarity
> :	programs can be clear and conceptually useful.

程序清晰度
:	程序可清晰，在概念上有用。

[^5]: [Church, A. The Calculi of Lambda-Conversion. Princeton U. Press, Princeton, N.J., 1941.](https://dl.acm.org/doi/10.5555/1096495)
[^6]: [Curry, H.B., and Feys, R. Combinatory Logic, Vol. 1. North- Holland Pub. Co., Amsterdam, 1958.](http://scholar.google.com/scholar?hl=en&q=Curry%2C+H.B.%2C+and+Feys%2C+R.+Combinatory+Logic%2C+Vol.+1.+North-+Holland+Pub.+Co.%2C+Amsterdam%2C+1958.)
[^17]: [McCarthy, J. Recursive functions of symbolic expressions and their computation by machine, Pt. 1. Comm. ,4CM 3, 4 (April 1960), 184-195.](https://dl.acm.org/doi/10.1145/367177.367199) 

> 2.2.3 Von Neumann models

#### 2.2.3 冯·诺伊曼模型 

> Examples
> :	von Neumann computers, conventional programming languages.

例如
:	冯·诺伊曼计算机，传统编程语言。

> Foundations
> :	complex, bulky, not useful.

基础
:	复杂，笨重，无用。

> History sensitivity
> :	have storage, are history sensitive.

前序敏感性
:	拥有存储，前序敏感。

> Semantics
> :	state transition with complex states.

语义
:	复杂状态间变换。

> Program clarity
> :	programs can be moderately clear, are not very useful conceptually.

程序清晰度
:	程序可以适度清晰，在概念上不是很有用。


> The above classification is admittedly crude and debatable. Some recent models may not fit easily into any of these categories. For example, the data-flow languages developed by Arvind and Gostelow [^1], Dennis [^7], Kosinski [^13], and others partly fit the class of simple operational models, but their programs are clearer than those of earlier models in the class and it is perhaps possible to argue that some have reduction semantics. In any event, this classification will serve as a crude map of the territory to be discussed. We shall be concerned only with applicative and von Neumann models. 

诚然，上述的分类是粗略地，有待商榷地。 一些最近的模型可能不容易归类其中。 例如，由Arvind和Gostelow开发的数据流语言[^1]，Dennis [^7]，Kosinski [^13]，以及其他人部分满足简单操作模型，但它们的程序比同类之前的模型更清晰，或许能勉强算得上归约语义。 无论如何，这个分类只是一个大框架性的讨论。 我们应该将焦点放在应用型模型和冯·诺伊曼模型上。

[^1]:  [Arvind, and Gostelow, K.P. A new interpreter for data flow schemas and its implications for computer architecture. Tech. Rep. No. 72, Dept. Comptr. Sci., U. of California, Irvine, Oct. 1975.](http://scholar.google.com/scholar?hl=en&q=Arvind%2C+and+Gostelow%2C+K.P.+A+new+interpreter+for+data+flow+schemas+and+its+implications+for+computer+architecture.+Tech.+Rep.+No.+72%2C+Dept.+Comptr.+Sci.%2C+U.+of+California%2C+Irvine%2C+Oct.+1975.)
[^7]:  [Dennis, J.B. First version of a data flow procedure language. Tech. Mem. No. 61, Lab. for Comptr. Sci., M.I.T., Cambridge, Mass., May 1973.](http://scholar.google.com/scholar?hl=en&q=Dennis%2C+J.B.+First+version+of+a+data+flow+procedure+language.+Tech.+Mem.+No.+61%2C+Lab.+for+Comptr.+Sci.%2C+M.I.T.%2C+Cambridge%2C+Mass.%2C+May+1973.)
[^13]:  [Kosinski, P. A data flow programming language. Rep. RC 4264, IBM T.J. Watson Research Ctr., Yorktown Heights, N.Y., March 1973.](http://scholar.google.com/scholar?hl=en&q=Kosinski%2C+P.+A+data+flow+programming+language.+Rep.+RC+4264%2C+IBM+T.J.+Watson+Research+Ctr.%2C+Yorktown+Heights%2C+N.Y.%2C+March+1973.)
