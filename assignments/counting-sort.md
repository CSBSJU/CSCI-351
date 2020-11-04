---
title: "Counting sort in OpenMP"
---

# Instructions
Parallelize the program provided in [this](https://github.com/CSBSJU/CSCI-351-counting-sort.git) Git repository using OpenMP. In particular, you should
parallelize the first and last for-loop of the `csort()` function.

# Background
A couple of things about the program as it is written. The program provided
requires two command line parameters. The first is the number of values which
will be sorted, the second is the number of bits to be used for values stored in
the array. For example, if your executable is called `csort` and you executed it
like so:

```
./csort 1000 10
```

An array would be created with 1000 values in it. Each value in the array would
be a random number between 0 and 2^10. Since the program must create an array
(`count`) that is sized based on the number of keys, in the above example, 2^10,
be careful not to make the number of keys too large.

The program also does an automatic check after calling the `csort()` function to
see if the results are correct, i.e., it checks to see if the output array is
sorted.
