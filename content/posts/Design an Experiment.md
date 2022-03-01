---
title: Design an Experiment
date: 2020-03-22 15:18:00
categories: 
- course notes
- data analytics
tags:
- course notes
- data analytics
- A/B testing

---

_Course note of [A/B testing on Udacity](https://www.udacity.com/course/ab-testing--ud257): Lesson 4_

<!--more-->

---

#Design an Experiment

## Choose "subject"

### Unit of diversion

**What an individual subject is in the experiment.**

#### Unit of diversion examples:

- **commonly used:**

  - user id

    - stable, unchanging

    - personally identifiable

  - Anonymous id (cookie)

    - changes when switching browser or device
    - users can clear cookies

  - Event

    - no consistent experience
    - use only for non-user-visible changes

- **less common:**

  - Device id
    - only available for **mobile** (so here the device id is just for mobile)
    - tied to specific device
    - unchangeable by user
  - IP address
    - changes when location changes

- **Quiz: **

  When would the user be switched to another group in experiement? (When the unit of diversion will change? ) 

  ![](https://tva1.sinaimg.cn/large/006tNbRwgy1gbh190hlrej31iw0u0npd.jpg)

  User-id: only valid when signing in

  Cookie: do not change if users do not clear cookies through these events, otherwise it would change (so some are "?")

  Event: change among every events

  Device id: only valid for mobile

  IP address: (hard to tell whether it changes in "?" )

##### 1. Consistency of Diversions

- user consistency

- Quiz:

  Choose event when event is enough; choose cookie when event is not good and cookie is enough; choose user-id when event and cookie are not enough for experiment

  ![](https://tva1.sinaimg.cn/large/006tNbRwgy1gbh2h85pm6j31h30u0u0x.jpg)

  Events: for the changes that users will not notice

  Cookie: it iwll be very strange if the button size and color change when user reload the pages.

  User-id: when cross device consistency is important

##### 2. Ethical Considerations for Diversion

1. User-id is identified, so using user-id must be careful.
2. Informed consent

![](https://tva1.sinaimg.cn/large/006tNbRwgy1gbh2ufice0j31lt0u01ky.jpg)

1st: when user log in, they have already submit their email and may have already approved that their data can be collected.

2nd: if emails are collected by cookies, then it will need inform user.

##### 3. variability

empirically/analytically computed varaibility

Sometimes empirically will be higher than analytically because unit of analysis is different from unit of diversion (unit of analysis: the denominator of metrics. For example, pageviews in CTR (clicks/pageviews)) is unit of analysis. If unit of diversion is pageviews, empirically $\approx$ analytically. If unit of diversion is cookie/user-id, varaibility will be higher, so it is better to use empirically given unit of diversion.  - why: when compute analytically, make assumption on distribution of data and indenpendence

![](https://tva1.sinaimg.cn/large/006tNbRwgy1gbhvu15fjaj31hp0u0npd.jpg)In the example above, metric is coverage and unit of analysis is query. If use cookie as unit of diversion, the standard error will be higher than that with query as unit of diversion. 

![](https://tva1.sinaimg.cn/large/006tNbRwgy1gbhvs6dzpsj31jt0u04qq.jpg)

1st: unit of analysis: pageviews; unit of diversion: cookie; unit of analysis (event) is "larger" than unit of diversion(cookie). All pageviews of one cookie will belong to one group.

2nd: unit of analysis: cookie; unit of diversion: pageview; unit of diversion (pageview) is too fine-grained. That is, one cookie may have multiple pageviews. So, 2 pageviews of one cookie may belong to different groups. 

3rd: two units are consistent.

## Choose "population"

### Inter-User experiment vs. Intra-User experiment

Inter-User experiment: A/B testing

Intra-User experiment: show different things to same user in different time

### Target Population

restrict the population by geo, language, browser; Also good for run multiple testing (not overlap) in company; 

In the example below, practical significance d_min is not given. So, we just use statistical significance as 0. 

![](https://tva1.sinaimg.cn/large/006tNbRwgy1gbi6ft0vhyj31kr0u0x6p.jpg)

![](https://tva1.sinaimg.cn/large/006tNbRwgy1gbi6hnsfmaj31e30u01ky.jpg)

For global, must add all data from New Zealand and data from Other. d_hat-m<0, so it is not significant.

The difference between these two results is due to the difference of d_hat. 

### Population vs. Cohort

For population, people may exit the experiment, or maybe their IP address can change in experiment. For cohort based on time, it is just people who enter the experiment as the same time. It is harder to analyze since it lose data. Typically, only use cohort when we need user to be stable and established.

![](https://tva1.sinaimg.cn/large/006tNbRwgy1gbi6x18obuj31mm0qe4oc.jpg)

![](https://tva1.sinaimg.cn/large/006tNbRwgy1gbi6xgkrq0j31ht0u0hdt.jpg)

## Size

**In lesson 1, size based on practical significance, statistical significance and sensitivity.**

Choice of metric/unit of diversion/population will influence variability, and variability will change size. 

![](https://tva1.sinaimg.cn/large/006tNbRwgy1gbj1ibkjyuj31ed0u0hdt.jpg)

![](https://tva1.sinaimg.cn/large/006tNbRwgy1gbj1igwbhtj31hi0u04qp.jpg)

- Quiz:

  ![](https://tva1.sinaimg.cn/large/006tNbRwgy1gbj203v6s1j31kf0u04qq.jpg)1st: Change the unit of diversion to the unit of analysis will decrese the variability (also, SE). 

  2nd: Other traffic will dilute the results and increase the variability.

  3rd: often it doesn't make significant difference. But if there is a difference, varaibility would probably go down because unit of analysis and unit od diversion are same. 

- Targeting the size to specific traffic will cause some problems:

  1. We do not know what results will this traffic lead to. It is hard to predict. 
  2. Hard to detect impact.

  Therefore, run a pilot, turn on the experiemnt for a little to see who's affected, or just use the first day/week to get a better guess.

## Duration

1. what duration?
2. when to run the experiment? 
3. what fraction of traffic are going to use? - given size, less proportion lead to a longer duration.

Why not run on all traffic: safety. press. run on multiple days for weekdays and weekends/ holidays and normal days. run multiple experiments and tasks.

![](https://tva1.sinaimg.cn/large/006tNbRwgy1gbjbbzyzphj31gd0u07wh.jpg)

![](https://tva1.sinaimg.cn/large/006tNbRwgy1gbjbc8dh83j31j40u0u0x.jpg)

Risky: may cause big problem if the result is not good enough.



**Learning effect: **

Some users do not like new changes, while other users are excited to see new changes.

Measure user learning: 

If there is learning effect, there won't be a big change right from beginning but increasing over time.