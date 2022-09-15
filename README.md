# maximum-subarray-math
Mathematical intuition behind an $O(n)$ time and $O(1)$ extra space solution to the "Maximum Subarray" problem

## The Problem
(Taken from Leetcode)
Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.
A subarray is a congiguous part of an array.

## Building Intuition
Consider this basic Calculus rule: 

$$\int_{a}^{c} f(x) ~dx - \int_{a}^{b} f(x) ~dx = \int_{b}^{c} f(x) ~dx$$

where $a < b < c$.

The **total accumulative** change from $x=a$ to $x=b$ is $\int_{a}^{b} f(x) \,dx$. Similarly, the total accumulation of change from $x=a$ to $x=c$ is $\int_{a}^{c} f(x) \,dx$. Then, since $a < b < c$, subtracting that change from $a$ to $b$ leaves us with to total change from $b$ to $c$.

Let's look at this idea with integers to get a better grasp:

Let $S=\[3, 6, 2, 11, -4, 1\]$. Lets look at the accumulation of change in $S$ (you can think of it as the 'integral' of S). $S_{accum}=\[3, 9, 11, 22, 18, 19\]$. Notice how we are simply adding the current value at each index.

$S_{accum}=\[3\, ~3+6\, ~3+6+2\, ~3+6+2+11\, ~\ldots\]$

That is the accumulation of change. So now, we can see how the same ideas from calculus can be applied here with discretized sequences of integers.

## Generalization

Let $x_0,x_1,\ldots,x_{n-1}$ be the integers in `nums` in the order which they appear in `nums`.

We can compute the accumulation of change as $Sums=\[x_0, ~x_0+x_1, ~\ldots, ~x_0+x_1+\ldots+x_{n-1}\]$.
Now, we must find how to determine the total accumulation of change between $x_a$ and $x_b$ inclusively such that $0 < a < b < n$. We can define this accumulation of change as $$x_a+x_{a+1}+\ldots+x_b=\sum_{i=a}^b x_i$$
We know that $$Sums\[a\]=\sum_{i=0}^a x_i$$ and $$Sums\[b\]=\sum_{i=0}^b x_i$$ Therefore, $$Sums\[b\]-Sums\[a\]=\left[\sum_{i=0}^b x_i\right] - \left[\sum_{i=0}^a x_i\right]=\sum_{i=a+1}^b$$ Notice how our result is the accumulation of change from $x_{a+1}$ to $x_b$ (inclusive)? That's because $Sums[a]$ *includes* $x_a$. Well, if we use that same result and plug in $a-1$ instead for our lower sum, we get $$Sums\[b\]-Sums\[a-1\]=\sum_{i=(a-1)+1}^b=\sum_{i=a}^b$$
Perfect! That is the accumulation of change between $a$ and $b$ inclusively!

If you have a keen eye, however, you might notice that this would not work if $a=0$. In fact, that is why the bounds for $a$ were $0 < a < b$. This is simply because $Sums\[a-1\]$ does not exist. So what do we do in this case? This is a special case, and in fact, our definition of $Sums\[i\]$ for all $0 \leq i < n$ is the total accumulation of change from $x_0$ to $x_b$. $$Sums\[b\]=\sum_{i=0}^b x_i = x_0+x_1+\ldots+x_b$$ Therefore, in the case that $a=0$, our total accumulation of change from $x_a$ to $x_b$ inclusively is $Sums\[b\]$. For simplicity, we will from here on state that $Sums\[m<0\]=0$. That way, even if $a=0$, our previously found property still holds.

Finally, all we have left to do is to use this property to find the maximum subarray of `nums`. Note that this can also be phrased as finding $0 \leq a < b < n$ such that $$\sum_{i=a}^b x_i$$ is the largest.
From the property we just found, we can reword this to finding the $0 \leq a < b < n$ such that $Sums\[b\]-Sums\[a-1\]$ is the largest. Intuitively, it makes sense that when finding these such elements we want to find a $Sums\[a-1\]$ that is as small as possible so that so that we are subtracting as little as possible from our upper bound.
This idea is quite similar to the Largest Profit from Stocks problem, and we can actually solve it in a very similar way. We can go from the beginning to the end of $Sums$ and keep track of the smallest sum and compare it to the current sum. If that difference is the largest that we have seen so far, then it is the largest subarray that we have seen so far. Here is a pseudocode of this idea implemented (I would recommend completing the "Best Time to Buy and Sell Stock" problem in $O(n)$ time first to get a better intuition of what's going on):

```
Sums = [length(nums)]
Sums[0] = nums[0]
min = 0
maxSum = Sums[0]

for i in [1, length(nums)-1]
  Sums[i] = Sums[i-1] + nums[i]
  
  min = min(Sums[i-1], min)
  maxSum = max(Sums[i] - min, maxSum)

return maxSum
```
