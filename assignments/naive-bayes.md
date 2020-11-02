---
title: "Naive Bayes in C"
---

# TL;DR
Augment the program developed in the activity [Machine learning in C]({{ site.canvas.prefix }}/courses/{{ site.canvas.course }}/pages/machine-learning-in-c)
to use a different algorithm for predicting user ratings. The Git tag
[`naive-bayes`](https://github.com/CSBSJU/CSCI-351-machine-learning/tree/naive-bayes) in the [repository](https://github.com/CSBSJU/CSCI-351-machine-learning.git) is a good place to start.

# Background
The context for the problem is exactly that of the activity [Machine learning in
C]({{ site.canvas.prefix }}/courses/{{ site.canvas.course
}}/pages/machine-learning-in-c). However, instead of finding the *k* most
similar users and averaging their rating for a particular movie in order to
predict a users rating for said movie, we will be using an idea that comes from
discrete probability. In particular we are interested in computing the
conditional probability that a user will rate a movie a certain numbers of
stars, given that they rated four other movies some number of stars. For
example, if we assume the user rated the four other movies, 3.5, 4.5, 4.0, and
3.5, then we want to compute the probability that they will will rate the fifth
movie 0.5, 1.0, 1.5, 2.0, etc. Thus, we must compute the conditional probability
for each of the possible outcomes. Once we have done that, we will use the
[maximum a posteriori](https://en.wikipedia.org/wiki/Maximum_a_posteriori_estimation) decision rule to predict their rating for the fifth movie, i.e., we will
choose the most likely of the outcomes.

For more details on Naive Bayes classifier see the [Wikipedia](https://en.wikipedia.org/wiki/Naive_Bayes_classifier) page.

# Computing conditional probability
In this problem, there will be a total of ten possible outcomes: 0.5, 1.0, 1.5,
2.0, etc., all the way up to 5.0. Put another way, we must compute:

```
p(movie5 = 0.5 | movie1 = urating[0], movie2 = urating[1], movie3 = urating[2], movie4 = urating[3])
p(movie5 = 1.0 | movie1 = urating[0], movie2 = urating[1], movie3 = urating[2], movie4 = urating[3])
p(movie5 = 1.5 | movie1 = urating[0], movie2 = urating[1], movie3 = urating[2], movie4 = urating[3])
p(movie5 = 2.0 | movie1 = urating[0], movie2 = urating[1], movie3 = urating[2], movie4 = urating[3])
...
```

The above would be very computationally expensive to compute, because there are
10,000 different combinations of user ratings for movies 1--4, resulting in
100,000 different probabilities we need to compute. Luckily, we have
[math](https://en.wikipedia.org/wiki/Mathematics) on our side, and an assumption
that the ratings for the movies are independent. As a result, we only need to
compute:

```
p(movie5 = 0.5)
p(movie5 = 1.0)
p(movie5 = 1.5)
p(movie5 = 2.0)
...
```

of which there are ten probabilities to compute. As well as:

```
p(movie1 = urating[0] | movie5 = 0.5)
p(movie1 = urating[0] | movie5 = 1.0)
p(movie1 = urating[0] | movie5 = 1.5)
...
p(movie2 = urating[1] | movie5 = 0.5)
p(movie2 = urating[1] | movie5 = 1.0)
p(movie2 = urating[1] | movie5 = 1.5)
...
```

of which there are 40 conditional probabilities to compute. In the above
example, `p(movie1 = urating[0] | movie5 = 1.5)` should be understood as the
conditional probability that a viewer's rating for movie 1 is equal to whichever
rating was input by the user for movie 1, given that the viewer rated movie 5 as
1.5.

To compute a conditional probability like `p(movie1 = urating[0] | movie5 =
1.5)`, compute the number of viewers who rated movie 1 the same value as
`urating[0]` AND rated movie 5, 1.5. Then divide that by the total number of
viewers who rated movie 5, 1.5.

# Making a prediction using conditional probabilities
If we can successfully compute the conditional probabilities mentioned in the
previous section, then a prediction can be made by computing:

```
p(movie5 = prediction) * p(movie1 = urating[0] | movie5 = prediction) * p(movie2 = urating[1] | movie5 = prediction) * p(movie3 = urating[2] | movie5 = prediction) * p(movie4 = urating[3] | movie5 = prediction)
```

for each of the ten possible rating predictions that could be assigned as the
user's rating for movie 5, then choosing among them the one that is most likely.
