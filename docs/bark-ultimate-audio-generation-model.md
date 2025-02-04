# Bark: 终极音频生成模型

> 原文：[`www.kdnuggets.com/2023/05/bark-ultimate-audio-generation-model.html`](https://www.kdnuggets.com/2023/05/bark-ultimate-audio-generation-model.html)

![Bark: 终极音频生成模型](img/e336ec3158f3927662904291bbcddec1.png)

图片由作者提供 | Canva Pro | Bing 图片创建者

我们正在见证文本到语音模型的快速进展，这些模型在实现更自然的输出方面表现出了显著的改进。这个领域的进步不仅限于语音生成；在音乐和环境声音生成以及语音克隆的发展上也取得了重大突破，进展迅速。

* * *

## 我们的前三个课程推荐

![](img/0244c01ba9267c002ef39d4907e0b8fb.png) 1\. [Google 网络安全证书](https://www.kdnuggets.com/google-cybersecurity) - 快速进入网络安全领域。

![](img/e225c49c3c91745821c8c0368bf04711.png) 2\. [Google 数据分析专业证书](https://www.kdnuggets.com/google-data-analytics) - 提升你的数据分析能力

![](img/0244c01ba9267c002ef39d4907e0b8fb.png) 3\. [Google IT 支持专业证书](https://www.kdnuggets.com/google-itsupport) - 支持你所在组织的 IT 工作

* * *

在这篇文章中，我们将学习 Bark，这个终极音频生成模型，能够生成各种语言的语音、环境声音、音乐和多讲者提示。我们将深入了解它的功能和关键特性，并提供入门指南。

# 什么是 Bark？

[Bark](https://github.com/suno-ai/bark)，由[Suno](https://suno.ai/)开发，是一种基于变换器的文本到音频模型，擅长生成高度逼真的多语言语音、音乐、背景噪音，甚至简单的声音效果。此外，该模型还可以产生各种非语言交流，如笑声、叹息和哭声。你可以访问已准备好的预训练模型检查点。

![Bark: 终极音频生成模型](img/6f584e5229d67ea4872d8fe22a09300e.png)

图片来源于[Bark by suno](https://huggingface.co/spaces/suno/bark)

# Bark 如何工作？

Bark，像[Vall-E](http://vall-e)以及该领域其他令人印象深刻的作品一样，采用 GPT 风格的模型从头生成音频。然而，与 Vall-E 不同，Bark 使用高级语义令牌来嵌入初始文本提示，而不依赖于音素。这使得 Bark 能够广泛适应超越语音的各种任意指令，包括音乐歌词、声音效果以及训练数据中的非语音声音。

生成的语义令牌随后由第二个模型处理，将其转换为音频编解码器令牌，从而生成完整的波形。为了通过公开代码让 Bark 对社区开放，我们将 Facebook 的卓越[EnCodec 编解码器](https://github.com/facebookresearch/encodec)作为音频表示进行了集成。

Bark 使用了 [nanoGPT](https://github.com/karpathy/nanoGPT) 来快速实现 GPT 风格的模型，使用 [EnCodec](https://github.com/facebookresearch/encodec) 实现了出色的音频编解码器，使用 [AudioLM](https://github.com/lucidrains/audiolm-pytorch) 进行训练和推理代码，并使用 [Vall-E](https://arxiv.org/abs/2301.02111)， [AudioLM](https://arxiv.org/abs/2209.03143) 以及类似论文来开发 Bark 项目。

# Bark 功能

## 多语言

Bark 支持多种语言，且能够自动检测输入文本的语言。即使文本中包含多种语言的混合，称为代码切换，Bark 也能准确识别并应用每种语言的本地口音。

**尝试提示：**

```py
Hallo, wie geht es dir?. ¿Qué haces aquí? Are you looking **for** someone?
```

## 非语音声音

Bark 可以添加非语音声音，如笑声、喘息声和清喉咙声。

只需添加标签或更改文本以使其听起来自然。

+   [笑声]

+   [叹气]

+   [音乐]

+   [喘息声]

+   [清喉咙]

+   … 用于犹豫

+   ♪ 用于歌词

+   用于强调单词的大写

+   MAN/WOMAN：用于倾向于说话者

**尝试提示：**

```py
" [clears throat] Hello, my name is Abid. And, uh -- and I like cheeseburgers. [laughs] But I also have other interests such as [music]... ♪ singing ♪."
```

## 音乐

Bark 可以生成所有类型的音频，并且不区分语音和音乐。虽然 Bark 有时可能会将文本生成音乐，但你可以通过在歌词周围添加音乐符号来提高其性能，以帮助它区分这两者。

**尝试提示：**

```py
♪ Almost heaven, West Virginia. Blue Ridge Mountains, Shenandoah River. Life is old there, older than the trees. Younger than the mountains, growin' like a breeze ♪
```

## 语音克隆

Bark 能够完全克隆声音。它可以准确复制说话者的语调、音高、情感和韵律，同时保留其他音频特征，如音乐和环境噪声。然而，为了防止这一先进技术的误用，他们实施了限制。用户只能从 Suno 提供的一组完全合成的选项中进行选择。

## 说话者提示

虽然你可以提供具体的说话者提示，例如“NARRATOR”，“MAN”，“WOMAN”等，但重要的是要注意，这些提示可能并不总是被遵守，特别是在存在冲突的音频历史提示时。

**尝试提示：**

```py
MAN: Can you buy me the coffee from starbucks?
WOMAN: Sure, what type of coffee  do you want?
```

# 入门指南

你可以通过在 [Bark by suno](https://huggingface.co/spaces/suno/bark) 上测试演示，或使用 [Google Colab Notebook](https://colab.research.google.com/drive/1eJfA2XUa-mXwdMy7DoYKVYHI1iTd9Vkt?usp=sharing) 进行自己的推理，来开始实验。

如果你想在本地运行，你需要使用下面的命令在终端中安装 bark 包。

```py
pip install git+https://github.com/suno-ai/bark.git
```

之后，在 Jupyter Notebook 中运行下面的代码。该代码将下载所有模型，然后将文本提示转换为音频。

```py
from bark import SAMPLE_RATE, generate_audio, preload_models
from IPython.display import Audio

# download and load all models
preload_models()

# generate audio from text
text_prompt = """
     Hello, my name is Abid Ali. And, uh -- and I like cheeseburgers. [laughs] 
     But I also have other interests such as playing online games like Dota 2.
"""
audio_array = generate_audio(text_prompt)

# play text in notebook
Audio(audio_array, rate=SAMPLE_RATE)
```

你可以使用 <code>scipy.io.wavfile</code> 将音频保存为 wav 格式。

```py
from scipy.io.wavfile import write as write_wav
write_wav("/project/sample_audio.wav", SAMPLE_RATE, audio_array)
```

查看其他资源，学习如何将 Bark 集成到你的应用程序中。

**资源：**

+   GitHub: [suno-ai/bark](https://github.com/suno-ai/bark)

+   Spaces 演示： [Bark by suno](https://huggingface.co/spaces/suno/bark)

+   Colab Notebook: [Bark Google Colab Demo](https://colab.research.google.com/drive/1eJfA2XUa-mXwdMy7DoYKVYHI1iTd9Vkt?usp=sharing)

+   模型卡片：[Bark](https://github.com/suno-ai/bark/blob/main/model-card.md)

+   许可证：CC-BY 4.0 NC。Suno 模型本身可以用于商业用途

+   Suno Studio（早期访问）：[Suno Studio(typeform.com)](https://3os84zs17th.typeform.com/suno-studio?typeform-source=github.com)

**[Abid Ali Awan](https://www.polywork.com/kingabzpro)** ([@1abidaliawan](https://twitter.com/1abidaliawan)) 是一位认证的数据科学专业人士，喜欢构建机器学习模型。目前，他专注于内容创作和撰写有关机器学习和数据科学技术的技术博客。Abid 拥有技术管理硕士学位和电信工程学士学位。他的愿景是利用图神经网络为那些在心理健康上遇到困难的学生打造 AI 产品。

### 更多相关内容

+   [WavJourney：音频故事生成的世界之旅](https://www.kdnuggets.com/wavjourney-a-journey-into-the-world-of-audio-storyline-generation)

+   [检索增强生成：信息检索如何与文本生成相遇](https://www.kdnuggets.com/retrieval-augmented-generation-where-information-retrieval-meets-text-generation)

+   [创建一个提取音频主题的 Python Web 应用程序](https://www.kdnuggets.com/2023/01/creating-web-application-extract-topics-audio-python.html)

+   [终极开源大型语言模型生态系统](https://www.kdnuggets.com/2023/05/ultimate-opensource-large-language-model-ecosystem.html)

+   [人工智能的未来：探索下一代生成模型](https://www.kdnuggets.com/2023/05/future-ai-exploring-next-generation-generative-models.html)

+   [检索增强生成如何使 LLM 更智能](https://www.kdnuggets.com/how-retrieval-augment-generation-makes-llms-smarter)
