---
layout: post
title: "UVa 11629 - Ballot evaluation"
date: 2018-05-22 10:36:00
categories: ACM
tags: ACM

---

* content
{:toc}

## Problem

There are p variables, ecah one has a float value. And there are g guesses, ecah one is combined with the sum of variables and a comparison with a float value. Judger if the expression is correct.

What is the probability of win of each people.




## Method

Using map save the values of the variables, calculating the expression and comparing.

## Code

```c++
#include <cstdio>
#include <cstdlib>
#include <cstring>
#include <cmath>
#include <iostream>
#include <algorithm>
#include <map>

using namespace std;

int main()
{
	int p, g;
	char buf[22];
	double value, guess;
	map <string, double> ballot;
	while (~scanf("%d%d", &p, &g)) {
		ballot.clear();
		for (int i = 1; i <= p; ++ i) {
			scanf("%s%lf", buf, &value);
			ballot[buf] = value;
		}
		
		for (int i = 1; i <= g; ++ i) {
			scanf("%s", buf);
			double ans = ballot[buf];
			scanf("%s", buf);
			while (!strcmp("+", buf)) {
				 scanf("%s", buf);
				 ans += ballot[buf];
				 scanf("%s", buf);
			}
			
			scanf("%lf", &guess);
			int flag = 0;
			if (!strcmp("<", buf)) {
				flag = (ans+0.001 < guess);
			}else if (!strcmp(">", buf)) {
				flag = (ans-0.001 > guess);
			}else if (!strcmp("<=", buf)) {
				flag = (ans-0.001 <= guess);
			}else if (!strcmp(">=", buf)) {
				flag = (ans+0.001 >= guess);
			}else if (!strcmp("=", buf)) {
				flag = (fabs(ans - guess) < 0.01);
			}
			
			printf("Guess #%d was ", i);
			if (flag) {
				printf("correct.\n");
			}else {
				printf("incorrect.\n");
			}
		}
	}
	
	return 0;
}
   
```
