# NLP

:cheese_wedge: 前置知识：NumPy, PyTorch

:mortar_board: 讲师：宋曦轩 @数学系

:date: 日期：7 月 27 日星期四

---

您是否厌倦了人类之间使用离散语言的低效交流？您是否希望学习更加抽象且高效的表达方式，或者渴望与计算机建立更加连续的沟通？本门课程将从自然语言中单词的最基本表示——词向量开始讲起，详细讲解当前 NLP (Natural Language Processing, 自然语言处理) 的主流模型 Transformer，并教授如何使用目前最热门的 NLP 模型托管平台 Hugging Face。如果您觉得自己的语言表达过于离散，希望学习具有连续性的表达方式；或者认为自己的表达过于直白，缺乏高层次的抽象；或者希望在本地部署类 ChatGPT 语言模型，那么请将本课程压入您的运行栈。本课程虽无益于提升您作为人的表达能力，即教会您个人使用词向量表达并对高层次抽象语义特征进行提取，但可以使您的模型具有更加完备的自然语言理解与自然语言生成能力，从而在语言类任务中实现对您的代替。

在本课程中，您（或者您的模型，如果比您更智能的话）可以：

1. 学习变形金刚的基本原理、结构，亲手组装并运行您的第一个变形金刚（模块无需自备）。

2. 了解大规模预训练语言模型的预训练、微调方法。

3. 熟练掌握抱抱脸🤗的使用场景与技巧。

4. 对预训练语言模型进行微调，完成简单的文本任务。

5. 在学习完计算机视觉课程后，尝试使用多模态模型完成文本 & 图像任务。

:movie_camera: [课程回放](https://www.bilibili.com/video/BV1kc411w7N5)

:memo: [讲义](/pdfs/nlp.pdf)

:books: [作业](https://github.com/sast-summer-training-2023/sast2023-nlp/tree/main)

## 课前准备

理论部分建议先修 [Mathematical Foundations of Machine Learning](https://oi-wiki.org/math/linear-algebra/)

实践部分建议了解 Python, PyTorch。

### 软件准备

建议使用 Linux 🐧 

安装以下 package:

[PyTorch](https://pytorch.org/)

[🤗 Transformers](https://huggingface.co/docs/transformers/installation)

```shell
pip install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple
```

```python title="requirements.txt"
protobuf
transformers
cpm_kernels
torch
gradio
mdtex2html
sentencepiece
accelerate
sse-starlette
streamlit
datasets
peft
tqdm
bitsandbytes

```

下载以下模型权重（可选）：

[gpt2 at main (huggingface.co)](https://huggingface.co/gpt2/tree/main)

[bert-base-chinese at main (huggingface.co)](https://huggingface.co/bert-base-chinese/tree/main)

[THUDM/chatglm2-6b-int4 at main (huggingface.co)](https://huggingface.co/THUDM/chatglm2-6b-int4/tree/main)

如果希望使用 CPU 推理 ChatGLM，可以下载：

[THUDM/chatglm-6b-int4 at main (huggingface.co)](https://huggingface.co/THUDM/chatglm-6b-int4/tree/main)

### 硬件准备

本次课程的实践中的部分内容需要 GPU 资源，如果缺少本地算力，可以尝试 [Google Colab](https://colab.research.google.com/)，或者尝试使用 CPU 进行训练。

### 数据准备

请提前下载：[openchat/openchat_sharegpt4_dataset at main (huggingface.co)](https://huggingface.co/datasets/openchat/openchat_sharegpt4_dataset/tree/main) 中的`sharegpt_gpt4.json`。

### 思想准备（可选）

阅读 [Attention Is All You Need](https://arxiv.org/pdf/1706.03762.pdf)