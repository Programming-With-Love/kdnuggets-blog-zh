# 马尔可夫链简介

> 原文：[`www.kdnuggets.com/2023/01/introduction-markov-chains.html`](https://www.kdnuggets.com/2023/01/introduction-markov-chains.html)

![马尔可夫链简介](img/2b3def6a15366290d414392551dbf644.png)

图片来自 Unsplash

# 介绍

* * *

## 我们的前三个课程推荐

![](img/0244c01ba9267c002ef39d4907e0b8fb.png) 1\. [谷歌网络安全证书](https://www.kdnuggets.com/google-cybersecurity) - 快速通道进入网络安全职业。

![](img/e225c49c3c91745821c8c0368bf04711.png) 2\. [谷歌数据分析专业证书](https://www.kdnuggets.com/google-data-analytics) - 提升你的数据分析技能

![](img/0244c01ba9267c002ef39d4907e0b8fb.png) 3\. [谷歌 IT 支持专业证书](https://www.kdnuggets.com/google-itsupport) - 支持你的组织的 IT

* * *

马尔可夫链是一种数学系统，它根据一定的概率规则从一个状态转移到另一个状态。它们由安德雷·马尔可夫在 1906 年首次提出，用于建模随机过程的行为，并且已被应用于物理学、生物学、经济学、统计学、机器学习和计算机科学等众多领域。

马尔可夫链以俄国数学家安德雷·马尔可夫的名字命名，他在 20 世纪初发展了这些系统的理论。马尔可夫对理解随机过程的行为感兴趣，并开发了马尔可夫链理论来建模这些过程。

![马尔可夫链简介](img/2297a131988d923dc625e0457dbaaa62.png)

图 1\. 两状态马尔可夫系统的可视化：箭头表示状态之间的转移。

马尔可夫链常用于建模具有无记忆行为的系统，其中系统的未来行为不受其过去行为的影响。

马尔可夫链在数据科学中的一个常见应用是文本预测。这是自然语言处理（NLP）中的一个领域，通常被谷歌、领英和 Instagram 等科技公司使用。当你写邮件时，谷歌会预测并建议单词或短语来[自动完成](https://builtin.com/artificial-intelligence/autocomplete-authorship)你的邮件。当你在 Instagram 或领英上收到消息时，这些应用程序会建议可能的回复。这些就是我们将要探讨的马尔可夫链的应用。不过，大规模公司在生产中使用的这些功能的模型更加复杂。

在数据科学中，马尔可夫链也可以用于建模各种现象，包括时间序列数据的演变、气体中粒子的运动、疾病的传播以及金融市场的行为。

## 时间序列示例

下面是一个马尔可夫链如何用于建模时间序列演变的例子：

假设我们有一个股票价格的时间序列，并且我们想使用马尔可夫链来建模股票价格随时间的演变。我们可以定义股票价格可以取的一组状态（例如“***上升***”、“***下降***”和“***稳定***”），并指定这些状态之间的转移概率。例如，我们可以定义如下的转移概率：

```py
 Increasing  Decreasing  Stable
Increasing    0.6         0.3     0.1
Decreasing    0.4         0.4     0.2
Stable        0.5         0.3     0.2
```

这个矩阵指定了在给定当前状态的情况下，从一个状态转移到另一个状态的概率。例如，如果股票的价格当前在上涨，则有 60%的可能性它会继续上涨，30%的可能性它会下跌，10%的可能性它会保持稳定。

一旦我们定义了马尔可夫链及其转移概率，我们可以通过模拟状态之间的转移来预测股票价格的未来演变。在每个时间步，我们将使用当前状态和转移概率来确定转移到每个可能的下一个状态的概率。

# 限制

马尔可夫链的一个限制是它们仅适用于表现出无记忆行为的系统。这意味着系统的未来行为不会受到过去行为的影响。如果系统确实存在记忆，那么马尔可夫链可能不是建模其行为的最佳工具。

马尔可夫链的另一个限制是它们只能建模具有有限状态数量的系统。如果系统可以有无限多个状态，那么马尔可夫链可能无法准确建模其行为。

马尔可夫链只能建模表现出平稳行为的系统，其中状态之间的转移概率随时间不变。如果转移概率随时间变化，则可能需要更复杂的模型来准确捕捉系统的行为。

# Python 示例

下面是如何在 Python 中实现马尔可夫链的示例：

对股票价格进行建模，以预测它是上涨、下跌还是稳定。

```py
import numpy as np

# Define the states of the Markov chain
states = ["increasing", "decreasing", "stable"]

# Define the transition probabilities
transition_probs = np.array([[0.6, 0.3, 0.1], [0.4, 0.4, 0.2], [0.5, 0.3, 0.2]])

# Set the initial state
current_state = "increasing"

# Set the number of time steps to simulate
num_steps = 10

# Simulate the Markov chain for the specified number of time steps
for i in range(num_steps):
    # Get the probability of transitioning to each state
    probs = transition_probs[states.index(current_state)]

    # Sample a new state from the distribution
    new_state = np.random.choice(states, p=probs)

    # Update the current state
    current_state = new_state

    # Print the current state
    print(f"Step {i+1}: {current_state}")
```

这段代码定义了一个简单的马尔可夫链，包含三个状态（“上升”、“下降”和“稳定”），并指定这些状态之间的转移概率。然后，它模拟了马尔可夫链 10 个时间步，在每个时间步根据转移概率采样一个新状态，并相应地更新当前状态。此代码的输出将是一系列状态，表示系统随时间的演变，如下所示：

![马尔可夫链简介](img/3c8cd88fae8339c42c69a753e4d24440.png)

图 2\. 三状态马尔可夫过程的输出，初始状态设置为**“*****上升”***。

如果我们将当前状态设置为“***下降***”并运行代码，我们会得到以下输出：

![马尔可夫链简介](img/7a5a552549eac1f3d19c84fad4b9f6f6.png)

图 3\. 三状态马尔可夫过程的输出，初始状态设置为**“*****decreasing”***。

请注意，这是一个非常简化的示例，实际上，你可能需要使用更多的状态，并考虑更复杂的转移概率，以准确地建模系统的行为。然而，这个例子说明了如何在 Python 中实现马尔可夫链的基本概念。

马尔可夫链可以应用于广泛的问题，并且可以使用各种工具和库在 Python 中实现，包括‘***numpy***’和***scipy.stats***库。

然而，在使用马尔可夫链建模系统之前，重要的是要仔细考虑马尔可夫链的假设以及它们是否适用于特定的问题。总之，马尔可夫链是数据科学家和研究人员在分析和建模表现出某些行为类型的系统时应考虑的有用工具。

**[本杰明·O·塔约](https://www.linkedin.com/in/benjamin-o-tayo-ph-d-a2717511/)** 是一位物理学家、数据科学教育者和作家，同时也是 DataScienceHub 的所有者。此前，本杰明曾在中央俄克拉荷马大学、Grand Canyon 大学和匹兹堡州立大学教授工程学和物理学。

### 更多相关内容

+   [使用 PyCaret 进行二分类介绍](https://www.kdnuggets.com/2021/12/introduction-binary-classification-pycaret.html)

+   [使用 PyCaret 进行 Python 中的聚类介绍](https://www.kdnuggets.com/2021/12/introduction-clustering-python-pycaret.html)

+   [数据科学中的基础数学：奇异值分解的视觉介绍](https://www.kdnuggets.com/2022/06/essential-math-data-science-visual-introduction-singular-value-decomposition.html)

+   [数据科学中的 Pandas 介绍](https://www.kdnuggets.com/2020/06/introduction-pandas-data-science.html)

+   [论文与代码的简要介绍](https://www.kdnuggets.com/2022/04/brief-introduction-papers-code.html)

+   [KDnuggets 新闻，4 月 27 日：论文与代码的简要介绍；…](https://www.kdnuggets.com/2022/n17.html)
