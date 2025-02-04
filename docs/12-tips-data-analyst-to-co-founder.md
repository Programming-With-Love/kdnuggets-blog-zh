# 12 个技巧：从数据分析师到创业联合创始人

> 原文：[`www.kdnuggets.com/2021/12/12-tips-data-analyst-to-co-founder.html`](https://www.kdnuggets.com/2021/12/12-tips-data-analyst-to-co-founder.html)

评论

**作者：[Roman Zykov](https://twitter.com/rzykov)，数据科学家和 TopDataLab 创始人**。

![](img/35070e880b2fd0609156e10fcb1d68ab.png)

* * *

## 我们的前三大课程推荐

![](img/0244c01ba9267c002ef39d4907e0b8fb.png) 1\. [谷歌网络安全证书](https://www.kdnuggets.com/google-cybersecurity) - 快速进入网络安全职业生涯。

![](img/e225c49c3c91745821c8c0368bf04711.png) 2\. [谷歌数据分析专业证书](https://www.kdnuggets.com/google-data-analytics) - 提升你的数据分析水平

![](img/0244c01ba9267c002ef39d4907e0b8fb.png) 3\. [谷歌 IT 支持专业证书](https://www.kdnuggets.com/google-itsupport) - 支持你的组织在 IT 领域

* * *

在我的职业生涯早期，作为数据分析师的我，像许多人一样，梦想做一些对人们有重大价值的事情。我想要有创意。我想要感受到自己工作的成果，而不仅仅是研究数据。我在几家初创公司工作了十年，然后于 2012 年共同创办了一家电子商务推荐服务公司。在 2020 年疫情期间，我休假了一年——写了一本书，在亚马逊上发布，并在 2021 年夏天完全离开了那家成功的公司（正现金流，150 多名员工分布在俄罗斯、欧洲和南美）。现在我正在从零开始开发下一个项目。

我决定分享一些对我当初创业时非常有用的技巧。此帖补充了我书中的第十二章（“挑战与创业”）。[书籍](https://topdatalab.com/book) [3]。

**为一个客户创建一个产品创意。** 首先，有了创意，然后是产品。如果你有一个创意，最好的测试方法是将其实施在你当前的工作中，为公司带来利益。例如，我的项目在我和我的伙伴们创建公司之前就已经诞生。我在还在职时就作为副业开发了推荐系统。所以我立刻知道该怎么做，特别是在最初阶段。我可以闭着眼睛创建一个最小可行产品（MVP）。

**找到廉价地将产品扩展到成千上万客户的方法**（理解工程）。能够以最小的努力扩展产品至关重要。为此，你需要学习将模型投入生产的实践。除了 Python 和 SQL，了解一些编译编程语言（Java, Scala, C#, C++）是个好主意。了解如何使用不同类型的数据库和 Hadoop 也很有帮助。我发现参观 Netflix 办公室非常有帮助，在那里我获得了一些关于开源软件和 Hadoop 的建议。我花了大约六个月的时间来学习和实施 Hadoop。我还在 O'Reilly STRATA 会议的视频中听说了 Spark。我们是最早在生产中实施 Spark 的团队之一。

**做少些长期研究，多做些业务**。在初创公司，你必须非常迅速地行动，同时获得保证的结果。假设你在两个机器学习算法之间做选择。第一个算法难以开发，但理论上能提供更好的结果。第二个算法简单，但指标一般——作为第一步，我总是会选择简单的那个。是的，你可以将第一个算法放在假设的待办事项中，但你可能会在几个月后改变它。

我花了两年时间在一个短期推荐算法上 [4]。我们做了很多复杂的事情。最终，最简单的算法版本赢得了所有的 A/B 测试。尝试找到完美的算法对我来说是浪费时间。

**理论与实践并不总是相同的。** 我过去十年一直在为电子商务开发推荐算法。关于这个主题的科学文章使用标准指标（Precision, Recall, Novelty, Diversity [2]）。看起来，拿一篇科学论文然后去做。这种方法在计算机视觉领域效果很好，但在我的领域却不适用。购买是一个延迟事件。买家可能在几个小时甚至几天后才进行购买。因此，准确性指标 [1] 与访客转化为买家的之间没有直接的关联。

另一个问题是 — 推荐算法会改变用户行为。当你在用户的过去行为日志上进行离线测试时 — 你没有考虑这一点。这一因素也对在 A/B 测试中预测在线表现的误差有所贡献。

**正确获取指标是成功的关键。** 看起来，选择一个标准指标来衡量你的机器学习模型，一切都会顺利。然而，事实并非如此。你听说过医疗保健中的分类指标问题吗？例如，你有两种不同的 COVID PCR 测试：

+   test A yields more false positives

+   test B yield more false negatives

测试 A 将把更多健康的人送入隔离，这将造成经济损害。测试 B 将漏掉更多病人，他们会传播疾病。测试的选择是一个复杂的问题，这将取决于具体情况。在 A/B 测试两个不同算法后，你也会面临同样的选择。例如，我在推荐系统中遇到过这样的情况：算法改进了商业指标，但推荐内容的视觉效果却变差了。这样的“改进”很难向客户推销。

**全职专注比在晚上做初创公司更好**。我曾经在晚上和周末编程。我甚至买了第二台笔记本电脑，带到现在的工作中，以便有时也能在那里编程。工作后的晚上我很疲倦，所以写的代码中有很多错误。第二天我不得不修复这些错误。有些错误我甚至是在几年后才发现的。因此，尽量找到全身心投入项目的机会。这将为你节省大量精力和时间。

**专业经验的重要性**。有了它，成功更容易而不需要吸引大量投资。但如果缺乏经验，你将不得不花费更多的钱。因此，最好在积极发展的公司中工作以学习更多。我以前的老板曾给过我这样的建议。如果你也曾在潜在客户的另一侧工作过，你将更容易理解他们的需求。大家都知道，客户在产品访谈中不会告诉你所有事情。许多问题甚至对客户自己来说都很难理解。我在电子商务中作为分析师的经验对我帮助很大。我基于在那里获得的知识创建了我的第一个初创公司。

**B2B 初创公司比 B2C 初创公司更有可能成功**。B2B 需要的投资较少，员工数量也较少，而且平均交易额要高得多。在 B2B 中，你需要获得的客户数量远少于 B2C 才能实现盈亏平衡。

**不要盲目模仿**。复制其他公司，尤其是 FAANG 公司的做法很容易。你的公司和内部文化是独特的。简单地将任何标准如开发、ML 模型部署或产品的模板拼凑在一起是不行的。你更可能根据常识和适合你的情况制定自己的规则。

**云计算更适合初创阶段**。现在云计算就像一个乐高构建器——你不必考虑硬件和软件问题，而且扩展相对简单。我在租用的硬件上做了第一个项目，部署了 Hadoop 并设置了所有计算算法。我立即在云中开始了第二个项目，花费的时间少得多。

**客户希望增加销售额而不是获得数据分析**。分析产品比起提升客户销售的系统要复杂得多。如果这种效果也容易检查，例如在 Google Analytics 中，那么你的产品将会非常畅销。这就是为什么我没有创建一个分析项目，而是直接去数据能够直接增加销售的地方——例如推荐系统。

**自助分析。** 尝试在公司中培养自助分析的文化。没有人喜欢被一连串可以用“计算器”完成的任务轰炸。这些是员工可以通过两三次鼠标点击完成的基本任务。你需要满足三个条件才能摆脱这些任务：

+   用户友好的互动分析系统（OLAP、Tableau、Metabase）。

+   最低的数据质量水平。

+   经过培训的用户。

在这三个领域投入努力。即使在发展非常迅速的初创环境中，这也会获得很好的回报。

### 参考资料

[1] Marco Rossetti, Fabio Stella, Markus Zanker, [RecSys 2016：论文会话 1——对比离线和在线推荐评估结果](https://medium.com/r/?url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3DHEsG5rTaPwE) (2016).

[2] Paolo Cremonesi, Yehuda Koren, Roberto Turrin, [推荐算法在 Top-N 推荐任务中的表现](https://www.researchgate.net/publication/221141030_Performance_of_recommender_algorithms_on_top-N_recommendation_tasks) (2010).

[3] Roman Zykov, [Roman 的数据科学：如何将数据货币化](https://topdatalab.com/book) (2021).

[4] Maxim Borisyak, Roman Zykov, Artem Noskov, [Kullback-Leibler 散度在短期用户兴趣检测中的应用](https://arxiv.org/abs/1507.07382) (2015).

**相关：**

+   [为你的数据科学初创公司打造电梯演讲](https://www.kdnuggets.com/2019/08/elevator-pitch-data-science-startup.html)

+   [如何向风险投资公司推介：我们用来筹集资金的演示文稿](https://www.kdnuggets.com/2021/05/vc-pitch-deck-open-source-elt-platform.html)

+   [数据科学家在初创公司成功的六种方法](https://www.kdnuggets.com/2020/05/six-ways-data-scientists-succeed-startup.html)

### 相关话题

+   [在 ChatGPT 时代构建深科技初创公司的 10 个难题](https://www.kdnuggets.com/2023/04/10-hurdles-building-deep-tech-startup-age-chatgpt.html)

+   [数据科学职位名称导航：数据分析师 vs 数据科学家…](https://www.kdnuggets.com/navigating-data-science-job-titles-data-analyst-vs-data-scientist-vs-data-engineer)

+   [数据科学家 vs 数据分析师 vs 数据工程师](https://www.kdnuggets.com/2022/01/data-scientist-data-analyst-data-engineer.html)

+   [从数据分析师到数据战略师：影响力职业路径](https://www.kdnuggets.com/2023/05/data-analyst-data-strategist-career-path-making-impact.html)

+   [准备数据分析师面试](https://www.kdnuggets.com/2022/08/datacamp-preparing-data-analyst-interview.html)

+   [通过 DataCamp 的分析师接管更快地实现数据驱动](https://www.kdnuggets.com/2022/10/datacamp-data-driven-faster-analyst-takeover.html)
