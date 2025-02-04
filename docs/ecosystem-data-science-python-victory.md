# 开源数据科学/机器学习生态系统的 6 个组成部分；Python 是否宣布击败了 R？

> 原文：[`www.kdnuggets.com/2018/06/ecosystem-data-science-python-victory.html`](https://www.kdnuggets.com/2018/06/ecosystem-data-science-python-victory.html)

![c](img/3d9c022da2d331bb56691a9617b91b90.png) 评论 在 5 月，我们报告了第 19 届 KDnuggets 软件调查的初步结果：Python 蚕食 R：2018 年分析、数据科学、机器学习的顶级软件：趋势与分析。

在这里，我们更详细地查看哪些工具能够很好地配合使用。我们去年确定的开源 Python 友好的数据科学工具新兴生态系统已有新成员 - 见下文。

我们在文章末尾提供了一个匿名数据集的链接 - 请告诉我你在数据中发现了什么，并请发布或通过电子邮件将结果发给我。

首先，我们查看哪些工具是相互配合的，为了使图表易于理解，我们选择了至少有 400 票的工具。共有 11 种这样的工具，这种选择也有意义，因为第 11 名（Apache Spark，有 442 票）与第 12 名（Java，309 票）之间存在较大差距。

有许多方法可以衡量两个二元特征之间关联的显著性，比如卡方检验或 T 检验，但我们使用了与我们的 2016 年分析和 2017 年分析相同的 Lift 度量。

然后，我们将关联最强的工具组合在一起，从 Tensorflow 和 Keras 开始，直到得到下面的图 1。为了减少杂乱，我们还过滤了图表，只显示 abs(Lift1) > 15%的关联。

![Poll Data Science 2018 Top11 Ecosystem](img/3dc7d1a3ce5534b576dffcc38fe97894.png)

**图 1：数据科学、机器学习顶级工具关联，2018 年**

条形长度对应于 lift1 的绝对值，颜色表示 lift 值（绿色：关联较强，红色：关联较弱）。工具前面的数字是它们在 KDnuggets 2018 软件调查中的排名，例如 Python 排名第 1，RapidMiner 排名第 2，等等。

我们注意到一组包含 6 种主要工具的现代开源数据科学生态系统，它们是：**Python、Anaconda、scikit-learn、Tensorflow、Keras 和 Apache Spark**。

Rapidminer 与上述所有工具有小的负相关，也没有与其他工具强烈关联。

R 与 Apache Spark、SQL 和 Tableau 有小的正相关。

另一个出现的组是 3 种支持数据科学和机器学习的工具，它们经常一起使用：**SQL、Excel 和 Tableau**。

我们注意到，虽然下面的图表相对于对角线是对称的（右上三角形与左下三角形相等），但在完整图表中，比在一半图表中更容易看到模式。

提升度定义：

> **提升度 (X & Y) = pct (X & Y) / ( pct (X) * pct (Y) )**
> 
> 其中 pct(X) 是选择 X 的用户百分比。
> 
> 提升度 (X&Y) > 1 表示 X&Y 一起出现的频率高于它们独立时的预期频率，
> 
> 如果 X 和 Y 的出现频率与它们独立时的预期频率相符，则提升度 = 1，并且
> 
> 如果 X 和 Y 一起出现的频率低于预期，则提升度 < 1（负相关）
> 
> 为了更容易观察差异，我们定义
> 
> **提升度 1 (X & Y) = 提升度 (X & Y) - 1**

### Python 与 R

接下来我们比较 Python 与 R。

设 **with_Py(X)** = 使用 Python 的工具 X 的百分比，以及 **with_R(X)** 为使用 R 的工具 X 的百分比。为了可视化每个工具与 Python 或 R 的接近程度，我们使用了一个非常简单的度量 **Bias_Py_R(X) = with_Py(X) - with_R(X)**，如果工具更常与 Python 一起使用则为正值，如果更常与 R 一起使用则为负值。

在图 2 中，我们绘制了最受欢迎的工具的偏见，这些工具至少获得了 100 票。正如我们所见，几乎所有工具都偏向于 Python。唯一的两个例外是 IBM SPSS Statistics 和 SAS Base。作为对比，在类似的 2017 年分析中，有 10 个这样的工具：SAS Base、Microsoft 工具、Weka、RapidMiner、Tableau 和 Knime，几乎所有这些工具的使用量都与 Python 一起增加。

![Python 与 R 2018 投票](img/195b6c7e44adf7b436712cb64fde2817.png) **图 2：KDnuggets 2018 数据科学、机器学习投票：Python 与 R 的偏见**

Python 是否战胜了 R？

我认为不是这样，因为 R 是一个极其优秀的平台，具有巨大的深度和广度，广泛用于数据分析和可视化，它仍然占有约 50% 的市场份额。我预计 R 会被许多数据科学家使用很长时间，但未来，我期待 Python 生态系统会有更多的发展和活力。

### 大数据与深度学习

大数据（Spark / Hadoop 工具）在 KDnuggets 2018 软件投票中被 33% 的受访者使用，这与 2017 年的比例完全相同。这表明，大多数数据科学家处理的是中小数据，不需要 Hadoop / Spark，或者他们使用的是其他云端解决方案。

然而，深度学习工具的比例从 32% 增长到了 43%。

对于每个工具 X，我们计算它与 Spark/Hadoop 工具的使用频率（纵轴），以及它与深度学习工具的使用频率（横轴）。

这是一个显示了顶级工具的图表（获得超过 100 票），排除了深度学习和大数据工具本身。

![2018 年大数据深度学习亲和度投票](img/add0b943eb3089682be7c0ebd30b7f11.png) **图 3：KDnuggets 2018 数据科学、机器学习投票：深度学习与 Spark/Hadoop 亲和度**

我们注意到 Scala 是在深度学习和大数据中最常用的语言。图表在左下角较重，几乎每个工具在深度学习中的使用频率都高于在大数据中的使用频率。

这是匿名调查数据的 CSV 格式链接，包含以下列

+   Nrand: 记录 ID（随机化，记录顺序与投票顺序无关）

+   region: usca: 美国/加拿大，euro: 欧洲，asia: 亚洲，ltam: 拉丁美洲，afme: 非洲/中东，aunz: 澳大利亚/新西兰

+   Python: 如果 Votes（最后一列）中包含 Python，则为 1，否则为 0。

+   RapidMiner: 如果 Votes 中包含 RapidMiner，则为 1，否则为 0。

+   R language: 如果 Votes 中包含“R Language”，则为 1，否则为 0。我们使用“R Language”而不是 R，以便更容易进行正则表达式匹配。

+   SQL Language: 如果 Votes 中包含“SQL Language”，则为 1，否则为 0。

+   Excel: 如果 Votes 中包含 Excel，则为 1，否则为 0。

+   Anaconda: 如果 Votes 中包含 Anaconda，则为 1，否则为 0。

+   Tensorflow: 如果 Votes 中包含 Tensorflow，则为 1，否则为 0。

+   Tableau: 如果 Votes 中包含 Tableau，则为 1，否则为 0。

+   scikit-learn: 如果 Votes 中包含 scikit-learn，则为 1，否则为 0。

+   Keras: 如果 Votes 中包含 KNIME，则为 1，否则为 0。

+   Apache Spark: 如果 Votes 中包含 Apache Spark，则为 1，否则为 0。

+   With DL: 如果 Votes 中包含深度学习工具，则为 1，否则为 0。

+   With BD: 如果 Votes 中包含大数据工具，则为 1，否则为 0。

+   ntools: Votes 中的工具数量

+   Votes: 投票列表，用分号“;”分隔

请告诉我你的发现！

**相关：**

+   Python 蚕食 R：2018 年分析、数据科学、机器学习的顶级软件：趋势与分析。

+   新兴生态系统：数据科学和机器学习软件分析，2017 年

+   分析、数据科学、机器学习软件的最新领导者、趋势和惊喜调查，2017 年

### 更多相关内容

+   [成为优秀数据科学家所需的 5 项关键技能](https://www.kdnuggets.com/2021/12/5-key-skills-needed-become-great-data-scientist.html)

+   [每个初学者数据科学家应该掌握的 6 种预测模型](https://www.kdnuggets.com/2021/12/6-predictive-models-every-beginner-data-scientist-master.html)

+   [2021 年最佳 ETL 工具](https://www.kdnuggets.com/2021/12/mozart-best-etl-tools-2021.html)

+   [它还活着！用 Python 和一些便宜的基本组件构建你的第一个机器人](https://www.kdnuggets.com/2023/06/manning-build-first-robots-python-cheap-basic-components.html)

+   [停止学习数据科学以寻找目标，并寻找目标去…](https://www.kdnuggets.com/2021/12/stop-learning-data-science-find-purpose.html)

+   [数据共享平台的 5 个关键组成部分](https://www.kdnuggets.com/2022/05/5-key-components-data-sharing-platform.html)
