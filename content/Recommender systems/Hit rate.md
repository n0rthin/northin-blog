$$\frac{hits}{users}$$
Generate top-n recommendations for all users in test set. If one of the recommendations is something that a user is really bought (rated) consider it a hit
Some up all hits in the test set and divide by users amount - the result is _hit rate_
Hit rate shows accuracy of top-n lists, not accuracy of the ratings itself
The problem with hit rate is that it uses train dataset to validate recommender system which is a bad practice. Recommender should be trained and validated on different datasets. One of the ways to achieve is to use leave-one-out cross validation

**Leave out out**
Remove one item from each user's top-n list in train dataset. After training is done generate recommendations for users. Each generated lists that contain removed item is considered as a hit. Divide all hits by users amount and you'll get leave-one-out hit rate
