---
title: Choosing and Characterizing metrics
date: 2020-03-22 14:48:02
categories: 
- course notes
- data analytics
tags:
- course notes
- data analytics
- A/B testing
---

_Course note of [A/B testing on Udacity](https://www.udacity.com/course/ab-testing--ud257): Lesson 3_

<!--more-->

---

# Choosing and Characterizing metrics

- Two types of metrics and their use cases:

  - invariant checking/sanity checking metrics: metrics should not change across the experiment and the control. For example, the number of users in two groups in experiment and do they have the same distribution, like country, age, etc. For sanity checking may use multiple metrics
  - evaludation metrics: high-level business metrics+detail metrics. For evaluation metrics #metrics depends company. For multiple metrics, can create a composed metric - an objective function, or OEC (overall evaluation criteria) to combine metrics.

- Steps:

  1. High-level business metrics:

     metrics that everyone will understand, such as active users, click-through-probability

  2. Figure out details:

     how do you define "active"?

  3. summarize them into a single metric:

     like sum, median, etc

## Define

**Brainstorm and establish metrics, from high-level to practical.**

### Refining the customer funnel

![](https://tva1.sinaimg.cn/large/006tNbRwgy1ga9ea9zqr1j31f40rndyz.jpg)

**Search "Adacity" may not be a good answer since not search is just one type of acquisition; **

**key idea: 1. break apart the original stage & insert before or after original stages 2. follow the business objective.** Since there is helping students get jobs in business objective, it is important to add get jobs in the final stage of tunnel.



![](https://tva1.sinaimg.cn/large/006tNbRwgy1ga9dwkoebbj31c00u0u0x.jpg)

![](https://tva1.sinaimg.cn/large/006tNbRwgy1ga9ehq61njj31c00u01ky.jpg)

Users may not use coaching; Users may also switch between homepage and course list. But it is still a funnel.

Each stage is a metric. Use more rates or probabilty than count since they are better at evaluation, such as the users switching between homepage and course list. It is better to use the convertion rate from homepage visits to course list visits.

### Choose metrics

![](https://tva1.sinaimg.cn/large/006tNbRwgy1ga9dwiwbfnj31c00u0b2a.jpg)

![](https://tva1.sinaimg.cn/large/006tNbRwgy1ga9dwy66lzj31c00u0npe.jpg)

我的答案是3； 1，2； 5

- Update a description on the course list page: aimed at increase the conversion rate from course list to specific course; can also use **continued progression down funnel** as supplement, that is CTR to the course list page, or a drop-off rate of courses (may increase if descriptions are misleding).
- Increase size of "start now" button: can also use probability. But it is better to use rates since **Rates are usually better for measuring the usability of a button**. (If it is hard to find or hard to click, users may click multiple times, and CTR will decrease?)
- Explain benefits of paid service: can also use user retention (How long do users continue paying for coach) or usage metrics (among the users using coaching, do they use more). 

###Difficult metrics

![](https://tva1.sinaimg.cn/large/006tNbRwgy1ga9dwpbpndj31c00u0x6p.jpg)

我的答案：2，3.

Rate of returning for 2nd course is also difficult because it will take too long to meature the metric (it will take a long time for users to return for 2nd course).

Note that difficult metrics are metrics **take too long **and **do not have data**.

#### Techniques for solving difficult metrics

1. external data

   (1) companys that collect data, like NIelsen; 

   (2) companys run surveys of users; 

   (3) academic research, like eye tracking. 

   Use for

   (1)brainstorming (think of new metrics), 

   (2) validation metrics, develop validation techiniques. 

2. use our own data: 

   (1) use all our existing data: 

   - retrospective analysis/observational analysis, can combined with surveys&focus groups&etc, shows correlation not causation ; 

   - running experiement: run an experiment to validate whether or not we can use a metrics for evaluating experiements, measure that metric is actually going to move as we make changes: for example, use time that student takes to complete the quiz as metrics to measure students' undertanding of the material, we need to try *different quizs/on different formulation*, and test which one move the proposed metric 

   (2) gather new data: user experience research, survey, focus groups, etc

   more robust to combine these methods. 

   ![](https://tva1.sinaimg.cn/large/006tNbRwgy1gaboqpzo1uj31c00u0x6p.jpg)

   **Pdf on website**

   UER: can use special equipment, like eye tracking; need to validate results, such as retrospective analysis to see how  it varies over time or experiments to see how it varies when make changes

   Surveys: users do not need to tell truth

- **Example of applying other techniques**: 

  ![](https://tva1.sinaimg.cn/large/006tNbRwgy1gabor8bqbjj31c00u04qq.jpg)

  ![](https://tva1.sinaimg.cn/large/006tNbRwgy1gaborn2c77j31c00u0kjl.jpg)

  - Rate of returning for 2nd course: if can find some metrics predictable, can use it as proxy in experiments, like the proxies in 3rd metrics.
  - Probability of finding information via search: Can use proxies, and validate them with External data; Human evaludation is pay human raters to evaluate the site.

- Quiz

  ![](https://tva1.sinaimg.cn/large/006tNbRwgy1gabos5rmhij31ga0u0b29.jpg)

  我的答案：4， 6； 1，6 ；2， 5

  - measure user engagement: use UER and observed how engaged users are; retrospective analysis of users who have completed the courses and see what they have in common.

  - Decide whether to excend inventory in shopping site: add new proeducts will be an expensive investment; user focus groups to get ideas from users about what they want 

  - which ads get most views: do retrospective analysis: assume that click is correlated with view, or see the lowest position where anyone has clicked and assume that they have viewed all before

## Build Intuition

**Build intuition and understand sensitivity and robustness.**

Turning a high-level metric into a well-defined metric:

- fully define exactly what data are going to look at to define the metrics: numerator/denominator/filter/ways to compute a metric

  Many nuances, for example, in CTR, use cookie or just click?  a user view in 11:55pm and click on 12:01am, is he/she users in first day or last day? Or a user view the page but click 2 hours later, do we count it as once?

  Consider the technology, JS ping back is different in IE and Safiri, so also need to work with engineering team to **understand nuances and get accurate data**.

- summarize metric

### Example of Define a metric

![](https://tva1.sinaimg.cn/large/006tNbRwgy1gaboswrajyj31c00u0kjl.jpg)

When using different time interval, get different value. 

In this example, user click, then reload  but do not click (5 minutes later). After 30 seconds, click. After 12 hours, reload but not click.

If per minute, orange rectangles show the groups; first and second groups have click, last one does not. 

If per hour, purple lines show the groups; first has click, last one does not.

If per day, all events belongs to one group. CTR = 1

![](https://tva1.sinaimg.cn/large/006tNbRwgy1gaboub05kxj31c00u0npd.jpg)

Definition2 (use page views instead of cookie) is easier to implement than definition1. To implement definition2, give each pageview a unique id. If user refresh page, it will generate a new page view but the cookie will remains same. So the CTR will be different. 

![](https://tva1.sinaimg.cn/large/006tNbRwgy1gabovjy851j31c00u0b29.jpg)

![](https://tva1.sinaimg.cn/large/006tNbRwgy1gabowl9f50j31kc0tex1r.jpg)

Double click: cookie and page view prob will count as single click.

Back button caches page: It will generate a new page view. cookie prob will count 1 page view while the other two will count 2 page views. 

Click-tracking bug: If two clicks are recorded instead of one, similar with double-click. If click is missing, all will be influenced.

### Filtering and Segmenting

- Filter: filter the traffic, aimed at **de-bias data or dull-bias data**

  external reasons: spam, fraud, etc; 

  internal reasons: test what if if only change on subset of traffic and increase the power and sensitivity of experiment. For example, only test on English traffic. 

  **Do not introduce bias when filtering**. For example, filter long session which may because of the website, or filter on user id where there are users without accounts. To test whether it introduce bias, slice the data (by country, etc) and complete metrics on all of these slices,  or look at week over week or day over day data. **Most important: Build intuition and know what changes are expected and what are not.**

#### Examples:

- week over week/ year over year

  ![](https://tva1.sinaimg.cn/large/006tNbRwgy1gabp02j4q3j31fx0u0kjl.jpg)

  week over week: # in Mon of this week/# in Mon of last week (here the spike shows that it is not due to week variation)

  year over year: # in day of this year/# in day of last year (the weekday may not correspond in two years, so if there is weekend effect, it will not be smooth)

- slice data: 

  ![](https://tva1.sinaimg.cn/large/006tNbRwgy1gabp0bik0fj31c00u0x6p.jpg)

- Quiz:![](https://tva1.sinaimg.cn/large/006tNbRwgy1gabp0z8ymwj31c00u0hdu.jpg)

  By platform: mobile or web

  我的答案：3，4，6

  CTR and CTP over time cannot tell whether there is a problem alone. 

  Both rate and probability on same graph: In general, rates are higher than probability. **So it is expected that rates are higher than probabilities. And it is hard to know how much higher would the rates be.**

  CTR by platforms: Users' behavior may be different on different platform.  It is hard to tell whether it is because of JS bug or just user behavior.

### Summary Metrics

![](https://tva1.sinaimg.cn/large/006tNbRwgy1gatu29qpsaj31c00u01ky.jpg)

#### sensititvity and robustness

- Mean: sensitive; median: robust

- how to measure sensitivity and robustness?

  1. running experiements or using experiments already have: whether the metrics respond to the changes

     use a vs. a experiment to determine whether metrics are too sensitive: do not change anything 

  2. retrospective analysis

- Example of retrospective analysis:

  plot histogram: (**The distributions are similar so these videos are comparable**)

  ![](https://tva1.sinaimg.cn/large/006tNbRwgy1gavwn64wepj31jx0u07wh.jpg)

  compare different metrics: (**Must make sure these 5 videos are comparable**)

  ![](https://tva1.sinaimg.cn/large/006tNbRwgy1gavwnehnqwj31mv0u04qp.jpg)

  90th and 99th percentile changes among different videos

- Example of experiment:

  Histogram:

  ![](https://tva1.sinaimg.cn/large/006tNbRwgy1gavwnu915vj31k10u07wh.jpg)

  Video 1 have the highest resolution and highest load time.

  ![](https://tva1.sinaimg.cn/large/006tNbRwgy1gbgr5as2nqj31lx0u07wh.jpg)

  Median and 80th percentile do not change among different videos.

## Characterize

**How to characterize the varaibility of the metrics.**

### variability

- Absolute difference vs. relative difference

#### calculating variability

![](https://tva1.sinaimg.cn/large/006tNbRwgy1gatwcprdj5j31c00u0hdt.jpg)

- Quiz: calculating variablity analytically (with distribution)

  ![](https://tva1.sinaimg.cn/large/006tNbRwgy1gavwtq7povj31fp0sah7c.jpg)

- calculating  variability empirically:

  - calculate with non-parametric: [sign test]([https://baike.baidu.com/item/%E7%AC%A6%E5%8F%B7%E6%A3%80%E9%AA%8C](https://baike.baidu.com/item/符号检验)) 

  - A vs A experiment: run many a/a experiment with large enough samples, or run a big a/a experiment and **bootstrap**

    in reality: analytical (with simple metrics) → bootstrap (when metrics become complicated) → are they consistent? (if not, many a/a experiments)

- Examples:

  ![](https://tva1.sinaimg.cn/large/006tNbRwgy1gavyfmn48vj31wc0rv7wh.jpg)

  1. ![](https://tva1.sinaimg.cn/large/006tNbRwgy1gaw4f70l4jj31dw0qttes.jpg)

     May plot the results of different experiments and  compare them with assumption distribution.

  2. ![](https://tva1.sinaimg.cn/large/006tNbRwgy1gaw4ax5rkqj31qo0u0b29.jpg)

     need to make an assumption of metrics, for example, metrics are normally distribution

     how to calculate SD (calculate the SD of difference between groups):![](https://tva1.sinaimg.cn/large/006tNbRwgy1gaw4e6nj0hj31920u0e81.jpg)

  3. ![](https://tva1.sinaimg.cn/large/006tNbRwgy1gaw4jqxlgbj31c00u0npd.jpg)

     discard 2.5% of values of each side, then the range of the remaining data will give 95% confidence interval.

     lower bound and higher bound of the range is just the confidence interval, **do not need to add average**.

- Quiz:

  Data:

  https://docs.google.com/spreadsheets/d/1IFtnCTjMw023ixJIm7QvqAQ1M5peQnchyegYs1iVfyw/edit#gid=0

  ![](https://tva1.sinaimg.cn/large/006tNbRwgy1gaw65cngu9j31p40u04qp.jpg)

## Summary

- use a lot of time validating metrics
- define metrics; consider a lot of things
- Sensitivity and robustness
- Variability: always start with a basic analytical estimated variability
- Necassary: sanity checking
- how these metrics perform in practice: anything not taken into consideration and influence the metrics; peoples' behaviors may shift through time or after some change