# 神经网络 & PyTorch

:cheese_wedge: 前置知识：NumPy

:mortar_board: 讲师：田倍闻 @tb5zhh

:date: 日期：7 月 24 日星期一

---

伴随着超高的数据增长速度，人为设计的模式和统计手段已难以反映整体数据分布的特征，传统的数据分析手段已经逐渐失效。在这样的背景下，这一节课将介绍人工神经网络这一强大的工具，从而学习通过数据驱动的方式提取海量数据中的关键特征。于此同时，我们也将介绍PyTorch 这一强大的工具。

PyTorch 是另一个基于 Python 的科学计算库，专注于深度学习任务。类似 NumPy 中多维数组的概念，张量（tensor）对象是 PyTorch 的核心处理对象，相比于 NumPy 中多维数组，Pytorch 对张量对象提供额外的功能与优化，用以支持深度学习。除此之外，PyTorch 提供了丰富的工具和借口，使得构建、训练和部署深度神经网络变得更加简单和高效。

## 课前准备

请参考 [Start Locally | PyTorch](https://pytorch.org/get-started/locally/) 安装 PyTorch。请注意你需要根据自己的操作系统、包管理器和计算平台选择合适的安装方式。

如果你不清楚应该如何选取，我们在课程中会介绍大致的安装流程，你可以先使用 `pip` 安装 CPU 版本的 PyTorch：

```shell
pip install torch
```

### 课程讲义

:movie_camera: [课程回放](https://www.bilibili.com/video/BV1oV4y1t7fg)

:memo: [讲义](/pdfs/torch.pdf)