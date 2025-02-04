# 调整神经网络中的超参数

> 原文：[`www.kdnuggets.com/tuning-hyperparameters-in-neural-networks`](https://www.kdnuggets.com/tuning-hyperparameters-in-neural-networks)

![调整神经网络中的超参数](img/b9de72ea3c51ae95da6057db4e0a857f.png)

超参数决定了您的神经网络学习和处理信息的效果。模型参数是在训练过程中学习的。与这些参数不同，超参数必须在训练过程开始之前设置。在本文中，我们将描述优化模型中超参数的技术。

* * *

## 我们的前三个课程推荐

![](img/0244c01ba9267c002ef39d4907e0b8fb.png) 1\. [谷歌网络安全证书](https://www.kdnuggets.com/google-cybersecurity) - 快速进入网络安全职业。

![](img/e225c49c3c91745821c8c0368bf04711.png) 2\. [谷歌数据分析专业证书](https://www.kdnuggets.com/google-data-analytics) - 提升您的数据分析技能

![](img/0244c01ba9267c002ef39d4907e0b8fb.png) 3\. [谷歌 IT 支持专业证书](https://www.kdnuggets.com/google-itsupport) - 支持您的组织的 IT 需求

* * *

## 神经网络中的超参数

### 学习率

学习率告诉模型基于其错误改变多少。如果学习率高，模型学习得快，但可能犯错误。如果学习率低，模型学习得慢但更仔细。这会导致较少的错误和更好的准确率。

![调整神经网络中的超参数](img/2b104f721c61169c260d51c2f1f83c47.png) 来源: https://www.jeremyjordan.me/nn-learning-rate/

有几种调整学习率以获得最佳结果的方法。这涉及在训练过程中在预定义的时间间隔调整学习率。此外，像 Adam 这样的优化器使学习率能够根据训练的执行进行自我调节。

### 批量大小

批量大小是模型在给定时间接受的训练样本数量。大批量大小意味着模型在更新参数之前处理更多的样本。这可以导致更稳定的学习，但需要更多的内存。另一方面，小批量大小会更频繁地更新模型。在这种情况下，学习可以更快，但每次更新的变化更多。

批量大小的值影响学习的内存和处理时间。

### 纪元数

纪元是指模型在训练过程中遍历整个数据集的次数。一个纪元包括多个周期，在这些周期中，所有数据批次都会展示给模型，模型从中学习，并优化其参数。更多的纪元有助于模型学习，但如果观察不当，可能导致过拟合。决定正确的纪元数对于获得良好的准确率是必要的。像早停这样的技术通常用于找到这种平衡。

### 激活函数

激活函数决定神经元是否应该被激活。这会导致模型的非线性。这种非线性特别有益，尤其是在尝试建模数据中的复杂交互时。

![神经网络中的超参数调整](img/bda31e9774872cf755f405bf06b7dd96.png)来源：https://www.researchgate.net/publication/354971308/figure/fig1/AS:1080246367457377@1634562212739/Curves-of-the-Sigmoid-Tanh-and-ReLu-activation-functions.jpg

常见的激活函数包括 ReLU、Sigmoid 和 Tanh。ReLU 使神经网络的训练更快，因为它只允许神经元中的正激活。Sigmoid 用于分配概率，因为它输出一个介于 0 和 1 之间的值。Tanh 尤其在不想使用从 0 到±无穷大的整个范围时是有利的。选择合适的激活函数需要仔细考虑，因为它决定了网络是否能够做出良好的预测。

### Dropout

Dropout 是一种用于避免模型过拟合的技术。它通过将神经元的输出在每次训练迭代时设置为零，随机停用或“丢弃”一些神经元。这个过程防止了神经元过度依赖特定的输入、特征或其他神经元。通过丢弃特定神经元的结果，Dropout 帮助网络在训练过程中专注于关键特征。Dropout 通常在训练期间实现，而在推理阶段则禁用。

## 超参数调整技术

### 手动搜索

这种方法涉及对决定机器学习模型学习过程的参数值进行反复试验。这些设置一次调整一个，以观察它对模型性能的影响。让我们尝试手动更改设置以获得更好的准确性。

```py
learning_rate = 0.01
batch_size = 64
num_layers = 4

model = Model(learning_rate=learning_rate, batch_size=batch_size, num_layers=num_layers)
model.fit(X_train, y_train) 
```

手动搜索很简单，因为你不需要任何复杂的算法来手动设置测试参数。然而，与其他方法相比，它有几个缺点。它可能需要很长时间，而且可能没有自动化方法高效地找到最佳设置。

### 网格搜索

网格搜索测试许多不同的超参数组合以找到最佳组合。它在部分数据上训练模型。之后，它检查模型在另一部分数据上的表现。我们可以使用 GridSearchCV 实现网格搜索，以找到最佳模型。

```py
from sklearn.model_selection import GridSearchCV

param_grid = {
    'learning_rate': [0.001, 0.01, 0.1],
    'batch_size': [32, 64, 128],
    'num_layers': [2, 4, 8]
}

grid_search = GridSearchCV(model, param_grid, cv=5)
grid_search.fit(X_train, y_train) 
```

网格搜索比手动搜索快得多。然而，它计算开销很大，因为检查每个可能的组合需要时间。

### 随机搜索

这种技术随机选择超参数组合以找到最有效的模型。对于每个随机组合，它训练模型并检查其表现如何。通过这种方式，它可以快速找到使模型表现更好的良好设置。我们可以使用 RandomizedSearchCV 实现随机搜索，以在训练数据上获得最佳模型。

```py
from sklearn.model_selection import RandomizedSearchCV
from scipy.stats import uniform, randint

param_dist = {
    'learning_rate': uniform(0.001, 0.1),
    'batch_size': randint(32, 129),
    'num_layers': randint(2, 9)
}

random_search = RandomizedSearchCV(model, param_distributions=param_dist, n_iter=10, cv=5)
random_search.fit(X_train, y_train) 
```

随机搜索通常优于网格搜索，因为只检查少量的超参数以获取合适的超参数设置。然而，当超参数空间较大时，它可能不会找到正确的超参数组合。

## 总结

我们已经涵盖了一些基本的超参数调优技术。高级技术包括贝叶斯优化、遗传算法和 Hyperband。

**[Jayita Gulati](https://www.linkedin.com/in/jayitagulati1998/)** 是一位对构建机器学习模型充满热情的机器学习爱好者和技术作者。她拥有利物浦大学计算机科学硕士学位。

### 相关话题

+   [调优随机森林超参数](https://www.kdnuggets.com/2022/08/tuning-random-forest-hyperparameters.html)

+   [调优 XGBoost 超参数](https://www.kdnuggets.com/2022/08/tuning-xgboost-hyperparameters.html)

+   [使用 PyTorch 进行可解释神经网络](https://www.kdnuggets.com/2022/01/interpretable-neural-networks-pytorch.html)

+   [使用线性回归模型而不是…的 3 个理由](https://www.kdnuggets.com/2021/08/3-reasons-linear-regression-instead-neural-networks.html)

+   [深度神经网络不会引领我们走向 AGI](https://www.kdnuggets.com/2021/12/deep-neural-networks-not-toward-agi.html)

+   [前沿的可解释预测与即时预测…](https://www.kdnuggets.com/2021/12/sota-explainable-forecasting-and-nowcasting.html)
