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


1. [传统编程语言：臃肿与乏力](./01-conventional-programming-languages.md)
2. [计算系统的模型](./02-models-of-compute-systems.md)
3. [冯·诺伊曼计算机](./03-von-neumann-computers.md)
4. [冯·诺伊曼语言](./04-von-neumann-languages.md)
5. [冯·诺伊曼与函数式编程的比较](./05-comparison-of-von-neumann-and-functional-programs.md)
6. [语言的框架与可变的部分](./06-language-frameworks-versus-changeable-parts.md)
7. [可变部分与组合形式](./07-changeable-parts-and-combining-forms.md)
8. [APL与逐字编程](./08-apl-versus-word-at-a-time-programming.md)
9. [冯·诺伊曼语言缺乏有用的数学性质](./09-von-neumann-languages-lack-useful-mathematical-properties.md)
10. [冯·诺伊曼语言替代方案是什么？](./10-what-are-the-alternatives-to-von-neumann-languages.md)
11. [函数式编程系统](./11-functional-programming-systems.md)
12. [FP系统里的程序代数](./12-the-algebra-of-programs-for-fp-systems.md)
13. [函数式编程的形式化系统](./13-formal-systems-for-functional-programming.md)
14. [应用型状态转换系统](./14-applicative-state-transition-systems.md)
15. [计算机设计的小结](./15-remarks-about-computer-design.md)
16. [总结](./16-summary.md)

> *Acknowledgments*. In earlier work relating to this paper I have received much valuable help and many suggestions from Paul R. McJones and Barry K. Rosen. I have had a great deal of valuable help and feedback in preparing this paper. James N. Gray was exceedingly generous with his time and knowledge in reviewing the first draft. Stephen N. Zilles also gave it a careful reading. Both made many valuable suggestions and criticisms at this difficult stage. It is a pleasure to acknowledge my debt to them. I also had helpful discussions about the first draft with Ronald Fagin, Paul R. McJones, and James H. Morris, Jr. Fagin suggested a number of improvements in the proofs of theorems. 

**致谢**

在撰写这篇论文之前的工作中，我便得到了 Paul R. McJones 和 Barry K. Rosen 的许多宝贵帮助和建议。在准备这篇论文的过程中，我同样得到了很多宝贵的帮助和反馈。James N. Gray 在审阅第一稿时慷慨地提供了他的时间和知识；Stephen N. Zilles 也仔细阅读了它。他们俩在这个艰难的阶段都提出了许多宝贵的建议和批评，我很荣幸能够感谢他们。我还与 Ronald Fagin、Paul R. McJones 和 James H. Morris Jr. 就初稿进行了收益良多的讨论，其中 Fagin 提出了几个改进定理证明的方法。

> Since a large portion of the paper contains technical material, I asked two distinguished computer scientists to referee the third draft. David J. Giles and John C. Reynolds were kind enough to accept this burdensome task. Both gave me large, detailed sets of corrections and overall comments that resulted in many improvements, large and small, in this final version (which they have not had an opportunity to review). I am truly grateful for the generous time and care they devoted to reviewing this paper. Finally, I also sent copies of the third draft to Gyula A. Mag6, Peter Naur, and John H. Williams. They were kind enough to respond with a number of extremely helpful comments and corrections. Geoffrey A. Frank and Dave Tolle at the University of North Carolina reviewed Mag6's copy and pointed out an important error in the definition of the semantic function of FFP systems. My grateful thanks go to all these kind people for their help.

由于论文的大部分内容都是技术性的，因此我请了两位杰出的计算机科学家来评审第三稿。David J. Giles 和 John C. Reynolds 都很乐意接受这项繁重的任务，并给了我大量详细的纠正和总体评论，从而使这个最终版本（他们没有机会审阅）得到了不少或大或小的改进。我真心地感谢他们为审阅这篇论文所付出的慷慨时间和精力。最后，我还将第三稿副本发送给了 Gyula A. Magó、Peter Naur 和 John H. Williams，他们都非常友善地回复了一些非常有帮助的评论和纠正。北卡罗来纳大学的 Geoffrey A. Frank 和 Dave Tolle 审查了 Magó 的副本，并指出了 FFP 系统语义函数定义中的一个重要错误。我对所有这些好心人提供的帮助表示衷心的感谢。