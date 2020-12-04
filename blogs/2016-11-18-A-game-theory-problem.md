---
layout: post
title: 一个有意思的博弈
tags: [game theory, acm/icpc]
---

## 题目描述
有两个人玩游戏，轮流取物品。每个物品对不同的人都会存在不同的价值。对手使用的贪心原则，也就是说在每一步对手都会选择对他价格最大的物品。当存在多个物品价格相同的时候，对手会随机选择一个物品。这个时候问我们可以最多得到多大的结果。

## 解题过程
咋一看，这是个明显贪心过程，我们按照两个关键字排序之后对两个人都采用贪心策略模拟就可以了。但是，事实上，这样做是不对的。因为A要取的物品也可能是对B很重要的物品，而B正在取的物品则对A没有那么重要，推迟一些取也是可以的。那么，到底怎么做呢？
我做出了一个比较强的结论：在使用了两个关键字排序之后，对于任意的i<n,我们都知道在前i个物品中A至少会取得i/2个物品。
证明：

1. 前i个物品至少需要i/2轮才可以取完。
这个完全不需要证明，每轮两个人各取1个物品，最快取完需要i/2轮
2. 我们按照A的逻辑顺序排序，所以A总是会取价值最大的元素，也就是标号较小的元素,即在前i/2轮，A一定不会取标号大于i的物品。
我们证明了这样的定理。
那么也就是说，在前i个物品中，我们最多取i/2个。
这样，就可以得到下面的转移方程：

$$dp[i][j]=max(dp[i−1][j],dp[i−1][j−1]+Brr[i]),for j < i/2$$  

迭代，就可以得到解

```c++
#include<iostream>
#include<cstdio>
#include<cstring>
#include<algorithm>
#include<utility>

using namespace std;
#define LL long long
#define MAXN 1005
#define pi pair<LL,LL>

LL dp[MAXN][MAXN];
int t,n;
pair<LL,LL>P[MAXN];
bool comp(pi a,pi b)
{
	if(a.first==b.first)return a.second>b.second;
	else return a.first>b.first;
}
int main()
{
	freopen("input","r",stdin);
	int i,j;
	scanf("%d",&t);
	while(t--){
		scanf("%d",&n);
		memset(dp,0,sizeof(dp));
		for(i=1;i<=n;i++){
			scanf("%lld",&P[i].first);
		}
		for(i=1;i<=n;i++){
			scanf("%lld",&P[i].second);
		}
		sort(P+1,P+n+1,comp);
		for(i=1;i<=n;i++){
			for(j=1;j<=i/2;j++)
				dp[i][j] = max(dp[i-1][j],dp[i-1][j-1]+P[i].second);
		}
		printf("%lld\n",dp[n][n/2]);
	}
	return 0;
}
```
