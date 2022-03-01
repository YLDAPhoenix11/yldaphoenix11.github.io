---
title: Overview of A/B Testing
date: 2020-03-19 21:29:58
categories: 
- course notes
- data analytics
tags:
- course notes
- data analytics
- A/B testing
---

_Course note of [A/B testing on Udacity](https://www.udacity.com/course/ab-testing--ud257): Lesson 1_

<!-- more -->

---

# Overview of A/B Testing

## Overview and Introduction

What is useful for A/B testing and what is not?

- Useful when there is clear control and experiment, and good metrics to evaluate.

- is not useful for testing new experience - change version/ a novelty effect; also not useful if missing something

- Quiz1:

  ![](https://tva1.sinaimg.cn/large/006tNbRwgy1g9s2zkiy82j31fz0qd1kx.jpg)

  - why A/B testing is not useful for "Online shopping company"?

    Try askinig users if there is something missing	

  - why A/B testing is not useful for "Add premium service"?

    Users need to opt in a premium service, so it is impossible to randomly assign them to groups. Thus, it cannot be controled. Could gather information by A/B testing on how many users will read the features and how many will upgrade if giving them the choices. But cannnot fully test on this change.

- Quiz2:

  ![](https://tva1.sinaimg.cn/large/006tNbRwgy1g9s2zlpqk5j31eu0qi4nd.jpg)

  - why A/B testing is not useful for "Website selling cars"?

    People buy cars rarely so the change will be too long. And it is hard to know whether people refer ot not, so there is no data.

  - why A/B testing is not useful for "Update brand"?

    Hard to collect behavior data about people's reaction to new logo. And they might need a long time to get used to the new logo.

##An Example

### Choose metrics

- Funnel/User Flow

- Do not choose the metrics that will take a long time to change 

  for example, #courses completed in udacity, since completing a course may take a long time

- Pay attention to the number and ratio

  for example, #clicks may be biased because more users in one group than in the other

- Can use #clicks/#page views (CTR) 

  or #unique visitors who click/#unique visitors to page (may called click-through-probability)

  The latter is better for estimating whether there are more students exploring courses to get rid of the influence of double clicking, reloading and etc.  

### Statistics Part

**Binomial Distribution**

![](https://tva1.sinaimg.cn/large/006tNbRwgy1g9thrs6slvj31ee0td7wh.jpg)

- drawing 20 card: not independent
- roll a die 50 times: independent events
- clicks on a search results page: if a user didn't find a result, he/she will search with a similar keyword immediately. These two events are not independent.
- students completion of courses: not purely independent since one student may have multiple accounts and some students may study with his/her friends, but can be regarded as independent events.
- Purchase of items: not independent events. Some items are purchases together (Recsys).

**Confidence Interval**

以下是一个binomial ditribution, one sample 计算confidence interval 的过程:

![](https://tva1.sinaimg.cn/large/006tNbRwgy1g9ti8vz5wmj31gr0u01gz.jpg)

当N很大或者p接近0.5时，二项分布近似为正态分布；N·p>5 and N(1-p)>5是个经验数字。

1. 首先计算p值:  p_hat = 0.1
2. 获得z值: 95%的confidence interval 对应的z值是1.96; 99%的confidence interval 对应的z值是2.58
3. 计算m (margin of error)：m = z*standard error (not standard deviation) 
4. Add m to the point of estimate(p_hat): （p-m, p+m）

**Hypothesis Testing**

**Compare Two samples & Pooled Standard Error** 

与之前one sample, binomial distribution不同，以下是two samples如何计算confidence interval，也是A/B testing中常用的分布，检测两个sample （control and experiment）的mean 是否相同：

![](https://tva1.sinaimg.cn/large/006tNbRwgy1g9ts3h31ruj31eh0oe7kp.jpg)

**practical significance level**

also called Minimum Detectable Effect in some calculators, determined by business.

### Design

**statistical power**

Small sample will lead to a high $\beta$ (fail to reject null hypothesis; type 2 error; false negative)

<img src="https://tva1.sinaimg.cn/large/006tNbRwgy1g9udozcjllj31el0nzdrw.jpg"  />

Large sample:

![](https://tva1.sinaimg.cn/large/006tNbRwgy1g9udoydybbj31ej0okh13.jpg)

**Calculate the size**

Online calculator: https://www.evanmiller.org/ab-testing/sample-size.html

![](https://tva1.sinaimg.cn/large/006tNbRwgy1g9uevmzuqqj31fj0r97vj.jpg)

Increasing CTR to get closer to 0.5 will increase p_hat. To get a same standard error, need to increase N. But when it increases more than 0.5, it is not a monotically increasing.

Increasing pratical significance level: **Larger changes are easier to detect**.

Increasing confidence level: need to be more confident; decrease alpha (type 1 error).

Higher sensitivity: decrease beta (type 2 error); need more data to narrow the distribution.

### Analyze Results

![](https://tva1.sinaimg.cn/large/006tNbRwgy1g9ufyg5j3pj31fc0sx1kx.jpg)

需要给出的值：

1. d_min：practical significance level

2. confidence level

3. N(control)：控制组page view的数量

   X(control) ：控制组click的数量

   N(experiement)：实验组page view的数量

   X(experiement)：实验组click的数量

需要计算的值：

1. 计算p_pool： $p_{pool}=(X_{cont}+X_{exp})/(N_{cont}+N_{exp})$ 

2. 计算SE_pool：$SE_{pool} = \sqrt{(p_{pool}*(1-p_{pool})*(\frac{1}{N_{cont}}+\frac{1}{N_{exp}})}$

3. 计算d_hat: $\hat{d} = p_{exp} - p_{cont}$

   (以上 in compare two samples Part)

4. 计算m (margin of error)：$m = z*SE_{pool}$

5. 计算lower bound and upper bound of confidence interval：$lower bound = \hat{d}-m$, $upper bound = \hat{d}+m$

比较最后的结果：

我们需要关注 **both statistical and practical significance**.

根据lower bound and upper bound of confidence interval, **there is at least 2% change**: lower bound 和 upper bound都大于0.02 (practical siginicance level). 所以选择launch 新功能。

![](https://tva1.sinaimg.cn/large/006tNbRwgy1g9uqiiu69fj31fh0ts7o0.jpg)

- 2nd: neutral: 

  1. no statistical significant change from 0 since the confidence interval include 0.
  2. there is not a practical significant change.

- 3rd:

  1. statistical significant.
  2. but there is not a practical significant change.

- 4th:

  It is not neutral. There is change, but whether it will lead to a better result or a worse one? Need addtional test.

- 5th:

  point estimate >= practical significant level but confidence interval includes 0. So it is potentially positive, also potentially have no effect.

- 6th:

  1. it is possible that there is pratical significant change (point estimate >= practical significant level )

  2. it is also possible that change is not practical significant. (lower bound <= d_min)

- 4，5，6： 

  - need addtional test and greater power.
  - If cannot do addtional tests, then can communicate with decision makers, and they might make decisions with other methods.

