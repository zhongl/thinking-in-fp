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

# 编程可以从冯·诺伊曼风格中解放出来吗？一种函数式风格及其程序的代数

