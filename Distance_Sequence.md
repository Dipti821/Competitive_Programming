## Problem Statement:

How many integer sequences A=(A1,........,AN) of length N satisfy all the conditions below?

- 1≤Ai≤M (1≤i≤N)
- ∣Ai−A(i+1)∣≥K (1≤i≤N−1)

Since the count can be enormous, find it modulo 998244353.

### Constraints: 

- 2≤N≤1000
- 1≤M≤5000
- 0≤K≤M−1
- All values in input are integers.


### Input:
Input is given from Standard Input in the following format:
N M K

### Output:
Print the count modulo 998244353.

## Approach:

We solve it with Dynamic Programming (DP).

Let dp[i][j] be the number of ways of determining the first i terms of A such that its i-th term is j. The transition of this dp is:

dp[i+1][j]=(dp[i][1]+…+dp[i][j−K])+(dp[i][j+K]+…+dp[i][M]).

Note that the transition is slightly different for 1>j−K or j+K>M. This DP has O(NM) states, and computing each element costs O(M), 

so the overall time complexity is O(NM^2), which does not fit in the time limit.

Instead, we may find the cumulative sum of dp[i] before considering the transitions to dp[i+1], so that each transition can now be

performed in an O(1) time, so that the problem is solved in a total of O(NM) time, which is fast enough.
