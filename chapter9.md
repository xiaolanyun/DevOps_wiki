### 9、Sonar

介绍

Sonar 是一个用于代码质量管理的开放平台。通过插件机制，Sonar 可以集成不同的测试工具，代码分析工具，以及持续集成工具。与持续集成工具（例如 Hudson/Jenkins 等）不同，Sonar 并不是简单地把不同的代码检查工具结果（例如 FindBugs，PMD 等）直接显示在 Web 页面上，而是通过不同的插件对这些结果进行再加工处理，通过量化的方式度量代码质量的变化，从而可以方便地对不同规模和种类的工程进行代码质量管理。 

在对其他工具的支持方面，Sonar 不仅提供了对 IDE 的支持，可以在 Eclipse和 IntelliJ IDEA 这些工具里联机查看结果；同时 Sonar 还对大量的持续集成工具提供了接口支持，可以很方便地在持续集成中使用 Sonar。 
此外，Sonar 的插件还可以对 Java 以外的其他编程语言提供支持，对国际化以及报告文档化也有良好的支持
最新版的Sonar需要至少JDK 1.8及以上版本。

Sonar的功能就是来检查代码是否有BUG。除了检查代码是否有bug还有其他的功能，比如说：你的代码注释率是多少，代码有一些建议，编写语法的建议。所以我们叫质量管理

Sonar还可以给代码打分