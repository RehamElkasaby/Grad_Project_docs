[Introduction to Recommendation Systems with TensorFlow (mlq.ai)](https://www.mlq.ai/recommendation-systems-tensorflow/) 
Recommendation systems are about personalization, allow us to personalize a user's experience. 
by recording interactions such as likes or dislikes, 
we can start to learn preferences unique to that user, 
and thus personalize future content and make personalized recommendations
[[Recommendation Engines]] + Data Pipeline = Recommendation Systems

![[Pasted image 20240228210112.png]]
## [[Content-Based Recommendation Systems]] :

-  Content-based method uses attributes of the items to recommend new items to a user
- It doesn't take into account the behavior or ratings of other users.
- need Feature Engineering 
- used if  a user has already rated a large number of items.

## [[Collaborative Filtering]] : 
- based on interactive matrix (user-item matrix)
the idea behind it is Matrix Factorization-> splitting the matrix into row factors and column factors that essentially are user and item embeddings.
- A collaborative filtering model works with the entire user item interaction matrix. They consider all users, all items, and all user item ratings. 
Loosely speaking, they work with the idea that **similar** users will like **similar** items. 
That is, they use similarities between the users 
and the items simultaneously to provide recommendations.
- doesn't need feature engineering.
- used when user has rated only a few items
## [[Knowledge-based recommender systems]] :
- are based on explicit knowledge about the user's preferences, items, and or recommendation criteria.
- used when we have no information about a user's previous item interactions or we like any information about a given user

*some research suggests that a hybrid approach combining multiple outcomes like this, can provide more accurate recommendations in a single approach on its own.*

### Recommendation System Pitfalls:
1. in the user item interaction matrix, know that the user space and the product space are **sparse and skewed**.
2. **cold start** can occur for both products and users. This happens when there aren't enough interactions or information for users or items, for example,
	1. when a new user is added to a system.
	2. when a new item is added to the catalog.
3. **lack of explicit** user feedback (ratings/thumbs up or down.)
	- Solution: using implicit feedback (number of clicks / plays and replays)
	- training a neural network on multiple implicit feedback as input to generate an explicit rating.


- [[Recommendation Systems ]]
- [[building a user vector]]
-  