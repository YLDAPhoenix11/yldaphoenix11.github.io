---
title: Policy and Ethics for Experiments
date: 2020-03-22 12:08:00
categories: 
- course notes
- data analytics
tags:
- course notes
- data analytics
- A/B testing

---

_Course note of [A/B testing on Udacity](https://www.udacity.com/course/ab-testing--ud257): Lesson 2_

<!-- more -->

---

# Policy and Ethics for Experiments

## Main principles

### 1. Risk

> *what risk is the participant undertaking*? The main threshold is whether the risk exceeds that of “minimal risk”. Minimal risk is defined as the probability and magnitude of harm that a participant would encounter in normal daily life. The harm considered encompasses physical, psychological and emotional, social, and economic concerns. If the risk exceeds minimal risk, then informed consent is required. 

![](https://tva1.sinaimg.cn/large/006tNbRwgy1g9wyu29ry7j31fh0s4tzv.jpg)

1. adding price information is just adding public information.
2. these information might be incorrect, thus will be harmful.  (And also they may need FDA regulation).
3. Changing the location of the search bar may be the least risky.

### 2. Benefits

> *what benefits might result from the study*? Even if the risk is minimal, how might the results help? (In most online A/B testing, the benefits are around improving the product. In other social sciences/ medicine,it will be different. ) It is important to be able to state what the benefit would be from completing the study.

### 3. Alternatives

> *what other choices do participants have*? For example, if you are testing out changes to a search engine, participants always have the choice to use another search engine. The main issue is that the fewer alternatives that participants have, the more issue that there is around coercion and whether participants really have a choice in whether to participate or not, and how that balances against the risks and benefits.
>
> In online experiments, the issues to consider are what the other alternative services that a user might have, and what the switching costs might be, in terms of time, money, information, etc.

### 4. Data Sensitivity

> *what data is being collected, and what is the expectation of privacy and confidentiality*? This last question is quite nuanced, encompassing numerous questions:
>
> - Do participants understand what data is being collected about them?
> - What harm would befall them should that data be made public?
> - Would they expect that data to be considered private and confidential?

**Difference between pseudonymous and anonymous data**

- **Identified** data means that data is stored and collected with personally identifiable information: names, IDs, Phone number... also device id in many instances.
- **Anonymous** data means that data is stored and collected without any personally identifiable information. This data can be considered **pseudonymous** if it is stored with a randomly generated id such as a cookie that gets assigned on some event, such as the first time that a user goes to an app or website and does not have such an id stored.
- **Anonymized data** is identified or anonymous data that has been looked at and guaranteed in some way that the re-identification risk is low to non-existent,

![](https://tva1.sinaimg.cn/large/006tNbRwgy1g9x0wictdxj31e30rp7wh.jpg)

1. Public data and too granular for identification.
2. Total number of visitors.
3. Timestamps can lead id information and medical data is sensitive.
4. Can also recover personal information, but game data is not sensitive.
5. Too granular for identification
6. Very sensitive.

#### Questions and Consent

**Questions**

1. Are users being informed?
2. What users identisiers are tied to the data?
3. What type of data is being collected? - is these health or financial data be collected?
4. What is the level of confidentiality and security? - Can anyone in the company access the data? Is the data secure with access logged?

**Informed Consent**

- not required when minimal risk and data is not identified.

### Summary of Principles

> Our recommendation is that there should be internal reviews of all proposed studies by experts regarding the questions:
>
> - Are participants facing more than minimal risk?
> - Do participants understand what data is being gathered?
> - Is that data identifiable?
> - How is the data handled?
>
> And if enough flags are raised, that an external review happen.

![](https://tva1.sinaimg.cn/large/006tNbRwgy1g9x9beyh5jj31c80nc1kx.jpg)

1. in most cases, surveys are not sensitive when no personal information is collected. In survey, users can voluteer to choose answer or not, and can also answer dishonestly. However, it is more sensitive when users can only read the articles after doing the survey.
2. minimal risky.
3. presentations may confuse the users. And the data collected is sensitive, which may need to be aggregated.

## Internal process

1. Every employee who might be involved in A/B test be educated about the ethics and the protection of the participants.
2. All data, identified or not, be stored securely, with access limited to those who need it to complete their job. 
3. You create a clear escalation path for how to handle cases where there is even possibly more than minimal risk or data sensitivity issues.

![](https://tva1.sinaimg.cn/large/006tNbRwgy1g9x9gwfw3gj31ft0qbau7.jpg)

- list of experiments: giving the information may skew the results.

![](https://tva1.sinaimg.cn/large/006tNbRwgy1g9x9itaw4mj31eu0roe13.jpg)

- principles to upload is the prerequisites to which questions to consider when evaludating ethics