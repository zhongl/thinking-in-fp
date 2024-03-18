
> Conventional programming languages are growing ever more enormous, but not stronger. Inherent defects at the most basic level cause them to be both fat and weak: their primitive word-at-a-time style of programming inherited from their common ancestor--the von Neumann computer, their close coupling of semantics to state transitions, their division of programming into a world of expressions and a world of statements, their inability to effectively use powerful combining forms for building new programs from existing ones, and their lack of useful mathematical properties for reasoning about programs.

传统的编程语言越来越庞大，但却没有变的更强大。 在最基本的层面上的固有缺陷使它们既臃肿又脆弱：它们原始地一次一字编程风格继承自其共同的祖先，即冯·诺伊曼计算机（Von Neumann Computer），它们紧密耦合语义与状态转换，它们区别对待表达式与语句，它们无力从现有程序中使用强大的组合形式来构建新的程序，它们甚至没有用于推理程序的数学性质。[^prog]

[^prog]: 程序，原文是 programs，在本文的所指并非是狭义的独立运行的程序，而是广义上的程序代码。这对理解全文至关重要。

> An alternative functional style of programming is founded on the use of combining forms for creating programs. Functional programs deal with structured data, are often nonrepetitive and nonrecursive, are hierarchically constructed, do not name their arguments, and do not require the complex machinery of procedure declarations to become generally applicable. Combining forms can use high level programs to build still higher level ones in a style not possible in conventional languages.

而另一种函数式编程风格是基于**组合形式**来创建程序的。函数式程序处理结构化数据，通常既不重复也不用循环，它是分层构建的，无需命名参数，也无需通过复杂的过程声明就能普遍应用。[^tips] **组合形式**能以传统语言不可能的方式，将高级程序构建更高级别的程序。

[^tips]: 若你对这句感到诧异，请别急于定论，毕竟这是1978年发表的。文中的观点都是针对当时编程现状而言的，不适合以当下的现状来评判。

> Associated with the functional style of programming is an algebra of programs whose variables range over programs and whose operations are combining forms. This algebra can be used to transform programs and to solve equations whose "unknowns" are programs in much the same way one transforms equations in high school algebra. These transformations are given by algebraic laws and are carried out in the same language in which programs are written. Combining forms are chosen not only for their programming power but also for the power of their associated algebraic laws. General theorems of the algebra give the detailed behavior and termination conditions for large classes of programs.

**将函数式编程风格关联起来的是一种程序的代数，其变量即是程序逻辑，其操作即是组合形式**。 这样的代数可用于变换程序并求解“未知数”为程序的方程，和高中代数中变换方程的差不多。 这些变换由代数定律给出，并使用编写程序的语言来实现。 选择组合形式不仅是因为它们的编程能力，还因为它们相关的代数定律的能力。 代数的一般定理能给出大型程序的详细行为和终止条件。

> A new class of computing systems uses the functional programming style both in its programming language and in its state transition rules. Unlike von Neumann languages, these systems have semantics loosely coupled to states--only one state transition occurs per major computation.

一类新型计算系统在其编程语言和状态转换规则中都使用函数式编程风格。 与冯·诺伊曼语言不同，这些系统的语义与状态低耦合，即每次计算只发生一次状态转换。

> Key Words and Phrases: functional programming, algebra of programs, combining forms, functional forms, programming languages, yon Neumann computers, yon Neumann languages, models of computing systems, ap- plicative computing systems, applicative state transition systems, program transformation, program correctness, program termination, metacomposition

关键词和短语：函数式编程、程序代数、组合形式、函数形式、编程语言、冯·诺伊曼计算机、冯·诺伊曼语言、计算系统模型、应用计算系统、应用状态转换系统、程序转换、程序正确性、程序终止、元组合

> Introduction 

## 介绍

> I deeply appreciate the honor of the ACM invitation to give the 1977 Turing Lecture and to publish this account of it with the details promised in the lecture. Readers wishing to see a summary of this paper should turn to Section 16, the last section.

我非常荣幸地受ACM邀请参加1977年图灵讲座，并出版了这篇演讲的记述以及讲座中承诺的细节。 希望查看本文摘要的读者应参阅第16节，即最后一节。
