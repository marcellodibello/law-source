---
title: Algorithms in Criminal Justice
author: ''
date: '2020-01-06'
slug: algorithms-criminal-justice
categories: []
tags: []
subtitle: ''
summary: ''
authors: []
lastmod: '2020-01-06T23:56:42-05:00'
featured: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
---

Algorithms are increasingly used in the criminal justice system to streamline decisions in policing, pre-trial risk assessment and sentencing. Individuals are assigned risk scores that are intended to track their probability of committing future crimes. The highere the score, the higher the probability of committing a crime. 

Risk scores are based on factors or predictors that correlate more or less strongly with crime, say prior arrests, prior convictions, failure to appear in court, etc. To identify the relevant predictors, different statistical and machine learning methods, such as [logistic regression](https://machinelearningmastery.com/logistic-regression-for-machine-learning/), 
are applied to historical data. 

Algorithms have taken the criminal justice system by storm. They are going to stay and become even more persivase, another manifestation of the power of Big Data. Algorithms promise to be more efficient, objective and less biased, but they may also exacerbate racial inequities and biases in society. Protected attributes, race or gender, are typically not part of the set of predictors, but if the training data are biased, algorithmic predictions will also be biased unless proper correctives are in place. Garbage in, garbage out.  I will not, however, discuss [this problem](https://www.technologyreview.com/s/612775/algorithms-criminal-justice-ai/) here. 

Even assuming that the training data are unbiased, other problems persist, often discussed under the heading of *algorithmic fairness*. There is a growing literature in computer science on the topic. Definitions of fairness [proliferate](https://www.youtube.com/watch?v=jIXIuYdnyyk), but a unified analytical framework is currently lacking. I will discussu some of the proposals for theorizing about algorithmic fairness. Before I do that, though, I will review some examples of algorithms used in criminal justice. 

## Predictive policing: SSL, SAID, HunchLab, PredPol, etc.

The Chigaco Police Department, following a [surge](https://www.nytimes.com/2013/06/11/us/chicago-homicides-fall-by-34-percent-so-far-this-year.html) in street violence  in 2013, adopted the **Strategic Subject List** or **SSL**. This is an algorithm that calculates risk scores for individuals who had interactions with the police and were in its database. The risk scores are intended to reflect someone's probability of being involved in a shooting incident either as a victim or an offender. The attributes used to calculate the risk scores are (see [data](https://data.cityofchicago.org/Public-Safety/Strategic-Subject-List-Dashboard/wgnt-sjgb) in the [Chicago Data Portal](https://data.cityofchicago.org/)): 
- times being the victim of a shooting incident
- age during the latest arrest
- times being the victim of aggravated battery or assault
- prior arrests for violent offenses 
- gang affiliation 
- prior narcotic arrests 
- trend in involvement in crime incidents 
- prior unlawful use of weapon arrests. 

Jessica Saunder and others in 2016 run an experimental analsys and [concluded](https://link.springer.com/article/10.1007/s11292-016-9272-0) 
that "[i]ndividuals on the SSL are not more or less likely to become a victim of 
a homicide or shooting than the comparison group" although "[t]he treated 
group is more likely to be arrested for a shooting."  

In 2019, SSL was [replaced](http://directives.chicagopolice.org/directives/data/a7a57b85-155e9f4b-50c15-5e9f-7742e3ac8b0ab2d3.html) 
by SAID (Subject Assessment and Information Dashboard). This tool relies, among other things, on information provided by [CVRM](https://home.chicagopolice.org/wp-content/uploads/2019/01/FACT-SHEET-Crime-and-Victimization-Risk-Model-1.pdf) (Crime and Victimization Risk Model), a statistical model developed by the Illinois Institute of Technology that estimates an individual's risk of becoming a victim or possible offender. This model was also used in SSL (see above list of predctors), but the newer CVRM model uses a shorter list of predictors, excluding previous narcotic arrests and gang activity. This is part of the larger Chigaco Police stratgey called [Violence Reduction Strategy]( https://home.chicagopolice.org/information/violence-reduction-strategy-vrs/). 


SSL and SAID are *person-focused* tools but there are also algorithms for predictive policing that are *place-focused* such as [HunchLab](https://www.theverge.com/2016/2/3/10895804/st-louis-police-hunchlab-predictive-policing-marshall-project), [PredPol](https://en.wikipedia.org/wiki/PredPol) or [CompStat](https://en.wikipedia.org/wiki/CompStat). Based on geographical crime patterns and other factors, these tools are used to direct police resources toward certain areas rather than others. 

## Pre-trial risk asessment: PSA and COMPAS

Many algorithms are used to guide pre-trial risk assessment decisions. These decisions have to do with whether a defedant awaiting trial can be released or should rather be held in preventative custody to ensure community safety.

[**PSA**](https://www.psapretrial.org/), an algorithm developed by [ArnoldVentures](https://www.arnoldventures.org/) is now widely used in several jurisdictions. A [report](https://www.mdrc.org/sites/default/files/PSA_New_Jersey_Report_%231.pdf) 
shows that the adoption of PSA in New Jersey as part of its 2017 [Criminal Justice Reform](https://njcourts.gov/courts/criminal/reform.html) seems to have "significantly reduced the length of time defendants spend in jail in the month following arrest". There was  a [20% reduction](https://www.njcourts.gov/courts/assets/criminal/cjrreport.pdf) in the pre-trial jail population in 2017 after PSA was adopted. The ACLU of New Jersey [endorsed](https://www.aclu-nj.org/theissues/criminaljustice/pretrial-justice-reform) the reform becasue it ended the pre-trial system of money and bail that disproportionately affects the poor.


But perhaps the most famous and most discussed algorithmic tool for pre-trial 
crime prevention is COMPAS. It was at the center of a controversy 
about what it means for an algorithm to be fair. 

## The ProPublica/Northpointe debate

In 2016, ProPublica published a [piece](https://www.propublica.org/article/machine-bias-risk-assessments-in-criminal-sentencing) asserting that COMPAS was racially biased against blacks. The argument was relatively simple. COMPAS assigns to individuals a score between 1 (low risk) and 10 (high risk). Suppose COMPAS classifies as *high risk* every individual with a score of 6 or higher and *low risk* any other individual. ProPublica compared the predictions made by COMPAS with the rearrest data and found out that blacks who were *not* rearrested were misclassified as high risk at almost twice the rate of similarly situated whites. In other words, the false positive rate for whites was half the false positive rate for blacks, 23.5% versus 44.9%. By contrast, blacks who were rearrested were misclassified as low risk at almost half the rate of whites. In other words, the false negative rate for whites was twice the false negative rate for blacks, 47.7% versus 28%.

Northpointe (now Equivant), the company that designed COMPAS, [responded](https://www.equivant.com/response-to-propublica-demonstrating-accuracy-equity-and-predictive-parity/) that comparing false positives and false negatives across racial groups was irrelevant. What mattered were the predictions, and COMPASS made equally accurate predictions across racial groups. Among the individuals predicted to be high risk, the same proportion did not reoffened for both racial groups. Further, among the individuals predicted to be low risk, the same proportion did reoffend for both racial groups. COMPAS was not, they argued, racially biased. 

## What to compare for fairnes?

The ProPublica/Northpointe debate underscores a fundamental disagreement about the nature of algorithmic 
fairness and racial bias. ProPublica's position was that what mattered for fairness was equality in false positive and false negative rates. That is, similarly situated groups of individuals -- specifically, whites and blacks who are *in fact* (or in fact are not) going to reoffend -- should be misclassified at the same rate.  Northpointe's position was that what matterred for fairness was equality in predictive accuracy. That is, similarly situated groups of individual -- specifically, whites and blacks who are *predicted* to be high risk (or *predicted* to be low risk) -- should be misclassified at the same rate.  

They take two different viewpoints. ProPublica singles out the group of actual non-reoffenders (or reoffenders) and then compares the algorithm classification errors for whites and blacks whithin this group, for example, what percetange of  white non-reoffenders are misclassified as high risk compared to the percentage of black non-reoffenders who are misclassified as high risk. Northpointe, instead, singles out the group of those predicted to be high risk (or low risk) and then compares the classification errors for whites and blakcs within this group, for example, what percetange of white high risk individuals are non-reoffenders compared to the percentage of black high risk individuals who are  non-reoffenders. But what are the relevant comparison classes for assessing algorithmic fairness?

## Mayson: Against classification equality 

Sandra G. Mayson in her 2019 article [Bias In, Bias Out](https://www.yalelawjournal.org/article/bias-in-bias-out) *Yale Law Journal* (128: 2218-2300) argues that equality in false positives and false negatives does not matter for algorithmic fairness. Her argument begins with two general premises: 

**(P1)** *Fairness requires to treat two similarly situated individuals the same.* 

This premise is Aristotele's principle of treating like cases alike. 
But wheh are two individuals "similarly situated"? Mayson writes:

> The question of what makes two people (or groups) relevantly “alike” for
purposes of a particular action is really a question about the permissible grounds
for that action. To judge that two people with equivalent skill and experience are
relevantly “alike” for purposes of a hiring decision is to judge that skill and experience are good grounds on which to make such a decision (2273)

In hiring decisions, two people with equal qualifications and work experience are similarly situated because work experience and qualifications are relevant grounds for making hiring decisions. That two people do not have the same ice-cream preferences does not matter as to whether they are similarly situated relative to hirign decisions because ice-cream preferences are not relevant for hiring decisions. The second premise is therefore as follows:

**(P2)** *Two individuals are similarly situated, relative to a certain decision, if and only if they share all the features that are relavant grounds for making the decision in question.* 

Suppose now we compare a white and a black individaul who differ from one another in terms of the ultimate outcome, that is, one is a reoffender and the other is not.  Does that difference count against them being similarly situated for the purpose of risk assessment? Mayson thinks it does not. 

> To hold that ultimate outcomes are
what render two people (or groups) alike for purposes of risk assessment is to
hold that outcomes are a good basis for risk assessment. But they cannot be the
basis for risk assessment because at the time of assessment they are unknown.
This is why we resort to risk assessment in the first place (2275). 

From this, we can extract two other premises in Mayson's argument:

**(P4)** *Outcomes such as being a reoffender (or being a non-reoffender) are not relevant grounds for risk assessments (simply becaue these outcomes are unknown).*

The other premise is that:

**(P5)** *If outcomes such as being a reoffender (or being a non-reoffender) were to make two individuals similarly situated, then these outcomes would be relevant grounds for risk assessment (because of what premise P2 says).*

By combining these two premises, we must conlude that ultimate outcomes 
cannot make two indidividuals similarly situated. Since by premise (P2) being similarly 
situated is relavent for fairness,  ultimate outcomes are irrelevant for fairness. 
Further, since the demand for equality in false positives and false negatives assumes 
that equality of outcomes makes two individuals similarly situated, 
that demand is ill-conceived. As Mayson out it,

> The demand for equal algorithmic treatment
for same-outcome groups amounts to a judgment that outcomes 
are the appropriate basis for prediction. And that judgment is nonsensical (2275).


## Hellman: Against predictive equality 

Deborah Hellman in her forthcoming paper [Measuring Algorithmic Fairness](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3418528), *Virginian Law Review*, 
reaches the opposite conclusion.









[Dangerous Defendants](https://www.yalelawjournal.org/article/dangerous-defendants), *Yale Law Journal* (127: 490-568) writes:






