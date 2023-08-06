# React

:cheese_wedge: 前置知识：Web, JS & TS

:mortar_board: 讲师：钱厚德 @Ashitemaru

:date: 日期：8 月 7 日星期一

---

Web 应用已经从简单的显示文字进化到展示图片等多媒体资源，乃至到如今复杂多样的高交互性内容展示。在这种进化的背后，是 Web 应用的开发方式的一轮轮迭代更新。本课程希望为大家介绍当下流行的 Web 应用前端开发框架之一——React 的基本使用方式，并希望大家利用 React 编写简单的 Web 应用前端。

## 课前准备

### 环境配置

如果你未参与过 TypeScript 语言课程，可以参考 [其课前准备部分](/frontend/js-ts/#_1) 配置 TypeScript 语言环境以及 Yarn 包管理器。

在此基础上，你可以尝试建立一个 React 起步项目。只需要在某个你想要建立该项目的目录下，运行 React 官方提供的脚手架：

```bash
yarn create react-app learn-react --template typescript
```

正确创建完毕后，你可以进入该项目并运行：

```bash
cd learn-react
yarn start
```

之后在浏览器中访问 `http://localhost:3000` 就应当能看到 React 的 Logo 和提示，这样你就启动了你的第一个 React 应用。

### 替换代码

然而由于 React 官方脚手架提供的起始文件并不都是必要的。我们提供了一个最小化的 React 应用代码，你可以从 <a href="../../../static/src.zip" target="_blank" download="src.zip">该链接</a> 下载一个压缩包，解压后用内部的 `src` 目录替换掉刚刚 React 项目中的 `src` 目录。如果你此时还没有用 Ctrl+C 中止 React 应用，只要保存代码修改，就应当能看到浏览器中的页面刷新，并且仅有一行 `Hello, React!` 提示文字。如果你已经中止 React 应用，重新使用 `yarn start` 启动即可。