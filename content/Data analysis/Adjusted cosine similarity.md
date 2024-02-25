---
description: Adjusted cosine similarity - similarity that accounts for different baselines in vectors
title: Adjusted cosine similarity
type: article
---

Adjusted cosine similarity (distance) - similarity that accounts for different baselines in vectors

$$CosSim = \frac{\sum_{i=1}^{n} (x_i - \bar{x})(y_i - \bar{y})}{\sqrt{\sum_{i=1}^{n} (x_i - \bar{x})^2} \sqrt{\sum_{i=1}^{n} (y_i - \bar{y})^2}}$$

$\bar{x}$ - average value from vector $X$

$\bar{y}$ - average value from vector $Y$
