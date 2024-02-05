A type of [[Recommender system|recommendation system]] that tries to recommend top N products that a user will like. There are different approaches to implementation.

**Item-based collaborative filtering**
Top level view
[[Item-based collaborative filtering.canvas]]
![[Pasted image 20230217155422.png]]The process looks like this:
1. Individual interests: a user shows interest in some product.
2. Item similarities: we collect information about similar items. Products are considered similar when users often by them together.
3. Candidate generation: take products user interested in and find similar products
4. Candidate ranking: rank products based on how often they're showing up, how popular they are, etc.
5. Filtering: filter out products that user already purchased and take top N 
6. Show Top-N recommendations to the user.
Simply put: if user A likes product A and user B likes product A and product B then user A might also like product B.

This process is called item-based collaborative filtering
item-based - it's based on item similarities
collaborative - we take into account other people actions to recommend items to the user