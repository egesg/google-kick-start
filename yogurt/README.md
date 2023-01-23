# Problem

Yogurt can be a nutritious part of an appetizer, main course, or dessert, but it must be consumed before it expires, and it might expire quickly! 
Moreover, different cups of yogurt might expire on different days.

Lucy loves yogurt, and she has just bought N cups of yogurt, but she is worried that she might not be able to consume all of them before they expire. The i-th cup of yogurt will expire Ai days from today, and a cup of yogurt cannot be consumed on the day it expires, or on any day after that.

As much as Lucy loves yogurt, she can still only consume at most K cups of yogurt each day. What is the largest number of cups of yogurt that she can consume, starting from today?

## Input
The first line of the input gives the number of test cases, T. T test cases follow. Each test case starts with one line containing two integers N and K, as described above. Then, there is one more line with N integers Ai, as described above.

## Output
For each test case, output one line containing Case #x: y, where x is the test case number (starting from 1) and y is the maximum number of cups of yogurt that Lucy can consume, as described above.

## Limits
1 ≤ T ≤ 100.
Time limit: 20 seconds per test set.
Memory limit: 1 GB.
1 ≤ K ≤ N.
1 ≤ Ai ≤ 109, for all i.
Small dataset (Test set 1 - Visible)
1 ≤ N ≤ 1000.
K = 1.
Large dataset (Test set 2 - Hidden)
1 ≤ N ≤ 5000.

# Analysis

Intuitively, if Lucy wants to maximize the amount of yogurt she consumes, she should consume as many cups as possible each day, and always choose a cup that is closest to expiring.

## Small dataset
We can directly implement the above strategy to solve the Small dataset, in which Lucy can only consume one cup per day. On each day, we scan the list for the smallest unselected cup that has not expired, consume it, and remove it from the list. Since we make up to N passes through a list with up to N items, the time complexity is O(N2).

## Large dataset
To improve the above strategy to solve the Large dataset, we can first sort the cups in non-decreasing order of time until expiration. Then, on each day, we remove all expired cups from the beginning of the list and then consume the next K. Since we only handle each cup in the sorted list once, the initial sorting step determines the overall time complexity, which is O(N log N).

But we can do even better! Notice that there are only N cups, and since K ≥ 1, Lucy could consume or discard all of them in at most N days. So any Aj ≥ N can be replaced with N. Then, we can count how may cups will expire on each day, and then proceed backwards from the Nth day to the first day. On each day, Lucy consumes at most K cups, and moves any remaining cups from that day to the previous day, since it is safe to consume them earlier. (Any extra cups left over on day 1 must be discarded.) We make one forward pass through the data to count the cups and one reverse pass to answer the question, so this strategy is O(N).
