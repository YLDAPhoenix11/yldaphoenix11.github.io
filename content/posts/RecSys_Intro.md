---
title: RecSys Intro
date: 2019-04-17 18:01:32
categories: 
- course notes
- recommender systems
tags:
- course notes
- recommender systems
---

_Course note: overview of Recommender systems_

<!--more-->

---

# 什么是推荐和推荐系统

(**待施工**)

# 推荐系统要考虑的问题

## 用户面临的问题

### 准确率 accuracy

如何量度准确性是主要问题？KPI or Off-line test or A/B test?

### 可解释性 interpreability

用户在意可解释性吗？

### 马太效应 the rich get richer

这是一个以item为中心的反馈循环：

popular items更容易被消费，然后被评高分，这使得它们更容易被推荐给用户，如此形成一个效果越来越强的正反馈循环，最终使得popular items被推荐的多，其他item被推荐的少。（这种情况同样与冷启动问题有关）

### 过滤气泡 The filter bubble 

这是一个以user为中心的反馈循环：

当用户始终通过个性化的行为与产品进行交互，同时推荐又缺乏多样性、比较集中时，推荐给用户的会越来越集中。常见的比如今日头条等网站上都是与自己观点一致的信息。

这种情况也会出现在社交网络中，当一个社交圈里的用户都非常相似时，推荐也会逐渐局限、集中。

### 偶然性的内容  Serendipity 

serenfipity 是可以给用户带来惊喜的内容。它和新颖性novelty有所不同。novelty所推荐的东西是新颖但有一定相关性的，serendipity则是偶然的、意外的。

Serendipity和推荐出的东西的相似度是一个trade-off。

### 多样性 Diversity

大多数算法把推荐出的每一个item视为一类，但是有可能推荐出的每一个item都属于一个类。可以加一个多样性参数来判断用户对于某一类更有兴趣。

### 用户的兴趣随着时间变化 Time-variance 

随着时间变化，用户可能对某一类感兴趣或者失去了兴趣，也可能其兴趣在好几个类中不断地变来变去

### 渴望的 vs.  实际的 aspirational vs actual 

用户的评分可能不是反映他们实际上会消费购买的，而是反映他们想要的。

[一篇medium文章谈到了这个](https://medium.com/the-graph/recommendations-spotify-actual-versus-aspirational-behaviour-85f1c481ffe)

## 工程中的问题

### 冷启动 cold-start

针对新加入的item：基于内容的推荐 content based等

针对新加入的user：基于地理位置location based, 用户描述user description 等

### 可扩展性 Scalability

在实际使用中机器学习算法必须考虑大数据的问题。有些算法能更好的处理大数据。通常我们需要在速度和准确度之间进行取舍。

### 实时 vs 批次 Real-time vs. Batch

分批次处理的系统可以处理更多的信息，获得更高的准确度；但是，实时系统可以获得更新的信息，对用户的行为立即作出反应。

### 要不要加新特征 add new feature

一个推荐系统只考虑user和item之间的交互，不考虑其他信息。有时候，加入其他信息，例如item的类别等，会带来更好的效果。

# 推荐系统的两大应用场景

### prediction 

评分预测

### ranking 

TOP-N 推荐

# 推荐系统常用算法分类

### Behavior-based

又可以分为memory-based和model-based

### Content-based

(**待施工**)