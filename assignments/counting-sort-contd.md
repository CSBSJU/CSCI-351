---
title: "Counting sort in OpenMP cont'd"
---

# Instructions
Correct the parallelization of the program provided in [this](https://gist.github.com/cae93e5840c7d3cc9cda07e0e00ccd95.git) Git repository using OpenMP. The
first and third loops have been parallellized. However, the results are
incorrect. You need to adjust the second loop so that it correctly computes each
thread's starting into the output array for each of the input values.

For more information about the parallelization strategy which led to incorrect
results, see the Zoom recording for [Friday 11/6](https://csbsju.zoom.us/rec/share/on-d5fCyYxADIc9IjKPd31qdw75iRHqBrTU9moFjetl9m477L5qB334X3vX7ogED.8yydi5-_nqY2lmWX)

# Experimental analysis
The program itself is parameterized on three different values: threads, input
size, and number of unique keys. Let's fix the number of keys at 2<sup>15</sup>
and focus on experimenting with the program by varying the number of threads and
the input size.

You should execute your program for thread counts: 1, 2, 4, and 8. Since we are
going up to 8 threads, I highly recommend running this code on the hpc\*
machines, which all have at least 8 threads.

For each thread count, you should execute your code for input sizes: all powers
of 2 from 2<sup>16</sup> up to and including 2<sup>26</sup>.

This would make a grand total of 44 different experiments. Remember that each
experiment should be executed multiple times and the minimum execution time
should be reported.

Collect your results in a table, then make a graph showing the execution times.
The x-axis should be the input size, the y-axis the execution time, and there
should be four lines on the graph, representing each of the four thread counts.

# Tips & tricks
Since there are only 9 hpc machines, and at any given point in time, a few of
them may be down, you will need to take turns on the machines. There is no limit
on how many of you can be logged in to the machines at a time, but if you all
run your experiments at the same time, you will be competing for the
computational resources of the machines. To avoid this, before running your
experiment, check to see that nobody else is running theirs as well. The easiest
way to do this is the program `top`. In a terminal which is connected to the hpc
machine on which you would like to run your program, type `top`. This will list
all processes running on that machine. If you see that there is a process using
a significant amount of the CPU, then it would be a good idea for you to wait or
find another machine to execute your code on.

# Submission
On Canvas, you need to submit a short report (PDF format) including the
following:
   * The source code for the second loop in the program.
   * A brief explanation of how your changes address the problems raised by the
     strategy used to parallelize the first and third loops.
   * A table of execution times, reporting only the minimum time for each
     experiment.
   * A graph summarizing the table, as explained above.

Upload the PDF document to Canvas.
