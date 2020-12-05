---
layout: post
title: 一个有意思的DP
tags: [DP, ACM/ICPC]
---

## 题目描述
给定一棵含有 n 个结点的树，结点从 1 标号。你从 1 号结点驾车出发，希望遍历一些关键结点（访问到就好，不需要按照这些关键结点的输入顺序）。每条边有两个权值，c0, c1 分别表示步行和驾车经过这条边的代价。每次你可以选择驾车经过一条边（当且仅当有车），或者将车停放在当前所在的结点（如果有车），步行经过一条边。

求遍历完所有关键结点的最少代价。

注意: 你可以在任意结点结束遍历，即使当前没有车。

## 解题思路
在这里说句实话，这道题我从看开始到今天解决这个问题，一共用了大半年的时间。不过今天终于是解决了。看来今天晚上可以睡个好觉了。

首先是划分子问题，这里对一棵子树的遍历可以采用5种方式，走路遍历且回来,开车遍历且回来,走路遍历不一定回来,开车遍历人一定回来但是车不一定回来,开车遍历人和车都不一定回来。
走路遍历且回来和开车遍历且回来这两种十分简单：

$$t=min(2∗w0(cur,dest)+dp[dest][0],2∗w1(cur,dest)+dp[dest][1])$$  
$$dp[cur][0]=2∗w0(cur,dest)+dp[dest][0]$$  
$$dp[cur][1]=∑_1^nti$$

3.下面看一看这几种情况：
首先是走路去但是不一定回来，这个问题还是比较好解决的，就是挑选一棵子树只是去遍历但是不回来，公式如下：

$$dp[cur][2]=dp[cur][0]+min(dp[dest][2]−dp[dest][0]−w0(cur,dest))$$ 

然后就是开车去而车不一定回来，这个也是比较简单的，就是存在一个替换就好了：

$$dp[cur][3]=dp[cur][1]+min(w0(cur,dest)+w1(cur,dest)+dp[dest][3]−t)$$  

最后一个问题就不是那么简单的了，开车去但是人和车都不一定回来。我们需要分两种情况进行讨论，一种是遍历到最后一棵子树的时候还有车，请注意，这个时候我们也不一定必须要用车，走路也是可以的呀，所以，我们得到下面的公式：

$$case41=min(min(w0(cur,dest)+dp[dest][2],w1(cur,dest)+dp[dest][4]))$$

下面一种情况就比较复杂了,就是车最后所在的位置和人不在同一棵子树当中，我们这个时候使用贪心的思维:  

找出$min(dp[dest][3]+w0(cur,dest)+w1(cur,dest)−t,0)$  
找出$min(dp[dest][2]+w0(cur,dest)−t,0)$  

但是，两个所代表的点又可能是相同的点，所以我们需要找的是前两个最小的数来解决这个问题。
最后一点，如果这棵子树当中不存在关键节点，那么我们没有必要对其进行动态规划操作，所以可以事先使用一个DFS遍历剪枝。  

## Code
```c++
#include<iostream>
#include<cstdio>
#include<cstring>
#include<algorithm>
#include<vector>
using namespace std;
#define MAXN 1000005
#define INF 0x3f3f3f3f
#define LL long long
struct Edge{
LL c0,c1;
int to;
int next;
}EdgeTable[2*MAXN];
int isEssiential[MAXN];
int n,m;
int numOfEss[MAXN];
LL dp[MAXN][5];
int head[MAXN];
int e;
void addEdge(int u,int v,LL c0,LL c1)
{
	EdgeTable[e].to = v;
	EdgeTable[e].next = head[u];
	EdgeTable[e].c0 = c0;
	EdgeTable[e].c1 = c1;
	head[u] = e++;
}
void Dfs1(int fa,int cur)
{//to cut off the subtree that has no important nodes
	if(isEssiential[cur])numOfEss[cur]=1;
	int i;
	for(i=head[cur];i!=-1;i=EdgeTable[i].next){
		int dest = EdgeTable[i].to;
		if(dest!=fa){
			Dfs1(cur,dest);
			numOfEss[cur] += numOfEss[dest];
		}
	}
	return;
}
void Dfs2(int fa,int cur)
{
	if(numOfEss[cur]==0 || (numOfEss[cur]==1 && isEssiential[cur]))return;
	int i;
	LL tmp1=0,tmp2=0,tmp3=0,tmp4=0;
	LL tf1=INF,tf2=INF,te1=INF,te2=INF,matche=-1,matchf=-1;
	//find the first two smallest number
	for(i=head[cur];i!=-1;i=EdgeTable[i].next){
		int dest = EdgeTable[i].to;
		if(dest!=fa && numOfEss[dest]>0){
			Dfs2(cur,dest);
			LL t = min(2*EdgeTable[i].c0+dp[dest][0],2*EdgeTable[i].c1+dp[dest][1]);
			dp[cur][0] += 2*EdgeTable[i].c0+dp[dest][0];
			dp[cur][1] += t;
			tmp1 = min(tmp1,EdgeTable[i].c0+EdgeTable[i].c1+dp[dest][3]-t);
			tmp2 = min(tmp2,dp[dest][2]-dp[dest][0]-EdgeTable[i].c0);
			tmp3 = min(tmp3,min(EdgeTable[i].c1+dp[dest][4],EdgeTable[i].c0+dp[dest][2])-t);
		LL ti = EdgeTable[i].c0+EdgeTable[i].c1+dp[dest][3]-t;
		if(ti<tf1){
			tf2 = tf1;
			tf1 = ti;
			matchf = i;
		}
		else if(ti<tf2)
			tf2 = ti;
		ti = EdgeTable[i].c0+dp[dest][2]-t;
		if(ti<te1){
			te2 = te1;
			te1 = ti;
			matche = i;
		}
		else if(ti<te2)
			te2 = ti;
	}
}
	if(matche!=-1 && matchf !=-1){
	if(matche != matchf)
		tmp4 = tf1 + te1;
	else
		tmp4 = min(tf1+te2,tf2+te1);
	}
	dp[cur][2] = dp[cur][0]+tmp2;
	dp[cur][3] = dp[cur][1]+min(tmp1,(LL)0);
	dp[cur][4] = dp[cur][1]+min(tmp4,tmp3);
	dp[cur][4] = min(dp[cur][4],dp[cur][3]);
	return;
}
int main()
{
	freopen("input","r",stdin);
	int i;
	int tmp1,tmp2;
	LL tmp3,tmp4;
	memset(head,-1,sizeof(head));
	memset(isEssiential,0,sizeof(isEssiential));
	e = 0;
	scanf("%d",&n);
	for(i=0;i<n-1;i++){
		scanf("%d%d%lld%lld",&tmp1,&tmp2,&tmp3,&tmp4);
		addEdge(tmp1,tmp2,tmp3,tmp4);
		addEdge(tmp2,tmp1,tmp3,tmp4);
	}
	scanf("%d",&m);
	for(i=0;i<m;i++){
		scanf("%d",&tmp1);
		isEssiential[tmp1]=1;
	}
	Dfs1(-1,1);
	Dfs2(-1,1);
	printf("%lld\n",min(dp[1][4],dp[1][2]));
	return 0;
}
```