![[Pasted image 20240312175914.png]]
1. we represent our items (movies) with some characteristic (like their genre) [[Content-Based Recommendation Systems]] 
2. then represent each as K hot encoding that would be **item-feature matrix**
3. multiply the movie feature matrix by their ratings given by that user. 
4. Then aggregate by summing across each feature dimension.
5. the normalization of that vector is the  **user feature vector** .
## Making Recommendation for 1 user :
The dot product is found by taking the component 
wise product across each dimension and adding the results. 
That is we multiply the **user feature vector** 
component-wise with the **movie feature vector**  for each movie, 
and then sum row-wise to compute the dot product. 
This gives us the dot product similarity between our user and each of the four movies. 
We'll use these values to make our recommendations
![[Pasted image 20240312195124.png]]


## making recommendation for multiple users:

we have two matrices:
- **item-feature matrix**: a matrix that include k-hot encoding between the item(movie) and their features.
- **user-item rating matrix:** is a matrix where user i gives movie j a rating r_ij
```python
# intialize them in tersorflow as const.
#each row represent a user
# each col represent a movie
import tensorflow as tf
users_movies = tf.constant([
						 [4,6,8,0,0],
						 [0,0,10,0,8],
						 [0,6,0,0,3],
						 [10,9,0,5,0]])
# the col represent the features:
movies_feat = tf.constant([
						[1,1,0,0,1],
						[1,1,0,0,0],
						[0,0,1,1,0],
						[1,0,1,1,0],
						[0,0,0,0,1]
])
```
then multiply each user vector(row in matrix user_movies matrix) by movie_feat matrix and get 
the **weighted feature matrix** for each user
stack them together and you get the **weighted user feature tensor** 
```python
wgtd_feature_matrices = [tf.expand_dims(tf.transpose(users_movies)[:,i],axis = 1)*movie_feats for i in range(num_users)]
users_movies_feats = tf.stack(wgtd_feature_matrices,axis = 0) # (#users,#movies,#features)
``` 
then sum across the feature columns then normalize ,we get the **user-feature tensor** (each row would represent the sum of the feature values for each user)
```python
user_movies_feats_sums = tf.reduce_sum(users_movies_feats, axis = 1)
user_movies_users_totals = tf.reduce_sum(user_movies_feats_sums,axis = 1)

users_feats = tf.stack([user_movies_feats_sums[i:,]/users_movies_feats_totals[i]for i in range(num_users)], axis = 0)
```
and finally to get recommendations, we get the dot product between the users_feats vector(user) and movie_feats(movie) to get a user_movie  predicting the rating each user will give to each movie.
![[Pasted image 20240312203339.png]]
```python
users_ratings = [tf.map_fn(lambda x: tf.tensordot(users_feats[i],x,axes = 1),
tf.cast(movies_feats,tf.float32)) for i in range(num_users)]

all_users_ratings = tf.stack(users_ratings)
```
now we have the user-movie ranking matrix we can compare it with the original user-movie matrix.

next step: to mask the ranking for the previously seen/rated movies and only leave the unseen.
```python
tf.where(
		 condition,
		 x = None,
		 y = None,
		 name = None
)
```
