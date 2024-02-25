Cosine similarity (distance) - distance between two vectors.
$$CosSim = \frac{\sum_{i=1}^{n} x_iy_i}{\sqrt{\sum_{i=1}^{n} x_i^2} \sqrt{\sum_{i=1}^{n} y_i^2}}&&$$

If you're trying to calculate similarity between user's ratings you will encounter problem of users having subjective understanding of what is 1 star or 5 stars.
To mitigate this problem [[Adjusted cosine similarity]] can be used. However, in case of sparse data, when most of users don't rate most of the items (movies, products) adjusted cosine similarity can be misleading. In this case [[(item-based) Pearson similarity]] can be used.
