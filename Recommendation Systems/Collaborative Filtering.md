-  the system learns about item and user similarity from the interaction data(likes/ratings).
- Collaborative filtering learns latent factors and can explore outside the user's personal bubble.
- uses explicit—i.e. ratings—and implicit user feedback, such as how they interacted with the item.
- The idea of collaborative filtering is that the large, sparse user by item matrix can be approximated by the product of two smaller matrices called **user factors** and **item factors**.
- The factorization splits the matrix into row factors and column factors that are essentially user and item embeddings.
- content-based systems *only use embedding spaces for items*, whereas collaborative filtering uses *both users and items*.
- where to get the features?
	- We can either choose the number of dimensions using *predefined features* 
	- or we use *latent features* that are learned from data ( embeddings can be learned from data)

In order to determine if a user will like a movie, all you need to do is take the row corresponding with the user and the column corresponding to the movie and multiply them to get the predicted rating.

- **Advantages:** 
	- One of the main benefits of collaborative filtering is that you don't need to know any metadata about the item and you don't need to do any market segmentation of users.
	- no domain knowledge
	- There's also serendipity. Imagine that you are on a movie site, and only watch Sci-Fi movies, because you like them. Instead of always recommending Sci-Fi movies do you, which might get a bit repetitive, by looking at what other users who watch Sci-Fi also watch, the site might recommend a couple of fantasy movies or maybe some action movies, because those other users also like those types of movies.
	- Great starting point for hybrid


### Matrix Factorization:
matrix factorization, which works as follows:

- We factorize the user-interaction matrix into user factors and item factors
- Given a user ID, we multiply by item factors to predict the rating of all items
- We return the top $k$ rated items to the user
- ![[Pasted image 20240323200256.png]]
- $$A \approx U x V^T$$

where:

- $A$ is the user-item interaction matrix (n * m)
- $U$ is the user-factor matrix (n* k ) 
- $V^T$ is the item-factor matrix ( k * m)
so if we have a user ID and multiply it by V we get the predicted ratings of this user to all items.
and if we have a item ID and multiply it by U we get the predicated ratings of that item by all users.
we can then return top K rated item for that user (movie/music example)
or the top K users for that item (ads example)

### Factorization Approaches:
so basically, $$A \approx U x V^T$$
in training, we need to minimize the mean square error to get (U and V)
	**stochastic gradient descent SGD**:
		 - very flexible.  *+1*
		 - parallel, scale out our matrix factorization and quickly tackle much larger problems. *+1*
		 - slower **-1**
		 - has a hard time handling unobserved user item interactions.  **-1** 

**alternating least squares, ALS**, which alternatively solves U holding V constant, and then solves for V holding U constant. 
	- only works for least squares problems. **-1**
	- parallel   *+1*
	- faster than SGD  *+1*
	- easily handle unobserved interaction pairs *+1*
- How to deal with missing values in the matrix:
In ALS, we just ignore the missing values. 
We are only summing the observed instances. 
with a minor tweak, we can obtain something that usually works very well.
	give the unobserved data a lower weight.
![[Pasted image 20240323215004.png]]

in predication, we use (U and V) to get A

### Implementing ALS in TensorFlow:
1 . Map data from table to matrix
![[Pasted image 20240324004740.png]]
2. Preprocess the data into TF records
![[Pasted image 20240324005930.png]]
	If we want to recommend items/users for a user / item, when we are writing out to the TF Record file:
	Our key train feature should be *user*/item
	Our indices train feature should be *itemID*/userId
	Our values train feature should be *rating*


### # Issues with Collaborative Filtering
- **Cold start problem** 