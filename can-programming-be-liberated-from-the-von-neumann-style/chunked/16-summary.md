> 16 . Summary

## 16. 总结

> The fifteen preceding sections of this paper can be summarized as follows. 

之前本文十五部分的总结如下：

> **Section 1**. Conventional programming languages are large, complex, and inflexible. Their limited expressive power is inadequate to justify their size and cost. 

### 第 1 节

传统编程语言庞大、复杂且缺乏灵活性。它们有限的表达能力不足以证明其规模和成本的合理性。

> **Section 2**. The models of computing systems that underlie programming languages fall roughly into three classes: (a) simple operational models (e.g., Turing machines), (b) applicative models (e.g., the lambda calculus), and (c) von Neumann models (e.g., conventional computers and programming languages). Each class of models has an important difficulty: The programs of class (a) are inscrutable; class (b) models cannot save information from one program to the next; class (c) models  have unusable foundations and programs that are conceptually unhelpful. 

### 第 2 节

支持编程语言的计算系统模型大致可分为三类：

1. 简单操作模型（例如，图灵机），
2. 应用型模型（例如，lambda 演算），
3. 冯·诺伊曼模型（例如，传统计算机和编程语言）。

每类模型都存在一个重要难点：

1. 第一类模型的程序难以理解；
2. 第二类模型无法将信息的保存从一个程序传递到下一个程序；
3. 第三类模型的基础难以使用，并且程序在概念上无益。

> **Section 3**. Von Neumann computers are built around a bottleneck: the word-at-a-time tube connecting the CPU and the store. Since a program must make its overall change in the store by pumping vast numbers of words back and forth through the von Neumann bottleneck, we have grown up with a style of programming that concerns itself with this word-at-a-time traffic through the bottleneck rather than with the larger conceptual units of our problems

### 第 3 节

冯·诺依曼计算机围是绕着一个瓶颈构建的，即，连接中央处理器和存储器的逐字传输管道。由于程序必须通过冯·诺依曼瓶颈大量地将单词前后传输来整体改变存储器中的内容，因此我们养成了关注通过瓶颈的逐字传输进行编程的风格，而不关注问题本身，这个更大的概念单元。

> **Section 4**. Conventional languages are based on the programming style of the von Neumann computer. Thus variables $=$ storage cells; assignment statements $=$ fetching, storing, and arithmetic; control statements $=$ jump and test instructions. The symbol " $:=$ " is the linguistic von Neumann bottleneck. Programming in a conventional--von Neumann--language still concerns itself with the word-at-a-time traffic through this slightly more sophisticated bottleneck. Von Neumann languages also split programming into a world of expressions and a world of statements; the first of these is an orderly world, the second is a  disorderly one, a  world that structured programming has simplified somewhat, but without attacking the basic problems of the split itself and of the word-at-a-time style of conventional languages.

### 第 4 节  

传统语言是基于冯·诺依曼机的编程风格的。因此，变量对应存储单元；赋值语句对应获取、存储和算术运算；控制语句对应跳转和测试指令。符号“:=” 是语言层面的冯·诺依曼瓶颈。传统（冯·诺依曼语言）编程，始终聚焦在如何经由这个稍微更复杂的瓶颈进行的逐字传输。冯·诺依曼语言也将编程分为表达式的世界和语句的世界；前者是一个有序的世界，后者是一个无序的世界，结构化编程在一定程度上简化了它，但并没有解决分裂本身和传统语言逐字风格的基本问题。

> **Section 5**. This section compares a von Neumann program and a functional program for inner product. It illustrates a number of problems of the former and advantages of the latter: e.g., the von Neumann program is repetitive and word-at-a-time, works only for  two vectors named $a$ and $b$ of a given length $n$, and can only be made general by use of a procedure declaration, which has complex semantics. The functional program is nonrepetitive, deals with vectors as units, is more hierarchically constructed, is completely general, and creates "housekeeping" operations by composing highlevel housekeeping operators. It does not name its arguments, hence it requires no procedure declaration. 

### 第 5 节

这一节比较了计算内积的冯·诺依曼程序和函数式程序，并说明前者的若干问题和后者的优势：例如，冯·诺依曼程序是重复的逐字操作，只适用于给定长度 $n$ 的名为 $a$ 和 $b$ 的两个向量，并且只能通过使用具有复杂语义的过程声明来使其通用。函数式程序是非重复的，将向量作为一个整体处理，具有更层次化的结构，完全通用，并且通过组合高级收拾操作符来创建“收拾”操作。它不用命名其参数，因此不需要过程声明。

> **Section 6**. A programming language comprises a framework plus some changeable parts. The framework of a von Neumann language requires that most features must be built into it; it can accommodate only limited changeable parts (e.g., user-defined procedures) because there must be detailed provisions in the "state" and its transition rules for all the needs of the changeable parts, as well as for all the features built into the framework. The reason the von Neumann framework is so inflexible is that its semantics is too closely coupled to the state: every detail of a  computation changes the state. 

### 第 6 节

一门编程语言包含框架和一些可变部分。冯·诺依曼语言的框架要求大多数特性都必须内置其中；它只能容纳有限的可变部分（例如用户定义的过程），因为“状态”及其转换规则中必须为可变部分的所有需求提供详细的规定，并内置的所有特性到框架中。冯·诺依曼框架如此缺乏灵活性，原因在于它的语义与状态耦合得太紧密：计算的每一个细节都会改变状态。

> **Section 7**. The changeable parts of von Neumann languages have little expressive power; this is why most of the language must be built into the framework. The lack of expressive power results from the inability of von Neumann languages to effectively use combining forms for building programs, which in turn results from the split between expressions and statements. Combining forms are at their best in expressions, but in von Neumann languages an expression can only produce a single word; hence expressive power in the world of expressions is mostly lost. A further obstacle to the use of combining forms is the elaborate use of naming conventions. 

#### 第 7 节

冯·诺依曼语言的可变部分表达能力较弱，这就是为什么大多数语言特性必须内置于框架中的原因。表达能力的缺乏源于冯·诺依曼语言无法有效地使用组合形式来构建程序，这又是由表达式和语句的分割所导致。组合形式能在表达式中发挥最佳的作用，但在冯·诺依曼语言中，表达式只能产生单字。因此，表达式世界中的表达能力大部分都消失了，而滥用命名约定又进一步阻碍了组合形式的使用。

> **Section 8**. APL is the first language not based on the lambda calculus that is not word-at-a-time and uses functional combining forms. But it still retains many of the problems of von Neumann languages. 

### 第 8 节

APL 是第一种非基于 lambda 演算、非逐字处理并且使用函数式组合形式的语言。但它仍然保留了许多冯·诺依曼语言的问题。

> **Section 9**. Von Neumann languages do not have useful properties for reasoning about programs. Axiomatic and denotational semantics are precise tools for describing and understanding conventional programs, but they only talk about them and cannot alter their ungainly properties. Unlike von Neumann languages, the language of ordinary algebra is suitable both for stating its laws and for transforming an equation into its solution, all within the "language." 

### 第 9 节

冯·诺依曼语言不具备用于程序推理的有用性质。公理语义和指称语义依旧是描述和理解传统程序的精确工具，但它们只能描述程序，无法改变程序笨拙的性质。与冯·诺依曼语言不同的是，普通代数语言既适合陈述其定律，又适合将方程转换为其解，所有这些都可以在“语言”之内完成。

> **Section 10**. In a history-sensitive language, a program can affect the behavior of a subsequent one by changing some store which is saved by the system. Any such language requires some kind of state transition semantics. But it does not need semantics closely coupled to states in which the state changes with every detail of the computation. "Applicative state transition" (AST) systems are proposed as history-sensitive alternatives to von Neumann systems. These have: (a) loosely coupled state-transition semantics in which a transition occurs once per major computation; (b) simple states and transition rules; (c) an underlying applicative system with simple "reduction" semantics; and (d) a programming language and state transition rules both based on the underlying applicative system and its semantics. The next four sections describe the elements of this approach to non-von Neumann language and system design.

### 第 10 节

在前序敏感型语言中，程序可以通过改变系统的存储来影响后续程序的行为。任何这样的语言都需要某种状态转换语义，但它并不需要与状态紧密耦合的语义，即计算的每一个细节都会改变状态。“应用型状态转换 (AST)”系统被提议作为冯·诺依曼系统的前序敏感的替代方案。它们具有以下特点：

1. 松散耦合的状态转换语义，其中一次主要计算发生一次转换；
2. 简单状态和转换规则；
3. 底层的应用型系统具有简单的“规约”语义；
4. 编程语言和状态转换规则，均基于底层应用型系统及其语义。
 
接下来的四节将描述这种非冯诺依曼语言和系统设计方法的元素。

> **Section 11**. A class of informal functional programming (FP) systems is described which use no variables. Each system is built from objects, functions, functional forms, and definitions. Functions map objects into objects. Functional forms combine existing functions to form new ones. This section lists examples of primitive functions and functional forms and gives sample programs. It discusses the limitations and advantages of FP systems. 

#### 第 11 节

描述了一类非正式的函数式编程 (FP) 系统，它们不使用变量。每个系统都由对象、函数、函数式和定义构建。函数将对象映射到对象。函数式组合现有函数以形成新的函数。本节列举了原始函数和函数式的例子，并给出了示例程序，用以讨论了 FP 系统的局限性和优势。

> **Section 12**. An "algebra of programs" is described whose variables range over the functions of an FP system and whose "operations" are the functional forms of the system. A list of some twenty-four laws of the algebra is followed by an example proving the equivalence of a nonrepetitive matrix multiplication program and a recursive one. The next subsection states the results of two "expansion theorems" that "solve" two classes of equations. These solutions express the "unknown" function in such equations as an infinite conditional expansion that constitutes a case-by-case description of its behavior and immediately gives the necessary and sufficient conditions for termination. These results are used to derive a "recursion theorem" and an "iteration theorem," which provide ready-made expansions for some moderately general and useful classes of "linear" equations. Examples of the use of these theorems treat: (a) correctness proofs for recursive and iterative factorial functions, and (b) a proof of equivalence of two iterative programs. A final example deals with a "quadratic" equation and proves that its solution is an idempotent function. The next subsection gives the proofs of the two expansion theorems. 
> 
> The algebra associated with FP systems is compared with the corresponding algebras for the lambda calculus and other applicative systems. The comparison shows some advantages to be drawn from the severely restricted FP systems, as compared with the much more powerful classical systems. Questions are suggested about algorithmic reduction of functions to infinite expansions and about the use of the algebra in various "lazy evaluation" schemes. 

### 第 12 节

描述了一个“程序代数”，它的变量是 FP 系统的函数，它的“操作”是系统的函数式。在列出大约 24 个代数定律之后，通过一个例子证明了，非重复矩阵乘法程序和递归程序的等价性。接下来的小节陈述了两个“展开定理”的结果，它们“解决”了两类方程。这些解将方程中的“未知”函数表示为一个无限条件展开，以逐案例地描述其行为，以及立即终止的必要和充分条件。这些结果可用于推导“递归定理”和“迭代定理”，而这些定理又为一些中等通用且有用的“线性”方程类别提供了现成的展开式。其使用示例包括：

1. 递归和迭代阶乘函数的正确性证明，以及
2. 两个迭代程序的等价性证明；
3. 最后一个例子处理了“二次”方程，还证明其解是一个幂等函数。

随后的子小节给出两个展开定理的证明。

在对比了 FP 系统 和 lambda 演算及其它应用型系统的代数后，不难发现与更强大的经典系统相比，严格限制的 FP 系统是具有一些优势的。此外，还提到了一些关于函数到无限展开式的算法归约，以及代数在各种“惰性求值”方案上的问题。

> **Section 13**. This section describes formal functional programming (FFP) systems that extend and make precise the behavior of FP systems. Their semantics are simpler than that of classical systems and can be shown to be consistent by a simple fixed-point argument. 

### 第 13 节  

描述了形式化函数式编程 (FFP) 系统，它扩展并精确了 FP 系统的行为。它们的语义比经典系统更简单，并且可以通过简单的固定点论证证明其一致性。

> **Section 14**. This section compares the structure of Algol with that of applicative state transition (AST) systems. It describes an AST system using an FFP system as its applicative subsystem. It describes the simple state and the transition rules for the system. A small self-protecting system program for the AST system is described, and how it can be installed and used for file maintenance and for running user programs. The section briefly discusses variants of AST systems and functional naming systems that can be defined and used within an AST system.

### 第 14 节

这一节将 Algol 的结构与应用型状态转换 (AST) 系统的结构进行比较，并描述了一个使用 FFP 系统作为其应用型子系统的 AST 系统，及其系统的简单状态和转换规则。此外，还描述了一个用于 AST 系统的小型自保护系统程序，以及如何安装和使用它进行文件维护和运行用户程序。最后，本节简要讨论了可以在 AST 系统内定义和使用的 AST 系统变体和函数式命名系统。

> **Section 15**. This section briefly discusses work on applicative computer designs and the need to develop and test more practical models of applicative systems as the future basis for such designs.

### 第 15 节

这一节概述了应用型计算机设计方面的工作，以及开发和测试更实用的应用型系统模型作为未来此类设计基础的必要性。

