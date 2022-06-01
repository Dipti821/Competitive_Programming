## Sparse Tables:

### Precomputation:

We will use 2-D array for storing the answers to the precomputed query. st[i][j] will store the answer for the range
[i , i+2^j-1] of length 2^j. The size of 2-D array will be MAXN*(K+1) where MAXN is the largest possible array length
and K>=log(2,MAXN).
  
For arrays with reasonable length (<=10^7), K=25 is a good value.
  
~~~
int st[MAXN][K + 1];
~~~

The range [i,i+2^j-1] of length 2^j splits into the ranges [i , i+2^(j-1)-1] and  [i+2^(j-1) ,i+2^j -1] both of length 2^(j-1),
We can generate table using dp

~~~
for (int i = 0; i < N; i++)
    st[i][0] = f(array[i]);

for (int j = 1; j <= K; j++)
    for (int i = 0; i + (1 << j) <= N; i++)
        st[i][j] = f(st[i][j-1], st[i + (1 << (j - 1))][j - 1]);
~~~

The function f will depend on type of query. For range sum queries it will compute the sum  ,for range minimum queries it will 
compute minimum.
  
## Time Complexity of precomputation
  0(NlogN)
  
  
 ## Range Sum Queries
  
  For this type of query f is f(x,y)=x+y.
  
~~~
  long long st[MAXN][K + 1];

for (int i = 0; i < N; i++)
    st[i][0] = array[i];

for (int j = 1; j <= K; j++)
    for (int i = 0; i + (1 << j) <= N; i++)
        st[i][j] = st[i][j-1] + st[i + (1 << (j - 1))][j - 1];
~~~

To answer the sum query for the range [L,R], we iterate over all powers of two, starting from the biggest one. As soon as a power of two 
2^j is smaller or equal to the length of the range (=R-L+1), we process the first part of the range [L,L+2^j-1] and continue with the remaining range
[L+2^j,R].
  
  ~~~
  long long sum = 0;
for (int j = K; j >= 0; j--) {
    if ((1 << j) <= R - L + 1) {
        sum += st[L][j];
        L += 1 << j;
    }
}
~~~

### Time complexity for a Range Sum Query is O(K)=O(log MAXN)

## Range Minimum Queries(RMQ)

These are the queries where the Sparse Table shines. When computing the minimum of a range, it doesn't matter if we process a value in the range 
 once or twice. Therefore instead of splitting a range into multiple ranges, we can also split the range into only two overlapping ranges with power
of two length. E.g. we can split the range [1,6] into the ranges[1,4] and [3,6] . The range minimum of [1,6] is clearly the same as the minimum of the range minimum of
[1,4] and the range minimum of [3,6]. So we can compute the minimum of the range[L,R]  with:

min(st[L][j], st[R-2^j+1][j])  where j=log2(R-L+1)

  
 ~~~
 int lg[MAXN+1];
lg[1] = 0;
for (int i = 2; i <= MAXN; i++)
    lg[i] = lg[i/2] + 1;

int st[MAXN][K + 1];

for (int i = 0; i < N; i++)
    st[i][0] = array[i];

for (int j = 1; j <= K; j++)
    for (int i = 0; i + (1 << j) <= N; i++)
        st[i][j] = min(st[i][j-1], st[i + (1 << (j - 1))][j - 1]);

int j = lg[R - L + 1];
int minimum = min(st[L][j], st[R - (1 << j) + 1][j]);

~~~

###  Time Complexity: O(1)


## Reference:
- [cp-algo](https://cp-algorithms.com/data_structures/sparse-table.html#range-minimum-queries-rmq)
- [video](https://youtu.be/6VC69SxdO9A)





