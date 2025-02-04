# Ollama 教程：本地运行 LLMs 变得超级简单

> 原文：[`www.kdnuggets.com/ollama-tutorial-running-llms-locally-made-super-simple`](https://www.kdnuggets.com/ollama-tutorial-running-llms-locally-made-super-simple)

![ollama-tutorial](img/1f45326dd049cd0966bfbd8d5988835b.png)

图片由作者提供

在本地运行大型语言模型（LLMs）非常有帮助——无论你是想玩玩 LLMs 还是使用它们构建更强大的应用程序。但是，配置工作环境并让 LLMs 在你的机器上运行并不简单。

* * *

## 我们的前三个课程推荐

![](img/0244c01ba9267c002ef39d4907e0b8fb.png) 1\. [Google 网络安全证书](https://www.kdnuggets.com/google-cybersecurity) - 快速进入网络安全职业生涯

![](img/e225c49c3c91745821c8c0368bf04711.png) 2\. [Google 数据分析专业证书](https://www.kdnuggets.com/google-data-analytics) - 提升你的数据分析技能

![](img/0244c01ba9267c002ef39d4907e0b8fb.png) 3\. [Google IT 支持专业证书](https://www.kdnuggets.com/google-itsupport) - 支持你的组织在 IT 方面

* * *

那么，如何在没有麻烦的情况下本地运行 LLMs 呢？**Ollama** 就是答案，它使得使用开源大型语言模型的本地开发变得轻而易举。使用 Ollama，你运行 LLM 所需的一切——模型权重和所有配置——都被打包成一个 Modelfile。**就像 Docker 对 LLMs 一样**。

在本教程中，我们将深入了解如何使用 Ollama 在本地运行大型语言模型。所以让我们直接进入步骤！

## 第一步：下载 Ollama 以开始

首先，你应该将 Ollama 下载到你的机器上。Ollama 支持所有主要平台：MacOS、Windows 和 Linux。

要下载 Ollama，你可以访问 [官方 GitHub 仓库](https://github.com/ollama/ollama) 并从那里跟随下载链接。或者访问 [官方网站](https://ollama.com/) 下载适用于 Mac 或 Windows 机器的安装程序。

我使用的是 Linux：Ubuntu 发行版。如果你也是像我一样的 Linux 用户，你可以运行以下命令来执行安装脚本：

```py
$ curl -fsSL https://ollama.com/install.sh | sh
```

安装过程通常需要几分钟。在安装过程中，任何 NVIDIA/AMD GPU 将被自动检测。确保你已安装驱动程序。仅 CPU 模式也可以正常工作，但可能会慢很多。

## 第二步：获取模型

接下来，你可以访问 [模型库](https://ollama.com/library) 查看当前支持的所有模型家族列表。默认下载的模型是带有 `latest` 标签的。在每个模型的页面上，你可以获取更多信息，如大小和量化方式。

你可以通过标签列表搜索以找到你想要运行的模型。对于每个模型系列，通常有不同大小的基础模型和经过指令调优的变体。我对运行来自 Google DeepMind 的 [Gemma 轻量级模型系列](https://ai.google.dev/gemma) 中的 Gemma 2B 模型感兴趣。

你可以使用 `ollama run` 命令来运行模型，以直接与模型进行交互。不过，你也可以先将模型下载到你的机器上，然后再运行。这与使用 Docker 镜像的方式非常相似。

对于 Gemma 2B，运行以下拉取命令将模型下载到你的机器上：

```py
$ ollama pull gemma:2b
```

模型的大小为 1.7B，拉取应该需要一两分钟：

![ollama-pull](img/d1a077a8dd047ac39c1a9b9b8e445478.png)

## 步骤 3：运行模型

使用如上所示的 `ollama run` 命令运行模型：

```py
$ ollama run gemma:2b
```

这样会启动一个 Ollama REPL，你可以在其中与 Gemma 2B 模型进行交互。以下是一个示例：

![ollama-response](img/8644500443780001ff507a342f3ec1f8.png)

对于关于 Python 标准库的简单问题，回应似乎相当不错。并且包括了最常用的模块。

## 步骤 4：通过系统提示自定义模型行为

你可以通过设置系统提示自定义 LLMs，以实现特定的期望行为：

+   设置系统提示以实现期望的行为。

+   通过给模型命名来保存它。

+   退出 REPL 并运行你刚刚创建的模型。

假设你希望模型始终用尽可能简单的英语解释概念或回答问题。以下是实现方法：

```py
>>> /set system For all questions asked answer in plain English avoiding technical jargon as much as possible
Set system message.
>>> /save ipe
Created new model 'ipe'
>>> /bye
```

现在运行你刚刚创建的模型：

```py
$ ollama run ipe
```

以下是一个示例：

![ipe-response](img/5818ee682cda05d60d9c3d1b28fa2057.png)

## 步骤 5：在 Python 中使用 Ollama

运行 Ollama 命令行客户端并在 Ollama REPL 本地与 LLMs 进行交互是一个很好的开始。但通常你会希望在应用程序中使用 LLMs。你可以在你的机器上将 Ollama 作为服务器运行，并运行 cURL 请求。

但也有更简单的方法。如果你喜欢使用 Python，你会想要构建 LLM 应用程序，以下是几种方法：

+   使用官方 Ollama Python 库

+   使用 Ollama 与 LangChain

在运行以下部分中的代码片段之前，请拉取你需要使用的模型。

### 使用 Ollama Python 库

要使用 Ollama Python 库，你可以像这样使用 pip 安装：

```py
$ pip install ollama
```

还有一个官方的 JavaScript 库，如果你更喜欢用 JS 开发，可以使用它。

一旦你安装了 Ollama Python 库，你可以在 Python 应用程序中导入它并使用大型语言模型。以下是一个简单语言生成任务的代码片段：

```py
import ollama

response = ollama.generate(model='gemma:2b',
prompt='what is a qubit?')
print(response['response'])
```

### 使用 LangChain

另一种在 Python 中使用 Ollama 的方法是使用 [LangChain](https://www.langchain.com/)。如果你有现有的使用 LangChain 的项目，集成或切换到 Ollama 会很容易。

确保你已安装 LangChain。如果没有，请使用 pip 安装：

```py
$ pip install langchain
```

这是一个示例：

```py
from langchain_community.llms import Ollama

llm = Ollama(model="llama2")

llm.invoke("tell me about partial functions in python")
```

在 Python 应用程序中使用 LLM 使得根据应用程序的需要在不同的 LLM 之间切换变得更加容易。

## 总结

使用 Ollama，你可以在本地运行大型语言模型，并通过几行 Python 代码构建由 LLM 驱动的应用程序。在这里，我们探讨了如何在 Ollama REPL 中以及在 Python 应用程序中与 LLM 进行交互。

接下来我们将尝试使用 Ollama 和 Python 构建一个应用程序。在那之前，如果你希望深入了解 LLM，请查看 [掌握大型语言模型的 7 个步骤](https://www.kdnuggets.com/7-steps-to-mastering-large-language-models-llms)。

**[](https://twitter.com/balawc27)**[Bala Priya C](https://www.kdnuggets.com/wp-content/uploads/bala-priya-author-image-update-230821.jpg)**** 是来自印度的开发者和技术作家。她喜欢在数学、编程、数据科学和内容创作的交汇点上工作。她的兴趣和专业领域包括 DevOps、数据科学和自然语言处理。她喜欢阅读、写作、编程和喝咖啡！目前，她正在通过撰写教程、操作指南、观点文章等与开发者社区分享她的知识。Bala 还创建了引人入胜的资源概述和编码教程。

### 更多相关主题

+   [在本地运行 LlaMA 2 的简单指南](https://www.kdnuggets.com/a-simple-guide-to-running-llama-2-locally)

+   [Pydantic 教程：Python 中的数据验证简化版](https://www.kdnuggets.com/pydantic-tutorial-data-validation-in-python-made-simple)

+   [在本地运行 Llama 3 的最简单方法](https://www.kdnuggets.com/easiest-way-of-running-llama-3-locally)

+   [简化 Pandas DataFrames 的合并](https://www.kdnuggets.com/2022/09/combining-pandas-dataframes-made-simple.html)

+   [简化个性化 AI：适应 GPT 的无代码指南](https://www.kdnuggets.com/personalized-ai-made-simple-your-no-code-guide-to-adapting-gpts)

+   [使用 BigQuery ML 为数据分析师简化机器学习](https://www.kdnuggets.com/machine-learning-made-simple-for-data-analysts-with-bigquery-ml)
