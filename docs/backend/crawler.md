# 爬虫

:cheese_wedge: 前置知识：Web, Python

:mortar_board: 讲师：刘铠铭 @kaiming

:date: 日期：8 月 3 日星期四

---

通过学习本课程，你将有能力自行编写一些爬虫工具来辅助完成简单的任务（例如批量下载网络学堂文件，大批量下载网站检索信息，下载 Bilibili 视频等），你也有可能初步了解 Scrapy 等更高级的爬虫框架，了解如何应对现代网络中对爬虫常见防范手段，以满足更进阶的需求。

## 一、什么是爬虫

不考虑复杂的内容，我们可以简单的将“上网”概括为“浏览器向服务器按照用户意愿发送一系列请求，并将服务器的响应呈现给用户“的过程。而爬虫便是一种可以模拟网页浏览器向网站发送、处理请求的自动化脚本，帮助我们获得服务器的数据，进而用于其他需求。

那么爬虫可以做什么呢？可以认为一切与网络请求相关的内容爬虫都可以按照我们的需要进行处理。

## 二、课前准备

### 1. 预备知识

我们期待您已经掌握了 Python 的使用，了解了 Web 的基本知识，如果您对这两方面有疑惑，可以参考：
- [2023 科协暑培 Web 部分](https://summer23.net9.org/basic/web/)
- [2023 科协暑培 Python 部分](https://summer23.net9.org/basic/python/)

HTTP 基本知识：
- HTTP 入门: [https://www.ruanyifeng.com/blog/2016/08/http.html](https://www.ruanyifeng.com/blog/2016/08/http.html)
- HTTP 方法: [https://www.w3schools.com/tags/ref_httpmethods.asp](https://www.w3schools.com/tags/ref_httpmethods.asp)
- HTTP Status Code: [https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status)
- HTTP Cookie: [https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Cookies](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Cookies)

Route yourself in XML:
- XPATH: [https://www.w3schools.com/xml/xpath_intro.asp](https://www.w3schools.com/xml/xpath_intro.asp)

### 2. 环境准备

请通过 [清华云盘](https://cloud.tsinghua.edu.cn/f/59a49e6c2eaa4d0fb8c3/?dl=1) 下载 requirements.txt 并执行：

```shell
conda create -n crawler python=3.10
conda activate crawler
pip install -r requirements.txt
```

## 三、授课计划

1. 建议爬虫构建；
2. Scrapy 初探；
3. 作业说明。