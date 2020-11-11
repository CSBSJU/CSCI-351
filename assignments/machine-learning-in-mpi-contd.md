---
title: "Machine learning in MPI cont'd"
---

# Instructions
Update the MPI implemention of our rating prediction program completed as part
of the activity [Machine learning in MPI]({{ site.canvas.prefix }}/courses/{{ site.canvas.course }}/pages/machine-learning-in-mpi) to use MPI collective
communications as opposed to point-to-point communications wherever appropriate.
The Git tag [`mpi`](https://github.com/CSBSJU/CSCI-351-machine-learning/tree/mpi) in this [repository](https://github.com/CSBSJU/CSCI-351-machine-learning.git) contains the MPI implementation using only point-to-point communications.

For more information about the point-to-point parallelization strategy, see the Zoom recordings for [Monday 11/9](https://csbsju.zoom.us/rec/share/suJUZmvinidevj1zI1Fwfrj01hT4MQUW3-uSsk29goXG_qrk0ZOb-f-y9Y-C9dSA.I_pGHsjw3Ho1FeBK) and [Tuesday 11/10](#)

# Experimental analysis
The program is parameterized on two different values: MPI processes and number
of viewers. Since this is real-world data, we will not be scaling the input
size. Rather we will perform a *strong scaling* study by fixing the input size
and only adjusting the number of MPI processes. In this case, you should use the
largest data file available.

You should execute your program for MPI process counts: 1, 2, 4, and 8, 16, 32,
64. To do this, it is critical that you use the university hpc\* machines.

Remember that each experiment should be executed multiple times and the minimum
execution time should be reported.

Collect your results in a table, then make a graph showing the execution times.
The x-axis should be the input size, the y-axis the execution time, and there
should be four lines on the graph, representing each of the four thread counts.

# Tips & tricks
Since executions above 8 MPI processes will require the use of multiple
machines, and at any given point in time, a few of them may be down, you will
need to take turns on the machines. There is no limit on how many of you can be
logged in to the machines at a time, but if you all run your experiments at the
same time, you will be competing for the computational resources of the
machines. To avoid this, before running your experiment, check to see that
nobody else is running theirs as well. The easiest way to do this is the program
`top`. In a terminal which is connected to the hpc machine on which you would
like to run your program, type `top`. This will list all processes running on
that machine. If you see that there is a process using a significant amount of
the CPU, then it would be a good idea for you to wait or find another machine to
execute your code on.

# Submission
On Canvas, you need to submit a short report (PDF format) including the
following:
   * The source code for the second loop in the program.
   * A brief description of which point-to-point communications were able to be
     replaced by collective communications.
   * A table of execution times, reporting only the minimum time for each
     experiment.
   * A graph summarizing the table, as explained above.

Upload the PDF document to Canvas.
