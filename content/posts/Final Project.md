---
title: Final Project
date: 2020-03-22 15:23:00
categories: 
- course notes
- data analytics
tags:
- course notes
- data analytics
- A/B testing

---

_Course note of [A/B testing on Udacity](https://www.udacity.com/course/ab-testing--ud257): Lesson 6_

<!-- more -->

---

# Final Project

## 0. Instruction

Instruction: https://docs.google.com/document/u/1/d/1aCquhIqsUApgsxQ8-SQBAigFDcfWVVohLEXcV6jWbdI/pub?embedded=True

### Experiment Overview: Free Trial Screener

At the time of this experiment, Udacity courses currently have two options on the course overview page: "start free trial", and "access course materials". If the student clicks "start free trial", they will be asked to enter their credit card information, and then they will be enrolled in a free trial for the paid version of the course. After 14 days, they will automatically be charged unless they cancel first. If the student clicks "access course materials", they will be able to view the videos and take the quizzes for free, but they will not receive coaching support or a verified certificate, and they will not submit their final project for feedback.

In the experiment, Udacity tested a change where if the student clicked "start free trial", they were asked how much time they had available to devote to the course. If the student indicated 5 or more hours per week, they would be taken through the checkout process as usual. If they indicated fewer than 5 hours per week, a message would appear indicating that Udacity courses usually require a greater time commitment for successful completion, and suggesting that the student might like to access the course materials for free. At this point, the student would have the option to continue enrolling in the free trial, or access the course materials for free instead. [This screenshot](https://www.google.com/url?q=https://drive.google.com/a/knowlabs.com/file/d/0ByAfiG8HpNUMakVrS0s4cGN2TjQ/view?usp%3Dsharing&sa=D&ust=1580895798643000) shows what the experiment looks like.

![](https://tva1.sinaimg.cn/large/006tNbRwgy1gbmspyrf9zj30wp0ixwkd.jpg)

The hypothesis was that this might set clearer expectations for students upfront, thus reducing the number of frustrated students who left the free trial because they didn't have enough time—without significantly reducing the number of students to continue past the free trial and eventually complete the course. If this hypothesis held true, Udacity could improve the overall student experience and improve coaches' capacity to support students who are likely to complete the course.

The unit of diversion is a cookie, although if the student enrolls in the free trial, they are tracked by user-id from that point forward. The same user-id cannot enroll in the free trial twice. For users that do not enroll, their user-id is not tracked in the experiment, even if they were signed in when they visited the course overview page.

## 1. Experiment Design

### 1.1 Metric Choice

**List which metrics you will use as invariant metrics and evaluation metrics here.** For each metric, explain both why you did or did not use it as an invariant metric and why you did or did not use it as an evaluation metric. Also, state what results you will look for in your evaluation metrics in order to launch the experiment. (These should be the same metrics you chose in the "Choosing Invariant Metrics" and "Choosing Evaluation Metrics" quizzes.)

The practical significance boundary for each metric, that is, the difference that would have to be observed before that was a meaningful change for the business, is given in parentheses. All practical significance boundaries are given as absolute changes. Any place "unique cookies" are mentioned, the uniqueness is determined by day. (That is, the same cookie visiting on different days would be counted twice.) User-ids are automatically unique since the site does not allow the same user-id to enroll twice.

- **Number of cookies:** That is, number of unique cookies to view the course overview page. (dmin=3000)
- **Number of user-ids:** That is, number of users who enroll in the free trial. (dmin=50)
- **Number of clicks:** That is, number of unique cookies to click the "Start free trial" button (which happens before the free trial screener is trigger). (dmin=240)
- **Click-through-probability:** That is, number of unique cookies to click the "Start free trial" button divided by number of unique cookies to view the course overview page. (dmin=0.01)
- **Gross conversion:** That is, number of user-ids to complete checkout and enroll in the free trial divided by number of unique cookies to click the "Start free trial" button. (dmin= 0.01)
- **Retention:** That is, number of user-ids to remain enrolled past the 14-day boundary (and thus make at least one payment) divided by number of user-ids to complete checkout. (dmin=0.01)
- **Net conversion:** That is, number of user-ids to remain enrolled past the 14-day boundary (and thus make at least one payment) divided by the number of unique cookies to click the "Start free trial" button. (dmin= 0.0075)

You should also decide now what results you will be looking for in order to launch the experiment. Would a change in any one of your evaluation metrics be sufficient? Would you want to see multiple metrics all move or not move at the same time in order to launch? This decision will inform your choices while designing the experiment.



1. <u>Firstly, draw the funnel to get the better understanding</u>

![](https://tva1.sinaimg.cn/large/0082zybpgy1gbnzbxi7etj30k00b9wf0.jpg)

2. <u>Choose invariant metrics</u>

   number of cookies, number of clicks and click-through-probabilty are invariant metrics. They happends before the scrinner is trigger. And #cookies is also the unit of diversion.

   Besides, *without significantly reducing the number of students to continue past the free trial and eventually complete the course* is in hypothesis. Therefore, Net conversion (I think it indicates whether the #user-ids remaining enrolled past the 14-day bounday has changed or not to come extent) is in evaluation metric instead of invariant metrics. Since it is after change of the screener and we are not certain that #user-ids remaining enrolled will not change.

3. <u>Choose evalution metrics</u>

   Metrics must be enough, relevant and accessible to evaluate the experiment. When choosing metrics, we need to **understand the hypothesis**.

   Hypothesis: *The hypothesis was that this might set clearer expectations for students upfront, thus reducing the number of frustrated students who left the free trial because they didn't have enough time—without significantly reducing the number of students to continue past the free trial and eventually complete the course.*

   本题有多个答案：

   1. Gross conversion + Rentention + Net conversion
   2. Rentention + Net conversion
   3. Gross conversion + Net conversion

   解释：

   1. I think Rentention is the most important, since it indicates the fraction of frustrated students who left the free trial. Rentention should increase. Gross conversion will also change. And net conversion can be calculated with the other two (Net conversion = rentention * gross conversion). 

      If the hypothesis is true, it must satisfied:

      - Rentention increases: *educing the number of frustrated students*
      - Gross conversion decreases: *set clearer expectations for students*
      - Net conversion does not change: *without significantly reducing the number of students to continue past the free trial* (to some extent, since **it will take too long to measure #user-ids to complete courses**) 

   2. 为什么没有#user-ids: #user-ids will be different in control and experiment groups if hypothesis is true. In (reference)[https://github.com/shubhamlal11/Udacity-AB-Testing-Final-Project], the author does not choose it because it is not normaled.  ANother reason might be that this metric just show a change of number, but does not indicate a change of rate; Compared with other metrics, it is less relevant. I chose it incorrectly. 

   3. Finally, I chose three metrics as evaluation metrics: Gross conversion, Rentention, Net conversion.

### 1.2 Measuring Variability

[This spreadsheet](https://www.google.com/url?q=https://docs.google.com/a/knowlabs.com/spreadsheets/d/1MYNUtC47Pg8hdoCjOXaHqF-thheGpUshrFA21BAJnNc/edit%23gid%3D0&sa=D&ust=1580895798646000) contains rough estimates of the baseline values for these metrics (again, these numbers have been changed from Udacity's true numbers).

![](https://tva1.sinaimg.cn/large/0082zybpgy1gbnzbuj64dj30my087q6k.jpg)

**List the standard deviation of each of your evaluation metrics. **For each metric you selected as an evaluation metric, estimate its standard deviation analytically, given a sample size of 5000 cookies visiting the course view page. Do you expect the analytic estimates to be accurate? That is, for which metrics, if any, would you want to collect an empirical estimate of the variability if you had time? (These should be the answers from the "Calculating standard deviation" quiz.)

4. <u>Figure out the distribution of metrics</u>

   Gross onversion, Rentention and Net conversion are all probability, so they are all binomial distribution. Considering the number of cookies/ clicks/ enroll, these binomial distribution can be approximated as normal distribution. (See Choosing and Characterizing metrics).

5. <u>Calculate the standard deviation analytically</u>

   unit of diversion : cookie

   **Attention: the unit of analysis and the unit in the sample size (that is, cookie visiting the course view page)**

   When approximate as normal, $SD = \sqrt{\frac{p*(1-p)}{N}}$ 

   Gross conversion (**based on click**): N = 5000*0.08 = 400, p = 0.20625, SD = 0.0202

   Rentention (**based on enroll**): N = 5000*(660/40000) = 82.5 , p = 0.53, SD = 0.0549

   Net conversion (**based on click**): N = 5000*0.08 = 400, p = 0.1093125, SD = 0.0156

   If unit of analysis and unit of diversion is different, then empirical and analytical will be different. So empirical variation and analytical variation of rentention might be different (unit of analysis of rentention: user-id). 

### 1.3 Sizing

#### 1.3.1 Choosing Number of Samples given Power

**Indicate whether you will use the Bonferroni correction during your analysis phase, and give the number of pageviews you will need to power you experiment appropriately. **Using the analytic estimates of variance, how many pageviews **total** (across both groups) would you need to collect to adequately power the experiment? Use an alpha of 0.05 and a beta of 0.2. Make sure you have enough power for **each** metric. (These should be the answers from the "Calculating Number of Pageviews" quiz.)

6. <u>Calculate size of A/B testing</u>

   Attetion: 

   1. When using calculator get the sample size, we need to **look at the unit of sample size in calculator and convert it to corresponded to the unit we need.** It is usually a more high-level unit. (In this example, it is the course overview pageviews.) **最好的方法是计算的时候就带上单位。**
   2. Using this online (calculator)[https://www.evanmiller.org/ab-testing/sample-size.html], it gives sample size of on group, but we need **two groups.**
   3. For **multiple metrics**, calculate the size respectively then choose the maximum one. Also, for multiple metrics, we need to look at Bonferroni correction.

   When I use $ \alpha = 2\% $ (Bonferroni correction, the calculator does not have $\alpha = 0.0167$),  $\beta = 80\%$ in the calculator above:

   - Gross conversion: 

     sample size in calculator: **33014 clicks per gruoup**; 

     pageviews: $33014/0.08*2$ = 825350 pageviews

   - Rentention: 

     sample size in calculator: **50013 enrollment per group**; 

     pageviews: $50013/\frac{660}{40000}*2$ = 6062182 pageviews​

   - Net conversion: 

     sample size in calculator: **35016 clicks per group**; 

     pageviews: $35016/0.08*2$ = 875400 pageviews

   Max: 6062182 pageviews

#### 1.3.2 Choosing Duration vs. Exposure

**Indicate what fraction of traffic you would divert to this experiment and, given this, how many days you would need to run the experiment.** What percentage of Udacity's traffic would you divert to this experiment (assuming there were no other experiments you wanted to run simultaneously)? Is the change risky enough that you wouldn't want to run on all traffic? Given the percentage you chose, how long would the experiment take to run, using the analytic estimates of variance? If the answer is longer than a few weeks, then this is unreasonably long, and you should reconsider an earlier decision. (These should be the answers from the "Choosing Duration and Exposure" quiz.)

7. <u>choose duration and exposure</u>

   According to the Baseline Value, Unique cookies to view course overview page per day is 40000. If we need 6062182 pageviews and all traffic, it will take 151 days. It is too long.

   Look at the pageviews needed by each metrics, evaluating on Rentention will take much more pageviews than the other two. In the Choose Evaluation Metrics part, it is also okay to choose "Gross conversion + Net conversion", since 

   1. If gross conversion decreases and net conversion remains unchanged (or increases), it can be infered that rentention increases. 
   2. To some extent, gross conversion itself can also indicates that whether the change set a clearer expectation for students. 

   (Similarly, rentention + net conversion is also okay.)

   **Attention: When using Bonferroni correction, change #metrics will change $\alpha$.**

   If using these two metrics, we will need 791500 pageviews; if we use all traffic, it will take about 20 days.

   if using these two metrics and without Bonferroni correction, we will need 685325 pageviews; If using all traffic, it will take about 18 days; If using 50% of the traffic, it will take about 35 days.

   All these three settings are okay. Since these experiment is not high-risky (not decrease #users remaining enrolled), it is okay to use all traffic. 

## 2. Experiment Analysis

The data for you to analyze is [here](https://www.google.com/url?q=https://docs.google.com/a/knowlabs.com/spreadsheets/d/1Mu5u9GrybDdska-ljPXyBjTpdZIUev_6i7t4LRDfXM8/edit%23gid%3D0&sa=D&ust=1580895798648000). This data contains the raw information needed to compute the above metrics, broken down day by day. Note that there are two sheets within the spreadsheet - one for the experiment group, and one for the control group.

![](https://tva1.sinaimg.cn/large/0082zybpgy1gbnzbs3rf6j30qr0cu44f.jpg)

The meaning of each column is:

- **Pageviews:** Number of unique cookies to view the course overview page that day.
- **Clicks:** Number of unique cookies to click the course overview page that day. (I think this should be click on "start free trial")
- **Enrollments:** Number of user-ids to enroll in the free trial that day.
- **Payments:** Number of user-ids who who enrolled on that day to remain enrolled for 14 days and thus make a payment. (Note that the date for this column is the start date, that is, the date of enrollment, rather than the date of the payment. The payment happened 14 days later. Because of this, the enrollments and payments are tracked for 14 fewer days than the other columns.)

### 2.1 Sanity Checks

**For each of your invariant metrics, give the 95% confidence interval for the value you expect to observe, the actual observed value, and whether the metric passes your sanity check.** 

Start by checking whether your invariant metrics are equivalent between the two groups. If the invariant metric is a simple count that should be randomly split between the 2 groups, you can use a binomial test as demonstrated in Lesson 5. Otherwise, you will need to construct a confidence interval for a difference in proportions using a similar strategy as in Lesson 1, then check whether the difference between group values falls within that confidence level.  (These should be the answers from the "Sanity Checks" quiz.)

If your sanity checks fail, look at the day by day data and see if you can offer any insight into what is causing the problem.

8. <u>Figure out the distribution of metrics</u>

   - **#cookies & #clicks**: binomial distribution with p = 0.5, either assigned in control group or experiment group. 
   - **click-through-probability (CTP): **binomial probability with p = Mean ($CTR_{control}$), N = $N_{exp}$ (If this metric is not influenced by experiment, then observed value = expected value; the probability is the expected value, and there are $N_{exp}$ trials.)

9. <u>Calculate the confidence interval and the observed value</u>

   - **#cookies & #clicks**:

     expected value = 0.5

     observed value = $\frac{N_c}{N_c+N_e}$      

     m = $1.96*SD= \sqrt{\frac{0.5*0.5}{N_{c}+N_{e}}}*1.96$

     confidence interval: (expected value - m,expected value + m)

      ($N_C$: numbers (such as #clicks, #cookies) in control group, $N_e$: numbers in experiment group)

   - **click-through-probability (CTP)**

     expected value = Mean ($CTR_{control}$)

     observed value = Mean ($CTR_{experiment}$)

     m = $1.96*SD= \sqrt{\frac{expected*(1-expected)}{N_{e}}}*1.96$

     confidence interval: (expected value - m,expected value + m)

      ($N$: based on cookies of course overview page)

### 2.2 Result Analysis

#### 2.2.1 Check for Practical and Statistical Significance

**For each of your evaluation metrics, give a 95% confidence interval around the difference between the experiment and control groups. Indicate whether each metric is statistically and practically significant.** A metric is statistically significant if the confidence interval does not include 0 (that is, you can be confident there was a change), and it is practically significant if the confidence interval does not include the practical significance boundary (that is, you can be confident there is a change that matters to the business.) 

If you have chosen multiple evaluation metrics, you will need to decide whether to use the Bonferroni correction. When deciding, keep in mind the results you are looking for in order to launch the experiment. Will the fact that you have multiple metrics make those results more likely to occur by chance than the alpha level of 0.05? (These should be the answers from the "Effect Size Tests" quiz.) 

10. <u>Calculate metrics and p_pool​</u>

    Now, this part is based on t-test (two samples).

    1. calculate the gross conversion and net conversion of control and experiment
    2. calculate their difference of experiment and control

    **Attention:**

    1. **Do not use the average of gross/net conversion every day to get the gross/net conversion of control/experiment group**

       **$GrossConversion_{con} = \sum{Enroll_{con}/\sum{Click_{con}}}$**

       **instead of** 

       **$GrossConversion_{con} = mean(GrossConversion^{daily}_{con})$**

       直接使用总体，不要使用每日平均

    2. **Gross/net conversion is based on first 23 days, not all days; do not include the last 14 days**

       $\sum{Click}$: do not include the click in last 14 days, since $\sum{Enroll/Payment}$ do not include the last 14 days.

11. <u>Calculate confidence interval and compare it with practical and statistical significance</u>

    Use the method in "Lesson 1: AB testing".

    1. $diff = p_{exp}-p_{con}$
    2. $p_{pool}=(X_{cont}+X_{exp})/(N_{cont}+N_{exp})$ 
    3. $SE_{pool} = \sqrt{(p_{pool}*(1-p_{pool})*(\frac{1}{N_{cont}}+\frac{1}{N_{exp}})}$
    4. $m = z*SE_{pool}$
    5. $lower bound = diff-m$, $upper bound = diff+m$

    **Attention:**

    **I do not use the method in "Lesson 5: Analyzing the Result", because I do not know the empirical SE, which need to be calculated by A/A tests. On the other hand, the metric is a probability soI can assume it as binomial distribution and calculate p_pool and SE_pool by appximating it as normal distribution.**

    Since I use Bonferroni correction, z = 2.24

    - For Gross conversion:

      $GrossConversion_{con} = \sum{Enroll_{con}/\sum{Click_{con}}}=0.2189$

      $GrossConversion_{exp} = \sum{Enroll_{exp}/\sum{Click_{exp}}}=0.1983$

      $GrossConversion_{diff} = GrossConversion_{exp}-GrossConversion_{con}=-0.0206$

      $GrossConversion_{pool} =  \frac{\sum{Enroll_{con}}+\sum{Enroll_{exp}}}{\sum{Click_{con}}+\sum{click_{exp}}} = 0.2086$

      $GrossConversion_{SE} = \sqrt{(GrossConversion_{pool}*(1-GrossConversion_{pool})*(\frac{1}{Click_{con}}+\frac{1}{Click_{exp}})} =0.0044$

      $GrossConversion_{m} = z*GrossConversion_{SE} = 0.0098$

      $GrossConversion_{lowerbound} = GrossConversion_{diff}-GrossConversion_{m} = -0.0303$

      $GrossConversion_{upperbound} = GrossConversion_{diff}+GrossConversion_{m}= -0.0108$

      It is both statistical significant and practical significant.

    - For Net conversion:

      $NetConversion_{con} = \sum{Payment_{con}/\sum{Click_{con}}}=0.1176$

      $NetConversion_{exp} = \sum{Payment_{exp}/\sum{Click_{exp}}}=0.1127$

      $NetConversion_{diff} = NetConversion_{exp}-NetConversion_{con}=-0.0049$

      $NetConversion_{pool} =  \frac{\sum{Payment_{con}}+\sum{Payment_{exp}}}{\sum{Click_{con}}+\sum{click_{exp}}} = 0.1151$

      $NetConversion_{SE} = \sqrt{(NetConversion_{pool}*(1-NetConversion_{pool})*(\frac{1}{Click_{con}}+\frac{1}{Click_{exp}})} =0.0034$

      $NetConversion_{m} = z*NetConversion_{SE} = 0.0077$

      $NetConversion_{lowerbound} = NetConversion_{diff}-NetConversion_{m} = -0.0126$

      $NetConversion_{upperbound} = NetConversion_{diff}+NetConversion_{m}= 0.0028$

      It is neither statistical significant nor practical significant.

#### 2.2.2 Run Sign Tests

**For each of your evaluation metrics, do a sign test using the day-by-day data, and report the p-value of the sign test and whether the result is statistically significant.**  For each evaluation metric, do a sign test using the day-by-day breakdown. If the sign test does not agree with the confidence interval for the difference, see if you can figure out why. (These should be the answers from the "Sign Tests" quiz.)

12. <u>Calculate the sign tests</u>

    onlinne calculator: https://www.graphpad.com/quickcalcs/binomial1/, p = 0.5

    For gross connversion: 23 trials, 4 success (For daily gross conversion, exp>con 4 times), p-value = 0.0026, statistical significant

    For net conversion: 23 trials, 10 success  (For daily net convzersion, exp>con 10 times), p-value =0.6776, not statistical significant

### 2.3 Make a Recommendation

Finally, make a recommendation. Would you launch this experiment, not launch it, dig deeper, run a follow-up experiment, or is it a judgment call? If you would dig deeper, explain what area you would investigate. If you would run follow-up experiments, briefIy describe that experiment. If it is a judgment call, explain what factors would be relevant to the decision.

13. <u>make a recommendation</u>

    The result analysis suggests that the screener will decrease the gross conversion, but do not significantly decrease the net conversion. However, considering that the lower bound of net conversion's confidence interval is -0.0126, whose value is higher than dmin = 0.075. Thus, there is possibility that the change will lead to a decrease of net conversion. Therefore, I will not launch this experiment now, but break down to every day and slice to find the reason of the change of net conversion. Besides, I also tend to continue this experiment for several days to collect more data.

## 3. Follow-Up Experiment: How to Reduce Early Cancellations

If you wanted to reduce the number of frustrated students who cancel early in the course, what experiment would you try? Give a brief description of the change you would make, what your hypothesis would be about the effect of the change, what metrics you would want to measure, and what unit of diversion you would use. Include an explanation of each of your choices.

14. <u>Follow-up experiment</u>

    (I do not think the meaning of the question is clear. I assume that the cancellation means the cancellations in the first 14-days, after enrollment.)

    Based on the experiment above, I would also try to measure whether the usre can handle this course or not by letting he/she take quizes about pre-requisite knowledge. After he/she pass the screener in the experiment above, there would be a quiz about pre-requisite kowledge; If completing this course does not need any prerequisite knowledge, there will not be this quiz. If he/she cannot pass the quiz, the system show a message to suggest him/her to take a lower level courses, or access the course materials for free . Otherwise, the user can enroll in the course and complete checkout. 

    The hypothesis will be similar to the hypothesis in the experiment above. 





Reference:

https://github.com/shubhamlal11/Udacity-AB-Testing-Final-Project

https://github.com/winkelman/udacity-dand-ab-test