---
layout: post
title: Suffix Array
tags: [Algorithm, ACM/ICPC]
---

## 基本概念
在了解后缀数组之前，很显然我们需要了解一些基本的概念。
字符集：构造了一个全序的关系，即集合里面的元素要么是大于关系要么是小于关系。
子串：记为$S[i..j]$,表示字符串第i个字符到j-1个字符的子序列
后缀：记为$Suffix(i)$,表示从第i个字符到结尾的子串。
后缀数组：将S的n个后缀经过排序之后得到的数组。(以开头位置代替了实际的后缀)
名次数组：就是后缀数组的反函数,$rank[i]$的意思就是$Suffix(i)$的排序。

构造方法
很显然，我们可以使用暴力排序的方法来解决，但是那样的复杂度就会相当的高，最少也是$O(n^2)$,但是，我们在这里还是可以使用二分的思想来解决构造的问题。
算法如下所示：

1. 首先我们对单个字符进行排序，得到一个序列。
2. 其次，我们以第一关键字为$rank[i]$,第二关键字为$rank[i+l]$对字符串再次进行排序。其中l从1开始使用倍增的策略。在这里，我们很显然可以采用基数排序来解决这个问题。

```c++
memset(cntA,0,sizeof(cntA));
for(i=1;i<=n;i++)cntA[arr[i]]++;
for(i=1;i<=n;i++)cntA[i] += cntA[i-1];
for(i=n;i>=1;i--)sa[cntA[arr[i]]--] = i;
ranki[sa[1]] = 1;
for(i=2;i<=n;i++){
  ranki[sa[i]] = ranki[sa[i-1]];
  if(arr[sa[i]]!=arr[sa[i-1]])
  ranki[sa[i]]++;
}
for(l=1;ranki[sa[n]]<n;l<<=1){
  memset(cntA,0,sizeof(cntA));
  memset(cntB,0,sizeof(cntB));
  for(i=1;i<=n;i++){
    cntA[A[i]=ranki[i]]++;
    cntB[B[i]=(i+l)<=n?ranki[i+l]:0]++;
}
for(i=1;i<=n;i++)cntB[i] += cntB[i-1];
for(i=n;i>=1;i--)tsa[cntB[B[i]]--] = i;
for(i=1;i<=n;i++)cntA[i] += cntA[i-1];
for(i=n;i>=1;i--)sa[cntA[A[tsa[i]]]--] = tsa[i];
ranki[sa[1]] = 1; 
for(i=2;i<=n;i++){
    ranki[sa[i]] = ranki[sa[i-1]];
    if(A[sa[i]]!=A[sa[i-1]]||B[sa[i]]!=B[sa[i-1]])ranki[sa[i]]++;
  }
}
```

## 最长公共前缀
我们在这里定义$LCP(i,j)=maxk|S[sa[i]..sa[i]+k]==S[sa[j]..sa[j]+k]$
在这里，我们需要证明几个定理:

Theorem1
$$LCP(i,k)=min(LCP(i,j),LCP(j,k)),for i<j<k$$
设$p=min(LCP(i,j),LCP(j,k))$
那么$LCP(i,j) \geq ,LCP(j,k)$
那么我们显然可以知道:

$$S[i…i+p]==S[j…j+p],S[i…i+p]==S[k…k+p]$$

我们现在就是要比较3个字符S[i+p+1],S[j+p+1],S[k+p+1]
那么根据我们的定义,如果三者完全相等,那么很显然p\neqLCP(i,j)
所以我们就证明了这样的一个定理。

## Theorem2

$$LCP(i,j)=minLCP(k−1,k)|i+1\leq \leq$$
这个嘛，是可以使用数学归纳法来证明的，就比较简单啦。
那么，我们发现height[i]=LCP(i−1,i)是个很有用的值，可以帮助我们求解最长公共前缀这个问题，但是，问题是我们怎么能够求解这样的一个问题呢？于是，我们又有了下面的一个性质:

Theorem3

$$height[rank[i]] ≥ height[rank[i−1]]−1$$
Proof:
我们在这里设h[i]=height[rank[i]]
那么，当h[i−1]≤1时，显然成立
那么,当h[i−1]>1时，也就是Rank[i−1]>1
令$j=i−1,k=SA[rank[j]−1]$
那么，我们十分显然的可以得到$Suffix(j)>Suffix(k)$
那么我们可以得到下面的结论$lcp(Suffix(k+1),suffix(i))=h[i−1]−1$
而我们也可以知道,$rank[k+1]$

```
for(i=1,j=0;i<=n;i++){ 
  if(ranki[i]==1)height[sa[i]]=0;
  else{
    if(j)j--;
    while(arr[i+j] == arr[sa[ranki[i]-1]+j])j++;
    height[ranki[i]] = j;
  }
}
```

