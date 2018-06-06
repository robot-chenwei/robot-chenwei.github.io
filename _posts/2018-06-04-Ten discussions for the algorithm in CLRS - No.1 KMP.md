---
layout: post
title: "Ten discussions for the algorithm in CLRS - No.1 KMP"
date: 2018-06-05 22:00:00
categories: algorithm 
tags: KMP
mathjax: true
---

* content
{:toc}

## 1 Background

### 1.1 String Matching

Text-editing programs frequently need to find all occurrences of a pattern in the text. Efficient algorithms for this problem - called "String Matching" - can greatly aid the responsiveness of the text-editing program.
Among their many other applications, string-matching algorithms search for particular patterns in DNA sequences. Internet search engines also use them to find Web pages relevant to queries.

### 1.2 Formula Symbol





The string-matching problem is formalized as follows. We assume that the text is an array T[1..n] of length n and that the pattern is an array P[1..m] of length m $\le$ n. We further assume that the elements of P and T are characters drawn from a finite alphabet $\Sigma$. For example, we may have $\Sigma = \{0, 1\}$ or $\Sigma = \{a, b, .., z\}$. The character arrays P and T are often called strings of characters.
The concatenation of two strings x and y denoted xy, has length |x|+|y| and consists of the characters from x followed by the characters from y.
We say that a string w is a prefix of a string x, denoted w $\sqsubset$ x, if x = wy for some string y. Similarly. we say that a string w is a suffix of a string x, denoted w $\sqsupset$ x, if x = yw for some y.

### 1.3 Basic Algorithm

Algorithm | Preprocessing time | Matching time
-|---
Naive | 0 | $O$((n-m+1)m)
Rabin-Karp | $\Theta$(m) | $O$((n-m+1)m)
Finite automation | $O$(m\|$\Sigma$\|) | $\Theta$(n)
Knuth-Morris-Pratt | $\Theta$(m) | $\Theta$(n)
The Naive algorithm is using a loop that checks the condition P[1..m] = T[s+1..s+m] for each of the valide value of s.
The Rabin-Karp is a method that translates T to string into a number array, whose value is the remainder of the continues five (or another length) items from that item divided by D. So the precondition of match is that the remainder is matched.
![Rabin-Karp](https://img-blog.csdn.net/20180604183255935?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L21vYml1c19zdHJpcA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
And the Finite automation method is to build a finite automaton that scans the text string T for all occurrences of the pattern P.
![Finite Automation](https://img-blog.csdn.net/20180604183347564?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L21vYml1c19zdHJpcA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
The KMP algorithm is a linear-time string-matching algorithm due to Knuth Morris, and Pratt.

## 2 Algorithm

### 2.1 Prefix function
The prefix function $\pi$ for a pattern encapsulates knowledge about how the pattern matches against shifts of itself.
$\pi[q] = max\{k: k \small q \quad and \quad P_{k}  \sqsupset P_{q}\}$
example:
![Prefix](https://img-blog.csdn.net/20180605174142504?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L21vYml1c19zdHJpcA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

### 2.2 Algorithmic process

```c++
KMP-MATCHER(T, P)
    n = T.length				
    m = P.length				
    π = COMPUTE-PREFIX-FUNCTION(P)
    q = 0					        // numnber of characters matched
	for i = 0 to n			        // scan the text from left to right
    	while q > 0 and P[q+1] ≠ T[i]
    	    q = π[q]                // next character does not match
    	if P[q+1] == T[i]
    	    q = q + 1				// next character matches
    	if q == m				    // is all of P matched?
    	    print "Pattern occurs with shift" i - m
    	    q = π[q]				// look for the next match
```

```c++
COMPUTE-PREFIX-FUNCTION(P)
    m = P.length				
    let π[1..m] be a new array
    π[1] = 0
    q = 0					        // numnber of characters matched
	for i = 2 to m			        // scan the text from left to right
    	while q > 0 and P[q+1] ≠ P[i]
    	    q = π[q]                // next character does not match
    	if P[q+1] == P[i]
    	    q = q + 1				// next character matches
    	π[i] = q
    return π
```

The two procedures have much in common, because both match a string against the pattern P. KMP-MATCHER matches the text T against P, and the COMPUTE-PREFIX-FUNCTION matches P against itself.

### 2.3 Analysis

The running time of COMPUTE-PREFIX-FUNCTION(P) as the same as KMP-MATCHER(T, P).
The only tricky part of COMPUTE-PREFIX-FUNCTION(P) is the while loop. 
The total increase of k is at most m-1. And the k cannot decrease to negative.
So the while loop makes at most m-1 iterations and the COMPUTE-PREFIX-FUNCTION(P) runs in time $\Theta$(m).

## 3 Proof

### 3.1 Brief Proof of COMPUTE-PREFIX-FUNCTION

First, it corrects when k = 0 and q = 1, and we suppose that it corrects when k = k and q = q.
Then $\pi$[q+1] = k+1, if P[k+1] == P[q+1]. Else $\pi$[q+1] = $\pi$[..$\pi$[k]..]+1, when P[$\pi$[..$\pi$[k]..]+1] == P[q+1].
So $\pi[q+1] = max\{k: k < q \quad and \quad P_{k+1} \sqsupset P_{q+1}\}$ corrects.

### 3.2 Proff of KMP-MATCHER

Suppose to the contrary that the algorithm is incorrect.
So there is a substring miss-match and it dues to the prefix function.
So $\pi[q] = max\{k: k \small q \quad and \quad P_{k}  \sqsupset P_{q}\}$ does not follow the definition, which is in contradiction with the above proof of COMPUTE-PREFIX-FUNCTION.
The assumption is not set up and KMP-MATCHER is correct.

## Conference

《Introduction to Algorithms》 the 3rd edition

