---
title: Sentiment Analysis
date: 2019-10-01 16:03:58
categories: 
- course notes
tags:
- course notes
- natural language processing
---

Taking some notes after I watched [Stanford Coursera course](http://web.stanford.edu/~jurafsky/NLPCourseraSlides.html) "Sentiment Analysis" by [Dan Jurafsky](http://www.stanford.edu/people/jurafsky) and [Christopher Manning](http://nlp.stanford.edu/manning/).

<!-- more -->

------

# Introduction

Sentiment Analysis, 也叫 opinion extraction/opinion mining/sentiment mining/subjectivity analysis，中文译作情感分析/文本情感分析，是自然语言处理 (Natural Language Processing) 的应用之一。

根据Wiki

> **文本情感分析**（也称为**意见挖掘**）是指用[自然语言处理](https://zh.wikipedia.org/wiki/自然语言处理)、[文本挖掘](https://zh.wikipedia.org/wiki/文本挖掘)以及[计算机语言学](https://zh.wikipedia.org/wiki/计算机语言学)等方法来识别和提取原素材中的主观信息。

注意这里说的是**主观信息**，并没有用简单的**情感**一词代替，这是因为sentiment analysis并不仅仅是抽取出情感。事实上，sentiment这个词虽然可以翻译为情感，有一个释义也是"emotion"，但是也有一个释义是 "an attitude, thought, or judgment prompted by feeling" (By [Merriam-webster](https://www.merriam-webster.com/dictionary/sentiment))，与opinion同义。因此sentiment analysis的sentiment不能单做为emotion看待。在本课中，Dan认为sentiment是attitude的子集，强调的主要是attitude.

## Tasks

要分析出sentiment，也就是要知道以下几个：

1. Source，是谁的sentiment
2. Target，对什么的sentiment
3. what/type，什么样的的sentiment
4. 除此之外，也需要知道包含sentiment的文本

根据难度的不同，可以将sentiment analysis 分成以下task:

1. Easy模式：Polarity detection，判断positive/negative
2. Medium模式：在判断的基础上为attitude给出强弱
3. Hard模式：判断target/source，以及更加复杂的attitude

## Some projects

1. [Google - Twitter Sentiment Analysis](https://www.kaggle.com/c/twitter-sentiment-analysis2/overview)

   判断sentiment是positive/negative/neural

2. [Twitter mood predicts the stock market](https://arxiv.org/pdf/1010.3003&)

3. [Twitter sentiment APP](http://help.sentiment140.com/)

# Polarity detection and Baseline Algorithm

baseline algorithm采取常见的自然语言处理分类算法。

以polarity detection为例，将sentiment看做类别，比如positive/negative，然后对文本进行分类。主要步骤包括：

1. Tokenization

2. Feature extraction

3. Classification

其中，常用的分类算法包括Naive Bayes, Max entropy, SVM, 且MaxEnt和SVM在该task中的表现比NB好。本课程并没有介绍前两者比后者好的原因，但是我认为应该主要是由于朴素贝叶斯分类器的“特征之间相互独立”条件无法达到（一个句子里各个词之间并不是相互独立的）。

## Deal with negation

本课中介绍了一种非常intuitive的处理否定的方式：

当分句中出现了否定，在分句后所有的词前加上not

举例（stole from Dan's slides）：

<img src="https://tva1.sinaimg.cn/large/006y8mN6ly1g7jbuqc1zkj316r07xdh5.jpg" style="zoom: 150%;" />

## Boolean Multinomial Naïve Bayes

本课程中选用了boolean multinomial naive bayes而不是在文本分类中常见的multinomial naive bayes。两者的区别在于前者只关注词是否出现，而后者会关注count。因此，我认为这实际上是一种伯努利朴素贝叶斯分类器。这样做的原因是因为对于sentiment analysis而言，一个代表positive/negative的词只要出现了一次，即可表明态度，多次出现与只出现一次表达的态度差别不大。（这里以polarity detection为例）

## Scaled likelihood

这是一个需要注意的点。

在一些文本，比如评分文本中，会出现给出不同评分的人数不同（打8-10分的比打2分的人多），不同词语的使用频率不同等问题，这时候要用scaled likelihood，不能直接使用frequency/count。

# Lexicon

sentiment analysis是一类非常依赖词典的任务，通常我们需要知道某个词属于哪一个attitude，也就是说我们要知道某个词属于哪一类。

## commonly-used lexicon

- **The General Inquirer**
- **LIWC(Linguistic Inquiry and Word Count)**
- MPQA Subjectivity Cues Lexicon
- Bing Liu Opinion Lexicon
- SentiWordNet

其中The General Inquirer是通用领域的；LIWC是社会学、心理学常用词典；除了SentiWordNet，其他字典的差别不大。

## Build lexicon 

建词典的基本思路是半监督学习的思路，首先要用种子集(seed-set)，然后通过种子集学习和标记其他词语。本课程中介绍了三种用来学习字典的算法，主要是针对Polarity detection：

1. **Hatzivassiloglou and McKeown**的算法

   基本思想是通过" and"和“but”来判断两个词的attitude是一致还是不一致，通过count来计算两者一致/不一致的程度。
2. **Turney Algorithm**

   基本思想是通过短语的共现来学习，如果一个短语与excellent一起出现了很多次，就更可能是positive的。Turney algorithm学习的是短语而非词的极性，可以通过学习某一领域的文档学习到domain-specific information，效果比较好。
3. **Use WordNet to learn Polarity**

   基本思想是用WordNet的同义词/近义词/反义词等来学习。