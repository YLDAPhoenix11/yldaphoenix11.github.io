---
title: Analyzing Results
date: 2020-03-22 15:20:00
categories: 
- course notes
- data analytics
tags:
- course notes
- data analytics
- A/B testing

---

_Course note of [A/B testing on Udacity](https://www.udacity.com/course/ab-testing--ud257): Lesson 5_

<!-- more -->

---

#Analyzing Results

## Sanity checks

**check invariant metrics**

1. population sizing metrics based on unit of diversion: experiment population and control population is comparable
2. other metrics that should not change in experiments

### Choosing Invariants

- Quiz: (choose the invariant metrics, that is, **choose the metrics that would be the same in experiment and control group**)

  ![](https://tva1.sinaimg.cn/large/006tNbRwgy1gbkd9glnxyj31ng0u0qv5.jpg)

  - 1st: user-id is the unit of diversion, so #signed in users are random in experiment group and control groups. For #cookies and #events, they are not directely randomized, but since #signed users are randomized, these two should be split evenly. If they are not split evenly, then there are some users in onne group who are likely to produce cookies or events, and we should figure oput why. For CTR, it is before course list page, so change in course list will not influence it. For time to complete, change in course list to cause the easiest course to the top of the list, which will cause the change of time to complete.

- 2nd: Similarly, #events are unit of diversion and random. Since #signed users and #cookies are "larger" than unit of diversion, they are also invariant. CTR happens before viewing videos and is not affected. For time to complete, **it is impossible to calculate since the unit of diversion is event, and it is possible that one user is both in experiment group and control group**. Even it can measure, the change of load time will also influence the time to complete because longer loading time may distract users, then users will need longer time to complete course. 

- Quiz:

  Change location of sign-in button: control: in course list page, and if user tries to enroll in a course without signing in, they are prompted to sign in; experiment: sign in added to every page, includes homepage.

  ![](https://tva1.sinaimg.cn/large/006tNbRwgy1gbkda3143zj31hw0u0npd.jpg)

  My answer: 1,3,5

  1st: same with the last quiz, these population metrics are invariant

  2nd: "Start now" button is on homepage, so adding sign-in button to homepage will affect it.

  3rd: Users often enroll a course after signing in, so change sign-in rate will influence praobability of enrolling. (I think the probability of enrolling above means #users enrolled/#users signed-in)

  4th: will change

  5th: will not influence video load time

### Checking Invariants

![](https://tva1.sinaimg.cn/large/006tNbRwgy1gbkdmbo1noj31g50u0npd.jpg)

Firstly, calculate total number; Then, if there is any problem, break down to see data on every day.

- **How to figure out whether this difference in within expectation?**

  Since each cookie is randomly assigned to group with probability = 0.5, so **the #cookies in one group follows binomial distribution**.

Since the number of cookies in the example above is greater than 120000, assume it to be a normal distribution.

1. Look at the total number and calculate the confidence interval:

   ![](https://tva1.sinaimg.cn/large/006tNbRwgy1gbke3dyb0fj31ie0u01ky.jpg)

2. Look at the data of each day:

   ![](https://tva1.sinaimg.cn/large/006tNbRwgy1gbke8jqjutj31hw0u0e82.jpg)

3. How to solve:

   ![](https://tva1.sinaimg.cn/large/006tNbRwgy1gbke9s4r2dj31td0u04qp.jpg)

- Quiz:

  ![](https://tva1.sinaimg.cn/large/006tNbRwgy1gbkehnfajdj31ed0rd7wf.jpg)

- What if do not pass sanity check?

  1. check where is the problem: 

     (1)is there something wrong technically? is there anything wrong with infrastructure/experiment setup/ experiement diversion

     (2) retrospective analysis

     (3) check whether there is problem in pre-period(lesson 4 design an experiment) or just in real experiment

  2. most common reasons: data capture, maybe not capture correctly, or change too quick; experiment setup, maybe prolem with filter; infrastructure, etc,

## Single Metrics

In lesson 1, there is a similar example with click-through-probability and in that example we assume binomial; In this example, we measure click-through-rate, which is more like Poisson distribution (in lesson 4). For poisson distribution, it is harder to calculate analytically, so calculate empirically.

![](https://tva1.sinaimg.cn/large/006tNbRwgy1gbkg5hnh0uj31hl0u07wi.jpg)![](https://tva1.sinaimg.cn/large/006tNbRwgy1gbkg5p3tstj31hp0u0x6p.jpg)

Double check with sign test: (what is the probability that result of 7 days are positive?)

![](https://tva1.sinaimg.cn/large/006tNbRwgy1gbkg9teaq5j31hf0u0b2a.jpg)

P-value = 0.0156 < 0.05 ($\alpha$)  (it is two-tail p-value)

- Quiz:

  ![](https://tva1.sinaimg.cn/large/006tNbRwgy1gbkhnmem68j31jc0u0kjm.jpg)

  ![](https://tva1.sinaimg.cn/large/006tNbRwgy1gbkhp67mnzj31ca0nuql3.jpg)

  - calculate:

    ![](https://tva1.sinaimg.cn/large/006tNbRwgy1gbki12fqv4j31mr0u0hdt.jpg)

    ![](https://tva1.sinaimg.cn/large/006tNbRwgy1gbki1vs4exj31d20oo4mj.jpg)

    https://www.graphpad.com/quickcalcs/binomial1/

  - Why it happenes (one is significant while another is not) and how to deal with?

    1. sign test has lower power
    2. Break down to look at each day, we can find that on weekends, they are all positive; In fact, the experiment is much stronger on weekends (confidence interval: weekends: (0.0361, 0.0553), weekdays: (-0.0078, 0.0043) )
    3. Recommend not launch this experiment right now, and figure out why it is much stronger on weekends.

### Gotchas

Other problems can cause difference on sign test and confidence interval:

- Simpson's Paradox

  ![](https://tva1.sinaimg.cn/large/006tNbRwgy1gbki9uo2xxj31vy0kwha2.jpg)

  Why: More women applied to B, which has a lower accpeted rate.

  create some number to show this paradox:

  ![](https://tva1.sinaimg.cn/large/006tNbRwgy1gblcdc7l8nj31b70n9aqv.jpg)

  ![](https://tva1.sinaimg.cn/large/006tNbRwgy1gblcde92knj31b70n9aqv.jpg)

## Multiple Metrics

### Difference between single metrics and multiple metrics:

1. The more metrics, the more likely to see significant chance just by chance.But it shouldn't be repeatale if breaking into days, or slice, or bootstrap. 
2. Techniques "Multiple Comparison": automatic detection of differences

#### Show difference

![](https://tva1.sinaimg.cn/large/006tNbRwgy1gbldugg2i0j31l90u0npd.jpg)

![](https://tva1.sinaimg.cn/large/006tNbRwgy1gbldujx31kj31l90u0npd.jpg)

<img src="https://tva1.sinaimg.cn/large/006tNbRwgy1gbldqyo6uij31990u04cf.jpg"  />

#### How to deal with:

1. use Bonferroni correction, simple but it tends to be conservative

   ![](https://tva1.sinaimg.cn/large/006tNbRwgy1gbldqhuw9bj31ik0u0kjl.jpg)

   ![](https://tva1.sinaimg.cn/large/006tNbRwgy1gbldsymb9vj31hy0u04qq.jpg)

   How to get the z score when $\alpha = 0.0125$?

   This is a z score table (attention to the table entry):

   $\alpha = 0.0125$       $\alpha/2 = 0.00625$

   In the table, it corresponds to z = -2.50 (0.0062)

   ![](https://tva1.sinaimg.cn/large/006tNbRwgy1gbll3ykp2fj30u0167kjl.jpg)

2. Judgment call, family wise error rate, false discovery rate

   ![](https://tva1.sinaimg.cn/large/006tNbRwgy1gbll4muzrej31vq0tbe81.jpg)

   ![](https://tva1.sinaimg.cn/large/006tNbRwgy1gbll6h5o53j31qx0u0npd.jpg)

   

#### how to recommend?

1. Multiple metrics can be unruly
2. Find an overall metric (OEC): understand the problem and goal of company, balance long term and short term

#### draw conclusion

1. **do you understand the change?**
2. do you want to launch the change?
   - Are there statistical significance and practical significance? 
   - Do we understand what the changes done to the user experience? 
   - is it worth it?

## Gotches

1. Ramp-up experiment; Gradually increase the size of experiment (and also remove filters in Google)

2. Effect may faltten out when ramp up the change
3. capture the seasonal effect: holdback: launch change to everyone except a small holdback (a set of users do not get the change)
4. Effect can also faltten out because of a novelty effect or change aversion (users find /adopt to the change or change their adoption to the change): just like measure learning effect, use pre- and post- period, combined with cohort analysis. 

