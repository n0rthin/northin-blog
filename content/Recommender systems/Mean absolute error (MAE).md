---
aliases: (MAE)
---

The lower the better
$$MAE = \frac{\sum_{i=1}^{n} |y_i - x_i|}{n}$$
Let's say test dataset has $n$ ratings. These are real ratings provided by users explicitly or implicitly.

1. We ask our recommender system to generate their own ratings for products.
2. Then we calculate difference between each rating from test dataset and corresponding rating provided by the system ($|y_i - x_i|$ where $y_i$ is rating predicted by recommender and $x_i$ is rating provided by user).
3. To get absolute mean error we calculate [[mean]] value of differences calculated on the last step
