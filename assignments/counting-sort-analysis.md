---
title: "Counting sort analysis"
---

# Update
To make the math *simpler*, assume that the number of keys, *k*=*n*. That way,
you will only have two variables in your expressions, *n* and *p*.

# Instructions
Complete the following tasks:

1. Compute the serial and parallel execution times for the counting sort
   algorithm that we parallelized in the [last assignment]({{ site.canvas.prefix }}/courses/{{ site.canvas.course }}/assignments/{% assignment Counting sort in OpenMP %}). Then, using these values, compute the speedup, efficiency, and
   cost for a system with *p* processing units, where *p*=*n*, and *n* is the
   size of the input array.

1. Repeat the computations for case when *p*<*n*.

Once finished, answer the following questions:

1. What is the best speedup that we can hope for given that we did not
   parallelize the second loop?

1. Can restricting the number of processing units below *n* improve the
   efficiency and cost of the algorithm?

Assuming that we can parallelize the second loop, and that its parallel
execution time (for the second loop only) is O(k/p + log p), complete the
following task:

1. Repeat the performance metric computations one more time, again assuming that
   *p*<*n*.

# Submission
Collect your answers in a text or word document or take a picture of your
hand-written solutions and upload to the assignment page on Canvas. Make sure
that your submissions are legible.
