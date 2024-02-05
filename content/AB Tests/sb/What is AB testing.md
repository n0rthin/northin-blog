---
alias: (A/B Test)
---
### Overview
AB testing is a method of verifying that a change to the product actually made significant effect on the metric we want to optimize. Besides that A/B testing is also a great tool to learn about our users.
To do an a/b test we need to randomly select two groups of users: control and experimental. Then the control group is exposed to the version of product without a change (version A). In meantime changed version of product (version B, variant) will be shown to the experimental group. 
Once experiment is finished we'll compare difference between metrics of the two groups. As a result we might observe that our change to the product performed better then control and we might be tempted to release it to all users. But it would be a bad decision since difference in metrics between groups could be simply caused by luck. What we want instead is to be *confident* that the result is *statistically significant* enough to make such decision.
[[Statistical significance]] - a probability that difference between control and variant is caused by something other than chance. There are tools for its calculation that return percent value between 0% and 100%. But it can't be 100%, there will always be probability that variant won due to pure luck.
Just knowing statistical significance of experiment result is not enough to make a decision. We also need to decide beforehand which level of statistical significance we're willing to accept. This is what usually referred as *confidence level* or *significance level*. Convention is to set confidence level at 95%.
So, after the experiment, we could find that conversion (or another metric) is higher for variant and this difference has, for example, 60% statistical significance. Since our confidence level is set to 95% and 60% is less then that we will reject the variant saying that "the effect on the metric caused by variant was not significant enough".
In opposite scenario, significance could be at 97% level, which is higher then 95%. In that case, we will assume with 97% confidence that our change positively affects metric (there's still 3% chance that we're wrong).

The process of A/B testing could be splitted in 3 parts: Before test, During test, and After test. Let's take an overview of each of these steps.

### Before test
Before we conduct any experiment we need to have several things prepared:
- a metric we want to optimize
- a variant that will presumably improve the metric
- minimal effect on metric we would want to observe (MEI)
- a [[hypothesis]]. Hypothesis is a statement that some **metric** and a specific **change** (variant) to the product are connected. Examples of hypotheses: 
	- "*If* we **show product suggestions in gallery** (variant) *then* **average revenue per customer** (metric) will increase by 5%"
	- "*If* we **offer product bundles** (variant) *then* **average revenue per customer** (metric) will increase by 10%".
- confidence level - how confident we want to be when we accept hypothesis
- statistical power - how confident we want to be when we reject hypothesis. Read [[False positives & False negatives]] for more details.
- [[experiment duration]] - how long we need to run an experiment to reach desired level of confidence.
- audience - which users will take part in the experiment. We might want to test changes only for trial users, paying clients, or any specific subscription plan, etc.

### During test
There's not much we need to do once experiment is launched. The only thing that we'd want to check during test is whether new change has negative impact on users so big that it might damage our business. In this case it makes sense to stop the experiment.
Other than that we just need to wait until statistical significance is achieved

### After test
After an experiment is finished we calculate statistical significance and [[confidence interval]]. Based on that our conclusion could look like this:
"We're 97% confident that variant improves metric by 4%-5%"
Or like this:
"The effect on the metric caused by variant was not significant enough".
In first case, the next logical step would be to rollout variant to all users. And in the second situation we would rollback it. 
Regardless of what conclusion we arrived to there's always room to learn something new from the experiment. Read [[Learning from experiment]]

### Terminology
The version A could also be called "status-quo", "control", or "baseline".
And the version B has following synonyms: "variant", "experiment", "challenger"
In context of ab testing the term "experiment" can be used interchangeably with the term "a/b test". However, generally speaking, experiment is more broad term.
Experiment - any type of investigation in which an independent variable (a change to a product)  is manipulated to study its effect on a dependent variable (metric).
A/B test - type of an experiment where two different versions of product are compared by showing them to two different groups of people.