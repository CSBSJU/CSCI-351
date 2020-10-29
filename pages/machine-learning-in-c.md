---
title: "Machine learning in C"
---

# TL;DR
Implement a program to predict the rating that the user will assign to a movie
based on their ratings for other movies and the ratings of other viewers for the
same movies.

# Background
The objective for the lab is to make an accurate prediction of the rating that
the user will assign to a particular movie based on their ratings for other
movies and the ratings of other viewers for the same movies. The basic idea is
to take the user's ratings for a set of movies and find other viewers with
similar ratings. These similar viewers can then be used to inform our
prediction.

This lab exercise uses a dataset that is maintained by the
[GroupLens](https://grouplens.org) research group at the University of
Minnesota. The dataset is part of the [MovieLens](https://movielens.org)
project. In their own words, MovieLens is a platform for "*Non-commercial,
personalized movie recommendations*"; think Netflix recommendations, but not for
profit. The dataset that we will be exploring consists of movie ratings for five
popular movies from 22419 unique viewers. In the file `ML-ratings.csv` each row
constitutes the ratings of a single viewer for each of the five movies listed in
the file `ML-titles.txt`. The first four rows in the file look like:

```
22419 5
4.0 4.5 4.0 4.0 3.0
3.0 4.0 5.0 4.0 5.0
5.0 5.0 5.0 5.0 5.0
```

This should be understood to mean that there are 22419 lines following the first
one, each representing the ratings for a unique viewer and that each unique
viewer has rated five movies. For example, viewer 1 rated movie 1, 4.5 stars out
of 5 possible; movie 2, 4.0 stars; movie 3, 4.0 stars and so on. Likewise for
viewer 2 and 3.

Now, suppose that we are given the ratings for four of the movies for a new
viewer, referred to as *the user*, who rated movies 1&ndash;4: 3.5, 4.5, 4.0,
and 3.5, respectively. Then the task at hand is to make a prediction for the
user's rating for movie 5.

A simple but unreliable way to do that would be to generate a random number
between 0.0 and 5.0. Hopefully you see the potential limitations of this
approach. If not, discuss it with someone around you.

Since we have at our disposal a dataset that contains the ratings of 22419 other
viewers, isn't it likely that some of them will have movie preferences
similar to the user's? If so, couldn't we somehow use their ratings for movie 5
to create a better than random prediction for the user's rating of movie 5? The
answer is *hopefully*; the accuracy of a prediction system like Netflix, and the
one that your are going to build, depends on it.

In order to identify viewers similar to the user, we must have some quantitative
way to determine similarity, i.e., a [similarity
measure](https://en.wikipedia.org/wiki/Similarity_measure). A common way to do
this is to calculate the absolute difference for each of the movie ratings
between the user and a viewer and add these together to compute a total
difference measurement. This difference measure is known as the [Manhattan
Distance](https://en.wikipedia.org/wiki/Taxicab_geometry) (a.k.a. Taxicab
distance). It is important to note that in this case, *distance* is the opposite
of *similarity* (what we are really after). So, to find the most similar
viewers, we should find the viewers that are the least distance from the user.

Since we will ultimately be trying to predict the rating for movie 5, we will
not include that rating in our distance calculation. Thus, if we take the user
with ratings 3.5, 4.5, 4.0, and 3.5, then the distance between the user and
viewer 1 is calculated as:

```
  |3.5-4.0| + |4.5-4.5| + |4.0-4.0| + |3.5-4.0|
=  0.5      +  0.0      +  0.0      +  0.5
=  1.0
```

So we would say that the Manhattan distance between the user and viewer 1 is
1.0. Likewise between the user and viewer 1:

```
  |3.5-3.0| + |4.5-4.0| + |4.0-5.0| + |3.5-4.0|
=  0.5      +  0.5      +  1.0      +  0.5
=  2.5
```

Of the two viewers, the user is least different (read: most similar) to viewer
1, since the distance calculation was 1.0 for viewer 1, compared with 2.5 for
viewer 2.

If we repeated this for all of the viewers in the dataset, we could determine
which viewer has movie preferences most similar to the user, at which point we
could use that viewer's rating of movie 5 to predict the user's rating of movie 5. However, as you will see, using a single viewer to inform predictions can
also be unreliable. So in a final attempt at a more accurate prediction, a
recommendation system could aggregate the ratings of many similar users to
inform the prediction. How many and how to combine their ratings will be
discussed more in later parts of this lab.

The development of such a system should proceed in steps.

# Instructions
1. Write a program that correctly echoes the contents of a file given as input.
   Echo here means print to standard out, the contents of the file, exactly as
   it appears in the file. You should assume that the contents of the file will
   have the particular form from the example above. Namely, the first line will
   contain two values, the number of viewers and the number of movies
   respectively. This will be followed by one line for each of the viewers,
   where each line includes space separated ratings for each of the movies.

1. Update your program to create five parallel arrays to store the ratings. In
   this case, corresponding positions in the parallel arrays will represent the
   ratings for a single viewer. The functionality of your program should be as
   follows. Load the data from the file into the parallel arrays, then iterate
   through the parallel arrays and print the output. In other words, the
   behavior of your program will be the same as the previous part.

1. Update your program to use a single block of dynamically allocated memory to
   store the ratings. This way, they number of viewers or movies is not
   hard-coded or limited by the environment we are using, only by the amount of
   memory available in the system. Once again, the behavior of your program does
   not change.

1. Update your program to prompt the user of the program for four inputs,
   representing the user's ratings for the first four movies. Then, instead of
   the output from the previous parts, it should compute the distance between
   the user and each of the viewers and store the result in a separate array.
   Then, iterate over the array and output its values in a table with the
   following format (the values in the following example are assuming the user
   input the values specified in [Background](#background)):

   ```
   Viewer ID   Distance
   --------------------
           1        1.5
           2        2.5
           3        4.5
         ...        ...
   --------------------
   ```

1. Update your program to find the minimum value in the *distances* array. Be
   sure to keep track of the index where the minimum value appeared. This index
   represents the id (minus one, since we are indexing from 0) of the viewer
   that is the least different from the user. Now make a prediction as to the
   rating for the user for movie 5 by using the rating for movie 5 of the viewer
   that is the least different from the user. Output the predicted rating in a
   message with the following format:

   ```
   The most similar viewer was viewer #77 and the distance calculated was 0.5.
   The predicated rating for movie 5 is 4.5.
   ```

1. As you may be able to tell, the simple model of finding the viewer from the
   dataset that is the least different from the user and using that viewer's
   rating for movie 5 to predict the user's rating for movie 5 is not very
   robust, i.e., it is likely to produce incorrect predictions.

   However, your work up to this point is not for naught. Rather than using just
   the viewer that is least different from the user, we can greatly improve the
   accuracy of our predictions by looking at the *k* least different viewers,
   where the value of *k* can be adjusted to tune the system's prediction
   accuracy.

   Unfortunately, finding the *k* least different viewers is more complicated
   than find just one, so as before, we will work through it in steps. The basic
   idea is to sort the *distances* array. By doing this, it will order the *k*
   minimum distances at the beginning of the array.

   Start by using the C standard library function, conveniently named `qsort`.
   Can you guess what sorting algorithm it is using internally? To do this, you
   would say:

   Next, output the sorted *distances* array to see that it is in fact sorted.
   For the input values 3.5, 4.5, 4.0, and 3.5, you should have output that
   looks like:

   ```
   0.5
   1.0
   1.0
   ...
   ```

   Now, can you tell which viewer is the least different from the user? Is it
   viewer 0? The problem that you are facing is the sorting the *distances*
   array does just that, but nothing else. Recall that the key to the previous
   part, i.e., using the minimum value to predict, was to keep track of the
   index in the *distances* array where the minimum value was found.
   Unfortunately `qsort()`, at least as we have used it above, does not keep
   track of the indices that each of the distances in their new sorted order,
   correspond to.

   One way to solve this problem is to make the *distances* array an array of
   *struct* values, rather than array of scalar values. A good starting point
   would be a *struct* like the following:

   ```
   struct distance_metric {
     size_t viewer_id;
     double distance;
   };
   ```

   Once you have completed that, reproduce the prediction from the previous
   part, i.e., predict based on the rating of the viewer that is the least
   different from the user. This time however, use the sorted array instead of
   computing the minimum distance in a loop. Output your prediction using the
   same statements as above. FYI, your output should be the same.

1. Update your program to ask the user to input an integer, *k*, that will be
   used to choose the *k* most similar viewers to the user. Using the sorted
   *distances* array output the *k* most similar viewers to the user in a table
   with the following format:

   ```
   Viewer ID   Movie five   Distance
   ---------------------------------
          77          4.5        0.5
          56          5.0        1.0
          48          4.0        1.0
          31          4.0        1.0
           5          3.5        1.0
           1          3.0        1.0
          97          4.0        1.5
          81          2.5        1.5
          70          4.0        1.5
          68          4.5        1.5
   ---------------------------------
   ```

1. Finally, update the program to find the average of the top *k* values and use
   this as a prediction. Below the table that was created in the previous part,
   you should output your prediction in a statement with the following format:

   ```
   Viewer ID   Movie five   Distance
   ---------------------------------
          77          4.5        0.5
          56          5.0        1.0
          48          4.0        1.0
          31          4.0        1.0
           5          3.5        1.0
           1          3.0        1.0
          97          4.0        1.5
          81          2.5        1.5
          70          4.0        1.5
          68          4.5        1.5
   ---------------------------------
   The predicted rating for movie five is 3.9.
   ```

1. If you would like more practice, it would be worth your while to refactor the
   code that you just finished. A couple things that you might consider: adding
   sufficient comments, extracting functions from the code that you have, etc.
