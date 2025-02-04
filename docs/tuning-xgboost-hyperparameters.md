# 调整 XGBoost 超参数

> 原文：[`www.kdnuggets.com/2022/08/tuning-xgboost-hyperparameters.html`](https://www.kdnuggets.com/2022/08/tuning-xgboost-hyperparameters.html)

![调整 XGBoost 超参数](img/0ed85dd2a0f411bb383af072d8093e46.png)

[Garett Mizunaka](https://unsplash.com/@garett3) via Unsplash

总结一下，XGBoost 代表极端梯度提升，是一种监督学习算法，属于梯度提升决策树（GBDT）家族的机器学习算法。

* * *

## 我们的前三大课程推荐

![](img/0244c01ba9267c002ef39d4907e0b8fb.png) 1\. [谷歌网络安全证书](https://www.kdnuggets.com/google-cybersecurity) - 快速进入网络安全职业生涯。

![](img/e225c49c3c91745821c8c0368bf04711.png) 2\. [谷歌数据分析专业证书](https://www.kdnuggets.com/google-data-analytics) - 提升你的数据分析技能

![](img/0244c01ba9267c002ef39d4907e0b8fb.png) 3\. [谷歌 IT 支持专业证书](https://www.kdnuggets.com/google-itsupport) - 支持组织的 IT 需求

* * *

他们通过将一组较弱的模型进行组合并通过 if-then-else 真/假特征问题来评估其他决策树。他们以序列形式创建，以评估和估计产生正确决策的概率。

```py
import xgboost as xgb
```

在我们深入调整 XGBoost 超参数之前，让我们了解为什么调优是重要的

# 为什么超参数调优很重要？

超参数调优是提高机器学习模型整体行为和性能的重要部分。它是一种在学习过程之前设置的参数，发生在模型之外。

如果损失函数没有被最小化，缺乏超参数调优可能会导致不准确的结果。我们的目标是使模型产生尽可能少的错误。

超参数用于计算模型参数，其中不同的超参数值能够生成不同的模型参数值。

超参数调优的目的是找到一组最佳的超参数值，这些值能够最大化模型性能、最小化损失并产生更好的输出。

# XGBoost 的特征

## 1\. 梯度树提升

添加了固定数量的树，每次迭代应显示损失函数值的减少。

## 2\. 正则化学习

正则化学习有助于最小化损失函数，并防止发生过拟合或欠拟合 - 有助于平滑最终学习到的权重。

## 3\. 收缩和特征子抽样

这两种技术用于进一步防止过拟合：收缩和特征子抽样。

这些特征将在 XGBoost 的超参数调优中进一步探讨。

# XGBoost 参数调优

XGBoost 参数分为 4 类：

## 1\. 一般参数

这与我们用于增强的提升器类型有关。最常见的类型是树模型或线性模型。

## 2\. Booster 参数

这取决于你选择了哪个 booster。

## 3\. 学习任务参数

这与决定学习场景有关。

## 4\. 命令行参数

这与 XGBoost 的 CLI 版本的行为有关。

一般参数、Booster 参数和任务参数在运行 XGBoost 模型之前设置。命令行参数仅在 XGBoost 的控制台版本中使用。

# 一般参数

这些是 XGBoost 中的一般参数：

`booster [default=gbtree]`

选择使用哪个 booster，如树基模型的 gbtree 和 dart，以及线性函数的 gblinear。

`verbosity [default=1]`

这是消息的打印，合法值为 0（静默）、1（警告）、2（信息）、3（调试）。

`validate_parameters [default to false, except for Python, R and CLI interface]`

当设置为 True 时，XGBoost 将执行输入参数的验证，以检查是否使用了某个参数。

`nthread`

这是用于运行 XGBoost 的并行线程数。

`disable_default_eval_metric [default=false]`

这将标记以禁用默认度量。你可以将其设置为 1 或 true 来禁用。

`num_feature`

在提升中使用的特征维度，设置为特征的最大维度。

## 基于树的学习器最常见的参数

`max_depth [default=6]`

增加此值将使模型更复杂，更容易过拟合，因此在选择值时需要小心。值必须是大于 0 的整数。

`eta [default=0.3, alias: learning_rate]`

这决定了每次迭代的步长。值必须在 0 和 1 之间，默认值为 0.3。较低的学习率使计算变慢，并且需要更多轮次来减少错误，相比之下，学习率较高的模型则更快。

`n_estimators [default=100]`

这是我们集成中的树的数量，即提升轮次的数量。

值必须是大于 0 的整数，默认值为 100。

`subsample [default=1]`

这表示每棵树需要采样的观察值的比例。较低的值有助于防止过拟合，但会增加欠拟合的可能性。值必须在 0 和 1 之间，默认值为 1。

`colsample_bytree, colsample_bylevel, colsample_bynode [default=1]`

这是用于列子采样的一系列参数。特征子采样有助于防止过拟合，并加速并行算法的计算。

```py
params = {
    # Parameters that we are going to tune.
    'max_depth':6,
    'n_estimators': 100,
    'eta':.3,
    'subsample': 1,
    'colsample_bytree': 1,
}
```

# 正则化参数

`alpha [default=0, alias: reg_alpha]`

对权重进行 L1（Lasso 回归）正则化。增加此值将使模型更保守。当特征数量较多时，可能会提高速度性能。可以是任何整数，默认值为 0。

`lambda [default=1, alias: reg_lambda]`

对权重进行 L2（岭回归）正则化。当你增加这个值时，它会使模型更为保守。它还可以帮助减少过拟合。这个值可以是任何整数，默认值是 1。

`gamma [default=0, alias: min_split_loss]`

使树的叶节点进一步分割所需的最小损失减少。Gamma 值越高，正则化越强。它可以是任何整数，默认值是 0。

你可以在这里找到 [XGBoost 参数的完整列表](https://xgboost.readthedocs.io/en/latest/parameter.html)。

# 结论

从这篇文章中，你应该了解 XGBoost 的 3 个特性是如何通过 4 个划分的参数调优组实现的。这些特性随后通过不同的 XGBoost 参数进行了进一步探索。

**[Nisha Arya](https://www.linkedin.com/in/nisha-arya-ahmed/)** 是一名数据科学家和自由职业技术作家。她特别关注提供数据科学职业建议或教程以及围绕数据科学的理论知识。她还希望探索人工智能如何/能如何促进人类寿命的延续。她是一位热心学习者，寻求拓宽技术知识和写作技能，同时帮助指导他人。

### 更多相关内容

+   [调优随机森林超参数](https://www.kdnuggets.com/2022/08/tuning-random-forest-hyperparameters.html)

+   [神经网络中的超参数调优](https://www.kdnuggets.com/tuning-hyperparameters-in-neural-networks)

+   [如何加快 XGBoost 模型训练](https://www.kdnuggets.com/2021/12/speed-xgboost-model-training.html)

+   [XGBoost 的假设是什么？](https://www.kdnuggets.com/2022/08/assumptions-xgboost.html)

+   [利用 XGBoost 进行时间序列预测](https://www.kdnuggets.com/2023/08/leveraging-xgboost-timeseries-forecasting.html)

+   [GBM 和 XGBoost 之间到底有什么区别？](https://www.kdnuggets.com/wtf-is-the-difference-between-gbm-and-xgboost)
