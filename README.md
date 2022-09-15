# maximum-subarray-math
Mathematical intuition behind an O(n) solution to the "Maximum Subarray" problem

## The Problem
(Taken from Leetcode)
Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.
A subarray is a congiguous part of an array.

## Building Intuition
Consider this basic Calculus rule: 

$$\int_{a}^{c} f(x) \,dx - \int_{a}^{b} f(x) \,dx = \int_{b}^{c} f(x) \,dx$$

where $a < b < c$.

The **total accumulative** change from $x=a$ to $x=b$ is $\int_{a}^{b} f(x) \,dx$. Similarly, the total accumulation of change from $x=a$ to $x=c$ is $\int_{a}^{c} f(x) \,dx$. Then, since $a < b < c$, subtracting that change from $a$ to $b$ leaves us with to total change from $b$ to $c$.

Let's look at this idea with integers to get a better grasp:

Let $S=\[3, 6, 2, 11, -4, 1\]$ and $S_0, S_1, \ldots , S_5$ be the integers in S in order of their appearance in the sequence. Now lets look at the accumulation of change in $S$ (you can think of it as the 'integral' of S). $S_{accum}=\[3, 9, 11, 22, 18, 19\]$. Notice how we are simply adding the current value at each index.

$S_{accum}=\[3\, ~3+6\, ~3+6+2\, ~3+6+2+4\, ~\ldots\]$

That is the accumulation of change. So now, we can see how the same ideas from calculus can be applied here with discretized sequences of integers.

## Generalization

Let $x_0,x_1,\ldots,x_{n-1}$ be the integers in `nums` in the order which they appear in `nums`.

We can compute the accumulation of change as $Sums=\[x_0, ~x_0+x_1, ~\ldots, ~x_0+x_1+\ldots+x_{n-1}\]$.
Now, we must find how to determine the total accumulation of change between $x_a$ and $x_b$ inclusively such that $0 < a < b < n$. We can define this accumulation of change as $x_a+x_{a+1}+\ldots+x_b=\sum_{i=a}^b x_i$.
We know that $Sums\[a\]=\sum_{i=0}^a x_i$ and $Sums\[b\]=\sum_{i=0}^b x_i$. Therefore, $Sums\[b\]-Sums\[a\]=\left[\sum_{i=0}^b x_i\right] - \left[\sum_{i=0}^a x_i\right]=\sum_{i=a+1}^b$. Notice how our result is the accumulation of change from $x_{a+1}$ to $x_b$ (inclusive)? That's because $Sums[a]$ *includes* $x_a$. Well, if we use that same result and add 1 to our lower sum, we get $Sums\[b\]-Sums\[a-1\]=\sum_{i=(a-1)+1}^b=\sum_{i=a}^b$.
Perfect! That is the accumulation of change between $a$ and $b$ inclusively!
