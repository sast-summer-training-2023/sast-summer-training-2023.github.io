# Linux & Git

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
