---
layout: post
title: "Turing Machine"
date: 2020-11-01
tags: ['complexity']
comments: false
# Does not change and does not remove 'script' variable.
script: [post.js]
---

# Turing Machine -- The Computation Model

## Turing Machine

- Single-Tape Turing Machine: a quadruple $$M = (K, \Sigma, \delta, s)$$
-- $$K$$: a finite set of states.
-- $$s \in K$$: initial state.
-- $$\Sigma$$: A finite set of symbols, includes $$\bigsqcup$$(Blank symbol) and $$\triangleright$$ (first symbol).
-- $$\delta$$: $$K \times \Sigma \to (K \cup \{h, yes,no\}) \times \Sigma \times \{\leftarrow, \rightarrow, -\}$$
-- Note that the cursor never falls off the left end of the string.

- The halting of a turing machine
-- "yes": $$M$$ accepts the input $$x$$, and $$M(x) = "yes"$$.
-- "no": $$M$$ rejects the input $$x$$, and $$M(x)="no"$$
-- $$h$$: $$M(x)=y$$ means the string consists of a $$\triangleright$$.
-- If $$M$$ never halts on $$x$$, then we write $$M(x)=\nearrow$$

- Multiple Strings Turing Machine: a quadrupe $$M = (K, \Sigma, \delta, s)$$
-- $$\delta$$: $$K \times \Sigma^k \to (K \cup \{h, yes,no\}) \times (\Sigma \times \{\leftarrow, \rightarrow, -\})^k$$
-- All strings are started with $$\triangleright$$.
-- The first string is the input and $$k$$th string is the output.

- Nondeterministic Turing machine: a quadrupe $$N=(K, \Sigma, \Delta, s)$$.
-- $$\Delta$$ is a relation, not a function anymore, there may be multiple next steps.  

## Languages

- We let $$L \subseteq (\Sigma - \{\bigsqcup\})^*$$  be a language.  
- Recursive and decidable: For a language $$L$$, if there exists a turing machine such that:  
-- if $$x \in L$$, then $$M(x)="yes"$$  
-- if $$x \notin L$$, then $$M(x)="no"$$
We will say $$M$$ decides $$L$$ and $$L$$ is recursive and decidable.

- Recursively enumerable or semidecidable: For a language $L$, if there exists a turing machine such that:  
-- if $$x \in L$$, then $$M(x)="yes"$$  
-- if $$x \notin L$$, then $$M(x)="\nearrow"$$
We will say $$M$$ accepts $$L$$ and $$L$$ is recursively enumerable and semidecidable.

Suppose $$M$$ is a turing machine accepting $$L$$, then we write $$L(M)=L$$. If $$M(x)=\nearrow$$ for all input, then we have $$L(M)=\varnothing$$.

A property of an RE language can be defined by the set $$C$$ of all RE languages that satisfy it. 
A property is **trivial** if $$C=RE$$ or $$C=\varnothing$$

**Rice Theorem**: Suppose $$C \neq \varnothing$$ is a proper subset of the set of all recursively enumerable languages. Then the question $$L(M) \in C$$ is undecidable.  

## Complexity

- If a turing machine $$M$$ operates within time $$f(n)$$ for $$f: \mathbb{N} \to \mathbb{N}$$ for any input string x, the time required by $$M$$ on x is at most $$f(|x|)$$, note as $$O(f(|x|))$$.
- Time complexity classes: Suppose language $$L \subseteq (\Sigma - \{\bigsqcup\})^*$$ is decided by a multistring TM operating in time $$f(n)$$. Then we say $$L \in TIME(f(n))$$, $$TIME(f(n))$$ is a complexity class.  
- **Linear Speedup Theorem**: Let $$L \in TIME(f(n))$$. Then for any $$\epsilon >0$$, $$L \in TIME(f'(n))$$, where $$f'(n)= \epsilon f(n)+n+2$$
- Linear speed up theorem tells us that any polynomial time bound can be represented by its leading term $$n^k$$ for some $$k \geq 1$$.
- If $$L \in TIME(n^k)$$ for some $$k \in \mathbb{N}$$, it is a polynomial decidable language.  
- If a turing machine can decide $$L$$ in a space bound $$f(n)$$, then we have $$L \in SPACE(f(n))$$
- **P and NP**: Specifically, if a language can be decided by a turing machine in a polynomial time bound, then we call it a **P** problem. If a language can be decided by a nondeterministic turing machine in polynomial time, then we call it an **NP** problem.  We have:  
$$P \subseteq NP$$
- A very important open problem: $P=NP$?

## Undecidability

- If a language can not be decided by a turing machine, then we call it **undecidable**.
- First, we introduce a famous language that can not be decided by turing machines, the **halting problem**.

Given such set:  

$$H = \{M,x | M \text{will halt on input x}\}$$

We assume that $$M_H$$ will decide this language, then we construct the following language:  

```
D(x):
  if M(D, x) halts:
    Run forever.
  else:
    halt
  endif
end
```

Then we find that if we input $$D$$ itself, it will run into contradiction, thus this language is undecidable.  

Moreover, for any language, if we can find a transformation $R$ to a undecidable language, then we can confirm this language is also a undecidable language.  

