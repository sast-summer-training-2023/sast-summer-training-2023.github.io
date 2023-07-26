# Java

:cheese_wedge: 前置知识：OOP

:mortar_board: 讲师：朱煜章 @Clancy

:date: 日期：7 月 26 日星期三

---

尽管近年来面临一些新兴语言的挑战，Java 由于它的跨平台性、良好的安全性、前向兼容性以及不算差的性能，仍是一门历史地位和业界地位都极其崇高的语言。庞大的 Java 社区和海量的 Java 项目使得对任何想要接触业界的贵系同学来说，你也许可以不精通它，但至少应当对这门简单、强大、通用的语言有一些了解。此外，本课程还会简单介绍 Kotlin, Scala 等基于 Java 虚拟机的（更现代化的）语言。

## 课前准备

**本课程需要先修《面向对象程序设计》（OOP）。**

要运行 Java 程序，你需要先安装 Java Developer Kit (JDK) 。Windows 或 Mac 用户建议直接在 Oracle 官网下载 JDK17（[Java Downloads | Oracle](https://www.oracle.com/java/technologies/downloads/#java17)）。而 Linux 用户（这里以 Ubuntu 为例，其余平台请自行百度 / Google）则可以使用如下命令：

```bash
sudo add-apt-repository ppa:linuxuprising/java
sudo apt update
sudo apt install oracle-java17-installer --install-recommends
```

本教程就会使用这一版本。请使用`java -version`命令来确认 JDK 是否安装完成。

你可以使用如下命令编译运行 Java 程序：

```bash
javac YourProgram.java  # 编译
java YourProgram        # 运行
# OR 
java YourProgram.java   # 编译 & 运行
```

你也可以使用`jshell`这一命令行式窗口运行一些简单的`java`脚本（~~玩具性质居多~~）。

建议使用 IntelliJ IDEA 这一广泛应用的 Java IDE 编写 Java 程序，可在 https://www.jetbrains.com/idea/ 下载。如果你是清华大学学生，可以使用清华邮箱（使用`mails.thu.edu.cn`后缀，而非`mails.tsinghua.edu.cn`），在 [免费教育许可证 - 社区支持 (jetbrains.com.cn)](https://www.jetbrains.com.cn/community/education/#students) 注册学生包，获取功能更加强大的 Ultimate 版本。