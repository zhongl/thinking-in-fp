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

在1950年代后期，Backus 效力于国际委员会，期间研发了 Algol 58 以及后继版本 Algol 60。Algol[^algol] 语言及其衍生编译器，作为一种开发程序的方式，和在此之上发布算法的正式手段，在欧洲获得广泛的认可。

[^algol]: <https://zh.wikipedia.org/zh-cn/ALGOL>

> In 1959, Backus presented a paper at the UNESCO conference in Paris on the syntax and semantics of a proposed international algebraic language. In this paper, he was the first to employ a formal technique for specifying the syntax of programming languages. The formal notation became known as BNF-standing for "Backus Normal Form," or "Backus Naur Form" to recognize the further contributions by Peter Naur of Denmark.

1959年，Backus 在巴黎的联合国教科文组织会议上发表了一篇论文，涉及拟议的国际代数语言的语法和语义。在本文中，他是第一个采用形式化技术来指定编程语言语法的人。这种形式符号系统俗称 BNF，全称 Backus Normal Form， 又或是因丹麦的Peter Naur的进一步贡献而得名的 Backus Naur Form 。

> Thus, Backus has contributed strongly both to the pragmatic world of problem-solving on computers and to the theoretical world existing at the interface between artificial languages and computational linguistics. Fortran remains one of the most widely used programming languages in the world. Almost all programming languages are now described with some type of formal syntactic definition.' "

因此，无论是在计算机上解决问题的现实世界，还是在人工语言与计算语言交互之间的理论世界，Backus 的贡献都是巨大的。Fortran 仍然是世界上使用最广泛的编程语言之一。 现在，几乎所有编程语言都用某种形式的句法定义来描述。’”

> Can Programming Be Liberated from the von Neumann Style? A Functional Style and Its Algebra of Programs

# 编程可以从冯·诺伊曼风格中解放出来吗？一种函数式风格及其程序的代数

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

> 1. Conventional Programming Languages: Fat and Flabby 

## 1. 传统编程语言：臃肿与乏力

> Programming languages appear to be in trouble. Each successive language incorporates, with a little cleaning up, all the features of its predecessors plus a few more. Some languages have manuals exceeding 500 pages; others cram a complex description into shorter manuals by using dense formalisms. The Department of Defense has current plans for a committee-designed language standard that could require a manual as long as 1,000 pages. Each new language claims new and fashionable features, such as strong typing or structured control statements, but the plain fact is that few languages make programming sufficiently cheaper or more reliable to justify the cost of producing and learning to use them. 

编程语言似乎遇到了麻烦。 每种后续语言都只经过少量的清理，却融合了其前身的所有功能，并再加入更多。 有些语言的手册超过 500 页；其他的则将复杂的描述塞进较短的手册中，满满的形式主义。 国防部目前计划制定一个由委员会设计的语言标准，该标准可能需要长达 1,000 页的手册。 每种新语言都声称拥有新的和流行的特性，例如强类型或结构化控制语句，但显而易见的事实是，很少有语言能够使编程足够容易或更可靠，以证明生产和学习使用它们的成本是合理的。

> Since large increases in size bring only small increases in power, smaller, more elegant languages such as Pascal continue to be popular. But there is a desperate need for a powerful methodology to help us think about programs, and no conventional language even begins to meet that need. In fact, conventional languages create unnecessary confusion in the way we think about programs.

尺寸变大，能力却提升很小，因此更小、更优雅的语言（例如 Pascal）才会持续流行。 但是我们迫切需要一种强大的方法来帮助我们思考编程，然而没有哪个传统的语言是从开始就满足这种需求的。 事实上，传统语言还给我们思考程序的方式带来了不必要的混乱。

> For twenty years programming languages have been steadily progressing toward their present condition of obesity; as a result, the study and invention of programming languages has lost much of its excitement. Instead, it is now the province of those who prefer to work with thick compendia of details rather than wrestle with new ideas. Discussions about programming languages often resemble medieval debates about the number of angels that can dance on the head of a pin instead of exciting contests between fundamentally differing concepts.

二十年来，编程语言一直稳步发展至今之臃肿，这让编程语言的研究和创新也再无往日的劲头。 取而代之的是，人们更愿意花精力在各种细节的考究上，而不是发力在一些新的思路上。 这让编程语言的讨论不是围绕着截然不同的核心概念展开唇枪舌战，而是像中世纪神学家们一般计较针尖上到底能有几个跳舞的天使[^angels]。

[^angels]: <https://en.wikipedia.org/wiki/How_many_angels_can_dance_on_the_head_of_a_pin%3F>

> Many creative computer scientists have retreated from inventing languages to inventing tools for describing them. Unfortunately, they have been largely content to apply their elegant new tools to studying the warts and moles of existing languages. After examining the appalling type structure of conventional languages, using the elegant tools developed by Dana Scott, it is surprising that so many of us remain passively content with that structure instead of energetically searching for new ones. 

许多富有创造力的计算机科学家已经放弃了发明语言，转而致力于发明描述它们的工具。 遗憾的是，他们大部分人满足于用这些优雅的新工具来研究现有语言的各种缺陷[^wart-mole]。 在使用Dana Scott[^scott]开发的优雅工具审视了传统语言中糟糕的类型结构之后，令人惊讶的是，许多人仍然安于现状，没有积极地去寻找新的结构。

[^wart-mole]: 缺陷在原文中是用疣（warts）和痣（moles）来表达的。
[^scott]: <https://en.wikipedia.org/wiki/Dana_Scott>

> The purpose of this article is twofold; first, to suggest that basic defects in the framework of conventional languages make their expressive weakness and their cancerous growth inevitable, and second, to suggest some alternate avenues of exploration toward the design of new kinds of languages.

这篇文章的目的是双重的：首先，想表明传统语言框架中的基本缺陷使得它们表达能力的弱化和“癌细胞式”的膨胀不可避免；其次，想提出一些探索新类型语言设计方向的替代途径。[^ewd692]

[^ewd692]: Edsger W.Dijkstra 写了一篇名为[A review of the 1977 Turing Award Lecture by John Backus](https://www.cs.utexas.edu/users/EWD/transcriptions/EWD06xx/EWD692.html)，表达了一些不同观点[^abs-ewd692]，值得搭配阅读。
[^abs-ewd692]: <https://g.co/gemini/share/5a8440984158>


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


> 2.2.2 Applicative models 

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

> 2.2.3 Von Neumann models

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


> 3. Von Neumann Computers 

## 3. 冯·诺伊曼计算机

> In order to understand the problems of conventional programming languages, we must first examine their intellectual parent, the von Neumann computer. What is a von Neumann computer? When von Neumann and others conceived it over thirty years ago, it was an elegant, practical, and unifying idea that simplified a number of engineering and programming problems that existed then. Although the conditions that produced its architecture have changed radically, we nevertheless still identify the notion of "computer" with this thirty year old concept. 

为了理解传统编程语言存在的问题，我们首先需要研究它们的“智力先父”（Intellectual Parent），冯·诺伊曼计算机。什么是冯·诺伊曼计算机？三十多年前，冯·诺伊曼等人构思出这个概念时，它还是一个优雅、实用且统一的思想，简化了许多当时存在的工程和编程问题。尽管催生冯·诺伊曼架构的条件已经发生根本性变化，但我们仍然将“计算机”的概念与这个三十年前的概念联系在一起。

> In its simplest form a von Neumann computer has three parts: a central processing unit (or CPU), a store, and a connecting tube that can transmit a single word between the CPU and the store (and send an address to the store). I propose to call this tube the von Neumann bottleneck. The task of a program is to change the contents of the store in some major way; when one considers that this task must be accomplished entirely by pumping single words back and forth through the von Neumann bottleneck, the reason for its name becomes clear. 

冯·诺伊曼计算机最简单的形式由三个部分组成：中央处理单元 (CPU)、存储器和连接管道。这条管道可以在 CPU 和存储器之间传输单个字 (Word)（同时可以向存储器发送地址）。我愿将这条管道称为冯·诺伊曼瓶颈。要知道，程序的任务是大幅改变存储器的内容，这一过程必须是一个字一个字地通过这条瓶颈来回传输来完成的，冯·诺伊曼瓶颈才得名于此。

> Ironically, a large part of the traffic in the bottleneck is not useful data but merely names of data, as well as operations and data used only to compute such names. Before a word can be sent through the tube its address must be in the CPU; hence it must either be sent through the tube from the store or be generated by some CPU operation. If the address is sent from the store, then its address must either have been sent from the store or generated in the CPU, and so on. If, on the other hand, the address is generated in the CPU, it must be generated either by a fixed rule (e.g., "add l to the program counter") or by an instruction that was sent through the tube, in which case its address must have been sent ... and so on.

讽刺的是，瓶颈里的大部分数据流并不是真正有用的数据，而仅仅是数据的名称、用于计算这些名称的操作和数据本身。因为在一个字通过管道发送之前，它的地址必须已经在 CPU 中；因此，它要么需要从存储器通过管道发送到 CPU，要么由某个 CPU 操作生成。 如果地址从存储器发送，那么它的地址要么必须已经从存储器发送，要么在 CPU 中生成，依此类推。 另一方面，如果地址在 CPU 中生成，它要么由固定规则生成（例如，“将程序计数器加 1”），要么由通过管道发送的指令生成，在这种情况下，它的地址必须已经发送过……依此类推。

> Surely there must be a less primitive way of making big changes in the store than by pushing vast numbers of words back and forth through the von Neumann bottleneck. Not only is this tube a literal bottleneck for the data traffic of a problem, but, more importantly, it is an intellectual bottleneck that has kept us tied to word-at-a-time thinking instead of encouraging us to think in terms of the larger conceptual units of the task at hand. Thus programming is basically planning and detailing the enormous traffic of words through the von Neumann bottleneck, and much of that traffic concerns not significant data itself but where to find it. 

一定存在比反复通过冯·诺伊曼瓶颈传输大量数据更原始的方法来大幅改变存储器内容。这个管道不仅是程序数据流动的瓶颈，更重要的是，它也是一个智力上的瓶颈，它将我们束缚在逐字处理的思维模式中，而不是鼓励我们从更大的概念单元去思考手头上任务。这使得，编程基本上就是规划和细化这些通过冯·诺伊曼瓶颈的大量数据，其中大部分流量甚至都不是真正重要的数据，而是有关如何找到这些数据的数据。

> 4. Von Neumann Languages

## 4. 冯·诺伊曼语言

> Conventional programming languages are basically high level, complex versions of the von Neumann computer. Our thirty year old belief that there is only one kind of computer is the basis of our belief that there is only one kind of programming language, the conventional--von Neumann--language. The differences between Fortran and Algol 68, although considerable, are less significant than the fact that both are based on the programming style of the von Neumann computer. Although I refer to conventional languages as "von Neumann languages" to take note of their origin and style, I do not, of course, blame the great mathematician for their complexity. In fact, some might say that I bear some responsibility for that problem. 

传统编程语言基本上是冯·诺伊曼计算机的高级、复杂版本。 我们三十年来一直认为只有一种计算机，这奠定了我们只有一种编程语言的观念， 传统冯·诺伊曼语言。Fortran 和 Algol 68 之间的区别虽然很大，但它们都基于冯·诺伊曼计算机的编程风格，因此这种差异相比之下并不那么重要。尽管我将传统语言称为“冯·诺伊曼语言”以强调它们的起源和风格，但这并不表示我把它们复杂性的问题归咎于这位伟大的数学家 (冯·诺伊曼)。事实上，有些人可能会说我对这个问题负有一定责任。

> Von Neumann programming languages use variables to imitate the computer's storage cells; control statements elaborate its jump and test instructions; and assignment statements imitate its fetching, storing, and arithmetic. The assignment statement is the von Neumann bottleneck of programming languages and keeps us thinking in word-at-a-time terms in much the same way the computer's bottleneck does.

冯·诺伊曼编程语言用变量来模拟计算机存储单元；用控制语句来模拟计算机的跳转和测试（指令）；用赋值语句来模拟数据的取、存以及算术运算。赋值语句就好比编程语言的冯·诺伊曼瓶颈将我们局限在一次一字的思维模式中，与计算机中的冯·诺伊曼瓶颈如出一辙。

> Consider a typical program; at its center are a number of assignment statements containing some subscripted variables. Each assignment statement produces a one word result. The program must cause these statements to be executed many times, while altering subscript values, in order to make the desired overall change in the store, since it must be done one word at a time. The programmer is thus concerned with the flow of words through the assignment bottleneck as he designs the nest of control statements to cause the necessary repetitions.

考虑一个典型的程序，核心部分可能包含许多带下标的变量赋值语句。每个赋值语句都会产生一个字大小的结果。由于程序需要逐字操作，因此为了实现整体上对存储器内容的改变，程序必须让这些语句执行多次，同时改变下标的值。程序员在设计控制语句嵌套来实现必要的重复时，实际上就是在关注赋值瓶颈中的字的流动。

> Moreover, the assignment statement splits programming into two worlds. The first world comprises the right sides of assignment statements. This is an orderly world of expressions, a world that has useful algebraic properties (except that those properties are often destroyed by side effects). It is the world in which most useful computation takes place. 

此外，赋值语句将编程分为两个世界。 第一世界是由赋值语句右侧的部分组成的， 一个有序的表达式的世界，这里存在有用的代数性质（尽管这些性质经常会被副作用破坏）。 最有用的计算都发生在这个世界。

>The second world of conventional programming languages is the world of statements. The primary statement in that world is the assignment statement itself. All the other statements of the language exist in order to make it possible to perform a computation that must be based on this primitive construct: the assignment statement. 

传统编程语言的第二世界是语句的世界。 该世界中的主要语句是赋值语句本身。 该语言所有其它语句的存在，目的是为了能够执行必须基于这个原始结构（赋值语句）的计算。

> This world of statements is a disorderly one, with few useful mathematical properties. Structured programming can be seen as a modest effort to introduce some order into this chaotic world, but it accomplishes little in attacking the fundamental problems created by the word-at-a-time von Neumann style of programming, with its primitive use of loops, subscripts, and branching flow of control.

语句的世界是一个混乱的世界，几乎没有有用的数学性质。结构化编程可以被看作是在这个混乱的世界中引入一些秩序的温和尝试，但对于解决逐字处理的冯·诺伊曼瓶颈编程风格带来的根本问题，它收效甚微。这些问题包括原始的循环 (loops)、下标 (subscripts) 和分支控制流 (branching flow of control) 的使用。

> Our fixation on von Neumann languages has continued the primacy of the von Neumann computer, and our dependency on it has made non-von Neumann languages uneconomical and has limited their development. The absence of full scale, effective programming styles founded on non-von Neumann principles has deprived designers of an intellectual foundation for new computer architectures. (For a brief discussion of that topic, see Section 15.)

我们对冯·诺伊曼语言的执念延续了冯·诺伊曼计算机的主导地位，并且我们对它的依赖使得非冯·诺伊曼语言变得不经济，限制了它们的开发。缺乏建立在非冯·诺伊曼原则之上的成熟、有效的编程风格，剥夺了设计者们建立新型计算机架构的智力基础。（关于该主题的简要讨论，请参阅第 15 节。）

> Applicative computing systems' lack of storage and history sensitivity is the basic reason they have not provided a foundation for computer design. Moreover, most applicative systems employ the substitution operation of the lambda calculus as their basic operation. This operation is one of virtually unlimited power, but its complete and efficient realization presents great difficulties to the machine designer. Furthermore, in an effort to introduce storage and to improve their efficiency on von Neumann computers, applicative systems have tended to become engulfed in a large von Neumann system. For example, pure Lisp is often buried in large extensions with many von Neumann features. The resulting complex systems offer little guidance to the machine designer. 

应用型计算系统缺乏存储和前序敏感性是它们没能为计算机设计的提供基础的根本原因。 此外，大多数应用型系统都采用lambda演算中的替换操作作为其基本操作。 这种操作功能几乎无限强大，但要完整且高效地实现它，对机器设计者来说非常困难。 此外，为了引入存储功能并提高在冯·诺伊曼计算机上的效率，应用型计算系统往往会深陷于庞大的冯·诺伊曼系统泥潭中。 例如，纯LISP就被埋葬在许多冯·诺伊曼特性的大型扩展中。 系统变得非常复杂的同时，又没有为机器的设计者提供太多指导意义。

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

> Composition $(\circ)$, $\text{Insert}\ (/)$, and $\text{ApplyToAll}\ (\alpha)$ are functional forms that combine existing functions to form new ones. Thus $f \circ g$ is the function obtained by applying first $g$ and then $f$, and $\alpha f$ is the function obtained by applying $f$ to every member of the argument. If we write $f:x$ for the result of applying $f$ to the object $x$, then we can explain each step in evaluating Innerproduct applied to the pair of vectors $<<1, 2, 3>, <6, 5, 4>>$ as follows: 

复合 $(\circ)$， $\text{Insert}\ (/)$ 和 $\text{ApplyToAll}\ (\alpha)$ 都是函数的形式，而函数又可以被组合为新的函数。因而有， $f\circ g$ 代表先应用函数 $g$，后应用函数 $f$ 。 $\alpha f$ 代表函数 $f$ 应用于参数的每个元素。当出现 $f:x$ 则代表对象 $x$ 应用了函数 $f$ 的结果。现在，我们可以逐步解释 $\text{Innerproduct}$ 应用于一对向量 $<<1, 2, 3>, <6, 5, 4>>$ 计算过程，如下：

$$
\begin{aligned}
    &\text{IP}:\ <<1,2,3>,<6,5,4>> && = \\
    &\text{Definition of IP} && \implies (/ +) \circ (\alpha \times) \circ \text{Trans}:\ <<1,2,3>,<6,5,4>>\\
    &\text{Effect of composition}, \circ && \implies (/ +) : ((\alpha \times) : (\text{Trans}:\ <<1,2,3>,<6,5,4>>))\\
    &\text{Applying Transpose} && \implies (/ +) : ((\alpha \times) :\ <<1,6>,<2,5>,<3,4>>)\\
    &\text{Effect of ApplyToAll},\alpha && \implies (/+):\ <\times:\ <1,6>, \times:\ <2,5>, \times:\ <3,4>>\\
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
2. 它是分层构建的，三个较小的函数（ $+$、 $\times$ 、 $\text{Trans}$ ），加上三个函数形式 $f \circ g$ 、 $\alpha f$ 、 $/f$。
3. 它是静态且非重复的，意味着其结构易于理解，而无需在脑中推演。比如，只要能够理解 $\alpha f$（全体应用）和 $f \circ g$（复合）形式的作用，便能理解 $\alpha \times$ （全体应用乘法）和 $(\alpha \times) \circ \text{Trans}$ （转置后全体应用乘法）的作用，以此类推。
4. 它操作在完整的概念单元上，而不是字。一共三步，却无一步是重复。
5. 它没有牵扯任何数据，是完全通用的。它可以用于任何一致成对的向量。
6. 它没有命名任何参数，因此可应用于任何成对向量，而无需任何过程声明，或是遵循复杂的替换规则。
7. 它采用“收拾”的函数形式和函数，统统适用于大多其它程序。事实上，只有 $+$ 和 $\times$ 是与“收拾”无关。这些函数形式和函数可以进行其它的组合，以创建更高级的“收拾”。


> Section 14 sketches a kind of system designed to make the above functional style of programming available in a history-sensitive system with a simple framework, but much work remains to be done before the above applicative style can become the basis for elegant and practical programming languages. For the present, the above comparison exhibits a number of serious flaws in von Neumann programming languages and can serve as a starting point in an effort to account for their present fat and flabby condition.

第14节概述了一种系统，旨在将上述函数式编程风格引入到一个具有前序敏感且框架简单的系统中。然而，要使上述应用型风格成为优雅实用编程语言的基础，还有很多工作要做。就目前而言，以上对比揭示了冯·诺伊曼编程语言的一些严重缺陷，可以作为理解其目前臃肿笨拙状态的出发点。

> 6. Language Frameworks versus Changeable Parts

## 6. 语言的框架与可变的部分

> Let us distinguish two parts of a programming language. First, its *framework* which gives the overall rules of the system, and second, its *changeable parts*, whose existence is anticipated by the framework but whose particular behavior is not specified by it. For example, the `for` statement, and almost all other statements, are part of Algol's framework but library functions and userdefined procedures are changeable parts. Thus the framework of a language describes its fixed features and provides a general environment for its changeable features.

让我们将编程语言分成两部分看。一个是*框架*，它给定了系统全部的规则；另一个是*可变的部分*，这是框架预期之内的，但又不指定其具体的行为。举个例子，`for`语句，和其它多有语句是 Algol 框架的部分，而库函数与用户定义的过程则是可变的部分。因此，一门语言的框架，既描述了它固定的特性，又为可变的特性提供了普遍的运行环境。

> Now suppose a language had a small framework which could accommodate a great variety of powerful features entirely as changeable parts. Then such a framework could support many different features and styles without being changed itself. In contrast to this pleasant possibility, von Neumann languages always seem to have an immense framework and very limited changeable parts. What causes this to happen? The answer concerns two problems of von Neumann languages.

现在假设有这么一个小型框架，它可以灵活的将各种强大的特性作为可变的部分融合起来，使得在不改变自身的情况下，支持许多不同的特性和编程风格。与这种理性情况恰恰相反的是，冯·诺伊曼语言通常拥有庞大的框架和非常有限的可变部分。这是是什么导致的呢？答案就在冯·诺伊曼语言的两个问题上。

> The first problem results from the von Neumann style of word-at-a-time programming, which requires that words flow back and forth to the state, just like the flow through the von Neumann bottleneck. Thus a von Neumann language must have a semantics closely coupled to the state, in which every detail of a computation changes the state. The consequence of this semantics closely coupled to states is that every detail of every feature must be built into the state and its transition rules. 

第一个问题源自冯式一次一字的编程风格，这让数据（words）向着状态来回流动，如同穿梭在冯·诺伊曼瓶颈中。它使得冯·诺伊曼语言必须含有一种与状态紧密耦合的语义，以表达一切改变状态的运算细节。进而导致每个特性的所有细节必须内含在状态及其转变的规则当中。

> Thus every feature of a von Neumann language must be spelled out in stupefying detail in its framework. Furthermore, many complex features are needed to prop up the basically weak word-at-a-time style. The result is the inevitable rigid and enormous framework of a von Neumann language. 

冯·诺伊曼语言的框架下，其每一个特性要表达出来都变了啰里八嗦[^eg-stupefy]。更过分的是，还需要许多复杂的特性以支撑逐字风格的运行方式[^eg-complex]。这些都不可避免的导致冯·诺伊曼语言框架的僵化和庞大。

[^eg-stupefy]: <https://g.co/gemini/share/2116ab990fc6>
[^eg-complex]: <https://g.co/gemini/share/8c1c646b930e>

> 7. Changeable Parts and Combining Forms 

## 7. 可变部分与组合形式

> The second problem of von Neumann languages is that their changeable parts have so little expressive power. Their gargantuan size is eloquent proof of this; after all, if the designer knew that all those complicated features, which he now builds into the framework, could be added later on as changeable parts, he would not be so eager to build them into the framework.

冯·诺伊曼语言的第二个问题是可变部分的表达能力太弱。其庞大的体积就是最好的证明。毕竟，如果设计者知道所有他现在内置到框架中的复杂特性都可以稍后作为可变部分添加，那么他就不必急于将它们内置到框架中了。

> Perhaps the most important element in providing powerful changeable parts in a language is the availability of combining forms that can be generally used to build new procedures from old ones. Von Neumann languages provide only primitive combining forms, and the von Neumann framework presents obstacles to their full use. 

或许，语言里能提供强大可变部分的最关键要素是，组合形式的有效性。即，它能普遍地用于将已有过程构建出新过程。冯·诺伊曼语言不仅提供组合形式是原始的，其框架还是充分利用它们的绊脚石。

> One obstacle to the use of combining forms is the split between the expression world and the statement world in von Neumann languages. Functional forms naturally belong to the world of expressions; but no matter how powerful they are they can only build expressions that produce a one-word result. And it is in the statement world that these one-word results must be combined into the overall result. Combining single words is not what we really should be thinking about, but it is a large part of programming any task in von Neumann languages. To help assemble the overall result from single words these languages provide some primitive combining forms in the statement world -- the `for`, `while`, and `if-then-else` statements -- but the split between the two worlds prevents the combining forms in either world from attaining the full power they can achieve in an undivided world. 

其中的一颗使用组合形式的绊脚石是，冯·诺伊曼语言被分裂为表达式世界和语句世界。函数式（组合）形式天然属于表达式世界，但无论它们多么强大，都只能构建单字（one-word）结果的表达式。这些单字的结果，再在语句世界里，被组合为整体的结果。这样的组合本不该是我们真正思考的东西，但在冯·诺伊曼语言里，大部分编程的过程都围绕于此。为了帮助组装这些单字（single words）成为最后的结果，语言提供了这么些原始的组合形式，如`for`, `while`, 和 `if-then-else` 语句。两个世界的分裂，使得组合形式的能力在怎么也无法达到在统一世界里的水平。

> A second obstacle to the use of combining forms in von Neumann languages is their use of elaborate naming conventions, which are further complicated by the substitution rules required in calling procedures. Each of these requires a complex mechanism to be built into the framework so that variables, subscripted variables, pointers, file names, procedure names, call-by-value formal parameters, call-by-name formal parameters, and so on, can all be properly interpreted. All these names, conventions, and rules interfere with the use of simple combining forms.

冯·诺伊曼语言里对复杂的命名惯例的应用是其第二个绊脚石，叠加调用过程所需的替换规则，让这一点进一步复杂化。为了正确的解释它们，框架需要内置复杂的机制，如变量、带下标的变量、指针、文件名、过程名、按值传递的形参、按名传递的形参等。所有这些名称、惯例以及规则都在干扰简单组合形式的使用。

> 8. APL versus Word-at-a-Time Programming

## 8. APL与逐字编程

> Since I have said so much about word-at-a-time programming, I must now say something about APL [^12]. We owe a great debt to Kenneth Iverson for showing us that there are programs that are neither word-at-a-time nor dependent on lambda expressions, and for introducing us to the use of new functional forms. And since APL assignment statements can store arrays, the effect of its functional forms is extended beyond a single assignment.

既然我已经讨论了太多逐字处理的编程，现在我也应该谈论一下 APL [^12] 语言。我们非常感谢 Kenneth Iverson，因为他向我们展示了既不是逐字处理的，也不依赖于 lambda 表达式的程序，并且引入了新的函数式形式。由于 APL 的赋值语句可以存储数组，因此其函数式形式的效果超越了单个赋值的操作。

[^12]: TODO

> Unfortunately, however, APL still splits programming into a world of expressions and a world of statements. Thus the effort to write one-line programs is partly motivated by the desire to stay in the more orderly world of expressions. APL has exactly three functional forms, called inner product, outer product, and reduction. These are sometimes difficult to use, there are not enough of them, and their use is confined to the world of expressions.

遗憾的是，APL 仍然将编程分割成表达式世界和语句世界。因此，编写单行程序的努力部分源于希望留在更井井有条的表达式世界。APL 只有三种函数式形式，称为内积、外积和归约。它们有时使用起来很困难，数量也不够多，而且只能用于表达式世界。[^eg-apl]

[^eg-apl]: <https://g.co/gemini/share/c5a61ca755af>

> Finally, APL semantics is still too closely coupled to states. Consequently, despite the greater simplicity and power of the language, its framework has the complexity and rigidity characteristic of von Neumann languages. 

最后，APL 的语义仍然与状态紧密耦合。因此，尽管语言本身更加简洁强大，但它的框架仍然具有冯·诺伊曼语言特有的复杂性和僵化性。


> 9. Von Neumann Languages Lack Useful Mathematical Properties 

## 9. 冯·诺伊曼语言缺乏有用的数学性质

> So far we have discussed the gross size and inflexibility of von Neumann languages; another important defect is their lack of useful mathematical properties and the obstacles they present to reasoning about programs. Although a great amount of excellent work has been published on proving facts about programs, von Neumann languages have almost no properties that are helpful in this direction and have many properties that are obstacles (e.g., side effects, aliasing).

我们已经讨论了冯·诺伊曼语言的庞大和缺乏灵活性；另一个重要缺陷是它们不仅缺乏用于程序推理的有用数学性质，还对推理造成阻碍。尽管已经发表了许多关于证明程序事实的优秀著作，然而冯·诺伊曼语言几乎没有利于该方向的性质，反倒是拥有许多障碍特性（例如，副作用、别名）。

> Denotational semantics [^23] and its foundations [^20] [^21] provide an extremely helpful mathematical understanding of the domain and function spaces implicit in programs. When applied to an applicative language (such as that of the "recursive programs" of [^16]), its foundations provide powerful tools for describing the language and for proving properties of programs. When applied to a von Neumann language, on the other hand, it provides a precise semantic description and is helpful in identifying trouble spots in the language. But the complexity of the language is mirrored in the complexity of the description, which is a bewildering collection of productions, domains, functions, and equations that is only slightly more helpful in proving facts about programs than the reference manual of the language, since it is less ambiguous. 

指称语义学 [^23] 及其基础 [^20] [^21] 提供了一种非常有用的数学方法，可以理解程序中隐含的域 (domain) 和函数空间。当应用于应用型语言（例如引用文献[^16] 中的“递归程序”）时，它的基础为描述语言和证明程序性质提供了强大的工具。另一方面，当应用于冯··诺伊曼语言时，它可以提供精确的语义描述，并有助于识别语言中的问题所在。但是，语言的复杂性会体现在描述的复杂性上，它由一系列令人困惑的产生式（Production）、域、函数和方程组成，在证明程序事实方面仅比语言的参考手册略有帮助，因为它是更少歧义的。

[^16]: TODO
[^20]: TODO
[^21]: TODO
[^23]: TODO

> Axiomatic semantics [^11] precisely restates the inelegant properties of von Neumann programs (i.e., transformations on states) as transformations on predicates. The word-at-a-time, repetitive game is not thereby changed, merely the playing field. The complexity of this axiomatic game of proving facts about von Neumann programs makes the successes of its practitioners all the more admirable. Their success rests on two factors in addition to their ingenuity: First, the game is restricted to small, weak subsets of full von Neumann languages that have states vastly simpler than real ones. Second, the new playing field (predicates and their transformations) is richer, more orderly and effective than the old (states and their transformations). But restricting the game and transferring it to a more effective domain does not enable it to handle real programs (with the necessary complexities of procedure calls and aliasing), nor does it eliminate the clumsy properties of the basic von Neumann style. As axiomatic semantics is extended to cover more of a typical von Neumann language, it begins to lose its effectiveness with the increasing complexity that is required. 

公理语义学将冯·诺伊曼程序 (通过状态转换) 的非优雅性质精确地重新表述为谓词 (predicate) 的转换。逐字处理、重复的游戏并没有因此改变，只是改变了赛场。证明冯·诺伊曼程序事实的公理游戏非常复杂，这使得实践者的成功更加令人钦佩。他们的成功除了才智之外，还依赖于两个因素：首先，游戏仅限于冯·诺伊曼语言的较小、较弱的子集，这些子集的状态比现实世界的状态简单得多。其次，新的赛场（谓词及其转换）比旧的赛场（状态及其转换）更丰富、更有序、更有效。但是，限制游戏范围并转移到更有效的领域并不能处理真实程序（具有必要的过程调用和别名复杂性），也不能消除冯诺·伊曼风格的基本笨拙特性。随着公理语义学扩展到涵盖更多典型的冯诺伊曼语言，其有效性会随着所需复杂性的增加而丧失。

> Thus denotational and axiomatic semantics are descriptive formalisms whose foundations embody elegant and powerful concepts; but using them to describe a von Neumann language can not produce an elegant and powerful language any more than the use of elegant and modem machines to build an Edsel can produce an elegant and modem car.

因此，指称语义学和公理语义学都是描述性的形式论，其基础包含着优雅而强大的概念。但是，用它们来描述冯诺伊曼语言并不能创造出优雅强大的语言，就像即便使用先进的机器制造 Edsel [^edsel] 也造不出优雅现代的汽车一样。

[^edsel]: <https://en.wikipedia.org/wiki/Edsel>

> In any case, proofs about programs use the language of logic, not the language of programming. Proofs talk about programs but cannot involve them directly since the axioms of von Neumann languages are so unusable. In contrast, many ordinary proofs are derived by algebraic methods. These methods require a language that has certain algebraic properties. Algebraic laws can then be used in a rather mechanical way to transform a problem into its solution. For example, to solve the equation 

无论如何，程序的证明使用的是逻辑语言，而不是编程语言。证明可以讨论程序，但由于冯·诺伊曼语言的公理如此难以使用，所以不能直接涉及程序本身。相比之下，许多普通的证明都由代数方法得出的。这些方法需要一种具有某些代数性质的语言。然后可以用代数定律以一种相当机械的方式将问题求解。比如，求解如下方程

$$
ax + bx = a + b
$$

> for $x$ (given that $a+b \not = 0$ ), we mechanically apply the distributive, identity, and cancellation laws, in succession, to obtain

对于 $x$ （假设 $a+b \not = 0$ ），我们依次使用分配律、幺元律和消去律，机械地将其变形得到

$$
\begin{aligned}
(a + b) x &= a + b\\
(a + b) x &= (a + b) 1\\
x &= 1
\end{aligned}
$$

> Thus we have proved that $x = 1$ without leaving the "language" of algebra. Von Neumann languages, with their grotesque syntax, offer few such possibilities for transforming programs.

因此，我们完全使用代数的“语言”证明了 $x = 1$ 。冯·诺伊曼语言由于其怪异的语法，无法像代数那样方便地进行程序变换。

As we shall see later, programs can be expressed in a language that has an associated algebra. This algebra can be used to transform programs and to solve some equations whose "unknowns" are programs, in much the same way one solves equations in high school algebra. Algebraic transformations and proofs use the language of the programs themselves, rather than the language of logic, which talks about programs.

正如我们稍后将看到的，程序可以用一种具有相关代数的语言来表达。这种代数可以用来变换程序，并解决一些未知数是程序的方程，就像高中代数解方程一样。代数变换和证明使用程序本身的语言，而不是谈论程序的逻辑语言。

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
  \bot\quad 1.5\quad \phi\quad AB3\quad &< AB,\ 1,\ 2.3 >\\
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
+:< 1,\ 2 > &= 3 &tl:< A, B, C > &= < B, C >\\
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
                       x &= < x_1, \dots , x_n > \And\ n \ge 2 &&\to\ < x_2, \dots , x_n >;
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
  \text{reverse} : x \equiv x &= \phi &\to& \phi ;\\
                            x &= < x_1, \dots, x_n > &\to& < x_n, \dots, x_1 > ;
                            \bot
\end{aligned}
$$

**Distribute from left; distribute from right**

$$
\begin{aligned}
  \text{distl} : x \equiv x &= < y, \phi > &&\to \phi;\\
                          x &= < y, < z_1, \dots, z_n > > &&\to\ < < y, z_1 >, \dots, < y, z_n > >;
                          \bot\\
  \text{distr} : x \equiv x &= < \phi, y > &&\to \phi;\\
                          x &= < < y_1, \dots, y_n >, z > &&\to\ < < y_1, z >, \dots, < y_n, z > >;
                          \bot
\end{aligned}
$$

**Length**

$$
\text{length} : x \equiv x = < x_1, \dots, x_n >\ \to\ n;
                  x = \phi \to 0;
                  \bot
$$

**Add, substract, multiply, and divide**

$$
\begin{aligned}    
  +: x \equiv x = < y, z > \And\ y,z\ \text{are numbers} \to\ y + z; \bot \\
  -: x \equiv x = < y, z > \And\ y,z\ \text{are numbers} \to\ y - z; \bot \\
  \times : x \equiv x = < y, z > \And\ y,z\ \text{are numbers} \to\ y \times z; \bot \\
  \div : x \equiv x = < y, z > \And\ y,z\ \text{are numbers} \to\ y \div z; \bot \\
  (\text{where}\ y \div 0 = \bot)
\end{aligned}
$$

**Transpose**

$$
\begin{aligned}
  \text{trans} : x \equiv x &= < \phi, \dots, \phi>\ &\to& \phi;\\
                          x &= < x_1, \dots, x_n >\ &\to& < y_1, \dots, y_m>;\bot\\
  \text{where}\\
                        x_i &= < x_{i1}, \dots, x_{im} > &&\text{and}\\
                        y_j &= < x_{1j}, \dots, x_{nj} > &&, 1 \le i \le n, 1 \le j \le m.                      
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
  \text{2r} : x \equiv x &= < x_1, \dots, x_n > \And\ n \ge 2 \ &&\to\ x_{n-1};\bot\\  
  \text{etc.} \\
  \text{tlr} : x \equiv x &= < x_1 >\ &&\to \phi;\\
                         x &= < x_1, \dots, x_n > \And\ n \ge 2 \ &&\to\ < x_1, \dots, x_{n-1} >;\bot
\end{aligned}
$$

**Rotate left; rotate right**

$$
\begin{aligned}
  \text{rotl} : x \equiv x &= \phi &&\to \phi;\\
                         x &= < x_1 > &&\to\ < x_1 >;\\
                         x &= < x_1, \dots, x_n > \And\ n \ge 2 \ &&\to\ < x_2, \dots, x_n, x_1 >;\bot\\
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
[ f_1, \dots, f_n ] : x \equiv\  f_1 : x, \dots, f_n : x >
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
                x &= < x_1, \dots, x_n > \And\ n \ge 2 && \to f : < x_1, /f : < x_2, \dots, x_n > > ;\bot
\end{aligned}
$$

> If $f$ has a unique right unit $u_f \not = \bot$ , where $f : < x, u_f >\ \in \set{ x, \bot }$ for all objects $x$ , then the above definition is extended: $/f : \phi = u_f$ . Thus 

当函数 $f$ 存在唯一的右单元（right unit）满足 $u_f \not = \bot$ [^ru]， 且对所有对象 $x$ 满足 $f : < x, u_f >\ \in \set{ x, \bot }$ ，由此可得  $/f : \phi = u_f$ 。具体来说：

$$
\begin{aligned}
&/+ : < 4, 5, 6 > &=&\ + : < 4, + : < 5, /+ : < 6 > > > \\
&                 &=&\ + : < 4, + : < 5, 6 > > \\
&                 &=&\ + : < 4, 11 > \\ 
&                 &=&\ 15 \\
&/+ : \phi = 0                 
\end{aligned}
$$

[^ru]: TODO

**Apply to all**

$$
\begin{aligned}
\alpha f : x \equiv x &= \phi &\to&\ \phi; \\
                    x &= < x_1, \dots, x_n > &\to& < f : x_1, \dots, f : x_n >;
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
(\text{bu}\ +\ 1) : x = 1 + x
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

> defines the function $\text{last}$, which is the same as $\text{last1}$ . Here in detail is how the definition would be used to compute $\text{last} : < 1, 2 >$ : 

函数 $\text{last}$ 和 $\text{last1}$ 其实是等价的。下面就来看看 $\text{last} : < 1, 2 >$ 的计算过程：

$$
\begin{aligned}
&\text{last} : < 1, 2 >\\
&\text{definition of last }             &\implies& (\text{null} \circ \text{tl} \to 1; \text{last} \circ \text{tl}) : < 1, 2 >\\
&\text{action of the form } (p \to f;g) &\implies& \text{last} \circ \text{tl} : < 1, 2 > \\
&                                       &&\text{since } \text{null} \circ \text{tl} : < 1, 2 > = \text{null} : < 2 > = F\\
&\text{action of the form } f \circ g   &\implies& \text{last} : (\text{tl} : < 1, 2 >)\\
&\text{definition of primitive tail }   &\implies& \text{last} : < 2 >\\
&\text{definition of last }             &\implies& (\text{null} \circ \text{tl} \to 1; \text{last} \circ \text{tl}) : < 2 >\\
&\text{action of the form } (p \to f;g) &\implies& 1 : < 2 >\\
&                                       &&\text{since } \text{null} \circ \text{tl} : < 2 > = \text{null} : \phi = T\\
&\text{definition of selector } 1       &\implies& 2
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

> Here are some of the intermediate expressions an FP system would obtain in evaluating $\text{!} : 2$:

让我们来以 $\text{!} : 2$ 为例，推导一下中间的过程[^fac]：

$$
\begin{aligned}
  \text{!} : 2 &\implies (\text{eq0} \to \bar{1}; \times \circ [ \text{id}, \text{!} \circ \text{sub1} ]) : 2\\
               &\implies \times \circ [ \text{id}, \text{!} \circ \text{sub1} ]) : 2\\
               &\implies \times : < \text{id} : 2, \text{!} \circ \text{sub1} :2 >\\
               &\implies \times : < 2, \text{!} : 1 >\\
               &\implies \times : < 2, \times : < 1, \text{!} : 0 > >\\
               &\implies \times : < 2, \times : < 1, \bar{1} > >\\   
               &\implies \times : < 2, \times : < 1, 1 > >\\   
               &\implies \times : < 2, 1 >\\   
               &\implies 2.
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
  &\qquad \text{where } m_i = < m_{i1}, \dots, m_{is}> \text{for } i = 1, \dots, r.\\
  &\textbf{Def } \text{MM} \equiv (\alpha \alpha \text{IP}) \circ (\alpha \text{distl}) \circ \text{distr} \circ [ 1, \text{trans} \circ 2 ]
\end{aligned}
$$

> The program $\text{MM}$ has four steps, reading from right to left; each is applied in turn, beginning with $[ 1, \text{trans} \circ 2 ]$ , to the result of its predecessor. 
> If the argument is $< m,n >$, then the first step yields $< m, n' > \text{where } n' = \text{trans}:n$. 
> The second step yields $< < m_1, n' >, ..., < m_r, n' > >$, where the $m_i$ are the rows of $m$. 
> The third step, $\alpha \text{distl}$ , yields $< \text{distl} : < m_1, n' >, \dots, \text{distl} : < m_r, n' > > = < p_1, \dots, p_r >$ where $p_i = \text{distl} : < m_1, n' > = < < m_i, n_1' >, \dots, < m_i, n_s' > > \text{for } i = 1, \dots, r$ and $n_j'$ is the jth column of $n$ ( the jth row of $n'$ ). Thus $p_i$, a sequence of row and column pairs, corresponds to the i-th product row. 
> The operator $\alpha \alpha \text{IP}$ , or $\alpha (\alpha \text{IP})$ , causes $\alpha \text{IP}$ to be applied to each $p_i$ , which in turn causes $\text{IP}$ to be applied to each row and column pair in each $p_i$ . The result of the last step is therefore the sequence of rows comprising the product matrix. 
> If either matrix is not rectangular, or if the length of a row of $m$ differs from that of a column of $n$, or if any element of $m$ or $n$ is not a number, the result is $\bot$ .

$\text{MM}$ 程序有四个步骤，从右往左，以此执行。从 $[ 1, \text{trans} \circ 2 ]$ 开始，得到最初的结果。当参数满足 $< m,n >$ ，则

1. 执行第一步得到 $< m, n' > \text{where } n' = \text{trans}:n$ ；
2. 执行第二步得到 $< < m_1, n' >, ..., < m_r, n' > >$ ， 其中 $m_i$ 是矩阵 $m$ 的一行；
3. 执行第三步， $\alpha \text{distl}$ ，得到 $< \text{distl} : < m_1, n' >, \dots, \text{distl} : < m_r, n' > > = < p_1, \dots, p_r >$ ，其中 $p_i = \text{distl} : < m_1, n' > = < < m_i, n_1' >, \dots, < m_i, n_s' > > \text{for } i = 1, \dots, r$ ， 且 $n_j'$ 是 $n$ 的第 $j$ 列（也就是 $n'$ 的第 $j$ 行）。 $p_i$ 则是行列对序列对应的第 $i$ 个行积；
4. 最后一步， $\alpha \alpha \text{IP}$ ，或是 $\alpha (\alpha \text{IP})$ ， 即对每个 $p_i$ 应用 $\alpha \text{IP}$ ，也就是对每个 $p_i$ 的行列对应用 $\text{IP}$ 。这样一个由行序列构成其结果就是矩阵积。

如果矩阵不是矩形，又或是 $m$ 的行数对不上 $n$ 的列数，还是二者的任意元素不是数字，其结果都是 $\bot$ 。

> This program $\text{MM}$ does not name its arguments or any intermediate results; contains no variables, no loops, no control statements nor procedure declarations; has no initialization instructions; is not word-at-a-time in nature; is hierarchically constructed from simpler components; uses generally applicable housekeeping forms and operators (e.g., $\alpha f, \text{distl}, \text{distr}, \text{trans}$ ); is perfectly general; yields $\bot$ whenever its argument is inappropriate in any way; does not constrain the order of evaluation unnecessarily (all applications of $\text{IP}$ to row and column pairs can be done in parallel or in any order); and, using algebraic laws (see below), can be transformed into more "efficient" or into more "explanatory" programs (e.g., one that is recursively defined). None of these properties hold for the typical von Neumann matrix multiplication program.

程序 $\text{MM}$ ，没有命名参数，或任何中间结果；它不包含变量，循环，控制语句，以及任何过程声明；它没有初始化指令，甚至天然不是逐字处理的；它由各种小组件有层次的构建而成，像是通用的“收拾”（housekeeping）组合形式和操作（比如， $\alpha f, \text{distl}, \text{distr}, \text{trans}$ ），适用性极强；即便在任何时候，面对任何可能的不恰当的参数，它都会得到 $\bot$ 。它不要求必须按顺序执行（对所有行列对应用 $\text{IP}$ 完全可以是平行或其它任意顺序），并且依据代数定律（见后文）可将其替换成更“高效”，或更“清晰”版本（例如，一个递归风格的版本）。相反，这些性质是一个典型的冯·诺伊曼式矩阵乘法程序所不具备的。

> Although it has an unfamiliar and hence puzzling form, the program $\text{MM}$ describes the essential operations of matrix multiplication without overdetermining the process or obscuring parts of it, as most programs do; hence many straightforward programs for the operation can be obtained from it by formal transformations. It is an inherently inefficient program for von Neumann computers (with regard to the use of space), but efficient ones can be derived from it and realizations of FP systems can be imagined that could execute MM without the prodigal use of space it implies. Efficiency questions are beyond the scope of this paper; let me suggest only that since the language is so simple and does not dictate any binding of lambda-type variables to data, there may be better opportunities for the system to do some kind of "lazy" evaluation [^9] [^10] and to control data management more efficiently than is possible in lambda-calculus based systems.

虽然程序 $\text{MM}$ 的形式可能看起来陌生让人费解，但它却清晰地描述了矩阵乘法的核心运算。不像大多数程序那样，过度限定计算过程或隐藏细节。由此可见，通过形式化变换可以得到许多简洁的程序。虽然，在冯诺依曼计算机上运行时，其效率天生低下，因为它会占用大量的空间；但是，我们可以从中推导高效的版本，可以想象一些 FP 系统的实现能够高效执行，并像程序本身那样浪费空间。关于效率的问题超出了本文的讨论范围，但我必须指出，函数式编程语言如此简单，且避免了 lambda 类型变量和数据的绑定关系，可能为系统带来一些优势。比如，可以采用某种形式的惰性求值 (lazy evaluation) [^9] [^10] ，以及更有效的数据管理，而这些是基于 lambda 演算的系统可能难以实现。

[^9]: TODO
[^10]: TODO

[^booch]: <https://x.com/Grady_Booch/status/1016041695501139968?s=20>
