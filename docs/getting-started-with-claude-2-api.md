# 开始使用 Claude 2 API

> 原文：[`www.kdnuggets.com/getting-started-with-claude-2-api`](https://www.kdnuggets.com/getting-started-with-claude-2-api)

![开始使用 Claude 2 API](img/23d6640d3c41a581cbde7bd6f9c39627.png)

图片由作者提供

# Claude 2 是什么？

* * *

## 我们的前 3 大课程推荐

![](img/0244c01ba9267c002ef39d4907e0b8fb.png) 1\. [谷歌网络安全证书](https://www.kdnuggets.com/google-cybersecurity) - 快速开启网络安全职业生涯。

![](img/e225c49c3c91745821c8c0368bf04711.png) 2\. [谷歌数据分析专业证书](https://www.kdnuggets.com/google-data-analytics) - 提升你的数据分析技能

![](img/0244c01ba9267c002ef39d4907e0b8fb.png) 3\. [谷歌 IT 支持专业证书](https://www.kdnuggets.com/google-itsupport) - 支持你的组织进行 IT 管理。

* * *

Anthropic 的对话 AI 助手，[Claude 2](https://www.anthropic.com/index/claude-2)，是最新版本，相比于前一版本在性能、响应长度和可用性方面有了显著的提升。最新版本的模型可以通过我们的 API 和 claude.ai 的新公共测试网站进行访问。

Claude 2 因其易于聊天、清晰解释推理、避免有害输出和拥有强大的记忆能力而闻名。它增强了推理能力。

Claude 2 在律师考试的多项选择题部分表现出显著的改进，得分为 76.5%，相比 Claude 1.3 的 73.0%有所提升。此外，Claude 2 在 GRE 阅读和写作部分超过了 90%的考生。在像 HumanEval 这样的编码评估中，Claude 2 的准确率达到了 71.2%，相比过去的 56.0%有了显著提高。

Claude 2 API 以与 Claude 1.3 相同的价格提供给我们的数千名企业客户。你可以通过网页 API 以及 Python 和 Typescript 客户端轻松使用它。本教程将指导你完成 Claude 2 Python API 的设置和使用，并帮助你了解它提供的各种功能。

# 设置

在我们开始访问 API 之前，我们需要首先申请[API 早期访问](https://www.anthropic.com/earlyaccess)。你需要填写表格并等待确认。确保你使用的是企业邮箱地址。我使用的是**@kdnuggets.com**。

收到确认邮件后，你将获得控制台访问权限。从那里，你可以通过访问[账户设置](https://console.anthropic.com/account/keys)来生成 API 密钥。

使用 PiP 安装 Anthropic Python 客户端。确保你使用的是最新的 Python 版本。

```py
pip install anthropic
```

使用 API 密钥设置 anthropic 客户端。

```py
client = anthropic.Anthropic(api_key=os.environ["API_KEY"])
```

除了为创建客户端对象提供 API 密钥外，你还可以设置`ANTHROPIC_API_KEY`环境变量并提供密钥。

# 访问 Claude 2

这里是使用提示生成响应的基本同步版本。

1.  导入所有必要的模块。

1.  使用 API 密钥初始化客户端。

1.  要生成响应，你必须提供模型名称、最大令牌数和提示。

1.  你的提示通常包括 `HUMAN_PROMPT` ('\n\nHuman:') 和 `AI_PROMPT` ('\n\nAssistant:')。

1.  打印响应。

```py
from anthropic import Anthropic, HUMAN_PROMPT, AI_PROMPT
import os

anthropic = Anthropic(
    api_key= os.environ["ANTHROPIC_API_KEY"],
)

completion = anthropic.completions.create(
    model="claude-2",
    max_tokens_to_sample=300,
    prompt=f"{HUMAN_PROMPT} How do I find soul mate?{AI_PROMPT}",
)
print(completion.completion)
```

**输出：**

如我们所见，我们得到了相当好的结果。我认为这甚至比 GPT-4 更好。

```py
Here are some tips for finding your soulmate:

- Focus on becoming your best self. Pursue your passions and interests, grow as a person, and work on developing yourself into someone you admire. When you are living your best life, you will attract the right person for you.

- Put yourself out there and meet new people. Expand your social circles by trying new activities, joining clubs, volunteering, or using dating apps. The more people you meet, the more likely you are to encounter someone special.........
```

你还可以使用异步请求调用 Claude 2 API。

同步 API 按顺序执行请求，阻塞直到接收到响应，然后再调用下一个请求，而异步 API 允许多个并发请求而不阻塞，通过回调、承诺或事件处理响应；这使得异步 API 具有更高的效率和可扩展性。

1.  导入 AsyncAnthropic 而不是 Anthropic

1.  定义一个具有异步语法的函数。

1.  每次 API 调用时使用 `await`

```py
from anthropic import AsyncAnthropic

anthropic = AsyncAnthropic()

async def main():
    completion = await anthropic.completions.create(
        model="claude-2",
        max_tokens_to_sample=300,
        prompt=f"{HUMAN_PROMPT} What percentage of nitrogen is present in the air?{AI_PROMPT}",
    )
    print(completion.completion)

await main()
```

**输出：**

我们得到了准确的结果。

```py
About 78% of the air is nitrogen. Specifically:
- Nitrogen makes up approximately 78.09% of the air by volume.
- Oxygen makes up approximately 20.95% of air. 
- The remaining 0.96% is made up of other gases like argon, carbon dioxide, neon, helium, and hydrogen.
```

> **注意：** 如果你在 Jupyter Notebook 中使用异步函数，请使用 `await main()`。否则，使用 `asyncio.run(main())`。

# Claude 2 流式处理

流式处理在大型语言模型中变得越来越受欢迎。你可以在响应完全生成之前开始处理输出，因为它会逐个令牌返回，而不是一次性返回。这种方法有助于通过逐个令牌返回语言模型的输出来减少感知延迟。

你只需在完成函数中将新参数 `stream` 设置为 `True`。Claude 2 使用服务器推送事件 (SSE) 支持响应流式传输。

```py
stream = anthropic.completions.create(
    prompt=f"{HUMAN_PROMPT} Could you please write a Python code to analyze a loan dataset?{AI_PROMPT}",
    max_tokens_to_sample=300,
    model="claude-2",
    stream=True,
)
for completion in stream:
    print(completion.completion, end="", flush=True)
```

**输出：**

![开始使用 Claude 2 API](img/39e8ce742bdd6aa34bbc6cd8cecaccdd.png)

# 计费

计费是将 API 集成到应用程序中最重要的方面。这将帮助你规划预算并向客户收费。所有 LLMs API 都基于令牌收费。你可以查看下面的表格来了解定价结构。

![开始使用 Claude 2 API](img/785f7e1734371aac50d7001a80d1d3b5.png)

来自 Anthropic 的图像

计算令牌数的一个简单方法是提供一个提示或响应给 `count_tokens` 函数。

```py
client = Anthropic()
client.count_tokens('What percentage of nitrogen is present in the air?')
```

```py
10
```

# 其他功能

除了基本的响应生成外，你还可以使用 API 完全整合到你的应用程序中。

+   **使用类型：** 请求和响应分别使用 TypedDicts 和 Pydantic 模型进行类型检查和自动补全。

+   **处理错误：** 错误包括用于连接问题的 APIConnectionError 和用于 HTTP 错误的 APIStatusError。

+   **默认标题：** anthropic-version 标头会自动添加。这可以自定义。

+   **日志记录：** 通过设置 ANTHROPIC_LOG 环境变量可以启用日志记录。

+   **配置 HTTP 客户端：** HTTPx 客户端可以为代理、传输等进行自定义。

+   **管理 HTTP 资源：** 客户端可以手动关闭或在上下文管理器中使用。

+   **版本控制：** 遵循语义版本控制规范，但一些不兼容的更改可能会作为次要版本发布。

# 结论

Anthropic Python API 提供了对 Claude 2 最先进对话 AI 模型的便捷访问，使开发人员能够将 Claude 的先进自然语言功能集成到他们的应用程序中。该 API 提供了同步和异步调用、流式传输、基于令牌使用的计费以及其他功能，以充分利用 Claude 2 相较于之前版本的改进。

到目前为止，Claude 2 是我最喜欢的，我认为使用 Anthropic API 构建应用程序将帮助你打造出色的产品。

如果你想阅读更高级的教程，请告诉我。也许我可以使用 Anthropic API 创建一个应用程序。

[](https://www.polywork.com/kingabzpro)****[Abid Ali Awan](https://www.polywork.com/kingabzpro)**** ([@1abidaliawan](https://www.linkedin.com/in/1abidaliawan)) 是一位认证的数据科学专业人士，热衷于构建机器学习模型。目前，他专注于内容创作，并撰写有关机器学习和数据科学技术的技术博客。Abid 拥有技术管理硕士学位和电信工程学士学位。他的愿景是使用图神经网络构建一个 AI 产品，帮助面临心理健康问题的学生。

### 更多相关主题

+   [开始使用 Claude 3 Opus：如何打败 GPT-4 和 Gemini](https://www.kdnuggets.com/getting-started-with-claude-3-opus-that-just-destroyed-gpt-4-and-gemini)

+   [认识 Gorilla：UC Berkeley 和微软的 API 增强型 LLM…](https://www.kdnuggets.com/2023/06/meet-gorilla-uc-berkeley-microsoft-apiaugmented-llm-outperforms-gpt4-chatgpt-claude.html)

+   [ChatGPT 被取代：Claude 如何成为新的 AI 领导者](https://www.kdnuggets.com/2023/07/chatgpt-dethroned-claude-became-new-ai-leader.html)

+   [检测 ChatGPT、GPT-4、Bard 和 Claude 的十大工具](https://www.kdnuggets.com/2023/05/top-10-tools-detecting-chatgpt-gpt4-bard-llms.html)

+   [免费访问 Claude AI 的三种方法](https://www.kdnuggets.com/2023/06/3-ways-access-claude-ai-free.html)

+   [开始使用 SQL 备忘单](https://www.kdnuggets.com/2022/08/getting-started-sql-cheatsheet.html)
