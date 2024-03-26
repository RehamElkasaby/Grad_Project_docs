
- the notion of similarity is often done by thinking of properties or features of items and 
users in the same embedding space where we can then compare how similar they are. 

- **An embedding** is a map from our collection of items or users to some finite dimensional vector space.
- it provides a way of giving a finite vector valued representation of the items and users in our data set. 

- **Embeddings** are commonly used to represent ***input features*** and machine learning problems.
- A **similarity measure** is just a metric that defines exactly how similar are close to items are in the embedding space, They have different types.
## dot product of two vectors:

we compute the sum of the product wise components of each vector. 
$$ u \cdot v = \sum_{i} a_ib_i $$

**The cosine similarity**
$$ u\cdot v = \frac{ \sum_{i} {a_ib_i}}{\vert \vec{a}\vert \vert \vec{b}\vert} $$
is another popularly used similarity measure, 
it's similar to the dot product that scaled with a norm of the movie feature vectors. 
 