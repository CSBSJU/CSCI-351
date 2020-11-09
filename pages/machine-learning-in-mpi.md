---
title: "Machine learning in MPI"
---

# TL;DR
To parallelize the program that was implemented in the activity [Machine learning in C]({{ site.canvas.prefix }}/courses/{{ site.canvas.course }}/pages/machine-learning-in-c) using MPI.

As always, the development of such a system should proceed in steps.

# Instructions
1. In small groups, determine a parallelization strategy for this problem. When
   finished, you should be able to answer the following questions:
   * What work is each process going to be responsible for?
   * How will each process get the data that it needs in order to complete its
     work?
   * Will the processes need to interact at all in order to complete
     computations? If so, how?

   One approach for determining a parallelization strategy would be to consider
   how you would parallelize this code in OpenMP. Once you have determined that,
   you can reason about what data each process will need in order to carry out
   its computations. Then you can figure out how each process will get said data
   as well as what interactions will need to take place among the processes.

1. Next, update the program to implement the steps you outlined in the previous
   part. I highly recommend breaking this step into more steps. For example:
   1. Implement I/O, so that each process has the data that it needs.
   1. Implement local calculations.
   1. ...

1. If you complete the previous two parts, read section 3.4 from the textbook.
   Update your code so that it uses the collective communication operations
   wherever appropriate.
