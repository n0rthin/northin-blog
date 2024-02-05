### Metrics
[[Mean absolute error (MAE)]] 
[[Root mean square error (RMSE)]] 
[[Hit rate]]
[[Average reciprocal hit rate (ARHR)]]
[[Coverage]]
[[Diversity]]
[[Novelty]]
[[Churn]]
[[Responsiveness]]

### Offline
To evaluate recommender system offline (without using active data and users, only historical data) **train/test split** technique could be used.
In this technique historical data is split into train dataset and test dataset.
Train dataset - this is data on which a system will be trained.
Test dataset - after the system is trained its accuracy should be checked on the data it has never seen. This is the purpose of the test dataset.
Often train dataset is much bigger than test dataset: 80%/20%.

![[Pasted image 20230217163059.png]]

### Online
Offline accuracy metrics are not always match with reality. To be sure that a recommender provides value to users and business it should be tested in real world (online). It can be done by:
1. Launching a [[What is AB testing|(A/B test)]].
2. Asking for user feedback on whether recommendation was useful or not.