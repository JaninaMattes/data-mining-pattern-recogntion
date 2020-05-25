# Recommender Systems

#### User (to User) Collaborative Filtering
________________________________
The _UCF_ approach deals with the problem of finding a set of _N_of other users whose ratings are _similar_ to the ratings of customer x.
Then estimate x's ratings based on ratings of users in N.

##### Similar Users
How can we define similar users? The issue is that looking on a matrix of users that have rated a set of movies
there might be missing values in between. This means, user A might have rated different movies then user B, leaving
us with no directly comparable information.

The main idea here is that users that rate movies similar might like the same movies. So we could make recommendations based
on the similar taste of a certain group of users. To calculate the similarity we need a similarity metric sim(x,y).
A way to capture the rating and similarity is cosine distance, because these ratings are vectors.

Calculate the similarity of two vectors by their _cosine distance_.

```
sim (A, B) = cos (rA, rB)
```

###### Normalization of ratings
Missing ratings can not be simply filled in with 0 values, as we don't know how the user would have rated the movie and in this case 0 would be the worst, whilst 5 would be the best rating. The idea here is to fill these _gaps_ in by substracting the _row mean_ of each user. This means for example, that a user, that has rated three movies out of ten with a rating of 4, 5 and 1, a mean value of 10/3 could be calculated. In this way some values can become negative.
If we sum up a row the values become again 0. This means we have centered the ratings of every user around 0 so that the average rating becomes 0.

Calculating cosine distance with normalized values ( _Centered Cosine Similarity_ ) captures intuition better as missing ratings are treated as an "average" and it can simply handle "tough raters", as well as "easy raters". This way a value close to zero shows a higher similarity.
This similarity measure is also known as ** Pearson Correlation ** ( _Centered Cosine Similarity_ ).

#### Item (to Item) Collaborative Filtering
__________________________

Instead of starting out at a user, this approach _ICF_ shows another view in which similar items are calculated for a certain item i. In this way ratings can be estimated for an item based on the ratings of a similar item. The similarity metrics and prediction functions of a user to user model can be used. With the Centered Cosine Similarity/Distance or Pearson Correlation as similarity metric can be used to find a neighbourhood of items similar to the item _i_. Then the prediction can be made based on a prediction function.

Compute the similarity from item i to all the other items and take in consideration the ratings of the user x and item i.

#### Performance Analysis item-item vs. user-user
________________________________

In practive item-item outperforms user-user in many use cases, as items are so called "simpler" then users. This means items belong to a small set of genres, whilst users have very varied tastes. Furthermore, item similarity is more meaningful then user similarity.
