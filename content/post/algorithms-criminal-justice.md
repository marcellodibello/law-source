---
title: Algorithmic Fairness in Criminal Justice
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

Algorithms are used in the criminal justice system to streamline decisions in policing, pre-trial risk assessment and sentencing. Individuals are assigned risk scores that track their probability of committing future crimes or being crime victims. Risk scores are based on factors that correlate more or less strongly with crime, say prior arrests, prior convictions, failure to appear in court, involvement in crime incidents. To identify the relevant factors, different statistical and machine learning methods, such as [logistic regression](https://machinelearningmastery.com/logistic-regression-for-machine-learning/), 
are applied to historical data about crime. 

Algorithms have taken the justice system by storm and are going to become even more persivase. They promise to be efficient, objective and unbiased. But they are not without problems of course. Protected attributes, race or gender, are typically not part of the set of predictors, but if the training data are biased, algorithmic decisions will [inherit](https://www.technologyreview.com/s/612775/algorithms-criminal-justice-ai/) 
the biases. Garbage in, garbage out. Biases due to biased data might 
compound over time throguh [feedback loops](http://proceedings.mlr.press/v81/ensign18a/ensign18a.pdf) and exacerbate racial inequities. 
Algorithms might actually [fail](https://chicagounbound.uchicago.edu/cgi/viewcontent.cgi?article=1021&context=public_law_and_legal_theory) at what they are supposed to do best, namely to reduce crime.  

I will focus on the question of whether the algorithms used in criminal 
justice are fair and more generally on what it means for an algorithm to be fair.
There is a growing literature in computer science, law and philosophy on algorithmic fairness. Definitions [proliferate](https://www.youtube.com/watch?v=jIXIuYdnyyk), but a unified analytical framework is lacking. I will discuss some of the proposals for theorizing about algorithmic fairness. Before I do that, I will review some examples of algorithms in criminal justice. 

## Predictive policing

The Chigaco Police Department, following a [surge](https://www.nytimes.com/2013/06/11/us/chicago-homicides-fall-by-34-percent-so-far-this-year.html) in street violence  in 2013, adopted SSL (Strategic Subject List), an algorithm that calculates risk scores for individuals known to the police. The risk scores are intended to reflect someone's probability of being involved in a shooting incident either as a victim or an offender. The attributes used to calculate the risk scores are (see [data](https://data.cityofchicago.org/Public-Safety/Strategic-Subject-List-Dashboard/wgnt-sjgb) in the [Chicago Data Portal](https://data.cityofchicago.org/)): 
- times being the victim of a shooting incident
- age during the latest arrest
- times being the victim of aggravated battery or assault
- prior arrests for violent offenses 
- gang affiliation 
- prior narcotic arrests 
- trend in involvement in crime incidents 
- prior unlawful use of weapon arrests 

Jessica Saunder and others in 2016 run an experimental analsys and [concluded](https://link.springer.com/article/10.1007/s11292-016-9272-0) 
that "[i]ndividuals on the SSL are not more or less likely to become a victim of 
a homicide or shooting than the comparison group."  


In 2019, SSL was [replaced](http://directives.chicagopolice.org/directives/data/a7a57b85-155e9f4b-50c15-5e9f-7742e3ac8b0ab2d3.html) 
by SAID (Subject Assessment and Information Dashboard). This tool relies, among other things, on information provided by [CVRM](https://home.chicagopolice.org/wp-content/uploads/2019/01/FACT-SHEET-Crime-and-Victimization-Risk-Model-1.pdf) (Crime and Victimization Risk Model), a statistical model developed by the Illinois Institute of Technology that estimates an individual's risk of becoming a victim or offender. CVRM was already part of SSL, but its newer version relies on a shorter list of predictors, excluding previous narcotic arrests and gang activity. This is part of the larger Chigaco Police stratgey called [Violence Reduction Strategy]( https://home.chicagopolice.org/information/violence-reduction-strategy-vrs/). 


SSL and SAID are *person-focused* tools but there are also algorithms for predictive policing that are *place-focused* such as [HunchLab](https://www.theverge.com/2016/2/3/10895804/st-louis-police-hunchlab-predictive-policing-marshall-project), [PredPol](https://en.wikipedia.org/wiki/PredPol) or [CompStat](https://en.wikipedia.org/wiki/CompStat). Based on geographical crime data and other factors, these tools help to allocate police resources toward certain areas rather than others. 

## Pre-trial risk assessment

Many algorithms are used to guide pre-trial risk assessment decisions. These decisions have to do with whether a defedant awaiting trial can be released or should be held in preventative custody to ensure public safety. 

[PSA](https://www.psapretrial.org/), an algorithm developed by [ArnoldVentures](https://www.arnoldventures.org/), is now widely used in several jurisdictions for this purpose. A [report](https://www.mdrc.org/sites/default/files/PSA_New_Jersey_Report_%231.pdf) 
shows that the adoption of PSA in New Jersey as part of the [Criminal Justice Reform](https://njcourts.gov/courts/criminal/reform.html) has "reduced the length of time defendants spend in jail in the month following arrest". There was  a [20% reduction](https://www.njcourts.gov/courts/assets/criminal/cjrreport.pdf) in the pre-trial jail population in 2017 after PSA was adopted. The ACLU of New Jersey [endorsed](https://www.aclu-nj.org/theissues/criminaljustice/pretrial-justice-reform) the reform becasue it ended the pre-trial system of money and bail that disproportionately affects the poor.

Perhaps, the most famous and most discussed algorithmic tool for pre-trial 
crime prevention is [COMPAS](https://en.wikipedia.org/wiki/COMPAS_(software)). It was at the center of a controversy 
about what it means for an algorithm to be fair. 

## The ProPublica/Northpointe debate

In 2016, ProPublica published a [piece](https://www.propublica.org/article/machine-bias-risk-assessments-in-criminal-sentencing) asserting that COMPAS was racially biased against blacks. ProPublica compared the risk asessments made by COMPAS with the rearrest 
[data](https://www.propublica.org/datastore/dataset/compas-recidivism-risk-score-data-and-analysis) for Broward County, Florida. Using rearrests as a proxy for recidivism, ProPublica found racial biases in COMPAS risk assessments. 

COMPAS assigns to people a risk score between 1 and 10. For simplicity, think of COMPAS as a binary classifier, sorting people into two classes: those with a score of 6 or higher (considered  *high risk*) and those with a score of 5 or lower (considered *low risk*).
The analysis by ProPublica showed that blacks who were *not* rearrested were misclassified as high risk (a false positive) at almost twice the rate of similarly situated whites, 44.9% versus 23.5%. By contrast, blacks who were rearrested were misclassified as low risk (a false negative) at almost half the rate of whites, 28% versus 47.7%. These are damning numbers. COMPAS prefers to label blacks high risk even when they do not reoffend, and label whites low risk even when they do reoffend. 

Northpointe (now [Equivant](https://www.equivant.com/)), the company that designed COMPAS, [responded](https://www.equivant.com/response-to-propublica-demonstrating-accuracy-equity-and-predictive-parity/) that comparing false positives and false negatives across racial groups was irrelevant. What mattered were the predictions, and COMPASS made equally accurate predictions across racial groups. Among the individuals labeled high risk, the same proportion did not reoffened for both racial groups. Further, among the individuals labeled low risk, the same proportion did reoffend for both racial groups. COMPAS was not, Northpointe argued, racially biased. 

This disagreement raises the question, *What are the relevant comparison classes for assessing algorithmic fairness?*

ProPublica singled out the group of actual non-reoffenders (or reoffenders) and then compared the algorithm classification errors for whites and blacks whithin this group, for example, what percentage of  white non-reoffenders are misclassified as high risk compared to the percentage of black non-reoffenders who are misclassified as high risk. 

Northpointe, instead, singled out the group of those labeled high risk (or low risk) by COMPAS and then compared the classification errors for whites and blakcs within this group, for example, what percentage of white high risk individuals are non-reoffenders compared to the percentage of black high risk individuals who are non-reoffenders. 

The conciliatory stance that they are both right must be ruled out. It is a [mathematical impossibility](https://arxiv.org/abs/1703.00056) for an algorithm to ensure  equality in false positive and false negative rates together with equality in prediction errors across groups. So long as the prevalence of recidivism varies across groups -- as is the case between whites and blacks -- the two dimensions of equality cannot be  satisfied at the same time. We are confronted with a seeming either/or choice between two criteria of fairness. 

## Against classification equality 

Sandra G. Mayson in her 2019 article [Bias In, Bias Out](https://www.yalelawjournal.org/article/bias-in-bias-out) *Yale Law Journal* (128: 2218-2300) argues that equality in false positives and false negatives does not matter for algorithmic fairness. Her argument begins with two general premises: 

**(P1)** *Fairness requires to treat two similarly situated individuals the same.* 

This is Aristotle's principle of treating like cases alike. 
But wheh are two people "similarly situated"? Mayson writes:

> The question of what makes two people (or groups) relevantly “alike” for
purposes of a particular action is really a question about the permissible grounds
for that action. To judge that two people with equivalent skill and experience are
relevantly “alike” for purposes of a hiring decision is to judge that skill and experience are good grounds on which to make such a decision (2273).

The thought is that, in hiring decisions, two people with equal qualifications and work experience are similarly situated because work experience and qualifications are relevant grounds for making hiring decisions. That two people do not have the same ice-cream preferences does not matter as to whether they are similarly situated relative to hiring decisions because ice-cream preferences are not relevant for hiring decisions. The second premise is therefore:

**(P2)** *Two individuals are similarly situated, relative to a certain decision, if and only if they share the features that are relavant grounds for making the decision in question.* 

Suppose we compare a white and a black individaul who differ from one another in terms of the ultimate outcome, that is, one is a reoffender and the other is not.  Does this difference count against them being similarly situated for the purpose of risk assessment? Mayson first notes that: 

> To hold that ultimate outcomes are
what render two people (or groups) alike for purposes of risk assessment is to
hold that outcomes are a good basis for risk assessment (2275). 

That is:
**(P3)** *If outcomes such as being a reoffender (or being a non-reoffender) were to make two individuals similarly situated, then these outcomes would be relevant grounds for risk assessment.*

**(P3)** follows from **(P2)** which posits a tight connection between features that are relevant decision-making grounds and features that make individuals similarly situated relative to the decision in question. 

Mayson further adds that 

> they [=ultimate outcomes] cannot be the
basis for risk assessment because at the time of assessment they are unknown.
This is why we resort to risk assessment in the first place (2275). 

So another premise of Mayson's argument reads:

**(P4)** *Outcomes such as being a reoffender (or being a non-reoffender) are not relevant grounds for risk assessments (simply becaue these outcomes are unknown).*


From **(P3)** and **(P4)**, it follows that ultimate outcomes 
cannot render two people similarly situated. Further, since by **(P1)** being similarly 
situated is relavent for fairness,  ultimate outcomes are irrelevant for fairness. 
Finally, since the demand for equality in false positives and false negatives assumes 
that equality of outcomes renders two individuals similarly situated, 
that demand is misplaced. In short,

> The demand for equal algorithmic treatment
for same-outcome groups amounts to a judgment that outcomes 
are the appropriate basis for prediction. And that judgment is nonsensical (2275).

This is an intriguing argument. 

But I wonder whether Mayson is too narrowly focused on risk assessment. The latter is a tool for informing pre-trial decisions about detention or release. True, what's at stake is the fairness of algorithms, but more broadly, what's at stake is the fairness of decisions based on algorithms. It is odd to say that recidivism is not a legitimate ground for decisions about detention or release. It is actually the definitive ground. After all, if one will recidivate, they should be detained, and if not, they should be released. 

Mayson might reply that, since outcomes are unknowable, they cannot be grounds for decision-making. It is unclear why that should be so. If two students are, in some objective sense, equally prepared, but a test systematically ranks one below the other, the test is unfair. Objective preparation might well be unknowable, but it would be the definitive ground that renders two students equally situated relative to test taking and assessment. Deborah Hellman in her forthcoming article [Measuring Algorithmic Fairness](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3418528), *Virginia Law Review*, 
uses a pedagogical example to argue that equality in false positive and false negative is relavent for fairness. 

## Another argument against classification equality

There are other reasons to resist equality in false positives and false negatives as a criterion for fairness. Suppose false positives are higher for blacks than for whites, say, 40% v. 20%. One way to equalize them is to increase the high risk threshold for blacks, say from 6 to 8, or conveserely lower the high risk threshold for whites, say from 6 to 4. 

If a more stringent threshold is adopted for black defedants,  more black reoffenders will be released. Since we know  crime is intraracial, this will adverserly affect the black community almost exclusively. In the name of equality, the black community will be put at even greater disadvantage.

If a less stringent threshold is adopted for white defedants, nobody will be better off. Blacks would still be subject to a 40% false positive rate, and whites also would be subject to a 40% false positive rate compared to the original 20%. Whites would be worse off with no gain for blacks. This is the so-called [levelling down objection](http://aristotle.rutgers.edu/joomlatools-files/docman-files/7Equality,Priority,andLDO.pdf) to egalitarianism.

Another problem is that, by changing the decision threshold, people in different groups would be classified high risk or low risk following different threholds, and this is a possible violation of equal treatment or procedural fairness. 

These arguments are quite damning for classification equality. They can only be escaped if it is possible to equalize false positives and false negatives *without* adjusting the decision threshold. The threshold must be held constant for different groups at whatever its optimal level might be. I believe that false positive and false negative can be equalized without touching the threshold, but I will leave this to another post. 

## Equal Protection Jurisprudence

A clear analytical framework is still missing. An obvious place to look is the Equal Protection Clause of the 14th Amendment as well as equal protection jurisprudence. But Aziz Z. Huq has shown this is not going to work; see his 2019 article [Racial Equity in Algorithmic Criminal Justice](https://scholarship.law.duke.edu/dlj/vol68/iss6/1/), *Duke Law Journal* (68: 1043-1134). 

One legal cartegory is *disparate treatment* on the basis of protected attributes such as race or sex. Dispare treatment can occur because of racial classification, racial animus or discriminatory intent. Any use of racial classification must be justified with a clear rationale, an inquiry known as "strict scrunity". But disparate treatment is unlikely to be helpful here. Algorithms hardly have racially discriminatory intention nor do they explicitly rely on race as a predictor.

The other category is *disparate impact*, common in [Title VII](https://www.eeoc.gov/laws/statutes/titlevii.cfm) discrimination cases. Evidence of disparate impact against a protected group is enough to make a *prima facie* case of discrimination; see e.g. [Hazelwood School District v. United States](https://en.wikipedia.org/wiki/Hazelwood_School_District_v._United_States) (1977). This applies to sectors such as emplyoment and housing. The criminal justice system, however, seems exempt. In [McClensky v. Kemp](https://www.oyez.org/cases/1986/84-6811) (1987), the US Supreme Court ruled that disparate racial impact is not enough to establish a constitutional violation. Disparate impact, then, is of no help either. 

## Racial Stratification








