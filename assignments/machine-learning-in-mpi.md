---
title: "Machine learning in MPI"
---

# Instructions
Complete the MPI implemention of our rating prediction program started as part
of the activity [Machine learning in MPI]({{ site.canvas.prefix }}/courses/{{ site.canvas.course }}/pages/machine-learning-in-mpi). The Git tag [`mpi-part-1`](https://github.com/CSBSJU/CSCI-351-machine-learning/tree/mpi-part-1) in this [repository](https://github.com/CSBSJU/CSCI-351-machine-learning.git) contains
the MPI implementation using point-to-point communications to distribute the
input data, both the viewer ratings as well as the user ratings.

For more information about the point-to-point parallelization strategy, see the
Zoom recordings for [Monday 11/9](https://csbsju.zoom.us/rec/share/suJUZmvinidevj1zI1Fwfrj01hT4MQUW3-uSsk29goXG_qrk0ZOb-f-y9Y-C9dSA.I_pGHsjw3Ho1FeBK) and [Tuesday 11/10](https://csbsju.zoom.us/rec/share/Rnmh2cErMoyRgkLraAuHUqcLcjD8SWeSXCZjLqXqHKtjsocukZS071jwlqv4IkWp.x4643r67uUbDRDFI).

To complete this program, you need to uncomment lines 176--215 and make the
consistent with the parallelization strategy begun in the activity. Some things
you will need to do:
  1. Adjust the calculation of distances so that each process is only computing
     the distances for which it is responsible.
  1. After completing their distance calculations, each process should send
     their distances back to rank 0, which will collect all of the results, sort
     them, and make a prediction. In other words, the code from `qsort()` onward
     should only be executed by rank 0.

# Testing
Test your program for correctness by checking to see that it makes the same
prediction in your new parallel version of the code that it did when run in
serial on the original version of the code. Remember, you can access the
original version of the code via the Git tag [`part-8`](https://github.com/CSBSJU/CSCI-351-machine-learning/tree/part-8) in this [repository](https://github.com/CSBSJU/CSCI-351-machine-learning.git).

# Submission
On Canvas, you need to submit a link to the GitHub repository containing your
solution.
