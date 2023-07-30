# Docker

:cheese_wedge: 前置知识：无

:mortar_board: 讲师：王博文 @abmfy

:date: 日期：7 月 31 日星期一

---

Docker 是一种应用容器化技术。通过将应用程序和它的依赖一起打包成为一个可移植的容器，我们可以在不同环境上快速、可靠地运行相同的程序。

以上的描述可能略微有些抽象。简单来说，设想你需要跑一个别人发给你的代码，而此时你首先需要配置环境。然而，各种不同的硬件、操作系统、编译工具链使得在不同的地方配置环境极为复杂，这一点想必各位同学在各种课程上深有体会。Docker 解决的正是这一问题：通过直接将环境与程序打包在一起分发这种既暴力又优雅的方式，只需要下载容器，就能在不同的环境上完全一致地运行程序，免去了配置环境的麻烦以及环境不同带来的运行差异。在软件工程等课程上，你将会大量应用本节课所学到的知识，来将你的应用在不同的环境上一致地部署。

通过学习本课程，你将能够利用 Docker 这一强大的工具来解决环境配置问题，并方便快速地分发你的应用。

## 课前准备

### 安装 Docker

你需要安装 Docker。

你可以在下方的选项卡中选取你的操作系统以获得安装指南。

=== "Linux"

    使用 Docker 提供的自动安装脚本进行安装：

    ``` shell
    export DOWNLOAD_URL="https://mirrors.tuna.tsinghua.edu.cn/docker-ce" # (1)
    curl -fsSL https://get.docker.com/ | sudo -E sh
    ```

    1. 在国内网络环境下，推荐将安装源设置为 TUNA 等镜像以加速下载。

    !!! warning
    
        Docker 需要 root 权限才能够安装，这意味着上述代码可以对你的系统执行**任何操作**。如果你不信任上述代码，你可以按照 [Get Started | Docker](https://www.docker.com/get-started/) 中的指引手动安装 Docker。

    接下来，你需要将你的用户添加到 `docker` 用户组中：

    ``` shell
    sudo usermod -aG docker $USER
    ``` 

    !!! info

        只有在 `docker` 用户组中的用户才能够使用 Docker。默认情况下，只有 `root` 用户处于 `docker` 组中，因此若你不希望每次使用 Docker 时都需要输入 `sudo`，你需要将你的用户添加到 `docker` 组中。

=== "Windows"

    推荐做法为在 WSL 中安装 Docker，具体安装方法与 Linux 相同。

    如果你希望在 Windows 原生环境中使用 Docker，你需要安装 [Docker Desktop](https://www.docker.com/products/docker-desktop/)。

=== "macOS"

    通过 [Homebrew](https://brew.sh/) 安装 Docker Desktop：

    ``` shell
    brew install --cask docker
    ```

### 更换镜像源

在国内网络环境下，Docker 拉取镜像的速度非常慢，因此我们需要更换 Docker 镜像源来加速下载。国内可访问的公共镜像源的可用情况可以在 [docker-registry-cn-mirror-test](https://github.com/docker-practice/docker-registry-cn-mirror-test/actions) 查看。

这里我们以 USTC 源为例，演示如何更换镜像源：

=== "Linux"

    在 `/etc/docker/daemon.json` 中添加以下内容：

    ``` json
    {
        "registry-mirrors": [
            "https://docker.mirrors.ustc.edu.cn"
        ]
    }
    ```

    之后重启 Docker 服务：

    ``` shell
    sudo systemctl restart docker
    ```

=== "Windows"

    在菜单栏中右键单击 Docker Desktop 图标，选择 “Settings”，在 “Docker Engine” 标签页中添加以下内容：

    ``` json
    {
        "registry-mirrors": [
            "https://docker.mirrors.ustc.edu.cn"
        ]
    }
    ```

    之后单击 “Apply & restart”。

=== "macOS"

    在菜单栏中单击 Docker Desktop 图标，选择 “Settings”，在 “Docker Engine” 标签页中添加以下内容：

    ``` json
    {
        "registry-mirrors": [
            "https://docker.mirrors.ustc.edu.cn"
        ]
    }
    ```

    之后单击 “Apply & restart”。

### 运行 `hello-world`

`hello-world` 是 Docker 官方提供的一个简单的镜像，用于测试 Docker 是否正确安装。你可以通过以下命令运行 `hello-world`：

``` shell
docker run --rm hello-world
```

如果看到以下输出，说明 Docker 安装成功：

``` text
Hello from Docker!
This message shows that your installation appears to be working correctly.
...
```

!!! info
    
    如果你感到好奇的话，`--rm` 参数表示在容器退出后自动删除容器。由于 `hello-world` 镜像只是用于测试，因此我们不希望它留在我们的系统中。