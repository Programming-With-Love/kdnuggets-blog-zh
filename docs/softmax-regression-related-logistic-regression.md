# 什么是 Softmax 回归以及它与逻辑回归的关系？

> 原文：[`www.kdnuggets.com/2016/07/softmax-regression-related-logistic-regression.html`](https://www.kdnuggets.com/2016/07/softmax-regression-related-logistic-regression.html)

Softmax 回归（同义词：多项式逻辑回归、最大熵分类器或仅多类逻辑回归）是逻辑回归的一种推广，适用于多类分类（假设各类别是相互排斥的）。相比之下，在二分类任务中，我们使用（标准）逻辑回归模型。

现在，让我简要解释一下这如何工作以及 softmax 回归与逻辑回归的区别。我在这里有一个关于逻辑回归的更详细的解释：[LogisticRegression - mlxtend](http://rasbt.github.io/mlxtend/user_guide/classifier/LogisticRegression/)，但让我重用其中一个图来使事情更清楚：

* * *

## 我们的前三大课程推荐

![](img/0244c01ba9267c002ef39d4907e0b8fb.png) 1\. [谷歌网络安全证书](https://www.kdnuggets.com/google-cybersecurity) - 快速通道进入网络安全职业。

![](img/e225c49c3c91745821c8c0368bf04711.png) 2\. [谷歌数据分析专业证书](https://www.kdnuggets.com/google-data-analytics) - 提升你的数据分析技能

![](img/0244c01ba9267c002ef39d4907e0b8fb.png) 3\. [谷歌 IT 支持专业证书](https://www.kdnuggets.com/google-itsupport) - 支持你的组织 IT

* * *

![](https://github.com/rasbt/python-machine-learning-book/blob/master/faq/softmax_regression/logistic_regression_schematic.png)

正如名字所示，在 softmax 回归（SMR）中，我们用所谓的 *softmax 函数* φ 替代了 sigmoid 逻辑函数：

![](https://github.com/rasbt/python-machine-learning-book/blob/master/faq/softmax_regression/1.png)

我们将净输入 z 定义为

![](https://github.com/rasbt/python-machine-learning-book/blob/master/faq/softmax_regression/2.png)

(*w* 是权重向量，*x* 是 1 个训练样本的特征向量，*w0* 是偏置项。)

现在，这个 softmax 函数计算这个训练样本 x(i) 属于类别 *j* 的概率，给定权重和净输入 z(i)。因此，我们计算每个类别标签 *j = 1, ..., k* 的概率 *p(y = j | x(i); wj)*。注意分母中的归一化项，这使得这些类别概率的总和为 1。

为了说明 softmax 的概念，让我们通过一个具体的例子来说明。假设我们有一个包含来自 3 个不同类别（0、1 和 2）的 4 个样本的训练集。

![](https://github.com/rasbt/python-machine-learning-book/blob/master/faq/softmax_regression/3.png)

首先，我们希望将类别标签编码成更容易处理的格式；我们应用独热编码：

![](https://github.com/rasbt/python-machine-learning-book/blob/master/faq/softmax_regression/4.png)

属于类别 0（第一行）的样本在第一个单元格中有一个 1，属于类别 2 的样本在其行的第二个单元格中有一个 1，依此类推。接下来，让我们定义我们 4 个训练样本的特征矩阵。在这里，我们假设我们的数据集包含 2 个特征；因此，我们创建一个 4×(2+1)维的矩阵（+1 是为了偏置项）。

![](https://github.com/rasbt/python-machine-learning-book/blob/master/faq/softmax_regression/5.png)

类似地，我们创建了一个(2+1)×3 维的权重矩阵（每个特征一行，每个类别一列）。

为了计算净输入，我们将 4×(2+1)的特征矩阵 X 与(2+1)×3 的权重矩阵 W 相乘。

Z = WX

这产生一个 4×3 的输出矩阵（n_samples × n_classes）。

![](https://github.com/rasbt/python-machine-learning-book/blob/master/faq/softmax_regression/6.png)

现在，到了计算我们之前讨论的 softmax 激活的时候了：

![](https://github.com/rasbt/python-machine-learning-book/blob/master/faq/softmax_regression/7.png)

![](https://github.com/rasbt/python-machine-learning-book/blob/master/faq/softmax_regression/8.png)

如我们所见，每个样本（行）的值现在很好地加起来等于 1。例如，我们可以说第一个样本

`[ 0.29450637 0.34216758 0.36332605]`有 29.45%的概率属于类别 0。现在，为了将这些概率转换回类别标签，我们可以简单地取每行的 argmax 索引位置：

![](https://github.com/rasbt/python-machine-learning-book/blob/master/faq/softmax_regression/9.png)

如我们所见，我们的预测完全错误，因为正确的类别标签是`[0, 1, 2, 2]`。现在，为了训练我们的逻辑回归模型（例如，通过优化算法如梯度下降），我们需要定义一个我们想要最小化的成本函数*J*：

![](https://github.com/rasbt/python-machine-learning-book/blob/master/faq/softmax_regression/10.png)

这是我们所有 n 个训练样本上的交叉熵的平均值。交叉熵函数定义为

![](https://github.com/rasbt/python-machine-learning-book/blob/master/faq/softmax_regression/11.png)

这里的 T 代表“目标”（真实类别标签），O 代表输出（通过 softmax 计算的概率；*不是*预测的类别标签）。

![](https://github.com/rasbt/python-machine-learning-book/blob/master/faq/softmax_regression/12.png)

为了通过梯度下降学习我们的 softmax 模型，我们需要计算导数

![](https://github.com/rasbt/python-machine-learning-book/blob/master/faq/softmax_regression/13.png)

然后我们用它来在梯度的反方向上更新权重：

![](https://github.com/rasbt/python-machine-learning-book/blob/master/faq/softmax_regression/14.png) 每个类别 j。

（注意 w_j 是类别 *y=j* 的权重向量。）我不想在这里详细讨论更多乏味的细节，但这个成本导数实际上是：

![](https://github.com/rasbt/python-machine-learning-book/blob/master/faq/softmax_regression/15.png)

使用这个成本梯度，我们迭代地更新权重矩阵，直到达到指定的训练周期（对训练集的遍历次数）或达到期望的成本阈值。

**简介： [Sebastian Raschka](https://twitter.com/rasbt)** 是一位“数据科学家”和机器学习爱好者，对 Python 和开源充满热情。著有《[Python 机器学习](https://www.packtpub.com/big-data-and-business-intelligence/python-machine-learning)》。密歇根州立大学。

[原文](https://github.com/rasbt/python-machine-learning-book/blob/master/faq/softmax_regression.md)。经许可转载。

**相关：**

+   深度学习何时比 SVM 或随机森林效果更好？

+   分类作为学习机器的发展

+   为什么从零开始实现机器学习算法？

### 更多相关话题

+   [数据科学定义幽默：一系列古怪的名言…](https://www.kdnuggets.com/2022/02/data-science-definition-humor.html)

+   [比较线性回归与逻辑回归](https://www.kdnuggets.com/2022/11/comparing-linear-logistic-regression.html)

+   [分类指标演示：逻辑回归与…](https://www.kdnuggets.com/2022/10/classification-metrics-walkthrough-logistic-regression-accuracy-precision-recall-roc.html)

+   [逻辑回归概述](https://www.kdnuggets.com/2022/02/overview-logistic-regression.html)

+   [线性回归与逻辑回归：简明解释](https://www.kdnuggets.com/2022/03/linear-logistic-regression-succinct-explanation.html)

+   [KDnuggets 新闻 22:n12，3 月 23 日：最佳数据科学书籍…](https://www.kdnuggets.com/2022/n12.html)
