# 在 Google Colab 上运行 Redis

> 原文：[`www.kdnuggets.com/2022/01/running-redis-google-colab.html`](https://www.kdnuggets.com/2022/01/running-redis-google-colab.html)

Google Colab 是一个流行的基于浏览器的环境，用于在托管的 Jupyter 笔记本上执行 Python 代码和训练机器学习模型，包括免费访问 GPU！这是数据科学家和机器学习（ML）工程师学习和快速开发 Python 中的 ML 模型的绝佳平台。[Redis](https://hub.docker.com/_/redis) 是一个内存中的开源数据库，越来越多地用于机器学习——从缓存、消息传递和快速数据摄取，到语义搜索和 在线特征存储。实际上，NoSQL 数据库——尤其是 Redis——被 Zynga 应用数据科学总监 Ben Weber 列为 2020 年他作为数据科学家学到的 8 种新工具之一。

## 在 Colab 上使用 Redis 进行机器学习

* * *

## 我们的三大课程推荐

![](img/0244c01ba9267c002ef39d4907e0b8fb.png) 1\. [Google 网络安全证书](https://www.kdnuggets.com/google-cybersecurity) - 快速进入网络安全职业轨道。

![](img/e225c49c3c91745821c8c0368bf04711.png) 2\. [Google 数据分析专业证书](https://www.kdnuggets.com/google-data-analytics) - 提升你的数据分析技能

![](img/0244c01ba9267c002ef39d4907e0b8fb.png) 3\. [Google IT 支持专业证书](https://www.kdnuggets.com/google-itsupport) - 支持你的组织 IT

* * *

由于 Redis 在数据科学和机器学习中的使用越来越广泛，能够直接从 Google Colab 笔记本中运行 Redis 非常方便！然而，在 Google Colab 上运行 Redis 与在本地机器或使用 Docker 上的设置有所不同。下面我将向你展示如何通过两个简单的步骤，在 Colab 笔记本上直接从浏览器运行 Redis。

![在 Google Colab 上运行 Redis](img/fe9fac2a42335c438f03197d92df2ef4.png)

图片由作者使用 Colab 标志创建（图片来源：[Medium](https://medium.com/@nanofaroque/google-colab-is-a-goldmine-for-machine-learning-or-deep-learning-enthusiast-894a80b4b349)）和 Redis 标志（[合理使用](https://redis.io/topics/trademark)）

## 在 Colab 上安装和运行 Redis

### 步骤 1：安装

要安装 Redis 和 Redis Python 客户端：

```py
​​%pip install redis-server redis
```

**备注**：

*虽然 Jupyter Notebooks 支持多种语言，但 Colab 仅支持 Python。要在 [Python](https://www.python.org/) 中使用 Redis，你需要一个 [Redis Python 客户端](https://docs.redis.com/latest/rs/references/client_references/client_python/)。在本教程中，我们演示了 [redis-py](https://github.com/andymccurdy/redis-py/) 的使用，这是一个 Redis Python 客户端，我们使用 `[%pip install](https://ipython.readthedocs.io/en/7.23.0/interactive/magics.html#magic-pip) redis` 命令进行安装。

**你可以在 Jupyter Notebook 或 Google Colab 中运行 shell 命令，通过在命令前加上 ! 字符或 % 来使用魔法命令。有关数据科学家的有用魔法命令列表，请参见文章 - [Jupyter Notebook 中的 8 个魔法命令](https://towardsdatascience.com/top-8-magic-commands-in-jupyter-notebook-c1582e813560)。

### 步骤 2：启动 Redis 服务器

要启动 Redis 服务器，请运行：

```py
import redis_server
!$redis_server.REDIS_SERVER_PATH --daemonize yes
```

**注意**：

另外，你可以通过 Python 子进程在不使用 shell 命令的情况下启动 Redis 服务器：

`import subprocess import redis_server subprocess.Popen([redis_server.REDIS_SERVER_PATH])`

就这样！就是这么简单。

## 连接到 Redis 服务器和 Redis 命令函数

现在让我们来看看我们需要哪些命令来验证 Redis 是否在运行、连接到它并读取和写入数据。

### 验证 Redis 是否在运行

如果你想验证 Redis 是否启动并运行，你可以连接到服务器并运行 "PING 命令"。我们使用 Python 客户端 redis-py 创建一个连接，然后对服务器进行 'ping'：

```py
import redis
client = redis.Redis(host = 'localhost', port=6379)

client.ping()
```

如果你得到 True，那么你就可以开始了！

### Redis 命令的示例代码

一旦连接到 Redis，你可以通过 [Redis 命令函数](https://docs.redis.com/latest/rs/references/client_references/client_python/) 读取和写入数据。在这个示例中，我们将 Redis 用作 [键值数据库](https://redis.com/nosql/key-value-databases/)（也称为键值存储）。下面的代码片段将值 bar 分配给 Redis 键 foo，读取它并返回：

```py
client.set('foo', 'bar')
client.get('foo')
```

## 总结

在这篇博客文章中，我们展示了如何在 Google Colab 上运行 Redis 数据库，全部通过你的浏览器完成！我们首先安装了 Redis 和 Redis Python 客户端，然后启动了 Redis 服务器，并通过创建连接来验证它是否正在运行。最后，我们看到如何使用 Redis 命令函数从 Redis 数据库中读取和写入数据。如果你想自己尝试命令，这里有一个 [Redis 与 Colab 笔记本](https://colab.research.google.com/drive/1jPgmnGdlVPLQq3c9YqAsxc_gu6YReKaS?usp=sharing) 的链接，其中包含了本教程中的代码。

**[Nava Levy](https://www.linkedin.com/in/nava1/?originalSubdomain=il)** 是 Redis 的数据科学和 MLOps 开发者倡导者。她在以色列国防军的研发部门开始了她的技术职业生涯，随后很幸运地能够与云计算、大数据以及深度学习/机器学习/人工智能技术一起工作，并成为这些技术浪潮中的一员。Nava 还是 MassChallenge 加速器的导师以及 LerGO——一个基于云的教育科技创业公司的创始人。她在空闲时间喜欢骑自行车、四球杂技，以及阅读奇幻和科幻书籍。

### 更多相关主题

+   [在 Google Colab 上免费运行 Mixtral 8x7b](https://www.kdnuggets.com/running-mixtral-8x7b-on-google-colab-for-free)

+   [从 Google Colab 到 Ploomber 流水线：使用 GPU 的大规模 ML](https://www.kdnuggets.com/2022/03/google-colab-ploomber-pipeline-ml-scale-gpus.html)

+   [在 Google Colab 上免费微调 LLAMAv2 与 QLora](https://www.kdnuggets.com/fine-tuning-llamav2-with-qlora-on-google-colab-for-free)

+   [在 Google Colab 上使用 RAPIDS cuDF 加速数据科学](https://www.kdnuggets.com/2023/01/rapids-cudf-accelerated-data-science-google-colab.html)

+   [如何入门 SQL - 免费学习资源列表](https://www.kdnuggets.com/2022/10/get-running-sql-list-free-learning-resources.html)

+   [在本地 CPU 上运行小型语言模型的 7 个步骤](https://www.kdnuggets.com/7-steps-to-running-a-small-language-model-on-a-local-cpu)
