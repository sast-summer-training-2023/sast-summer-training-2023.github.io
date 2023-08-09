# React

:cheese_wedge: 前置知识：Web, JS & TS

:mortar_board: 讲师：钱厚德 @Ashitemaru

:date: 日期：8 月 7 日星期一

---

Web 应用已经从简单的显示文字进化到展示图片等多媒体资源，乃至到如今复杂多样的高交互性内容展示。在这种进化的背后，是 Web 应用的开发方式的一轮轮迭代更新。本课程希望为大家介绍当下流行的 Web 应用前端开发框架之一——React 的基本使用方式，并希望大家利用 React 编写简单的 Web 应用前端。

:movie_camera: [课程回放](https://www.bilibili.com/video/BV1K44y1A7vv)

:books: 作业将与后端作业一同将于近日发布。

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

## You are doing React!

- HTML、CSS、JS
- 我们可以弄一个框架，用 JS/TS 语言写，然后框架帮我们转换到 HTML、CSS、JS 上并在浏览器上运行
- 当前常用的框架：Vue、React、Angular

### Step 1 理解 React 项目的结构

- 各个配置文件的作用
- `index.tsx, index.html` 的作用
- `App.tsx` 的作用

### Step 2 理解 HTML/TSX

- 理解标签语言的语法糖

### Step 3 理解组件（Component）

- React 框架支持两种组件，一种是类组件，一种是函数组件
  - 但是目前 React 推荐使用函数组件，官方文档也是函数组件为主
- 函数组件的返回值，就是这个组件在屏幕上（浏览器里的）展示形式

### Step 4 理解属性（Props）

- props 会包装成一个对象传入函数组件的参数之中
- 实践中，一般写函数组件的时候都会有一个参数的接口声明
- 使用的时候和普通的 HTML 规定标签属性语法一样
- 属性：本质上是父组件对子组件的控制（瀑布数据流）

### Step 5 理解状态（State）

- 函数组件之中需要使用 Hooks，形而上地写成 `const [state, setState] = useState(initState);`
- 状态是组件自我管理的数据，不需要依赖父组件的控制
- 额外提醒，`setState` 并不是即时的，如果需要依赖上一次的状态，可以在 `setState` 内传入回调函数（reducer）

### Step 6 理解副作用（Effect）

- 函数组件的主作用是渲染组件，所有其他的操作都归类于副作用
- 所有的副作用都应当写成回调函数使用 `useEffect` Hook 裹住
- 什么时候执行副作用，依赖于 `useEffect` Hook 的第二个参数（依赖列表）
  - 如果依赖列表缺失（即 `undefined`），每一次渲染都会执行副作用
  - 如果依赖列表是空列表（即 `[]`），只在第一次渲染时执行副作用（多用于组件初始化的时候从服务器拉取数据）
  - 如果依赖列表里面有变量，则在依赖列表中变量发生改变的时候执行副作用
- 副作用的清除？在表示副作用的回调函数里返回一个回调函数，这个返回的回调函数用来清除副作用（例如释放计时器等资源）
  - 编码上建议将副作用拆开，一个副作用对应一个副作用的清除

### Step 7 理解反向数据流

- 所谓的子组件控制父组件，并没有违反瀑布数据流，本质是父组件通过 props 将 state 的控制权下放给子组件

### Extra

- 在上述的数据传递中，数据依然局限于父子之间，如果需要在多个复杂的组件树上共享状态，我推荐使用 Redux
- 组件库，帮助大家很快写出来“有设计感的” UI，组件库比如说 Ant Design 之类