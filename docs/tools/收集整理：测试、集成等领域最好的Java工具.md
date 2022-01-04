## 收集整理：测试、集成等领域最好的Java工具
(本文转载于：https://www.evget.com/article/2017/7/18/26597.html)

概述：在涉及到使用Java进行开发、测试、模拟、安全性以及集成时，你如何对众多的工具进行挑选呢？

[# 31款JAVA开发必备控件和工具 ](https://www.evget.com/article/2020/10/22/38763.html)[# 开发软/控件产品年终优惠](https://www.evget.com/zt/2021/10/)

无论你是刚入门，还是进行了一段时间的开发，使用合适的工具编程都会让你事半功倍，它能够让你更快的编写代码，能够快速及时的为你识别出Bug，能够让你的代码质量更上一层楼。

如果你选择的编程语言是Java，那么从编码、测试到服务器集成、文档，你都可以找到专注于开发的每个方面的工具。现在，让我们来挑选其中的佼佼者吧。

### **Java编辑器与开发**

------

![img](http://image.evget.com/images/article/2017/javatools-20170718-1.PNG)

#### **1.Java开发工具包（JDK）**

对于任何计划开发小程序和应用程序的人来说，[JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)都是必不可少的工具。它包括Java运行时环境、Java编译器和Java API。换句话说，它拥有从Java初学者到经验丰富的程序员所需要的一切东西。

#### **2.NetBeans**

在讨论Java最受欢迎的IDE时，NetBeans总是会被人所提及。作为一个开源的工具，它拥有以下强大的功能：

- 支持多种语言
- 包含丰富的插件。比如用于Java和PHP的ResinTemplateModule，可用于开发iOS、Android和Windows本地化Java应用程序的插件， CSS minifier等等
- 开箱即用的Git和Maven集成
- 帮助分析和修复代码中错误的调试器和配置文件

#### **3. Eclipse IDE**

Eclipse IDE是另外一个广受欢迎的IDE，有54%的Java开发人员使用。和NetBeans一样，它也是开源的，同时也有大量的插件和可定制的接口。它还拥有许多其它特性，比如代码实现辅助、语法检查和重构等。

#### **4. Groovy**

Groovy不是一种编辑器，而更像一种编程语言，它通过添加新关键字以及自动导入常用类和可选的变量声明来扩展Java的功能。它还提供了强大的脚本功能，支持你将类编译为Java字节码，者通过Groovy Shell动态地执行它们。

### **测试**

------

![img](http://image.evget.com/images/article/2017/javatools-20170718-2.PNG)

#### **1. Mockito**

[Mockito](http://mockito.org/)作为一个模拟框架，支持你创建和使用简化版本的对象和过程，以实现自动化单元测试。由于它简单而干净的API以及在程序执行后可以提问的特点，许多程序员非常青睐它。Mockito还可以：

- 模拟具体的类和接口
- 提供干净的验证错误
- 允许你指定顺序以进行灵活的验证
- 支持精确次数和至少一次的验证

#### **2. JRat**

[JRat](http://jrat.sourceforge.net/)（Java Runtime Analysis Toolkit）是Java平台的性能分析器。它可以监视应用程序的执行以及对持续性能进行测量，并支持你通过JRat桌面应用程序查看和分析数据。此外，你还可以使用它来识别可能影响应用程序性能的潜在问题区域。

#### **3. JUnit**

JUnit是一个可以让你一次测试一个代码块的单元测试工具。换句话说，你不必等到完成全部代码才来测试它。特性包括：

- 用于测试预期结果的断言
- 共享通用测试数据的测试装置
- 用于运行测试的测试运行器

### **集成**

------

![img](http://image.evget.com/images/article/2017/javatools-20170718-3.PNG)

#### **1. Apache Ant**

该工具由Apache开发，它为你提供了内置的任务，这些任务不仅有助于开发、编译和测试Java应用程序，还能帮助自动化完成重复的任务。

#### **2. Apache Maven**

有超过68%的Java开发人员青睐的Maven是一个项目管理构建工具，它提供了统一的构建系统、质量项目信息和最佳实践开发指南。Maven的主要特性包括：

- 遵循最佳实践的简单项目设置
- 优越的依赖关系管理，包括自动更新和依赖闭包
- 能够同时轻松地处理多个项目
- 一个庞大且不断增长的库和元数据存储库
- 用Java或脚本语言编写的可扩展插件

#### **3. Gradle**

Gradle是一个构建自动化的系统，它包含了软件包以及其它类型项目的自动化构建、测试和部署。它结合了ANT的最佳特性以及Maven优越的依赖关系管理，使你能够更好地使用这两个工具特性，更舒适的编写代码。

### **安全**

------

![img](http://image.evget.com/images/article/2017/javatools-20170718-4.PNG)

#### **1. FindBugs**

正如名称所示，该工具通过将文档与已知错误的数据库相匹配来帮助识别代码中的错误。它可以作为一个独立的GUI，也可以作为包括Eclipse和NetBeans在内的许多代码编辑器的插件。

#### **2. SonarQube**

[SonarQube](https://www.sonarqube.org/)支持你访问整个平台来分析代码的bug和漏洞。功能包括：

- 关于重复代码、编码标准、单元测试、代码覆盖率、复杂代码、潜在bug等的报告
- 与大多数持续集成工具集成
- 多语言支持

### **服务器**

------

![img](http://image.evget.com/images/article/2017/javatools-20170718-5.PNG)

#### **1. Apache Tomcat**

[Apache Tomcat](http://tomcat.apache.org/)是最流行的web服务器之一。它实现了一系列Java EE规范，如Java Servlet、JavaServer Pages(JSP)、Java EL和WebSocket。它还提供了运行代码的HTTP服务器环境。

#### **2. WildFly**

[WildFly](http://wildfly.org/)是由Red Hat开发的，另外一种流行的web服务器。它实现了Java平台的企业版功能，你可以在上面访问任意平台上的企业功能。