# 一、Java的概念、安装与配置

-------------------

[TOC]

## 1、Java简介

> Java是由Sun Microsystems公司于1995年5月推出的Java面向对象程序设计语言和Java平台的总称。由James Gosling和同事们共同研发，并在1995年正式推出。

Java分为三个体系：

> + **JavaSE (J2SE)**  —— Java 2 Platform Standard Edition，标准版
> + **JavaEE (J2EE)**   —— Java 2 Platform,Enterprise Edition，企业版
> + **JavaME (J2ME)** —— Java 2 Platform Micro Edition，微型版


2005年6月，JavaOne大会召开，SUN公司公开Java SE 6。此时，Java的各种版本已经更名以取消其中的数字"2"：J2EE更名为`Java EE`, `J2SE`更名为`Java SE`，`J2ME`更名为`Java ME`。

做过开发的朋友，或者对互联网开发有过了解的朋友可能会知道，Java作为编程语言，一直在各大公司中广泛使用。其实Java与其它语言相比，并没有什么技术上的优势。我们也会经常看到一些diss，说Java语言设计不如C#，对native的精确控制和灵活性不如C++。动态性、开发效率的简易性不如Ruby，Python，Node。在高并发领域又不如Erlang。中间应用层又远不如Go、Swift等。**既然这样，为什么Java如此备受青睐？那关于其本质的优势又是什么呢？**这依赖于Java的几大主要特性

## 2、Java主要特性

+ 入门简单，容易学习

Java语言的语法与C语言和C++语言相接近。另一方面，Java丢弃了C++中很少使用的、很难理解的、令人迷惑的那些特性，如操作符重载、多继承、自动的强制类型转换。特别地，Java语言不使用指针，而是引用。并提供了自动的垃圾收集（GC机制），使得程序员不必为内存管理而担忧。

+ 面向对象设计

基于人的思维逻辑，Java提供了一套面向对象的语言设计，使得Java能够进行模块化式的开发。将程序中的逻辑以对象的形式呈现，具备对用户公开的特定功能或隐藏的私有属性，使得业务的实现能够简单化，增强代码的复用性。

+ 开源，有强大的后援支持

Java经过多年的沉淀，拥有活跃的社区成员，并且有大量的第三方库，对软件的开发与生产效率的提升具备强大的后援保障。优秀的顶级项目，如Spring、Apache、Hadoop、Spack......并且相关的IDE工具（Eclipse、IDEA、MyEclipse等等），使用也十分便捷。

+ 安全、高性能、跨平台

Java属于强类型机制的语言，通常被用在网络环境中，而Java提供了异常处理、垃圾回收（GC）、安全机制保障等一系列健全的机制。并且Java编写的程序可以实现跨平台的特性，Java程序在Java平台上被编译为字节码格式，在运行时，Java平台中的Java解释器对这些字节码进行解释执行，执行过程中需要的类在联接阶段被载入到运行环境中。

+ 发展迅猛

Java从1995年诞生，1997年社区成员超过10万人次，随后在1998年发布J2EE，在1999年发行三大版本（J2SE、J2EE、J2ME）到2006年底，先后发布了从1.3 - 1.6 的版本更新。2009年被Oracle公司收购，2011年7月28日，甲骨文发布 Java7.0 的正式版。截至2019年3月20日，Java已经发布了Java SE 12的版本更新。**但从9之后的版本为近几年的更新迭代，目前国内的大多数企业使用的java版本为Java 8**。


## 3、开发环境配置
以Window系统环境为例（IOS、Linux的朋友如有不适自行上网查阅~）

+ 下载JDK：[官网地址](http://www.oracle.com/technetwork/java/javase/downloads/index.html)

选择与自己电脑相匹配的安装包下载即可（exe文件，可以一键安装），如`Windows x64/Window x86`等等。如果是下载zip包的朋友，需要在下载之后配置环境变量在进行使用即可。

+ 配置环境变量（下载zip的情况）

安装完成后，右击`"我的电脑"`，点击`"属性"`，选择`"高级系统设置"`；选择`"高级"`选项卡，点击`"环境变量"`；（win10略有区别，大体上类似，找到`"环境变量"`），新建`PATH`，`JAVA_HOME`

```
PATH > %JAVA_HOME%\bin;
#注意配置PATH，不能把原先PATH里的值删除，否则可能会导致系统的未知错误，正确操作是在最前或最后添加，以;号隔开。
JAVA_HOME > C:\Program Files (x86)\Java\jdk1.8.0_91
#你的jdk下载根路径
```

+ 测试是否安装成功

打开cmd窗口，输入`java -version`，如果出现版本号，证明安装正常。

## 4、第一个程序，HelloWorld

+ 创建一个HelloWorld.java文件，使用编辑器打开
``` java
public class HelloWorld {
    public static void main(String []args) {
        System.out.println("Hello World"); // 打印 Hello World
    }
}
```

+ 打开cmd窗口，进入该文件的所在位置，输入命令`javac HelloWorld.java`按回车键编译
+ 输入命令`java HellowWorld`便可以看到你的窗口中输出了`HelloWorld`。

