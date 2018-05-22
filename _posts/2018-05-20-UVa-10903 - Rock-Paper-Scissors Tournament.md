---
layout: post
title: "UVa 10903 - Rock-Paper-Scissors Tournament"
date: 2018-05-20 22:28:00
categories: ACM
tags: ACM

---

* content
{:toc}

## Problem

There are n people play the Rock-Paper-Scissors game. 

What is the probability of of each people win the game.

## Method

Calculate as the problem said: count the times of each people win and lose (w and l), and the probability is w/(w +l)

If w and l are equal to zero, then output '-'.





## Code

```c++
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int w_count[101];
int l_count[101];
int judger[3][3] = {0, -1, 1,  1, 0, -1,  -1, 1, 0};
int get_id(char buf[])
{
	if (!strcmp(buf, "rock")) {
		return 0;
	}else if (!strcmp(buf, "paper")) {
		return 1;
	}else if (!strcmp(buf, "scissors")) {
		return 2;
	}
	return -1;
}

int main()
{
	int  n, k, p1, p2, m1, m2, cases = 0;
	char buf[10];
	while (~scanf("%d", &n) && n) {
		if (cases ++) {
			printf("\n");
		}
		
		for (int i = 1; i <= n; ++ i) {
			w_count[i] = 0;
			l_count[i] = 0;
		}
		
		scanf("%d", &k);
		int t = k*n*(n-1)/2;
		int size = 0;
		for (int i = 1; i <= t; ++ i) {
			scanf("%d%s", &p1, buf);
			m1 = get_id(buf);
			scanf("%d%s", &p2, buf);
			m2 = get_id(buf);
			if (judger[m1][m2] == 1) {
				w_count[p1] ++;
				l_count[p2] ++;
			}else if (judger[m1][m2] == -1) {
				w_count[p2] ++;
				l_count[p1] ++;
				
			}
		}
		
		for (int i = 1; i <= n; ++ i) {
			if (!w_count[i] && !l_count[i]) {
				printf("-\n");
			}else {
				printf("%.3lf\n", (w_count[i]+0.0)/(w_count[i]+l_count[i]));
			}
		}
	}
	
	return 0;
} 
   
```
{% if page.comments %}
<div id="disqus_thread"></div>
    <script type="text/javascript">
        /* * * CONFIGURATION VARIABLES: EDIT BEFORE PASTING INTO YOUR WEBPAGE * * */
        var disqus_shortname = 'perfectlyrandom'; // required: replace example with your forum shortname
        // var disqus_developer = 1; // Comment out when the site is live
        var disqus_identifier = "{{ page.url }}";

        /* * * DON'T EDIT BELOW THIS LINE * * */
        (function() {
            var dsq = document.createElement('script'); dsq.type = 'text/javascript'; dsq.async = true;
            dsq.src = '//' + disqus_shortname + '.disqus.com/embed.js';
            (document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(dsq);
        })();
    </script>
    <noscript>Please enable JavaScript to view the <a href="http://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
    <a href="http://disqus.com" class="dsq-brlink">comments powered by <span class="logo-disqus">Disqus</span></a>
{% endif %}