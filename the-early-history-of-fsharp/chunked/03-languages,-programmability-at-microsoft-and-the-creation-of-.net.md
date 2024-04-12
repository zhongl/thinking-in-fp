> 3 BACKGROUND: LANGUAGES, PROGRAMMABILITY AT MICROSOFT AND THE CREATION OF .NET

## 3 背景：语言、微软的可编程性和 .NET 的创建

> The 1970s-80s saw continual, rapid expansion of the computing industry, from transistor design and chip fabrication to software development and applications. Software development tooling both boomed and consolidated with the development and adoption of many different programming paradigms and languages, including BASIC, PASCAL, Prolog, Modula 2 and C. Accompanying each were commercial variations (Visual Basic, Turbo Pascal, Borland C for example). Languages such as Logo served to spark the imagination of a new generation that programming could be "different"[^3] and a bold new era of "fourth generation languages" was promised.

70 年代和 80 年代，从晶体管设计、芯片制造，到软件开发和应用程序，整个计算行业得到了快速地发展。像 BASIC、PASCAL、Prolog、Modula 2 和 C，随着这些不同编程范式和语言的开发采用，带动其软件开发工具的大爆发，并更加巩固。每种语言都还伴随着商业上的变体（例如 Visual Basic、Turbo Pascal 和 Borland C）。编程语言（如Logo）让人们相信下一代的编程可以是另一番景象 [^3]，并承诺了一个“第四代语言”的大胆新纪元。

> At this time, Microsoft also saw massive expansion as an operating system and applications company. Microsoft started by building programming tools in 1975 and the importance of programmability both as a commercial and technical undertaking - was "in the bones" of the company and its CEO Bill Gates [Wikipedia 2020b]. Through the 1980s his primary concern with regard to programmability was commercial: how to support the creation of applications and a commercial ecosystem of independent software vendors (ISVs) for the DOS and Windows ecosystems. What mattered most was the sheer number of developers using these platforms, for developers would feed the growth of these ecosystems. The company created tools such as Visual Basic to satisfy the mass-developer market, and versions of C for more hard-core developers, a distinction that later got characterized as tools for "Mort" (Visual Basic) and "Einstein" (C++) [Wikipedia 2019d].[^4] Such tooling was pitted against a myriad of rapid development environments such as HyperCard [Wikipedia 2019b] and [Wikipedia 2019e], and Microsoft succeeded hands-down, becoming dominant in application development worldwide and achieving a monopoly position in operating systems. Microsoft also made numerous other programming tools including FoxPro [Wikipedia 2000] and a FORTRAN compiler, later discontinued [WinWorld 2016].

此时，微软作为操作系统和应用程序公司也经历了大规模扩张。微软从 1975 年开始构建编程工具，可编程性作为一项商业和技术事业的重要性已经“根植于”公司及其首席执行官比尔盖茨的“骨子里” [维基百科 2020b]。在整个 80 年代，他对可编程性的主要关注点是商业性，即如何支持应用程序的创建，以及那些 DOS 和 Windows 之上的独立软件供应商 (ISV) 的商业生态。最重要的是使用这些平台的开发人员数量，因为开发人员将推动这些生态系统的增长。该公司创建了诸如 Visual Basic 之类的工具来满足大众开发人员市场，以及针对更硬核开发人员的 C 版本，这种区别后来被描述为“Mort”（Visual Basic）和“Einstein”（C++）的工具 [维基百科 2019d][^4]。此类工具与诸如 HyperCard [Wikipedia 2019b] 和 [维基百科 2019e] 等快速开发环境竞争，微软取得了压倒性胜利，成为全球应用程序开发的领导者，并在操作系统领域取得了垄断地位。微软还制作了许多其他编程工具，包括 FoxPro [维基百科 2000] 和后来停产的 FORTRAN 编译器 [WinWorld 2016]。

[^3]: > I recall my primary school librarian telling me about Logo on a school walk in 1981, when I was 10. It was my first exposure to diversity in the world of programming languages.
    
    1981年，那时我才10岁，我和校图书管理员在学校漫步时，他跟我讲起了 Logo 这门编程语言。那是我第一次感受到编程语言的世界可以如此不同。

[^4]: > The term "Elvis" was used later for C# programmers. 

    “Elvis”一词后来也被用来特指 C# 程序员。

> The prospect of an industry-shifting nexus between this new wave of software development methodology and an operating system company drew tantalizingly near. For example, the launch of NEXTStep 3.0 in 1993 featured heavy focus on "objects" as a concept that the NEXTStep OS somehow supported (in practice this meant that NeXTStep application development was based on Objective C - the OS itself, was written in C). This was used by Jobs to demonstrate its sophistication and technical maturity. When Java was developed in 1991-95, and released in 1996, it was a deep challenge to Microsoft in at least six ways:

这种新的软件开发方法与操作系统公司之间可能改变行业格局的联系变得越来越诱人。例如，1993 年发布的 NEXTStep 3.0 突出强调了“对象”的概念，其操作系统在某种程度上支持了该概念（实际上这意味着 NeXTStep 的应用程序是基于 Objective-C 开发 - 而操作系统本身是用 C 编写的）。乔布斯利用这一点来展示其复杂性和技术成熟度。当 Java 在 1991-1995 年开发，并于 1996 年发布，它至少在六个方面对微软提出了重大挑战：

> - Java was object-oriented and "modern";
> - Java promised Write Once Run Anywhere software development that could in theory cut the
dependence on a particular operating system;
> - Java was developed by a direct rival in the upper-end operating system market;
> - Java was positioned as a web-technology at the dawn of the web, potentially capable of delivering end-user applications via the browser;
> - Java used a set of technical devices such as a virtual machine (VM) and garbage collection (GC)[^5]; and
> - Java was recognized as a contribution to applied academic computer science[^6], bringing on board a constituency who had been largely ignored by Microsoft. As a result, Java became embraced as a de-facto standard for typed object-orientation.

- Java 是面向对象的且“现代”的；
- Java 承诺“一次编写，到处运行”的软件开发，理论上可以减少对特定操作系统的依赖；
- Java 由高端操作系统市场上的直接竞争对手开发；
- Java 在网络刚刚兴起时被定位为一种网络技术，有可能通过浏览器提供最终用户应用程序；
- Java 使用了一套技术手段，例如虚拟机 (VM) 和垃圾回收 (GC) [^5]；
- Java 被认为是对应用学术计算机科学的贡献 [^6]，吸引了微软以前基本上忽略的受众。因此，Java 被奉为类型化面向对象的事实标准。

[^5]: Garbage collection was present in Visual Basic. However it was not present in the highly influential Microsoft COM programming architecture, which used reference counting for memory management.

    Visual Basic 是有垃圾回收的。然而，有着更高影响力的微软 COM 编程架构却不具备这种靠引用计数管理内存的特性。

[^6]: For example [^Alves-Foss-1999].

[^Alves-Foss-1999]: [Formal Syntax and Semantics of Java. Lecture Notes in Computer Science, Vol. 1523. Springer Berlin Heidelberg.](https://doi.org/10.1007/3-540-48737-9) .

> Microsoft was initially slow to respond. Internally, the company was committed to C for implementing its flagship products but had plenty of assembly code as well. Given the target hardware specs it was unrealistic to write Windows or Microsoft Word in a heap-allocating "toy" language like Java, so Java was not going to become the major language of internal use at Microsoft quickly. Further, external-facing RAD environments like Visual Basic didn’t immediately benefit from the structured approach to OO found in class-oriented languages. With a tidal wave of Java hype flooding the industry, Microsoft responded by embracing Java, licensed from Sun in 1996 (Microsoft J++), but subsequently faced legal action for extending the language. This formed part of the background to United States v. Microsoft Corp, a legal case running from formally from 1998 to 2001 though with its roots in earlier actions. In this case the U.S. government accused Microsoft of illegally maintaining its monopoly position in the PC market, through restrictions on PC manufacturers relating to internet browser software and other programs such as Netscape and Java. The initial trial recommendations were to break-up Microsoft as a company, later settled to lesser remedies.

面对 Java 浪潮席卷整个行业，微软最初反应迟钝。公司内部致力于使用 C 语言来实现其旗舰产品，同时也有大量汇编代码。考虑到目标硬件规格，用像 Java 这样分配堆内存的“玩具”语言来编写 Windows 或 Microsoft Word 是不现实的，因此 Java 不会很快成为微软内部使用的主要语言。此外，面向外部的 RAD 环境（例如 Visual Basic）也不能立即从面向类的语言中找到的面向对象结构化方法中受益。由于行业充斥着 Java 的炒作热潮，微软通过接受 Java 做出了回应，并于 1996 年从 Sun 获得了许可（Microsoft J++）。但随后因扩展语言而面临法律诉讼。这是美国诉微软公司案 (United States v. Microsoft Corp) 的背景的一部分，该案案发时间正式为 1998 年至 2001 年，但根源可以追溯到更早的诉讼。在此案中，美国政府指控微软通过限制个人电脑制造商使用互联网浏览器软件和其他程序（例如 Netscape 和 Java）的方式，非法维持其在 PC 市场上的垄断地位。最初的审判建议是将微软公司拆分，后来以较少的补救措施达成和解。

> In 1997, Microsoft changed tack and started the internal development of a new programmability platform which could address the fundamental challenge of Java, while also addressing the needs specific to Windows programmability. Initially called COM+ 2.0 or Lightning, and eventually .NET, the founding principles of the runtime environment were as follows:

1997 年，微软改变了策略，开始内部开发一个新的可编程性平台，该平台可以应对 Java 的根本挑战，同时还能满足 Windows 可编程性的特定需求。该平台最初称为 COM+ 2.0 或 Lightning，最终命名为 .NET。运行环境的创始原则如下：

> - It would support multiple programming languages, including Visual Basic, C++ and Java. Additionally, a new language was started, under the design of Anders Hejlsberg, initially called COOL and later C#.
> - It would support a bytecode, garbage collection, JIT compilation and "middleware" features such as stack-based security checks and remoting. Additionally, the runtime would support unsigned integers, unboxed representations and install-time compilation.
> - It would be made specifically for application development on Windows, including native interoperability to C-based Win32 APIs and built-in support for COM. However, it would also be sufficiently general that porting to other operating systems would be theoretically possible.
> - Its SDK would be offered free and aligned with emerging efforts in academic relations, then managed by Microsoft Research, founded in 1992.

- 它将支持多种编程语言，包括 Visual Basic、C++ 和 Java。此外，还启动了一种新语言，由 Anders Hejlsberg 设计，最初称为 COOL，后来改名 C#；
- 它将支持字节码、垃圾回收、即时编译 (JIT) 和“中间件”功能，例如基于堆栈的安全检查和远程调用。此外，运行环境还将支持无符号整数、解包表示和安装时编译；
- 它将专为在 Windows 上进行应用程序开发，包括与基于 C 的 Win32 API 的原生互操作性以及对 COM 的内置支持。但是，它也足够通用，理论上可以移植到其他操作系统；
- 其 SDK 将免费提供，且与学术关系方面的新兴努力保持一致，并由 1992 年成立的微软研究院 (Microsoft Research) 管理。

> The decisions around Lightning were regularly reviewed by Bill Gates. Through the efforts of two "developer evangelists" - Peter and James Plamondon[^7] - a key decision was made: Lightning would be a multi-language runtime rather than just a fixed set of languages decided by Microsoft. An outreach project called "Project 7" was initiated: the aim was to bring seven commercial languages and seven academic languages to target Lightning at launch. While in some ways this was a marketing activity, there was also serious belief and intent. For help with defining the academic languages James Plamondon turned to Microsoft Research (MSR).

关于 Lightning 的决策由比尔·盖茨定期审查。通过两名“开发布道者”——Peter 和 James Plamondon [^7] 的努力——做出了一个关键决定：Lightning 将成为一个多语言运行环境，而不是由微软决定的一组固定语言。启动了一个名为“Project 7”的外联项目：目标是在发布时让七种商业语言和七种学术语言支持 Lightning。尽管在某种程度上这是一项营销活动，但也存在着严肃的信念和意图。为了帮助定义学术语言，James Plamondon 求助于微软研究院 (MSR)。

[^7]: Known as "The Flying Plamondon Brothers"

> From the perspective of the history of F#, this is a moment when largely unrelated traditions in the history of computer science began to merge and intertwine: the worlds of Robin Milner and Bill Gates began to meet.

从 F# 历史的角度来看，这是一个计算机科学史上按原本毫不相关的风格开始融合交织的时刻：罗宾·米尔纳 (Robin Milner) 和比尔·盖茨 (Bill Gates) 的世界开始相遇。

> MSR had been founded in 1992 and expanded to Cambridge UK in September 1997. Andy Gordon (a high-profile young researcher in programming language theory) and Luca Cardelli (author of one of the first ML implementations and prolific researcher) were hired, followed in September 1998 by Simon Peyton Jones (a leading Haskell contributor), Nick Benton (a theorist and initiator of MLj, discussed later), Cedric Fournet (a core member of the OCaml team), Sir Tony Hoare (world famous computer scientist) and Don Syme (the author of this paper; undergraduate student of early ML contributor Malcolm Newey in Australia; PhD student of Mike Gordon; with a background in functional programming, formal verification and Java). MSR eventually employed over 500 researchers and engineers in various locations.

微软研究院 (MSR) 成立于 1992 年，并于 1997 年 9 月扩展到英国剑桥。Andy Gordon（一位引人注目的年轻编程语言理论研究员）和 Luca Cardelli（第一批 ML 实现者之一，多产研究员）受雇于此，随后在 1998 年 9 月，Simon Peyton Jones（主要的 Haskell 贡献者）、Nick Benton（理论家和稍后讨论的 MLj 发起人）、Cedric Fournet（OCaml 团队核心成员）、Sir Tony Hoare（世界著名计算机科学家）和 Don Syme（本文作者；澳大利亚早期 ML 贡献者 Malcolm Newey 的本科生；Mike Gordon 的博士生；拥有函数式编程、形式验证和 Java 背景）加入 MSR。MSR 最终在多个地方雇佣了 500 多名研究人员和工程师。

> Suddenly Microsoft was brimming with academic computer scientists, though in a separate "org" to the "product teams". Many were eager to make an impact on Microsoft’s product range, and there was cultural memory from Bell Labs (Cardelli), DEC-SRC (Cardelli), Compaq (Gordon) and Intel (Syme) that this was how such labs "paid the bills". Each researcher was in their own way deeply evangelical about one point-of-view or another in computer science and often held tribal allegiances to their corresponding communities in academia, both of which shaped their interactions with product teams and the projects they chose. Many in the formal verification and theory areas had experience of strongly-typed functional programming. Robin Milner, the originator of the ML family of languages, was head of department at Cambridge University "across the road" and was held in high esteem as a pioneer in the field of research.

突然之间，微软内部挤满了学术计算机科学家，尽管他们与“产品团队”分属不同的“组织”。许多人都渴望对微软的产品线产生影响，贝尔实验室 (Cardelli)、DEC-SRC (Cardelli)、康柏  (Gordon) 和英特尔 (Syme) 的文化记忆告诉他们，这才是这类实验室“养家糊口”的方式。每位研究人员都以自己独特的方式对计算机科学中的某个观点或另一个观点充满热情，并且经常忠于他们各自所在学术界的社区，这两者都塑造了他们与产品团队以及他们选择的项目的互动。形式验证和理论领域的许多人都有强类型函数式编程的经验。而 ML 语言家族的创始人 Robin Milner 是剑桥大学计算机系主任，就在“马路对面”，作为该领域的先驱受到高度尊敬。

> On the other side, Microsoft was entering a phase where it was becoming deeply committed to a multi-language runtime and wanted to be seen to innovate positively. Lightning already had many of the core elements of a typical functional language implementation (GC, JIT, bytecode), and promised to unite disparate themes in programming, though initially within the confines of the Windows operating system. The scene was set for interesting things to happen. The Lightning effort was renamed NGWS and then finally called .NET on launch in 2000.

另一方面，微软正进入一个深度致力于多语言运行环境并希望被视为积极创新的阶段。Lightning 已经拥有了典型函数式语言实现 (GC、JIT、字节码) 的许多核心元素，并承诺统一编程中的不同主题，尽管最初仅限于 Windows 操作系统的范围内。而这一切都开始变得有趣了起来。Lightning 项目随后更名为 NGWS，最终在 2000 年发布时称为 .NET。