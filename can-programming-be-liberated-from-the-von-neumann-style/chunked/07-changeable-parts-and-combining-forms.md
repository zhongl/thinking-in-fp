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
