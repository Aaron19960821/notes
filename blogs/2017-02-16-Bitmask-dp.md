---
layout: post
title: bitmask dp
tags: [algorithm, ACM/ICPC]
---

The link of essay:
https://github.com/Aaron19960821/icpcarchive/blob/master/essayFromNationTeam/动态规划之状态压缩.pdf

Bitmask is a very important technique to divide a huge problem into smaller ones to ensure they are independent from each other. After reading the essay from Chou Wei on the train, I acquired more understanding of this topic.

## What we have to do
- We have to make sure the definition of the problems.
- We have to know if one situation can transform to another one.(Usually we use bitmask calculation).
- We do not always use binary to represent our problem, other methods is welcomed if it is necessary.
- We use this method when the problem is referring to conbination rather than permutation.
Sample problems in this essay
[poj1185](https://github.com/Aaron19960821/icpcarchive/blob/master/dp/poj1185.cpp)
[poj2411](https://github.com/Aaron19960821/icpcarchive/blob/master/dp/poj2411.cpp)
[poj2441](https://github.com/Aaron19960821/icpcarchive/blob/master/dp/poj2441.cpp)
[poj2663](https://github.com/Aaron19960821/icpcarchive/blob/master/dp/poj2663.cpp)