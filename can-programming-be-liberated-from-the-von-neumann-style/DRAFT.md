---
title: "Can Programming Be Liberated from the von Neumann Style? A Functional Style and Its Algebra of Programs"
author: "John Backus"
origin: https://dl.acm.org/doi/epdf/10.1145/359576.359579
---

> The 1977 ACM Turing Award was presented to John Backus at the ACM Annual Conference in Seattle, October 17. In introducing the recipient, Jean E. Sammet, Chairman of the Awards Committee, made the following comments and read a portion of the final citation. The full announcement is in the September 1977 issue of Communications,page 681.

1977年的ACM图灵奖在10月17日在西雅图举行的ACM年度会议上颁发给John Backus。在介绍他时，奖项评委会主席Jean E. Sammet发表了如下评论，并宣读了最终表彰的部分原文。 其完整的内容刊登在同年9月的《通讯》第681页。[^681]

[^681]: https://dl.acm.org/doi/10.1145/359810.1232487

> "Probably there is nobody in the room who has not heard of Fortran and most of you have probably used it at least once, or at least looked over the shoulder of someone who was writing a Fortran program. There are probably almost as many people who have heard the letters BNF but don't necessarily know what they stand for. Well, the B is for Backus, and the other letters are explained in the formal citation. These two contributions, in my opinion, are among the half dozen most important technical contributions to the computer field and both were made by John Backus (which in the Fortran case also involved some colleagues). It is for these contributions that he is receiving this year's Turing award.

“可能房间里无人不知 Fortran[^fortran]，而且你们中的大多数可能都使用过，又或者至少在人身后看过编写的 Fortran 程序。可能同样多的人都听过字母 BNF，但不一定知道它们都代表什么。嗯，B 代表就是 Backus，其他字母在正式表彰中都有解释[^bnf]。在我看来，它们是计算机领域最重要的六个技术贡献之二， 且都是出自 John Backus（以及一些参与到 Fortran 的同事）之手 。正是由于这些贡献，他获得了今年的图灵奖。

[^fortran]: https://fortran-lang.org/
[^bnf]: https://en.wikipedia.org/wiki/Backus%E2%80%93Naur_form

> The short form of his citation is for 'profound, influential, and lasting contributions to the design of practical high-level programming systems, notably through his work on Fortran, and for seminal publication of formal procedures for the specifications of programming languages.'

对他的表彰有这么一句简述，‘他在 Fortran 语言上的成果，以及编程语言规范形式化的创举，对实用高级编程系统产生了深刻，巨大且长期的影响’

> The most significant part of the full citation is as follows:

完整表彰中最重要的部分如下：

> '... Backus headed a small IBM group in New York City during the early 1950s. The earliest product of this group's efforts was a high-level language for scientific and technical computations called Fortran. This same group designed the first system to translate Fortran programs into machine language. They employed novel optimizing techniques to generate fast machine-language programs. Many other compilers for the language were developed, first on IBM machines, and later on virtually every make of computer. Fortran was adopted as a U.S. national standard in 1966.

‘... 上世纪50年代早期 Backus 在纽约市领导了一个IBM小组。该小组致力于研发的最早产品是一种服务于科学与技术计算的高级语言，名为 Fortran 。也是这个小组设计了第一个将 Fortran 程序转化为机器语言的系统。他们采用了新颖的优化技术来生成快速的机器语言程序。 此后众多这个语言的编译器被开发出来，并率先于IBM机器应用，再扩展到所有计算机上。 Fortran 也于 1966 年被列为美国国家标准。

> During the latter part of the 1950s, Backus served on the international committees which developed Algol 58 and a later version, Algol 60. The language Algol, and its derivative compilers, received broad acceptance in Europe as a means for developing programs and as a formal means of publishing the algorithms on which the programs are based.

在1950年代后期，Backus 效力于国际委员会，期间研发了 Algol 58 以及后继版本 Algol 60。Algol 语言及其衍生编译器，作为一种开发程序的方式，和在此之上发布算法的正式手段，在欧洲获得广泛的认可。

> In 1959, Backus presented a paper at the UNESCO conference in Paris on the syntax and semantics of a proposed international algebraic language. In this paper, he was the first to employ a formal technique for specifying the syntax of programming languages. The formal notation became known as BNF-standing for "Backus Normal Form," or "Backus Naur Form" to recognize the further contributions by Peter Naur of Denmark.

1959年，Backus 在巴黎的联合国教科文组织会议上发表了一篇论文，涉及拟议的国际代数语言的语法和语义。在本文中，他是第一个采用形式化技术来指定编程语言语法的人。这种形式符号系统俗称 BNF，全称 Backus Normal Form， 又或是因丹麦的Peter Naur的进一步贡献而得名的 Backus Naur Form 。

> Thus, Backus has contributed strongly both to the pragmatic world of problem-solving on computers and to the theoretical world existing at the interface between artificial languages and computational linguistics. Fortran remains one of the most widely used programming languages in the world. Almost all programming languages are now described with some type of formal syntactic definition.' "

因此，无论是在计算机上解决问题的现实世界，还是在人工语言与计算语言交互之间的理论世界，Backus 的贡献都是巨大的。Fortran 仍然是世界上使用最广泛的编程语言之一。 现在，几乎所有编程语言都用某种形式的句法定义来描述。’”

> # Can Programming Be Liberated from the von Neumann Style? A Functional Style and Its Algebra of Programs

# 编程可以从冯·诺伊曼风格中解放出来吗？一种函数式风格及其程序的代数

> Conventional programming languages are growing ever more enormous, but not stronger. Inherent defects at the most basic level cause them to be both fat and weak: their primitive word-at-a-time style of programming inherited from their common ancestor--the von Neumann computer, their close coupling of semantics to state transitions, their division of programming into a world of expressions and a world of statements, their inability to effectively use powerful combining forms for building new programs from existing ones, and their lack of useful mathematical properties for reasoning about programs.

传统的编程语言越来越庞大，但却没有变的更强大。 在最基本的层面上的固有缺陷使它们既臃肿又脆弱：它们原始地一次一字编程风格继承自其共同的祖先，即冯·诺伊曼计算机（Von Neumann Computer），它们紧密耦合语义与状态转换，它们区别对待表达式与语句，它们无力从现有程序中使用强大的组合形式来构建新的程序，它们甚至没有用于推理程序的数学性质。[^prog]

[^prog]: 程序，原文是 programs，在本文的所指并非是狭义的独立运行的程序，而是广义的计算表达式。这对理解全文至关重要。

> An alternative functional style of programming is founded on the use of combining forms for creating programs. Functional programs deal with structured data, are often nonrepetitive and nonrecursive, are hierarchically constructed, do not name their arguments, and do not require the complex machinery of procedure declarations to become generally applicable. Combining forms can use high level programs to build still higher level ones in a style not possible in conventional languages.

而另一种函数式编程风格是基于**组合形式**来创建程序的。函数式程序处理结构化数据，通常既不重复也不用循环，它是分层构建的，无需命名参数，也无需通过复杂的过程声明就能普遍应用。[^fn-dec] **组合形式**能以传统语言不可能的方式，将高级程序构建更高级别的程序。

[^fn-dec]: 这里所指的可能是匿名函数和闭包。？？？

> Associated with the functional style of programming is an algebra of programs whose variables range over programs and whose operations are combining forms. This algebra can be used to transform programs and to solve equations whose "unknowns" are programs in much the same way one transforms equations in high school algebra. These transformations are given by algebraic laws and are carried out in the same language in which programs are written. Combining forms are chosen not only for their programming power but also for the power of their associated algebraic laws. General theorems of the algebra give the detailed behavior and termination conditions for large classes of programs.

**将函数式编程风格关联起来的是一种程序的代数，其变量即是程序逻辑，其操作即是组合形式**。 这样的代数可用于变换程序并求解“未知数”为程序的方程，和高中代数中变换方程的差不多。 这些变换由代数定律给出，并使用编写程序的语言来实现。 选择组合形式不仅是因为它们的编程能力，还因为它们相关的代数定律的能力。 代数的一般定理能给出大型程序的详细行为和终止条件。[^fn-algebra]

[^fn-algebra]: 这段话高度概括了函数式编程的本质。

> A new class of computing systems uses the functional programming style both in its programming language and in its state transition rules. Unlike von Neumann languages, these systems have semantics loosely coupled to states--only one state transition occurs per major computation.

一类新型计算系统在其编程语言和状态转换规则中都使用函数式编程风格。 与诺依曼语言不同，这些系统的语义与状态低耦合，即每次计算只发生一次状态转换。

> Key Words and Phrases: functional programming, algebra of programs, combining forms, functional forms, programming languages, yon Neumann computers, yon Neumann languages, models of computing systems, ap- plicative computing systems, applicative state transition systems, program transformation, program correctness, program termination, metacomposition

关键词和短语：函数式编程、程序代数、组合形式、函数形式、编程语言、诺依曼计算机、诺依曼语言、计算系统模型、应用计算系统、应用状态转换系统、程序转换、程序正确性、程序终止、元组合

> ## Introduction 

## 介绍

> I deeply appreciate the honor of the ACM invitation to give the 1977 Turing Lecture and to publish this account of it with the details promised in the lecture. Readers wishing to see a summary of this paper should turn to Section 16, the last section.

我非常荣幸地受ACM邀请参加1977年图灵讲座，并出版了这篇演讲的记述以及讲座中承诺的细节。 希望查看本文摘要的读者应参阅第16节，即最后一节。

> ## 1. Conventional Programming Languages: Fat and Flabby 

## 1. 传统编程语言：臃肿与乏力

> Programming languages appear to be in trouble. Each successive language incorporates, with a little cleaning up, all the features of its predecessors plus a few more. Some languages have manuals exceeding 500 pages; others cram a complex description into shorter manuals by using dense formalisms. The Department of Defense has current plans for a committee-designed language standard that could require a manual as long as 1,000 pages. Each new language claims new and fashionable features, such as strong typing or structured control statements, but the plain fact is that few languages make programming sufficiently cheaper or more reliable to justify the cost of producing and learning to use them. 

编程语言似乎遇到了麻烦。 每种后续语言都只经过少量的清理，却融合了其前身的所有功能，并再加入更多。 有些语言的手册超过 500 页；其他的则将复杂的描述塞进较短的手册中，满满的形式主义。 国防部目前计划制定一个由委员会设计的语言标准，该标准可能需要长达 1,000 页的手册。 每种新语言都声称拥有新的和流行的特性，例如强类型或结构化控制语句，但显而易见的事实是，很少有语言能够使编程足够容易或更可靠，以证明生产和学习使用它们的成本是合理的。

> Since large increases in size bring only small increases in power, smaller, more elegant languages such as Pascal continue to be popular. But there is a desperate need for a powerful methodology to help us think about programs, and no conventional language even begins to meet that need. In fact, conventional languages create unnecessary confusion in the way we think about programs.

尺寸变大，能力却提升很小，因此更小、更优雅的语言（例如 Pascal）才会持续流行。 但是我们迫切需要一种强大的方法来帮助我们思考编程，然而没有哪个传统的语言是从开始就满足这种需求的。 事实上，传统语言还给我们思考程序的方式带来了不必要的混乱。

> For twenty years programming languages have been steadily progressing toward their present condition of obesity; as a result, the study and invention of programming languages has lost much of its excitement. Instead, it is now the province of those who prefer to work with thick compendia of details rather than wrestle with new ideas. Discussions about programming languages often resemble medieval debates about the number of angels that can dance on the head of a pin instead of exciting contests between fundamentally differing concepts.

二十年来，编程语言一直稳步发展至今之臃肿，这让编程语言的研究和创新也再无往日的劲头。 取而代之的是，人们更愿意花精力在各种细节的考究上，而不是发力在一些新的思路上。 这让编程语言的讨论不是围绕着截然不同的核心概念展开唇枪舌战，而是像中世纪神学家们一般计较针尖上到底能有几个跳舞的天使[^angels]。

[^angels]: <https://en.wikipedia.org/wiki/How_many_angels_can_dance_on_the_head_of_a_pin%3F>

> Many creative computer scientists have retreated from inventing languages to inventing tools for describing them. Unfortunately, they have been largely content to apply their elegant new tools to studying the warts and moles of existing languages. After examining the appalling type structure of conventional languages, using the elegant tools developed by Dana Scott, it is surprising that so many of us remain passively content with that structure instead of energetically searching for new ones. 

许多富有创造力的计算机科学家已经放弃了发明语言，转而致力于发明描述它们的工具。 遗憾的是，他们大部分人满足于用这些优雅的新工具来研究现有语言的各种缺陷[^wart-mole]。 在使用Dana Scott[^scott]开发的优雅工具审视了传统语言中糟糕的类型结构[^typec]之后，令人惊讶的是，许多人仍然安于现状，没有积极地去寻找新的结构。

[^wart-mole]: 缺陷在原文中是用疣（warts）和痣（moles）来表达的。
[^scott]: <https://en.wikipedia.org/wiki/Dana_Scott>
[^typec]: 可能指的是那些复杂繁琐数据类型。？？？

> The purpose of this article is twofold; first, to suggest that basic defects in the framework of conventional languages make their expressive weakness and their cancerous growth inevitable, and second, to suggest some alternate avenues of exploration toward the design of new kinds of languages.

这篇文章的目的是双重的：首先，想表明传统语言框架中的基本缺陷使得它们表达能力的弱化和“癌细胞式”的膨胀不可避免；其次，想提出一些探索新类型语言设计方向的替代途径。

> ## 2. Models of Computing Systems

## 2. 计算系统的模型

> Underlying every programming language is a model of a computing system that its programs control. Some models are pure abstractions, some are represented by hardware, and others by compiling or interpretive programs. Before we examine conventional languages more closely, it is useful to make a brief survey of existing models as an introduction to the current universe of alternatives. Existing models may be crudely classified by the criteria outlined below.

每种编程语言的底层都包含着一个计算系统的模型，程序可以控制这个模型。有些模型是纯粹的抽象概念，有些由硬件表示，还有一些由编译器或解释器程序表示。在更仔细研究传统语言之前，为了让我们了解当前可替代方案的范围，对现有模型进行简要概述会很有帮助。我们可以根据以下标准粗略地对现有模型进行分类。

> ### 2.1 Criteria for Models 

### 2.1 模型标准

> #### 2.1.1 Foundations

#### 2.1.1 基础

> Is there an elegant and concise mathematical description of the model? Is it useful in proving helpful facts about the behavior of the model? Or is the model so complex that its description is bulky and of little mathematical use? 

对于模型是否存在优雅且简洁的数学描述？ 该描述是否有助于证明模型行为有效的事实？或者，该模型是否过于复杂，以至于其描述庞大且数学用途有限呢？

> #### 2.1.2 History sensitivity

#### 2.1.2 前序敏感性（History sensitivity）

> Does the model include a notion of storage, so that one program can save information that can affect the behavior of a later program? That is, is the model history sensitive? 

模型是否具有存储的概念，以便程序能保存影响后序程序行为的信息？也就是，模型是否是前序敏感的？

> #### 2.1.3 Type of semantics

#### 2.1.3 语义类型

> Does a program successively transform states (which are not programs) until a terminal state is reached (state-transition semantics)? Are states simple or complex? Or can a "program" be successively reduced to simpler "programs" to yield a final "normal form program," which is the result (reduction semantics)?

程序能否连续变换状态（，状态不是程序），直到结束（即**状态变化语义**）？状态是简单还是复杂，或者说，“程序”能否连续简化为更简单的“程序”，以产生最终的“规范形式程序”（normal form program），是哪种（即**归约语义**）？

> #### 2.1.4 Clarity and conceptual usefulness of programs

#### 2.1.4 程序的清晰性和概念性

> Are programs of the model clear expressions of a process or computation? Do they embody concepts that help us to formulate and reason about processes?

模型的程序能否清楚地表达过程或计算？ 该表达能否体现出有助于过程的形式化及推导的概念？


> ### 2.2 Classification of Models 

### 2.2 模型分类

> Using the above criteria we can crudely characterize three classes of models for computing systems--simple operational models, applicative models, and von Neumann models. 

根据上述标准，我们可以粗略地将计算系统的模型分为三类：简单操作模型，应用型模型和冯·诺伊曼模型。

> #### 2.2.1 Simple operational models 

#### 2.2.1 简单的操作模型

> Examples
 ~ Turing machines, various automata.

例如
 ~ 图灵机，各种自动机。
 
> Foundations
 ~ concise and useful.

基础
 ~ 简洁而有用。

> History sensitivity
 ~ have storage, are history sensitive.

前序敏感性
 ~ 拥有存储，前序敏感。

> Semantics
 ~ state transition with very simple states.

语义
 ~ 在极简状态间变换。

> Program clarity
 ~ programs unclear and conceptually not helpful.

程序清晰度
 ~ 程序不清晰，在概念上没有用。


> #### 2.2.2 Applicative models 

#### 2.2.2 应用型模型

> Examples
 ~ Church's lambda calculus[^5], Curry's system of combinators[^6], pure Lisp[^17], functional programming systems described in this paper.

例如
 ~ 邱奇的Lambda演算[^5]，Curry的组合系统[^6]，纯LISP[^17]，本文提到的函数式编程系统。

> Foundations
 ~ concise and useful.

基础
 ~ 简洁而有用。

> History sensitivity
 ~ no storage, not history sensitive.

前序敏感性
 ~ 没有存储，前序不敏感。

> Semantics
 ~ reduction semantics, no states.

语义
 ~ 归约语义，无状态。

> Program clarity
 ~ programs can be clear and conceptually useful.

程序清晰度
 ~ 程序可清晰，在概念上有用。

[^5]: TODO 
[^6]: TODO 
[^17]: TODO 

> #### 2.2.3 Von Neumann models

#### 2.2.3 冯·诺伊曼模型 

> Examples
 ~ von Neumann computers, conventional programming languages.

例如
 ~ 冯·诺伊曼计算机，传统编程语言。

> Foundations
 ~ complex, bulky, not useful.

基础
 ~ 复杂，笨重，无用。

> History sensitivity
 ~ have storage, are history sensitive.

前序敏感性
 ~ 拥有存储，前序敏感。

> Semantics
 ~ state transition with complex states.

语义
 ~ 复杂状态间变换。

> Program clarity
 ~ programs can be moderately clear, are not very useful conceptually.

程序清晰度
 ~ 程序可以适度清晰，在概念上不是很有用。


> The above classification is admittedly crude and debatable. Some recent models may not fit easily into any of these categories. For example, the data-flow languages developed by Arvind and Gostelow [^1], Dennis [^7], Kosinski [^13], and others partly fit the class of simple operational models, but their programs are clearer than those of earlier models in the class and it is perhaps possible to argue that some have reduction semantics. In any event, this classification will serve as a crude map of the territory to be discussed. We shall be concerned only with applicative and von Neumann models. 

诚然，上述的分类是粗略地，有待商榷地。 一些最近的模型可能不容易归类其中。 例如，由Arvind和Gostelow开发的数据流语言[^1]，Dennis [^7]，Kosinski [^13]，以及其他人部分满足简单操作模型，但它们的程序比同类之前的模型更清晰，或许能勉强算得上归约语义。 无论如何，这个分类只是一个大框架性的讨论。 我们应该将焦点放在应用型模型和冯·诺伊曼模型上。

[^1]:  TODO
[^7]:  TODO
[^13]:  TODO


> ## 3. Von Neumann Computers 

## 3. 冯·诺伊曼计算机

> In order to understand the problems of conventional programming languages, we must first examine their intellectual parent, the von Neumann computer. What is a von Neumann computer? When von Neumann and others conceived it over thirty years ago, it was an elegant, practical, and unifying idea that simplified a number of engineering and programming problems that existed then. Although the conditions that produced its architecture have changed radically, we nevertheless still identify the notion of "computer" with this thirty year old concept. 

为了理解传统编程语言存在的问题，我们首先需要研究它们的“智力先父”（Intellectual Parent），冯·诺依曼计算机。什么是冯·诺依曼计算机？三十多年前，冯·诺依曼等人构思出这个概念时，它还是一个优雅、实用且统一的思想，简化了许多当时存在的工程和编程问题。尽管催生冯·诺伊曼架构的条件已经发生根本性变化，但我们仍然将“计算机”的概念与这个三十年前的概念联系在一起。

> In its simplest form a von Neumann computer has three parts: a central processing unit (or CPU), a store, and a connecting tube that can transmit a single word between the CPU and the store (and send an address to the store). I propose to call this tube the von Neumann bottleneck. The task of a program is to change the contents of the store in some major way; when one considers that this task must be accomplished entirely by pumping single words back and forth through the von Neumann bottleneck, the reason for its name becomes clear. 

冯·诺依曼计算机最简单的形式由三个部分组成：中央处理单元 (CPU)、存储器和连接管道。这条管道可以在 CPU 和存储器之间传输单个字 (Word)（同时可以向存储器发送地址）。我愿将这条管道称为冯·诺依曼瓶颈。要知道，程序的任务是大幅改变存储器的内容，这一过程必须是一个字一个字地通过这条瓶颈来回传输来完成的，冯·诺依曼瓶颈才得名于此。

> Ironically, a large part of the traffic in the bottleneck is not useful data but merely names of data, as well as operations and data used only to compute such names. Before a word can be sent through the tube its address must be in the CPU; hence it must either be sent through the tube from the store or be generated by some CPU operation. If the address is sent from the store, then its address must either have been sent from the store or generated in the CPU, and so on. If, on the other hand, the address is generated in the CPU, it must be generated either by a fixed rule (e.g., "add l to the program counter") or by an instruction that was sent through the tube, in which case its address must have been sent ... and so on.

讽刺的是，瓶颈里的大部分数据流并不是真正有用的数据，而仅仅是数据的名称、用于计算这些名称的操作和数据本身。因为在一个字通过管道发送之前，它的地址必须已经在 CPU 中；因此，它要么需要从存储器通过管道发送到 CPU，要么由某个 CPU 操作生成。 如果地址从存储器发送，那么它的地址要么必须已经从存储器发送，要么在 CPU 中生成，依此类推。 另一方面，如果地址在 CPU 中生成，它要么由固定规则生成（例如，“将程序计数器加 1”），要么由通过管道发送的指令生成，在这种情况下，它的地址必须已经发送过……依此类推。

> Surely there must be a less primitive way of making big changes in the store than by pushing vast numbers of words back and forth through the von Neumann bottleneck. Not only is this tube a literal bottleneck for the data traffic of a problem, but, more importantly, it is an intellectual bottleneck that has kept us tied to word-at-a-time thinking instead of encouraging us to think in terms of the larger conceptual units of the task at hand. Thus programming is basically planning and detailing the enormous traffic of words through the von Neumann bottleneck, and much of that traffic concerns not significant data itself but where to find it. 

一定存在比反复通过冯·诺依曼瓶颈传输大量数据更原始的方法来大幅改变存储器内容。这个管道不仅是程序数据流动的瓶颈，更重要的是，它也是一个智力上的瓶颈，它将我们束缚在逐字处理的思维模式中，而不是鼓励我们从更大的概念单元去思考手头上任务。这使得，编程基本上就是规划和细化这些通过冯·诺依曼瓶颈的大量数据，其中大部分流量甚至都不是真正重要的数据，而是有关如何找到这些数据的数据。

> ## 4. Von Neumann Languages

## 4. 冯·诺依曼语言

> Conventional programming languages are basically high level, complex versions of the von Neumann computer. Our thirty year old belief that there is only one kind of computer is the basis of our belief that there is only one kind of programming language, the conventional--von Neumann--language. The differences between Fortran and Algol 68, although considerable, are less significant than the fact that both are based on the programming style of the von Neumann computer. Although I refer to conventional languages as "von Neumann languages" to take note of their origin and style, I do not, of course, blame the great mathematician for their complexity. In fact, some might say that I bear some responsibility for that problem. 

传统编程语言基本上是冯·诺依曼计算机的高级、复杂版本。 我们三十年来一直认为只有一种计算机，这奠定了我们只有一种编程语言的观念， 传统冯·诺依曼语言。Fortran 和 Algol 68 之间的区别虽然很大，但它们都基于冯·诺依曼计算机的编程风格，因此这种差异相比之下并不那么重要。尽管我将传统语言称为“冯·诺依曼语言”以强调它们的起源和风格，但这并不表示我把它们复杂性的问题归咎于这位伟大的数学家 (冯·诺依曼)。事实上，有些人可能会说我对这个问题负有一定责任。

> Von Neumann programming languages use variables to imitate the computer's storage cells; control statements elaborate its jump and test instructions; and assignment statements imitate its fetching, storing, and arithmetic. The assignment statement is the von Neumann bottleneck of programming languages and keeps us thinking in word-at-a-time terms in much the same way the computer's bottleneck does.

冯·诺依曼编程语言用变量来模拟计算机存储单元；用控制语句来模拟计算机的跳转和测试（指令）；用赋值语句来模拟数据的取、存以及算术运算。赋值语句就好比编程语言的冯·诺依曼瓶颈将我们局限在一次一字的思维模式中，与计算机中的冯·诺依曼瓶颈如出一辙。

> Consider a typical program; at its center are a number of assignment statements containing some subscripted variables. Each assignment statement produces a one word result. The program must cause these statements to be executed many times, while altering subscript values, in order to make the desired overall change in the store, since it must be done one word at a time. The programmer is thus concerned with the flow of words through the assignment bottleneck as he designs the nest of control statements to cause the necessary repetitions.

考虑一个典型的程序，核心部分可能包含许多带下标的变量赋值语句。每个赋值语句都会产生一个字大小的结果。由于程序需要逐字操作，因此为了实现整体上对存储器内容的改变，程序必须让这些语句执行多次，同时改变下标的值。程序员在设计控制语句嵌套来实现必要的重复时，实际上就是在关注赋值瓶颈中的字的流动。

> Moreover, the assignment statement splits programming into two worlds. The first world comprises the right sides of assignment statements. This is an orderly world of expressions, a world that has useful algebraic properties (except that those properties are often destroyed by side effects). It is the world in which most useful computation takes place. 

此外，赋值语句将编程分为两个世界。 第一世界是由赋值语句右侧的部分组成的， 一个有序的表达式的世界，这里存在有用的代数性质（尽管这些性质经常会被副作用破坏）。 最有用的计算都发生在这个世界。

>The second world of conventional programming languages is the world of statements. The primary statement in that world is the assignment statement itself. All the other statements of the language exist in order to make it possible to perform a computation that must be based on this primitive construct: the assignment statement. 

传统编程语言的第二世界是语句的世界。 该世界中的主要语句是赋值语句本身。 该语言所有其它语句的存在，目的是为了能够执行必须基于这个原始结构（赋值语句）的计算。

> This world of statements is a disorderly one, with few useful mathematical properties. Structured programming can be seen as a modest effort to introduce some order into this chaotic world, but it accomplishes little in attacking the fundamental problems created by the word-at-a-time von Neumann style of programming, with its primitive use of loops, subscripts, and branching flow of control.

语句的世界是一个混乱的世界，几乎没有有用的数学性质。结构化编程可以被看作是在这个混乱的世界中引入一些秩序的温和尝试，但对于解决逐字处理的冯·诺依曼瓶颈编程风格带来的根本问题，它收效甚微。这些问题包括原始的循环 (loops)、下标 (subscripts) 和分支控制流 (branching flow of control) 的使用。

> Our fixation on von Neumann languages has continued the primacy of the von Neumann computer, and our dependency on it has made non-von Neumann languages uneconomical and has limited their development. The absence of full scale, effective programming styles founded on non-von Neumann principles has deprived designers of an intellectual foundation for new computer architectures. (For a brief discussion of that topic, see Section 15.)

我们对冯·诺伊曼语言的执念延续了冯·诺伊曼计算机的主导地位，并且我们对它的依赖使得非冯·诺伊曼语言变得不经济，限制了它们的开发。缺乏建立在非冯·诺伊曼原则之上的成熟、有效的编程风格，剥夺了设计者们建立新型计算机架构的智力基础。（关于该主题的简要讨论，请参阅第 15 节。）

> Applicative computing systems' lack of storage and history sensitivity is the basic reason they have not provided a foundation for computer design. Moreover, most applicative systems employ the substitution operation of the lambda calculus as their basic operation. This operation is one of virtually unlimited power, but its complete and efficient realization presents great difficulties to the machine designer. Furthermore, in an effort to introduce storage and to improve their efficiency on von Neumann computers, applicative systems have tended to become engulfed in a large von Neumann system. For example, pure Lisp is often buried in large extensions with many von Neumann features. The resulting complex systems offer little guidance to the machine designer. 

应用型计算系统缺乏存储和前序敏感性是它们没能为计算机设计的提供基础的根本原因。 此外，大多数应用型系统都采用lambda演算中的替换操作作为其基本操作。 这种操作功能几乎无限强大，但要完整且高效地实现它，对机器设计者来说非常困难。 此外，为了引入存储功能并提高在冯·诺伊曼计算机上的效率，应用型计算系统往往会深陷于庞大的冯·诺伊曼系统泥潭中。 例如，纯LISP就被埋葬在许多冯·诺伊曼特性的大型扩展中。 系统变得非常复杂的同时，又没有为机器的设计者提供太多指导意义。

> ## 5. Comparison of von Neumann and Functional Programs 

## 5. 冯·诺伊曼与函数式编程的比较

> To get a more detailed picture of some of the defects of von Neumann languages, let us compare a conventional program for inner product with a functional one written in a simple language to be detailed further on. 

为了更详细地了解冯·诺伊曼语言的缺陷，让我们比较一下传统语言编写的内积程序和一个即将详细讲解的简单函数式语言编写的内积程序。

> ### 5.1 A von Neumann Program for Inner Product 

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
> 7. Its "housekeeping" operations are represented by symbols in scattered places (in the for statement and the subscripts in the assignment). This makes it impossible to consolidate housekeeping operations, the most common of all, into single, powerful, widely useful operators. Thus in programming those operations one must always start again at square one, writing "for i ~ ..." and "for j ~ ..." followed by assignment statements sprinkled with i's and j's.


1. 它的语句遵循复杂规则操作隐式状态[^invi-stat]。
2. 它缺乏层次结构。除了赋值语句的右边部分，程序没有能分解成更小的、可重用的部分，以构建复杂的操作。（大型程序通常会更有层次）
3. 它动态且重复。需要在脑中推演整个过程才能理解其逻辑。
4. 它通过重复（赋值）和修改（变量`i`）来逐字计算。
5. 程序中有数据的部分，`n`， 只能作为向量的长度信息，限制程序的实用性。
6. 它命名的参数，只能使用向量`a`和`b`，要使其变得通用，则需声明过程，这会引入复杂问题（如，是`call-by-name`还是`call-by-value`）。
7. 它那些“收拾”[^hk]操作，以符号形式散落各处（`for`语句里和下标赋值语句里），无法整合为一个通用操作。因而，这样的编程就需要反复使用类似`for i := ...`和`for j := ...`，并伴随满是`i`和`j`相关的赋值语句。

[^invi-stat]: 隐式状态是指`c := c + ...`。
[^hk]: 原文用 Housekeeping，指代处理数据的逻辑操作和步骤。

> ### 5.2 A Functional Program for Inner Product 

### 5.2 函数式内积程序

$$
\begin{aligned}
    \text{Def Innerproduct}\\
    &\equiv (\text{Insert}\ +) \circ (\text{ApplyToAll}\ \times) \circ \text{Transpose} 
\end{aligned}    
$$

> Or, in abbreviated form:

或以缩写形式：

$$
\text{Def IP} \equiv (/ +) \circ (\alpha \times) \circ Trans.
$$

> Composition $(\circ)$, $\text{Insert}\ (/)$, and $\text{ApplyToAll}\ (\alpha)$ are functional forms that combine existing functions to form new ones. Thus $f \circ g$ is the function obtained by applying first $g$ and then $f$, and $\alpha f$ is the function obtained by applying $f$ to every member of the argument. If we write $f:x$ for the result of applying $f$ to the object $x$, then we can explain each step in evaluating Innerproduct applied to the pair of vectors $<<1, 2, 3>, <6, 5, 4>>$ as follows: 

复合 $(\circ)$，$\text{Insert}\ (/)$ 和 $\text{ApplyToAll}\ (\alpha)$ 都是函数的形式，而函数又可以被组合为新的函数。因而有，$f\circ g$ 代表先应用函数$g$，后应用函数 $f$。$\alpha f$ 代表函数 $f$ 应用于参数的每个元素。当出现 $f:x$ 则代表对象 $x$ 应用了函数 $f$ 的结果。现在，我们可以逐步解释 $\text{Innerproduct}$ 应用于一对向量 $<<1, 2, 3>, <6, 5, 4>>$ 计算过程，如下：

$$
\begin{aligned}
    &\text{IP}:\ <<1,2,3>,<6,5,4>> && \ = \\
    &\text{Definition of IP} && \implies (/ +) \circ (\alpha \times) \circ \text{Trans}:\ <<1,2,3>,<6,5,4>>\\
    &\text{Effect of composition}, \circ && \implies (/ +) : ((\alpha \times) : (\text{Trans}:\ <<1,2,3>,<6,5,4>>))\\
    &\text{Applying Transpose} && \implies (/ +) : ((\alpha \times) :\ <<1,6>,<2,5>,<3,4>>)\\
    &\text{Effect of ApplyToAll},\alpha && \implies (/+):<\times:\ <1,6>, \times:\ <2,5>, \times:\ <3,4>>\\
    &\text{Applying}\ \times && \implies (/+):\ <6,10,12>\\
    &\text{Effect of Insert},/ && \implies +:\ <6,+:\ <10,12>>\\
    &\text{Applying}\ + && \implies +:\ <6,22>\\
    &\text{Applying}\ + \text{again} && \implies 28
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
2. 它是分层构建的，三个较小的函数（$+$、$\times$、$\text{Trans}$），加上三个函数形式 $f \circ g$、$\alpha f$、$/f$。
3. 它是静态且非重复的，意味着其结构易于理解，而无需在脑中推演。比如，只要能够理解 $\alpha f$（全体应用）和 $f \circ g$（复合）形式的作用，便能理解 $\alpha \times$（全体应用乘法）和 $(\alpha \times) \circ \text{Trans}$（交替后全体应用乘法）的作用，以此类推。
4. 它操作在完整的概念单元上，而不是字。一共三步，却无一步是重复。
5. 它没有牵扯任何数据，是完全通用的。它可以用于任何一致成对的向量。
6. 它没有命名任何参数，因此可应用于任何成对向量，而无需任何过程声明，或是遵循复杂的替换规则。
7. 它采用“收拾”的函数形式和函数，统统适用于大多其它程序。事实上，只有 $+$ 和 $\times$ 是与“收拾”无关。这些函数形式和函数可以进行其它的组合，以创建更高级的“收拾”。


> Section 14 sketches a kind of system designed to make the above functional style of programming available in a history-sensitive system with a simple framework, but much work remains to be done before the above applicative style can become the basis for elegant and practical programming languages. For the present, the above comparison exhibits a number of serious flaws in von Neumann programming languages and can serve as a starting point in an effort to account for their present fat and flabby condition.

第14节概述了一种系统，旨在将上述函数式编程风格引入到一个具有前序敏感且框架简单的系统中。然而，要使上述应用型风格成为优雅实用编程语言的基础，还有很多工作要做。就目前而言，以上对比揭示了冯诺依曼编程语言的一些严重缺陷，可以作为理解其目前臃肿笨拙状态的出发点。
