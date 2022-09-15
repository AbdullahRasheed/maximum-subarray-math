# maximum-subarray-math
Mathematical intuition behind an O(n) solution to the "Maximum Subarray" problem

## The Problem
(Taken from Leetcode)
Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.
A subarray is a congiguous part of an array.

## Building Intuition
Consider this basic Calculus rule: 

$`\int_{a}^{c} f(x) \,dx - \int_{a}^{b} f(x) \,dx = \int_{b}^{c} f(x) \,dx`$

where $a < b < c$.
