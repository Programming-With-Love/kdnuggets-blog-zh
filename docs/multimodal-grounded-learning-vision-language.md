# 多模态基础学习与视觉和语言

> 原文：[`www.kdnuggets.com/2022/11/multimodal-grounded-learning-vision-language.html`](https://www.kdnuggets.com/2022/11/multimodal-grounded-learning-vision-language.html)

![具有视觉和语言的多模态基础学习](img/68641d86fe3e5850bdca92677a85e49b.png)

图片由编辑提供

大家好！我叫博格丹·波诺马尔，我是 AI HOUSE 的首席执行官——一个将人才聚集在一起的乌克兰 AI 社区，涵盖了几十个以教育为主的计划。我们是 [Roosh](http://roosh.tech) 技术生态系统的一部分。

* * *

## 我们的前三名课程推荐

![](img/0244c01ba9267c002ef39d4907e0b8fb.png) 1\. [Google 网络安全证书](https://www.kdnuggets.com/google-cybersecurity) - 快速进入网络安全职业的捷径。

![](img/e225c49c3c91745821c8c0368bf04711.png) 2\. [Google 数据分析专业证书](https://www.kdnuggets.com/google-data-analytics) - 提升你的数据分析能力

![](img/0244c01ba9267c002ef39d4907e0b8fb.png) 3\. [Google IT 支持专业证书](https://www.kdnuggets.com/google-itsupport) - 支持你的组织的 IT

* * *

在 2022 年 8 月，我们推出了一个新的教育项目 [“AI for Ukraine”](https://aiforukraine.aihouse.club/)——由国际人工智能专家举办的一系列研讨会和讲座，以支持乌克兰科技社区的发展。领先的国际 AI/ML 专家参与了这个慈善项目，我们决定分享一些最具洞察力和引人入胜的 AI for Ukraine 会议的摘要。

系列中的第一个摘要是关于乔书亚·本吉奥的讲座，主题是“弥合当前深度学习与人类高级认知能力之间的差距”。你可以在 这里 阅读。

接下来的主题是“具有视觉和语言的多模态基础学习”，由 UC 伯克利的研究科学家安娜·罗尔巴赫（Anna Rohrbach）讲授。

让我们首先承认，人类使用各种感知方式，最显著的是视觉和语言，来感知他们的环境和相互交流。描述我们观察到的事物是人类的一项基本能力。我们有一个共享的现实，这对于理解彼此至关重要，因为我们将概念与我们周围的世界相结合。

在大多数情况下，人类也使用语言来传递关于新事物的知识。

因此，我们可以仅通过语言进行学习。在她的讲座中，加州大学伯克利分校的研究科学家安娜·罗赫巴赫讨论了如何为人工智能模型提供类似的能力，如沟通、基础建立和从语言中学习。尽管在经典的视觉和语言任务中取得了显著进展，尤其是在视觉标注方面，人工智能模型有时仍然面临困难。多模态学习中最具挑战性的方面之一正是基础建立，即——准确地将语言概念映射到视觉观察上。缺乏适当的基础建立可能会通过产生偏见或幻觉对模型产生负面影响。

此外，即使是能够进行交流和基础建立的模型，仍可能需要人类的“建议”，或者学习如何更像人类。语言越来越多地被用来通过实现零-shot 能力、改善泛化、最小化偏见等方式来提升视觉模型。安娜·罗赫巴赫特别感兴趣于开发可能使用语言建议来改善其行为的模型。在讲座中，安娜介绍了她和其他领域研究人员如何实现上述能力以及面临的挑战和即将到来的令人兴奋的机遇。

人工智能已经无处不在，影响着我们生活的各个方面，从医疗保健和辅助技术到自动驾驶和智能家居。此外，更类似人类的人工智能互动将会建立。我们将与人工智能进行更多的交流并建立信任。

在我们的多模态世界中，主要的互动方式有视觉和语言。人与人之间的互动形式包括：

+   关于你看到的内容的沟通（例如，*看，一个蓝松鸦正坐在树枝上*）

+   将概念基础建立到共同现实中

+   从语言中学习（例如，*你知道吗，蓝松鸦喜欢吃橡果？*）

这三点是人类与人工智能互动的关键优先事项。研究人员通过视觉标注来实现这一目标，包括协助视力受限用户和生成解释（例如，蓝松鸦——是一种上部蓝色、下部白色、带有大冠和黑色项链的鸟）。这些解释应该是忠实和自省的。

# 基础建立

视觉基础建立的任务包括名词或短语的定位（例如，一个黑色的喙，一个蓝色的翅膀）。最近，对将其规模化的兴趣增加了。

我们期望 AI 训练模型在模态之间的对齐问题经常出现。我们希望它们将正确的词汇与图像相关联。然而，实际上情况并非总是如此。例如，系统可能会说“鸟儿正坐在树枝上”，但我们在图像中看不到树枝。这是基础建立失败的一个例子。缺乏基础建立有时甚至可能伤害用户。

安娜建议将语言作为人工智能模型的知识来源，就像我们人类一样。我们可以利用语言进行零样本学习。这种方法已经被使用过。例如，当你被要求列出需要了解的新物种的属性时。最近，随着大型模型的出现，这种方法得到了进一步的发展。

实现基础的另一种方法是使用建议性学习。我们不仅仅通过经验或做事来学习，我们还可以通过阅读和听其他人来学习。同样，人工智能也可以通过纠正不良模型行为来进行训练。例如，如果有一张鸟在水面上飞翔的照片，机器可能会对鸟的类型感到困惑，因此我们可以告诉它关注鸟而不是水面。因此，机器不会将其与鸭子混淆。

因此，我们需要构建能够交流、具有基础并从语言中学习的人工智能模型。

安娜·罗尔巴赫将讲座概述为以下几个方面：

+   交流需要有基础。

+   有建议性的基础交流。

+   从语言中学习以提高视觉鲁棒性和迁移能力。

# 交流需要有基础。

如果有一张人骑滑雪板的照片。机器很可能将其识别为“他”。描述模型即使在人类不会提及性别的情况下也会谈论性别。模型不仅捕捉到不平等（男性的数据更多），还夸大了这种不平衡。例如，在一张女人坐在桌前使用笔记本电脑的照片中，机器仍然将此人识别为“男人”。模型甚至没有看到这个人，它看到的是一个显示器，并基于一些相关性假设这是一个男人。在一个男人拿着网球拍的例子中，模型正确地识别了性别，但不是通过看人，而是通过看网球拍。因此，在讨论性别时，模型并没有关注到这个人。

安娜和其他研究人员正在通过将注意力转移到正确的对象上来克服这个问题。为此，他们将描述正确性损失应用于性别。他们引入了置信度损失和外观混淆损失。这提供了更加公平的模型行为：对男性和女性的错误率相似。

在 Baseline-FT 和 UpWeight 中，模型识别了“一个男人和一只狗在雪地里”。

在模型无法清晰识别图片中的性别时，均衡器更关心性别错误，并将其识别为“一个人牵着狗散步”。

缺乏基础可能会导致的问题包括：不适当、有害和冒犯性的内容。

# 有建议性的基础交流。

当你自驾时，汽车在减速时可以与你沟通，因为它即将左转。有一个描述（汽车减速）和一个行动解释（因为它即将左转）。安娜和她的同事们在伯克利大学进行了 DeepDrive eXplanation (BDD-X) 数据集实验。模型试图预测车辆的未来自我运动。

他们引入了一种解释生成器，用于生成驾驶模型背后的合理性解释的自然语言。在注意力对齐过程中，关键思想是将车辆控制器和文本解释器对齐，使它们关注相同的输入区域。他们得到的关键结果是最弱对齐的注意力，“作为额外损失的解释”可解释且不影响性能。问题在于系统没有关注行人，也没有对其存在作出反应。

## 可建议的驾驶模型

如何通过建议让模型识别行人？观察到的行动，而不是相反。这样，模型学习将其视觉观察总结成自然语言，并预测适当的行动响应。在 CARLA 模拟器中，研究人员研究了一个不可解释的模型、一个可解释的模型和一个建议的模型。人们对建议模型的信任度最高。

因此，将语言建议纳入深度模型可以导致性能更好、更具可解释性的模型，从而获得更高的人类信任。

# 从语言中学习以提高视觉鲁棒性

## 大规模视觉语言模型

CLIP——一个预训练模型，学习将图像与说明匹配。它可以识别和定位许多高层次的概念，但不能识别细粒度的类别，如犬种。

研究人员发现了许多存在于将概念与上下文分离的情境偏差。他们引入了 GALS：通过语言规范引导视觉注意力。这通过提示（如鸟的照片）改善了模型学习。他们将高层次语言任务规范转化为空间注意力，从而引导 CNN 远离偏差。

# 从语言中学习以提高视觉迁移能力

大规模的视觉+语言模型在高层次概念上表现良好，但在细粒度概念上效果不佳。其理念是大量的通用知识被捕捉在外部资源中。

## Zero-Shot Learning

传统的类别级迁移旨在将知识泛化到未见过的对象类别。新的任务级迁移旨在将知识泛化到未见过的数据集或任务。然而，建模外部知识尚未被探索。相比之下，传统的类别级迁移建模外部知识探讨了如何通过一些辅助信息，如嵌入或属性，将已见类别与未见类别关联起来。

在外部知识中，我们可以使用解释。人类利用先前（结构化的）知识。AI 能否做到这一点？研究人员使用了 K-Lite：知识增强语言图像训练和评估。知识有助于提升对细粒度概念的表现，比如 sashimi——一种日本特色菜，由新鲜的生鱼或肉切成薄片，通常配以酱油食用。然而，当知识覆盖范围低且包含虚假信息时，性能会受到影响。研究人员发现，我们可以通过从外部语言中学习进一步提升语言学习。

# 下一步是什么？

AI 模型可以从语言中学习。然而，可能的限制是难以扩展的人类监督。安娜预测，将会引入具有开放式场景、任意概念、复杂关系和世界知识的大规模预训练模型。她的长期愿景是基础的、有根有据的模型将是可组合的和结构化的，这样 AI 将能够进行沟通，更加扎实，并能够从语言中学习。它们还将具有更高的样本效率，减少对人类监督的依赖。

**[Bohdan Ponomar](https://www.linkedin.com/in/bogdan-ponomar-41866328/)** 是 AI HOUSE 社区的首席执行官。他正在为乌克兰的学生和专家创建一个领先的 AI 生态系统，以便建立世界级的 AI 企业。

### 更多相关话题

+   [NExT-GPT 简介：任何对任何的多模态大语言模型](https://www.kdnuggets.com/introduction-to-nextgpt-anytoany-multimodal-large-language-model)

+   [多模态模型解析](https://www.kdnuggets.com/2023/03/multimodal-models-explained.html)

+   [MiniGPT-4：GPT-4 的轻量级替代方案，增强视觉语言理解](https://www.kdnuggets.com/2023/04/minigpt4-lightweight-alternative-gpt4-enhanced-visionlanguage-understanding.html)

+   [数据管理你需要了解的 6 件事及其重要性](https://www.kdnuggets.com/2022/05/6-things-need-know-data-management-matters-computer-vision.html)

+   [TensorFlow 在计算机视觉中的应用——简化迁移学习](https://www.kdnuggets.com/2022/01/tensorflow-computer-vision-transfer-learning-made-easy.html)

+   [KDnuggets 新闻 2022 年 3 月 9 日：在 5 天内构建机器学习 Web 应用](https://www.kdnuggets.com/2022/n10.html)
