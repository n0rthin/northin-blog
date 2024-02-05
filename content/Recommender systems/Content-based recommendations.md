Content-based recommendation is a recommendation that is based on the content of an item (product, movie, etc). If user bought a poster then probably they would like to see other poster products.

To make such recommendation we need to calculate similarity between items first.
One of the common ways to do it is to use [[cosine similarity]]. 
Firstly, we need to present attributes of each item as a vector.
For example, we could have following attributes of a product: 
1. Product group - prints, wallart.
2. Dimension - portrait, landsape
Vectors for products could look like this:
| Product   | prints | wallart | portrait | landscape |
| --------- | ------ | ------- | -------- | --------- |
| Product A | 1      | 0       | 1        | 0         |
| Product B | 1      | 0       | 0        | 1         |
| Product C | 0      | 1       | 1        | 0          |
Now to we could calculate cosine similarity between all vectors and find which products are more similar to each other than other.
```run-python
import math
def compute_cosine_similarity(v1, v2):
	sumxx, sumxy, sumyy = 0, 0, 0
	for i in range(len(v1)):
		x = v1[i]
		y = v2[i]
		sumxx += x * x
		sumyy += y * y
		sumxy += y * y
	return sumxy/math.sqrt(sumxx * sumyy)
	
p1 = [1, 0, 1, 0]
p2 = [1, 0, 0, 1]
p3 = [0, 1, 0, 1]
similarities = []
all = [p1, p2, p3]
for i in range(len(all)):
	row = []
	for j in range(len(all)):
		row.append(compute_cosine_similarity(all[i], all[j]))
	similarities.append(row)


for row in similarities:
	print(f"{row[0]} {row[1]} {row[2]}")
```
