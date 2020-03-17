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