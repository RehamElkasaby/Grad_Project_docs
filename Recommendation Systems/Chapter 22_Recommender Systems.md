from: [[Data Science from Scratch]] book
*The problem* : recommending new interests to a user based on her currently specified interests
```python 
users_interests = [ 
["Hadoop", "Big Data", "HBase", "Java", "Spark", "Storm", "Cassandra"],
["NoSQL", "MongoDB", "Cassandra", "HBase", "Postgres"],
["Python", "scikit-learn", "scipy", "numpy", "statsmodels", "pandas"],           ["R", "Python", "statistics", "regression", "probability"],                           ["machine learning", "regression", "decision trees", "libsvm"],              ["Python", "R", "Java", "C++", "Haskell", "programming languages"],
["statistics", "probability", "mathematics", "theory"], 
["machine learning", "scikit-learn", "Mahout", "neural networks"], 
["neural networks", "deep learning", "Big Data", "artificial intelligence"], ["Hadoop", "Java", "MapReduce", "Big Data"], 
["statistics", "R", "statsmodels"], 
["C++", "deep learning", "artificial intelligence", "probability"], 
["pandas", "R", "Python"], 
["databases", "HBase", "Postgres", "MySQL", "MongoDB"], 
["libsvm", "regression", "support vector machines"]
]
```
### 1st approach: recommend what's popular:
compute what's popular
```python 
popular_interests = Counter(interest for user_interests in users_interests for interest in user_interests).most_common()
```
then suggest to the user the most popular interests that they are not already interested in:
```python
def most_popular_new_interests(user_interests, max_results=5):

	 suggestions = [(interest, frequency)

	for interest, frequency in popular_interests

	if interest not in user_interests]

	return suggestions[:max_results]

most_popular_new_interests(["NoSQL", "MongoDB", "Cassandra", "HBase", "Postgres"]
#[('Python', 4), ('R', 4), ('Big Data', 3), ('Java', 3), ('statistics', 3)]
```
That's the best way if someone is new to the site 

### User-Based Collaborative Filtering
similar users have similar interests.

collect interest then assigning indices to them
```python
# similar users are similar
#set comprehension to find the unique interests,putting them in a list, and then sorting them
# to collect interest then assigning indices to them
unique_interests = sorted(list({ interest

 for user_interests in users_interests

 for interest in user_interests }))```
 
we need a measure for similarity: Cosine Similarity
```python
def cosine_similarity(v, w):
	return dot(v, w) / math.sqrt(dot(v, v) * dot(w, w))
```

each vector v representing one user’s interests, where v[i]is 1 if user have interest $i$ and 0 otherwise.
```python
def make_user_interest_vector(user_interests):

 """given a list of interests, produce a vector whose ith element is 1

 if unique_interests[i] is in the list, 0 otherwise"""

 return [1 if interest in user_interests else 0

 for interest in unique_interests]
 #**************
 #map the last function to all user interests
 user_interest_matrix = map(make_user_interest_vector, users_interests)
```
 calculate the similarity between two users:
 ```python
 user_similarities = [[cosine_similarity(interest_vector_i, interest_vector_j)
 for interest_vector_j in user_interest_matrix]
 for interest_vector_i in user_interest_matrix]
```
then calculate the most similar:
```python 
def most_similar_users_to(user_id):

 pairs = [(other_user_id, similarity)                  

 for other_user_id, similarity

 in enumerate(user_similarities[user_id])                

 if user_id != other_user_id and similarity > 0] #find other nonzero users

 return sorted(pairs,key=lambda p:p[1], reverse=True)
```
finally make suggestions:
```python 
from collections import defaultdict

def user_based_suggestions(user_id, include_current_interests=False):

 # sum up the similarities

 suggestions = defaultdict(float)

 for other_user_id, similarity in most_similar_users_to(user_id):

    for interest in users_interests[other_user_id]:

        suggestions[interest] += similarity

 # convert them to a sorted list

 suggestions = sorted(suggestions.items(),key=lambda w: w[1],reverse=True)

 # and (maybe) exclude already-interests

 if include_current_interests:

    return suggestions

 else:

    return [(suggestion, weight)

    for suggestion, weight in suggestions

    if suggestion not in users_interests[user_id]]
```
problems with this approach: doesn't scale well
### Item-Based Collaborative Filtering:
