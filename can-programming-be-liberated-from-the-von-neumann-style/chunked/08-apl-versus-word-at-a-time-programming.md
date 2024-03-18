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
