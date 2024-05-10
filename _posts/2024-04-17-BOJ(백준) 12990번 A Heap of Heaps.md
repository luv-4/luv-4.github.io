---
title: "BOJ(백준) 12990번 A Heap of Heaps"
excerpt: "ㅤ"
header:
  overlay_image: https://onlinejudgeimages.s3-ap-northeast-1.amazonaws.com/images/boj-og.png
  overlay_filter: linear-gradient(to right, rgba(0, 0, 0, 0.9) 25%, rgba(0, 0, 0, 0))
  teaser: https://onlinejudgeimages.s3-ap-northeast-1.amazonaws.com/images/boj-og.png
categories:
  - Baekjoon
tags:
  - [Dev]

toc: true
toc_sticky: true

date: 2024-04-17
last_modified_at: 2024-04-17
---

<https://www.acmicpc.net/problem/12990>


문제 풀이 아이디어 자체는 상당히 단순한 편이다.

1 ~ N-1진 힙 각각에 대해서 각각의 노드의 자식들 중에 값이 자신보다 작은 자식의 개수를 세어 더한 뒤 출력해주면 된다.

우선 문제를 살펴보면 어떤 노드의 자식 노드들은 연속한다는 것을 알 수 있다.

또한 k진 힙에서 i번째 노드의 자식 노드의 구간이 2+(i-1)*k ~ 1+i*k이라는 것도 확인할 수 있다.

이제 구간에서 특정 값 이하의 개수를 세야 되므로 머지 소트 트리를 사용하면 각 쿼리를 O(logN)에 처리가 가능하다. 

만약에 범위의 끝이 N보다 크면 끝을 N으로 계산하고 범위의 시작점이 N보다 크면 반복문을 끝낸다.

하지만 문제가 있다. 위는 2중 반복문으로 O(logN)의 쿼리를 처리하는 방식이므로 O(N^2logN)이 되어 tle가 나오지 않을까? 그래서 연산이 일어나는 횟수를 좀 더 자세히 계산해보았다.

k진 힙에서 쿼리가 몇번 필요한지 생각해보면 2~N의 구간을 k로 나눈만큼 쿼리가 발생하므로 대략 N/k만큼 쿼리가 필요하다.

그런데 0 < k < N이므로 쿼리의 개수는 약 N*(1/1 + 1/2 + 1/3 + ... + 1/N)이다. 

결국 (1/1 + 1/2 + 1/3 + ... + 1/N)의 값이 중요해지는데 수학 비전공자의 지식으로 보기에 대학 수학에서 봤던 p급수인가..?하는 생각이 들어 찾아보니 p급수는 아니고 조화수라는 것이었다.

<div style="text-align : center;"><img style="width: 50%;" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FFsN1h%2FbtsEFRpKKJh%2Fs17R1Yl51PkVhhtCfTkCrk%2Fimg.png"/></div>
<br/>

그리고 이 수열의 합은 일반적인 공식으로는 표현하기는 쉽지 않지만 ln(n)으로 근사가 가능하다.

<div style="text-align : center;"><img style="width: 50%;" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FsAUEp%2FbtsEGMVR99E%2Ft4k747WSklHFYK0wsqMD5k%2Fimg.png"/></div>
<br/>
이유는 위와 같이 1/x의 적분이 ln(x)이기 때문이다.

따라서 N*(1/1 + 1/2 + 1/3 + ... + 1/N)은 NlnN으로 근사가 가능하고, 쿼리의 개수가 NlnN이므로 시간복잡도는 O(N(logN)^2)이 되어 AC를 받을 수 있다.

AC code
```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
int N;
vector<vector<ll>> mtree;
vector<ll> arr;
 
vector<ll>& minit(int node,int start,int end) {
	if(start==end) return mtree[node]={arr[start]};
	int mid=(start+end)/2;
	auto l=minit(node*2,start,mid),r=minit(node*2+1,mid+1,end);
	mtree[node].resize(l.size()+r.size());
	merge(l.begin(),l.end(),r.begin(),r.end(),mtree[node].begin());
	return mtree[node];
}

ll mquery(int node,int start,int end,int left,int right,int val) {
	if(left>end||right<start) return 0;
	if(left<=start&&right>=end) return lower_bound(mtree[node].begin(),mtree[node].end(),val)-mtree[node].begin();
	int mid=(start+end)/2;
	return mquery(node*2,start,mid,left,right,val)+mquery(node*2+1,mid+1,end,left,right,val);
}


int main() {
	ios::sync_with_stdio(0);
	cin.tie(0);
	cout.tie(0);
	cin>>N;
	mtree.resize(4*N+1);
	arr.resize(N+1);
	for(int i=1;i<=N;i++) cin>>arr[i];
	minit(1,1,N);
	for(int k=1;k<N;k++) {
		int sol=0;
		for(int i=1;2+(i-1)*k<=N;i++) sol+=mquery(1,1,N,2+(i-1)*k,1+i*k>N?N:1+i*k,arr[i]);
		cout<<sol<<" ";
	}
}
```

뜬금없이 오랜만에 수학 공부를 하게 됐지만 괜찮은 경험이었던 거 같다.
