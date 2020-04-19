## Machine Learning Techniques - 1

### Three goals of Machine Learning techniques

- Exploit and regularize numerous features => SVM models.  
- Construct and blend predictive features => Adaboost models.
- Identify and learn implicit features => Deep learning features.  

### Basic ideas of SVM

When we solve a linear classification problem, we are looking for a hyperplane to divide a set of points into 2 groups. And this time, we consider the maximize distance between the hyperplane to the point set we are looking at. That is:  

Maximize $Distance(w, b, X, Y)$, where
- for every $x_i \in X$, we have $y_i (w^Tx_i + b) > 0$
- $Distance(w, b, X, Y) = min_{i} \frac{1}{||w||}y_i(w^Tx_i + b)$

And then we find that we can normalize $y_i(w^Tx_i + b)$ by multiplying a scale. Then the optimization problem turns out to be:  

Minimize $\frac{1}{2}w^Tw$
- $min_i y_i(w^T x_i + b) = 1$

And then we find that $min_i y_i(w^T x_i + b) = 1$ is equivalent to the following formula $min_i y_i(w^T x_i + b) \geq 1$, we can simply prove this by **proof of contradiction**. Then the optimization problem turns out to be:  

Minimize $min_{b, w} = \frac{1}{2}w^Tw$
- $y_i(w^Tx_i + b) \geq 1$ for all $i$.  

We will solve this optimization question by **Quadratic Programming**.

#### Quadratic Programming

**Quadratic Programming** aims to solve the following question:  

minimize $\frac{1}{2}x^T Q x + c^Tx$
subject to $A_ix \geq b$ for $m \in [1, m]$

Then for our case, we will set:  

$$x = \begin{bmatrix}
b \\
w
\end{bmatrix}, 
Q = \begin{bmatrix}
0 & 0 \\
0_d & I_d^T
\end{bmatrix},
c = 0_{d+1}
$$

$$
A = y_i[1, x_i^T], c_i = 1, m = n 
$$

#### VC Dimension of SVM

It is very clear that VC dimension will be less than the origin linear classification problem when we take **margin** into account. When we use **hyperplanes** and feature transform, we will have not so many hyperplane(This is good for generization) and more sophisticated boundary.  

## Dual SVM

Now we know that SVM is solving the following optimization question:  

Minimize $\frac{1}{2}w^Tw$
$y_i(w^Tx_i + b) \geq 1$

Then we use **Lagrange Multipliers** to combine our optimization function and optimization constrains together. We have the following **Lagrange Function**:  

$$L(b, w, \alpha) = \frac{1}{2}w^Tw + \sum_{i=1}^n \alpha_i(1 - y_i(w^Tx_i + b))$$

The aim of SVM is going to compute the following thing:  

$$min_{b, w}\left(max_{\alpha_i \geq 0} L(b, \omega, \alpha)\right)$$

The inner $max$ ensure that the formula above does not break the constraints of our optimization problem.(When it breaks, then the whole formula will go infinity). The outer $min$ ensure that what we find will be the optimized solution.  

## Soft-Margin SVM

In hard margin SVM, we intend to correctly classify all samples in our dataset. That is, we have:  

$$y_i(\omega^T x_i + b) \geq 0$$

However, we may met **overfitting** problem from this constraint. So we introduce **soft-margin** in this case. Thus, the SVM become the following optimization problem:  

$$min_{b, \omega, \zeta} \frac{1}{2}\omega^T \omega + C * \sum_{n=1}^N \zeta_n$$
$$y_i(\omega^T x_i + b) \geq 1 - \zeta_i, \zeta_i \geq 0$$

In our new optimization problem, $\zeta$ is setting to measure the violation of this sample and $C$ is for the scale of penalty when we find some samples false.  

Thus we can set up the **dual problem** with lanrange multipliers.  

$$
\begin{aligned}
O(b, \omega, \zeta, \alpha, \beta) = & \frac{1}{2}\omega^T\omega + C*\sum_{n=1}^N \zeta_n \\ & + \sum_{n=1}^N \alpha_n[1-\zeta_n-y_n(\omega^Tx_n+b)]+\sum_{n=1}^N\beta_n(-\zeta_n)
\end{aligned}
$$

To solve this dual problem, we take partial derivatives and set it to 0:  

$$\frac{\partial O}{\partial \zeta_n} = C - \alpha_n - \beta_n = 0$$

Then we will find that $\beta_n = C - \alpha_n$, we put this into our origin dual problem and we will get rid of $\beta$:  

$$O(b, \omega, \zeta, \alpha, \beta) = \frac{1}{2}\omega^T\omega + \sum_{n=1}^N \alpha_n[1-y_n(\omega^Tx_n+b)]$$

Then:  

$$\frac{\partial O}{\partial \omega_i} = \sum_{n=1}^N \alpha_n y_n x_{n,i} = 0 \rightarrow \omega = \sum_{n=1}^N \alpha_n y_n x_n$$

$$\frac{\partial O}{\partial b} = \sum_{n=1}^N \alpha_n y_n = 0$$

Finally, the optimization problem turns out to be:  

$$
\begin{aligned}
min & \left\{ \frac{1}{2} \sum_{n=1}^N\sum_{m=1}^N \alpha_m \alpha_n y_m y_n x_m^T x_n - \sum_{n=1}^N \alpha_n\right\} \\
& \sum_{n=1}^N \alpha_n y_n = 0 \\
& 0 \leq \alpha_n \leq C, \beta_n = C - \alpha_n \\ 
& \omega = \sum_{n=1}^N \alpha_ny_nx_n \\
\end{aligned}
$$

We can classify feature vectors via the values of $\alpha$ and $\beta$.  

- When $\alpha = 0$, this means that this vector is not a support vector.  
- When $\alpha = C, \beta = 0$, then this means that this vector is on the margin.  
- When $0 \leq \alpha \leq C$, then this vector is a free vector.  
