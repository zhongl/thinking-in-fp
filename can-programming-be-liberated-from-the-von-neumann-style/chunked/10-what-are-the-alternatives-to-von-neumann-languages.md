> 10. What Are the Alternatives to von Neumann Languages? 

## 10. 冯·诺伊曼语言替代方案是什么？

> Before discussing alternatives to von Neumann languages, let me remark that I regret the need for the above negative and not very precise discussion of these languages. But the complacent acceptance most of us give to these enormous, weak languages has puzzled and disturbed me for a long time. I am disturbed because that acceptance has consumed a vast effort toward making von Neumann languages fatter that might have been better spent in looking for new structures. For this reason I have tried to analyze some of the basic defects of conventional languages and show that those defects cannot be resolved unless we discover a new kind of language framework.

在讨论冯诺伊曼语言的替代方案之前，我想先对上面关于这些语言的负面且不够精确的讨论表示歉意。但是，我们大多数人对这些庞大而薄弱的语言所表现出的满足接受让我困惑和不安了很长时间。我不安的是，大家花在去扩展冯·诺伊曼语言的力气，本可以用在寻找新的语言结构上。因此，我试图分析传统语言的一些基本缺陷，并表明如果不发现一种新的语言框架，这些缺陷就无法解决。

> In seeking an alternative to conventional languages we must first recognize that a system cannot be history sensitive (permit execution of one program to affect the behavior of a subsequent one) unless the system has some kind of state (which the first program can change and the second can access). Thus a history-sensitive model of a computing system must have a state-transition semantics, at least in this weak sense. But this does not mean that every computation must depend heavily on a complex state, with many state changes required for each small part of the computation (as in von Neumann languages). 

在寻找传统语言的替代方案时，我们首先必须认识到，除非系统具有一些状态（第一个程序可以改变，第二个程序可以访问），否则系统就不可能是前序敏感的（允许一个程序的执行影响后续程序的行为）。因此，一个前序敏感的计算系统模型必须具有“状态转换语义”，哪怕是最弱的形式。但这并不意味着每个计算都必须严重依赖于复杂的状态，也不意味着每个计算的微小部分都需要大量的状态变化（就像冯·诺伊曼语言那样）。

> To illustrate some alternatives to von Neumann languages, I propose to sketch a class of history-sensitive computing systems, where each system: 
> a) has a loosely coupled state-transition semantics in which a state transition occurs only once in a major computation; 
> b) has a simply structured state and simple transition rules; 
> c) depends heavily on an underlying applicative system both to provide the basic programming language of the system and to describe its state transitions. 

为了展示冯诺伊曼语言的一些替代方案，我建议概述一类前序敏感的计算系统，每个系统都具有以下特点：

1. 具有松散耦合的状态转换语义，即主要计算过程中只会发生一次状态转换；
2. 具有结构简单的状态和简单的转换规则；
3. 重度依赖于底层的应用型系统，该系统既提供基本的编程语言，又描述其状态转换。

> These systems, which I call applicative state transition (or AST) systems, are described in Section 14. These simple systems avoid many of the complexities and weaknesses of von Neumann languages and provide for a powerful and extensive set of changeable parts. However, they are sketched only as crude examples of a vast area of non-von Neumann systems with various attractive properties. I have been studying this area for the past three or four years and have not yet found a satisfying solution to the many conflicting requirements that a good language must resolve. But I believe this search has indicated a useful approach to designing non-von Neumann languages.

这些系统，我称之为应用型状态转换 (AST) 系统，将在第 14 节进行描述。这些简单的系统避免了冯诺伊曼语言的许多复杂性和缺陷，并提供了一套强大且可扩展的可变部分。然而，它们只是非冯·诺伊曼系统领域中各种具有吸引力的性质的粗略示例。过去三四年的时间里，我一直在研究这个领域，但还没有找到一个令人满意的解决方案，去处理好许多相互冲突的要求，这是一个好的语言必须做到的。但我相信，这种探索指明了一种设计非冯·诺伊曼语言的有效方法。

> This approach involves four elements, which can be summarized as follows.

这个方法涉及四个要素，总结如下：

> a) *A functional style of programming without variables*. A simple, informal functional programming (FP) system is described. It is based on the use of combining forms for building programs. Several programs are given to illustrate functional programming. 
> 
> b) *An algebra of functional programs*. An algebra is described whose variables denote FP functional programs and whose "operations" are FP functional forms, the combining forms of FP programs. Some laws of the algebra are given. Theorems and examples are given that show how certain function expressions may be transformed into equivalent infinite expansions that explain the behavior of the function. The FP algebra is compared with algebras associated with the classical applicative systems of Church and Curry. 
> 
> c) *A formal functional programming system*. A formal (FFP) system is described that extends the capabilities of the above informal FP systems. An FFP system is thus a precisely defined system that provides the ability to use the functional programming style of FP systems and their algebra of programs. FFP systems can be used as the basis for applicative state transition systems. 
> 
> d) *Applicative state transition systems*. As discussed above. The rest of the paper describes these four elements, gives some brief remarks on computer design, and ends with a summary of the paper. 

1. *无变量的函数式编程风格*。这是一种简单非正式的函数式编程 (FP) 系统。它基于使用组合形式 (combining forms) 构建程序。后文会提供了几个程序示例来说明函数式编程。
2. *函数程序的代数*。这种代数，其变量表示 FP 的程序，其“运算”是 FP 的形式，即 FP 程序的组合形式。会有一些代数的定律。给定的定理和示例，将呈现如何把某些函数表达式转换为等价的无限展开式，以解释函数的行为。还会将 FP 的代数，与经典的 Church 和 Curry 应用型系统相关代数，进行比较。
3. *形式化函数式编程系统*。这样正式的（FFP）系统，扩展了非正式函数式编程系统的能力。它也是一个定义明确的系统，提供了使用函数式编程风格及其程序代数的能力。它还是应用型状态转换系统的基础。
4. *应用型状态转换系统*。如上所述。论文的其余部分描述了这四个要素，并对计算机设计做了一些简要评论，最后以论文摘要结尾。
