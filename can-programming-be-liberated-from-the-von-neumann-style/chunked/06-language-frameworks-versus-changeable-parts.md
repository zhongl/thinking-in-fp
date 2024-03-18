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
