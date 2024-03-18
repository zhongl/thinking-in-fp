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
