# Linux & Git

🧀 前置知识：无

🎓 讲师：虞皓翔 @jkjkmxmx

📅 日期：7 月 9 日星期日

---

Linux 是由 Linus Torvalds 发布的自由和开源的类 UNIX 操作系统，它开源的特性使得 (在遵循 GNU 下) 任何人都可以自由地使用源代码并对其进一步开发，使之在当今如服务器、嵌入式系统等领域中广泛应用。在之后的计算机课程以及计算机相关行业中，Linux 也将成为你得心应手的工具之一，熟悉对其的使用是非常有必要的。

Git 作为全世界最流行的分布式版本控制系统，不仅完美地解决了多人合作开发、版本控制的问题，其分布式的特性也受到开发者的青睐。GitHub、GitLab 等无数开源仓库都使用 Git 进行版本控制。熟练地使用 Git 将会对你之后的软件开发、作业管理如虎添翼，养成良好的版本控制习惯。

本节课将以文档 + Capture-the-flag 的形式进行，旨在通过亲手实践来加深对 Linux 和 Git 的理解（毕竟这些知识可不能死记硬背哦，要养成肌肉记忆），CTF 的游戏形式又不乏乐趣，希望本课程能在欢乐的实践中为你之后的技能树打下基础。

## 课前准备

### Linux

你需要一个 *nix (类 Unix) 系统。

**如果你是 Linux 或 macOS 用户**：你已经拥有了一个 *nix 系统。

**如果你是 Windows 用户**：我们推荐你安装 WSL (Windows Subsystem for Linux)。参考链接：

- [安装 WSL | Microsoft Learn](https://learn.microsoft.com/zh-cn/windows/wsl/install)

### Git

你需要安装 Git。请参考 [Git - Downloads](https://git-scm.com/downloads) 来安装 Git。以下是一些常见的安装方法：

**如果你是 Windows 用户**：推荐安装 [Git for Windows](https://gitforwindows.org)。如果连接不佳，你可以在 [CNPM Binaries Mirror](https://registry.npmmirror.com/binary.html?path=git-for-windows/) 或 [清华大学开源软件镜像站](https://mirrors.tuna.tsinghua.edu.cn/github-release/git-for-windows/git/) 得到 Git for Windows 的镜像。

**如果你是 macOS 用户**：一般情况下，你的系统已经自带了 Git。如果你使用 [Homebrew](https://brew.sh)，你可以通过以下命令安装 Git：

```sh
brew install git
```

或者你可以通过 [git-osx-installer](https://sourceforge.net/projects/git-osx-installer/) 安装 Git。

**如果你是 Linux 用户**：一般情况下，你的系统已经自带了 Git。如果没有，以 Ubuntu 为例，你可以通过以下命令安装 Git：

```sh
sudo apt install git
```

### Docker

由于课程实验在 Docker 容器中进行，你需要一个拥有 Docker 的环境。

**对于清华大学学生**：我们已经在科协的 Zeus 服务器上为你准备好了 Docker 容器，你可以直接跳过这一环节。

**对于其他同学**：由于服务器资源所限，你需要手动在你的 *nix 环境上安装 Docker。参考链接：

- [Get Started | Docker](https://www.docker.com/get-started/)
- 对于 WSL 用户：[在 Windows 10 中启动 WSL2 并安装 Linux（Ubuntu 为例）并运行 Docker - CSDN 博客](https://blog.csdn.net/yushuzhen2008/article/details/104944579)

## 课程讲义 & 课后作业

📄 [课程讲义](../pdfs/linux-handout.pdf)
