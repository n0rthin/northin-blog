Describes how broad recommendations produced by a recommender system
For example, a recommender that suggests only next book in series is less diverse than a recommender that can recommend books from other series
To calculate diversity:
1. Calculate similarity between items
2. Calculate average similarity between recommendations in top-n list ($S$)
3. Diversity is opposite of similarity, so to get it subtract $S$ from $1$ ($1 - S$)

Unusually high diversity could mean bad recommendations