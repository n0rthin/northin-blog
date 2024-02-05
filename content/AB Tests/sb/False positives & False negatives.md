Important thing to know about A/B testing and experimentation in general is that when we accept or reject our hypothesis we can never be 100% confident in our conclusion.
It means that sometimes we will be accepting hypothesis when in reality it's false and rejecting when it's true.
Situation when we accept false hypothesis is called **false positive** and sometimes referred as Type 1 error.
Respectfully, situation when we reject true hypothesis is called **false negative** or Type 2 error. 

In statistics probability of false positive is denoted as α (alpha), and probability of false negative is ß (beta). The opposite of *alpha*, 1 - α, is what's referred as **[[statistical significance]]** which simply means probability of **not** making type 1 error (false positive), or probability that when we conclude that our hypothesis is true, it's really true. 
The same logic applies to *beta*. 1 - ß is what's called **[[statistical power]]** - probability of **not** making type 2 error (false negative), or probability that when we conclude that our hypothesis is false, it's really false.

Significance level and power are chosen before conducting an experiment. Usually significance level is set at 95% and power at 80%.

**Why significance level is larger than power?**
Read how statistical significance and statistical power are related to the [[experiment duration]].
It comes from two facts: most of the hypothesis are rejected, and amount of hypothesis we can test in given period depends on experiment duration which directly depends on significance level and power. So if most of the hypothesis are rejected we want to have as much tests and as fast as possible. We can achieve it by decreasing significance level or power. But what would happen if we'd done it? 

Significance level is probability that accepted hypothesis is true. The worst scenario in this case is that we accepted false hypothesis. As a result we'll have a feature in product that doesn't bring any value but should be maintained, integrated with new changes, and supported. Also, we will be thinking that our assumption behind accepted hypothesis is also true. Which might be even worse since we'll probably have new hypotheses based on this false assumption and new changes introduced to product

What worse can happen if we rejected true hypothesis? We wont't have any new changes that have additional costs and we won't be spending resources pursuing 
ideas based on false assumptions. We will be still believing that something is false when it's true but it's not as bad as thinking that something is true when it's not.

So the best strategy would be to stay conservative and accept hypothesis only when we're really confident in them. So we can decrease experiment duration by decreasing power and keeping confidence level high.

Small note on terminology. In statistics, "confidence" is another way to describe probability. So sometimes the term confidence level is used instead of significance level since significance is just probability of being of hypothesis being true.