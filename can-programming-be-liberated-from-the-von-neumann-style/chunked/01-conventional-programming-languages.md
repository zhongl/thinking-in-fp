
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
