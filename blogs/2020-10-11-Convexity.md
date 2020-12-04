---
layout: post
title: "Convexity"
date: 2020-10-11
tags: ['Optimization','math']
comments: false
# Does not change and does not remove 'script' variable.
script: [post.js]
---

<!-- Write from here your post !!! -->

# Convexity

**Convex Set**: For any $$x,y \in \mathrm{X}$$, we have:  
$$\alpha x + (1 - \alpha)y \in \mathrm{X}$$

To define the convex functions, first we introduce two concepts: **domain** and **epigraph** of a function.  

$$\text{dom}f := \{x \in \mathrm{R}^D | f(x) < +\infty \}$$  
$$\text{epi}f := \{(x,t) \in \text{dom}f * R | t \geq f(x)\}$$  
**Convex Function**: A function $$f$$: $$\mathrm{R}^D \to [-\infty, +\infty]$$ is convex if and only if $$\text{epi} f$$ is convex.

**Proposition 1**: A function $$f$$: $$\mathrm{X} \to [-\infty, +\infty]$$ is convex if and only if $$\text{dom} f$$ is convex and for any $$x,y \in \text{dom}f$$, we have:   
$$f(\alpha x + (1-\alpha x)y) \leq \alpha f(x) + (1-\alpha)f(y)$$

From **Proposition 1**, we will get:   
$$E[f(\epsilon)] \geq f(E[\epsilon])$$

**Differentiability**: We say a function $$f: \mathrm{R}^D \to [-\infty, +\infty]$$ is differentiable at $$x \in \text{dom}f$$ if and only if there exists some $$g_x \in \mathrm{R}^D$$, such that:  

$$f(y) = f(x) + \langle g_x, y-x \rangle + o(||y-x||_2)$$

If such $$g_x$$ exists, then we call it **gradient**, noted as $$\nabla f(x)$$ and we have: 

$$[\nabla f(x)]^{(d)} = \frac{\partial f}{\partial x^{(d)}}(x), \forall d \in [D]$$

**Proposition 2**: Let $$f: \mathrm{R}^D \to (-\infty, +\infty]$$ ve convex and differentiable on $$\text{dom}f$$, Let $$\mathrm{X} \subseteq R^D$$, then we have:  

$$x^{*} \in \text{argmin}_{x \in \mathrm{X}} f(x)$$ 
if and only if:  
$$\langle \nabla f(x^*), x-x^* \rangle \geq 0, \forall x \in \mathrm{X}$$

**Proof**:  
$$=>$$    
Suppose we have some $z$ that have:  
$$\langle \nabla f(x^*), z-x^* \rangle < 0$$
Consider the function $$\phi(\alpha) = f(x^* + \alpha(z-x^*)), \alpha \in [0,1]$$, then we have: \\

$$\phi^{'}(0) = \langle \nabla f(x^*), z-x^* \rangle < 0$$
Then if $\alpha$ is small enough, then we have $$f(x^* + \alpha(z-x^*)) < f(x^*)$$ and it is a contradiction.  
$$<=$$  
Follow the convexity, it is very easy to prove.  

**Proposition 3**: A function is a differentiable convex function if and only if the **Hessian** of this function is semi-positive definite. 

**Proof**:  

For 1-D case, we have this proposition equals to:  
$$\langle \nabla_f y - \nabla_f x, y-x \rangle \geq 0$$  

And this proposition follows.  

Then we define:  
$$\phi(t;x,y) = f(x+t(y-x))$$

Since $$\phi$$ can be seen as a part of $$f$$, then we know that $$f$$ is convex if and only if $$\phi$$ is convex.  

Then we follow the 1-D dimention discussion above, we know that:  

$$\phi^{''}(t;x,y) = \langle y-x, [\nabla^2 f(x+t(y-x))](y-x) \geq 0$$