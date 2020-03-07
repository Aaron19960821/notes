# Monte Carlo Methods

## Review of Probability Theory

### Discrete Random Variables

- Expected Value: $E(x) = \sum_{i=1}^n p_i x_i$.
- Variance: $\sigma^2 = E[(x - E(x))^2]$

### Continuous Random Variables

- Expected Value: $\int_{-\infty}^{\infty}xp(x)dx$
- Variance: $\sigma^2 = E[(x - E(x))^2] = \int(x-E(x))^2p(x)dx$

### Conditional and Marginal Probabilities

In this part we consider a pair of random variables $x$ and $y$. We have a joint probability distribution function $p(x, y)$.

- The marginal density function of $x$ is defined as: $p(x) = \int p(x, y)dy$
- The conditional density function: $p(y|x) = \frac{p(x,y)}{p(x)} = \frac{p(x,y)}{\int p(x,y)dy}$

### Chebyshev Inequality

Firstly we will introduce **Markov Inequality**.
- Markov Inequality: If $X > 0$ and $a > 0$, then $p(X \geq a) \leq \frac{E[X]}{a}$.

Proof:  

$$E[X] = E[x | x \geq a]p(x \geq a) + E[x | x < a]p(x < a)$$
$$\geq E[x|x \geq a]p(x \geq a) \geq ap(x \geq a)$$

Then we prove that:  

$$p(x \geq a) \leq \frac{E[X]}{a}$$  

After we know **Markov Inequality**, we will go to introducing **Chebyshev Inequality**.  

- Chebyshev Inequality: $p(|x-\mu| \geq c) \leq \frac{\sigma^2}{c^2}$.

$$p(|x-\mu| \geq c) = p[(x-\mu)^2 \geq c^2]$$

Applying **Markov Inequality**, we will get that:  

$$p(|x-\mu| \geq c) \leq \frac{E[(x-\mu)^2]}{c^2} = \frac{\sigma^2}{c^2}$$

## Monte Carlo Integration

### Basics of Monte Carlo methods

Firstly assume that we have $N$ random variables $g(x_1), ..., g(x_N)$. The $x_i$ variables are independent with each other. Assume that the weighted sum of these variables is $G(x)$.

$$G(x) = \sum_{i=1}^N w_ig(x_i)$$

Assume that each of $x$ has the same weight, $w_i = \frac{1}{N}$.

The expected value of $G(x)$ is that:  

$$E[G(x)] = \sum_i w_i g(x_i) = \frac{1}{N} \sum_{i=1}^{N}E[g(x)] = E[g(x)]$$

Then the variance of $G(x)$ is that:  

$$\sigma^2(G(x)) = \sigma^2(\sum_i\frac{g(x_i)}{N}) = \frac{\sigma^2(g(x))}{N}$$

That means, the variance of $G(x)$ will decrease as the number of samples $N$ increases.  