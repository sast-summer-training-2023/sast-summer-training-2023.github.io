#Unity 环境配置

---

Unity 自 2005 年推出以来，已经迭代了多个版本。与其他众多的开发项目一样， Unity 方案也需要各个协作者共用同一个 Unity 开发版本。类似于 Python 的 pip， Rust 的 Cargo， Node.js 的 npm/yarn， Unity 官方提供了一个 Unity 版本的管理工具 -- Unity Hub。

## Unity Hub 的配置

1. 请到 Unity 官网下载 [Unity Hub](https://unity.com/download)。

2. 完成 Unity Hub 的安装。

3. 打开 Unity Hub，点击 `Create account` 注册账号。如果已经有 Unity 账号，可以直接登录，跳到第 6 步。

![Unity Hub 启动页面] (/images/unity-hub-2.PNG)

4. 注册 Unity 账号。 

这里需要注意的是， Unity 账号类型按地区分为国内版和国外版，如果需要配置国外版，请自行搭建好相应的网络环境。

打开注册网页，把有关信息完善，完成注册后回到 Unity Hub，点击登录。

这时，浏览器自动登录，把有关信息转移到 Unity Hub 内。登录完成后， Unity Hub 跳转到授权页面，选择个人版授权即可。

![Unity 用户授权] (/images/unity-hub-3.png)

其后， Unity Hub 将询问是否安装 Unity IDE，跳过即可。
5. 下载 Unity IDE

点击左侧栏 `Installs`，看到界面右上方有 `Locate` 和 `Install Editor` 两个按钮。

由于课程组推荐使用 2020.2.5f1 版本，这个版本需要[另外下载]()，可以点击 `Locate` ，指定 Unity 的安装目录（默认为 `C:\Program Files\Unity\Hub\Editor\2020.2.5f1\Editor`），定位该版本。

另一方面，读者可以按需下载其他的 Unity 版本，点击 `Install Editor`，并选择需求版本即可。

无论是直接安装 Unity IDE, 还是通过 Unity Hub 间接处理，读者都可以加入不同的子模块，支持日后的开发活动。下面列出两个比较常见的子模块：

- WebGL。 Unity 可以用于网络游戏的开发。在 Unity 设计好游戏之后，可以对项目建置，Unity 基于 OpenGL 和 IL2CPP、emscripten 等工具生成 HTML 模块和与之配套的 JS 代码。把 WebGL 模块嵌入到 HTML 文件里，即可做出一个网络游戏。

![Unity WebGL 套件] (/images/unity-hub-5.png)

- Android。一方面，Unity 具有跨平台能力，可以直接应用于手机游戏开发。著名的原神、崩铁等游戏都是基于 Unity 技术的，另一方面， Oculus Quest 等虚拟现实平台背后运行的也是 Android 操作系统，配合 ADB 和 Oculus 提供的套件工具，将极大加速 XR 项目的开发进度。

另一方面，Unity 默认的代码编辑器为 Visual Studio，而不是传统的 Visual Studio Code。虽然 VSCode 比 VS 轻量的多，但是 Visual Studio 提供更完善的自动代码补全和库中继信息的查询服务。如果读者没有安装，可以按需配置。 

![Visual Studio] (/images/unity-hub-4.png)

6. 项目管理

我们把目光转到左侧栏的 `Projects` 部分。这个部分显示开发者有过的开发项目列表。可以点击右上角的 `NEW` 创建项目，也可以点 `ADD` 加入现有的 Unity 项目，例如读者之后可以选择完成的作业。

