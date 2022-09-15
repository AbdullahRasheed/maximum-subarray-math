# maximum-subarray-math
Mathematical intuition behind an O(n) solution to the "Maximum Subarray" problem

## The Problem
(Taken from Leetcode)
Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.
A subarray is a congiguous part of an array.

## Building Intuition
Consider this basic Calculus rule: 

$\int_{a}^{c} f(x) \,dx - \int_{a}^{b} f(x) \,dx = \int_{b}^{c} f(x) \,dx$

where $a < b < c$.

The **total accumulative** change from $x=a$ to $x=b$ is $\int_{a}^{b} f(x) \,dx$. Similarly, the total accumulation of change from $x=a$ to $x=c$ is $\int_{a}^{c} f(x) \,dx$. Then, since $a < b < c$, subtracting that change from $a$ to $b$ leaves us with to total change from $b$ to $c$.

Let's look at this idea with integers to get a better grasp:

Let $S=\[3, 6, 2, 11, -4, 1\]$ and $S_0, S_1, \ldots , S_5$ be the integers in S in order of their appearance in the sequence. Now lets look at the accumulation of change in $S$ (you can think of it as the 'integral' of S). $S_{accum}=\[3, 9, 11, 22, 18, 19\]$. Notice how we are simply adding the current value at each index.

$S_{accum}=\[3\, 3+6\, 3+6+2\, 3+6+2+4\, \ldots\]$

That is the accumulation of change. So now, we can see how the same ideas from calculus can be applied here with discretized sequences of integers.

## Generalization

