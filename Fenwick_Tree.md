## BIT (Binary Indexed Tree) functions:

~~~
#include<bits/stdc++.h>
using namespace std;

const int N = 1e5+10;
int bit[N];

void update(int i, int x){
	for(; i < N; i += (i&-i))
		bit[i] += x;
}

int sum(int i){
	int ans = 0;
	for(; i > 0; i -= (i&-i))
		ans += bit[i];
	return ans;
}

int main(){
	
}
~~~

## Question 1:

/*
Question 1 Given array of size N and Q querries
Solve two type of quereies
Type1 : i x : replace ith index by value x
Type 2 : l r : find sum from l to r
Input :
N Q
N elemnts of array
Type i x / Type l r(Q lines)


Example :
5 4
3 4 5 6 3
2 2 4
1 2 6
2 2 4
2 1 5
Output : 
15
17
23


*/

~~~
#include<bits/stdc++.h>
using namespace std;

const int N = 1e5+10;
int bit[N];

void update(int i, int x){
	for(; i < N; i += (i&-i))
		bit[i] += x;
}

int sum(int i){
	int ans = 0;
	for(; i > 0; i -= (i&-i))
		ans += bit[i];
	return ans;
}

int main(){
	int n, q;
	cin >> n >> q;
	int a[n+10];
	for(int i = 1;i <= n; ++i){
		cin >> a[i];
		update(i, a[i]);
	}

	while(q--){
		int type;
		cin >> type;
		if(type == 1){
			int i, x;
			cin >> i >> x;
			update(i, x - a[i]);
			a[i] = x;
		}
		else{
			int l, r;
			cin >> l >> r;
			cout << sum(r) - sum(l-1) << endl;
		}
	}
}
~~~

## Question 2:

/*
Question 2 find inversion count of array
Input :
N
N elemnts of array

Example :
5
8 4 9 2 8
Output : 
5

Large input : 
5
100000000 10000 10000000000 10 100000000
Output : 
5
*/

~~~
#include<bits/stdc++.h>
using namespace std;

const int N = 1e5+10;
int bit[N];

void update(int i, int x){
	for(; i < N; i += (i&-i))
		bit[i] += x;
}

int sum(int i){
	int ans = 0;
	for(; i > 0; i -= (i&-i))
		ans += bit[i];
	return ans;
}

int main(){
	int n;
	cin >> n;
	long long a[n+10];
	map<long long,int> mp;
	for(int i = 1;i <= n; ++i){
		cin >> a[i];
		mp[a[i]];
	}


	// compression of numbers for the case where a[i] > 10 ^ 6
	int ptr = 1;
	for(auto &pr : mp){
		pr.second = ptr++;
	}

	for(int i = 1; i <= n; ++i){
		a[i] = mp[a[i]];
	}

	// Finding Inversion count


	int inversion_ct = 0;
	for(int i = 1; i<= n; ++i){
		inversion_ct += (sum(N-5) - sum(a[i]));
		update(a[i], 1);
	}

	cout << inversion_ct << endl;


}
~~~

## Reference:

You can see this [video](https://youtu.be/DPiY9wFxGIw).
