# Monte Carlo Integration

Our goal: Do high-dimensional integration. The main problem is that usually we can not find analytical form of these integrations. So we use a lot of random samples to find a approximately result. The method is called Monte Carlo Integration.  

## Basic Concepts We Use

$X$: Random variable

$P(X) = Pr\{ X \leq x \}$: Called Cumulative Distribution Function.

$p(x) = \frac{dP(X)}{dx}$: Called Probability Density Function.

$E_p[f(x)] = \int_D{f(x)p(x)dx}$: Expected value.

$V[f(x)] = E[(f(x)-E[f(x)])^2]$

## General Monte Carlo Integration

- Given a random variable drawn from a PDF $p(x)$, we get that:  

$$F_N = \frac{1}{N}\sum_{i=1}^n \frac{f(x_i)}{p(x_i)}$$

- Convergence of Monte Carlo method

Introduction: Chebyshev's inequality.  

$$Pr\{|X - \mu| \geq k\sigma\} \leq \frac{1}{k^2}$$

Apply **Chebyshev's inequality**:  
$$
Pr\{|F_N - E[F_N]| \geq (\frac{V[F_N]}{\delta})^{\frac{1}{2}}\} \leq \delta
$$

We let: $y_i = \frac{f(x_i)}{p(x_i)}$, then we will get that:  

$$V[F_N] = V[\frac{1}{N}\sum_{i=1}^Ny_i]  = \frac{1}{N^2}V[\sum_{i=1}^Ny_i] = \frac{1}{N^2}\sum_{i=1}^NV[Y] = \frac{1}{N}V[Y]$$

We plug these stuff into **Chebyshev's inequality**, we can get that:  
$$Pr\{|F_N - E[F_N]| \geq \frac{1}{\sqrt{N}}(\frac{V[Y]}{\sigma})^{\frac{1}{2}}\} \leq \sigma$$