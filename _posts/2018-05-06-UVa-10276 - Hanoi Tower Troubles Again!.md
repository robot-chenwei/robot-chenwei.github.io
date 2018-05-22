---
layout: post
title: "UVa 10276 - Hanoi Tower Troubles Again!"
date: 2018-05-06 12:00:00
categories: ACM
tags: ACM

---

* content
{:toc}

## Problem

There is one n-peg Hanoi Tower, we will put the balls (id from 1) on it. The rule is that, each time from the first page, and check if the sum of the last ball id on the peg and the new ball id is a square number. If not, the next peg will be selected and check again, until it succeeds or gets new null pegs.

So, which is the biggest number can be put on the n-peg Hanoi Tower.

## Method

Simulation as the problem and when there are not enough pegs, it comes to over.





## Code

```c++
#include <stdio.h>
#include <math.h>

int pegs[55];

int main()
{
	int t, n;
	while (~scanf("%d", &t)) 
	while (t --) {
		scanf("%d", &n);
		for (int i = 1; i <= n; ++ i) {
			pegs[i] = 0;
		}
		for (int i = 1; ; ++ i) {
			int index = 1, sqrt_v = 0, value = 0;
			while (pegs[index] && index <= n) {
				value = pegs[index] + i;
				sqrt_v = (int)sqrt(value + 0.1);
				if (sqrt_v*sqrt_v == value) {
					pegs[index] = i;
					break;
				}else {
					index++;
				}
			}
			
			if (index > n) {
				printf("%d\n", i-1);
				break;
			}else {
				pegs[index] = i;
			}
		}
	}
	
	return 0;
}    
```
