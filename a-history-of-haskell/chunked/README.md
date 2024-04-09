---
title: "A History of Haskell: Being Lazy With Class"
origin: https://dl.acm.org/doi/10.1145/1238844.1238856
authors:
  - name: "Paul Hudak"
    orgnization: "Yale University"
    email: "paul.hudak@yale.edu"
  - name: "John Hughes"
    orgnization: "Chalmers University"
    email: "rjmh@cs.chalmers.se"
  - name: "Simon Peyton Jones"
    orgnization: "Microsoft Research"
    email: "simonpj@microsoft.com"
  - name: "Philip Wadler"
    orgnization: "University of Edinburgh"
    email: "wadler@inf.ed.ac.uk"
---


> Abstract

## 摘要

> This paper describes the history of Haskell, including its genesis and principles, technical contributions, implementations and tools, and applications and impact.

本文描述了 Haskell 的历史，涵盖了它的起源和原则、技术贡献、实现和工具，以及应用和影响。

> 1 . Introduction

## 1. 介绍

> > In September of 1987 a meeting was held at the conference on Functional Programming Languages and Computer Architecture in Portland, Oregon, to discuss an unfortunate situation in the functional programming community: there had come into being more than a dozen non-strict, purely functional programming languages, all similar in expressive power and semantic underpinnings. There was a strong consensus at this meeting that more widespread use of this class of functional languages was being hampered by the lack of a common language. It was decided that a committee should be formed to design such a language, providing faster communication of new ideas, a stable foundation for real applications development, and a vehicle through which others would be encouraged to use functional languages.

> 1987 年 9 月，在俄勒冈州波特兰举行的一次函数式编程语言和计算机体系结构会议上，讨论了函数式编程社区不幸的局面：出现了十多种非严格的纯函数式编程语言，它们在表达能力和语义基础上都非常相似。这次会议强烈一致认为，缺乏一种通用语言阻碍了这类函数式语言的更广泛使用。与会者决定成立一个委员会来设计这种语言，以便更快地交流新思想，为真正的应用程序开发提供一个稳定的基础，并成为鼓励其他人使用函数式语言的载体。

> These opening words in the Preface of the first Haskell Report, Version 1.0 dated 1 April 1990, say quite a bit about the history of Haskell. They establish the motivation for designing Haskell (the need for a common language), the nature of the language to be designed (non-strict, purely functional), and the process by which it was to be designed (by committee).

上述引文是 1990 年 4 月 1 日发布的 Haskell 报告 1.0 版本的序言开头，它揭示了 Haskell 的历史。 它阐明了设计 Haskell 的动机（需要一种通用语言）、要设计的语言的性质（非严格的、纯函数式的）以及设计过程（由委员会设计）。

> Part I of this paper describes genesis and principles: how Haskell came to be. We describe the developments leading up to Haskell and its early history (Section 2) and the processes and principles that guided its evolution (Section 3).

本文的 **第一部分** 描述了语言的起源和原则，即 Haskell 的何去何从。其中包括了导致 Haskell 出现的事件以及早期历史（第二节），和指导 Haskell 演化的过程与原则（第三节）。

> Part II describes Haskell’s technical contributions: what Haskell is. We pay particular attention to aspects of the language and its evolution that are distinctive in themselves, or that developed in unexpected or surprising ways. We reflect on five areas: syntax (Section 4); algebraic data types (Section 5); the type system, and type classes in particular (Section 6); monads and input/output (Section 7); and support for programming in the large, such as modules and packages, and the foreign-function interface (Section 8).

**第二部分** 描述了 Haskell 的技术贡献，即 Haskell 是什么。这里会重点突出语言及其演变中的一些独特之处，亦或是在意料之外喜中发展出来的点。它们可以分五个方面：语法（第四节）；代数数据类型（第五节）；类型系统，尤其是类型族（type classes）（第六节）；Monad 及输入输出（第七节）；大型系统的相关支持，如模块、包和外函数（foreign-function）接口（第八节）。

> Part III describes implementations and tools: what has been built for the users of Haskell. We describe the various implementations of Haskell, including GHC, hbc, hugs, nhc, and Yale Haskell (Section 9), and tools for profiling and debugging (Section 10).

**第三部分** 描述了实现与工具，即为 Haskell 用户构建了什么。这些 Haskell 的实现有， GHC、hbc、hugs、nhc 和 Yale Haskell（第九节），以及用于分析调试的工具（第十节）。

> Part IV describes applications and impact: what has been built by the users of Haskell. The language has been used for a bewildering variety of applications, and in Section 11 we reflect on the distinctive aspects of some of these applications, so far as we can discern them. We conclude with a section that assesses the impact of Haskell on various communities of users, such as education, opensource, companies, and other language designers (Section 12).

**第四部分** 描述了应用和影响，即 Haskell 用户能用它们来构建什么。在第十一节里，将突出语言之所以被用于各种令人困惑的应用场景里的独特之处。最后的一节里，将评估 Haskell 对教育、开源社区、公司以及其他语言设计者等不同社群的影响。

> Our goal throughout is to tell the story, including who was involved and what inspired them: the paper is supposed to be a history rather than a technical description or a tutorial.

我们从头到尾都在讲述故事，告诉大家参与其中的人员以及他们的灵感来源。因此，本文应仅仅只是一段历史，而不是一篇技术性描述或教程。

> We have tried to describe the evolution of Haskell in an evenhanded way, but we have also sought to convey some of the excitement and enthusiasm of the process by including anecdotes and personal reflections. Inevitably, this desire for vividness means that our account will be skewed towards the meetings and conversations in which we personally participated. However, we are conscious that many, many people have contributed to Haskell. The size and quality of the Haskell community, its breadth and its depth, are both the indicator of Haskell’s success and its cause.

我们力求客观地描述 Haskell 的发展历程，但也希望通过一些轶事和个人反思来传达当时激动和热情的氛围。由于加入了个人参与过的会议和对话细节，描述不可避免的会存在一定偏向。当然，正是因为有许许多多人参与到 Haskell 的贡献中，才使得社区无论在规模还是质量，在广度还是深度，让 Haskell 变得如此成功。

> One inevitable shortcoming is a lack of comprehensiveness. Haskell is now more than 15 years old and has been a seedbed for an immense amount of creative energy. We cannot hope to do justice to all of it here, but we take this opportunity to salute all those who have contributed to what has turned out to be a wild ride.

缺乏全面性必然是本文的不足之处。毕竟，Haskell 已经有超过 15 年的历史，并且孕育了大量富有创造力的成果。我们无法寄期望于在此完全涵盖所有内容，但仍然想借此机会向所有做出贡献的人们致敬，是他们让这段旅程变得如此狂野刺激。