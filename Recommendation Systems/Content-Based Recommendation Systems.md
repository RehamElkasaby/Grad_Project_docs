- uses the metadata about the content(items) 
- recommend an item **similar** to the items the users explicitly liked.
- it can be  a simple rule-based engine that assigns tags to items and users. This wouldn't need any machine learning.
- content-based systems only use embedding spaces for items, whereas collaborative filtering uses both users and items.
- **Advantages:**
	- don't rely on information about other users or other user item interactions
	- can recommend niche items.
- **Disadvantages:**
	- Require domain knowledge to hand-engineer features.
	- difficult to expand interests of users. 
-[[Similarity Measures]] 
### using Tensorflow:
#tensorflow
We'll build a content-based filtering model to recommend articles to readers.
building a tensorflow graph
```python
import tensorflow as tf
# content Id col. is the Id of the current article being read
# it will be treated as a catigorical feature
#using hash bukets as number of id will change over time 
content_id_column = tf.feature_column.catigorical_column_with_hash_bucket(key='content_id',hash_bucket_size=(len(content_id_list)))
# embedde it before feeding it to the model
embedded_content_column = tf.feature_column.embedding_column(catigorical_column='content_id_column',dimentions=10)
```

```python
# category is a col describing what a catgory an article belong to.
category_column_categorical = tf.feature_column.catigorical_column_with_vocabulary_list(key='category',vocabulary_list = category_list,num_oov_bucket = 1)
# 
category_column = tf_feature_column.indicator_column(category_column_categorical)

```

```python 
# title col: title of the article 
embedded_title_col = hub.text_embedding_column(key='title',module_spec="http://tfhub.dev/google/nnlm-de-dim50/1",trainable=False)
```


```python
# author col: who wrote the article
# we have a limited number of authors
author_column = tf.feature_column.catigorical_column_with_hash_bucket(key='author',hash_bucket_size =len(authour_list)+1)
embedded_author_column = tf.feature_column.embedding_column(catigorical_column='author_column',dimentions=3)
```

```python
# month since epoch col: represent the how new the article is
month_since_epoch_column
```