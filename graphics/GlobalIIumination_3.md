# Rendering Equation

## Overview of Rendering Equation

The origin version of rendering equation is below:  

$$L(x \rightarrow \Theta) = L_e(x \rightarrow \Theta) + \int_{\Omega_x} f_r(x, \Phi \leftrightarrow \Theta) L(y \rightarrow -\Phi) cos(N_x, \Phi)d \omega_{\Phi}$$

Where $f_r(x, \Phi \leftrightarrow \Theta)$ is **BRDF** of the surface. $L(x \rightarrow \Theta)$ is the radiance from $x$ to direction $\Theta$.  

In the origin form of **rendering equation**, we compute radiance by integrate over the solid angle of point $x$.  

[](./pic/rendering_equation.png)

Another way to compute radiance is that we integrate over all surface points, that is:  

$$L(x \rightarrow \Theta) = L_e(x \rightarrow \Theta) + \int_A f_r(x, \Phi \leftrightarrow \Theta)L(y \rightarrow yx)V(x, y)G(x, y)dA_y$$

Where $G(x, y) = \frac{cos(N_x, \Phi)cos(N_y, -\Phi)}{r_{xy}^2}$, $V$ is visibility check function. Usually we compute it in **Ray tracing** algoritms.  

For energy conservation, exitant radiance can be transformed to incident radiance. So we have the following 2 forms of rendering equations:  

$$L(x \leftarrow \Theta) = L_e(x \leftarrow \Theta) + \int_{\Omega_y} f_r(y, \Phi \leftrightarrow -\Theta) L(y \leftarrow \Phi) cos(N_y, \Phi)d \omega_{\Phi}$$

$$L(x \leftarrow \Theta) = L_e(x \leftarrow \Theta) + \int_A f_r(y, \Phi \leftrightarrow yz)L(y \leftarrow yz)V(x, z)G(y, z)dA_z$$

## Importance Function

We have known that we want to compute the radiance from all points along all directions to solve global illumination problems. We firstly define a set $S = A_s \times \Omega_s$. Then the flux leaving S can be computed through the following formula:  

$$\Phi(S) = \int_{A_s}\int_{\Phi_s}L(x \rightarrow \Phi)cos(N_x, \Theta)d\omega_{\Theta}dA_x$$  

We will turn this integration to integrating all surface points and directions by introducing **initial importance function**.

$$W_e(x \leftarrow \Theta) = 
\begin{cases}
1 \text{   if } (x, \Theta) \in S \\
0 \text{   if } (x, \Theta) \notin S 
\end{cases}$$

Then the average radiance value can be expressed in following form:  

$$L_{average} = \frac{\int_A \int_{\Omega} L(x \rightarrow \Theta)W_e(x \leftarrow \Theta)cos(N_x, \Omega)d\omega_{\Theta}dA_x}{\int_A \int_{\Omega} L(x \rightarrow \Theta)cos(N_x, \Omega)d\omega_{\Theta}dA_x}$$

Then based on physical, we know that $\Phi(S)$ may have 2 sources:  

- Self-contribution, means that $(x, \Theta) \in S$. We use $W_e$ to address this situation.  
- Contribution through one or more reflections/refractions.

Then the overall **Importance Function** can be written as the following:  

$$W(x \rightarrow \Theta) = W_e(x \leftarrow \Theta) + \int_{\Omega_z}f_r(z, \Phi \leftrightarrow -\Theta)W(z \leftarrow \Phi)cos(N_{r(x, \Theta)}, \Phi)d \omega_{\Phi}$$  

If we look the radiance transfer over the whole scene, we can see the reflection/refraction as a remap of radiance over the entire scene. Thus, we denote a linear operator $\tau$, then the radiance can be written in the following form:  

$$L(x \rightarrow \Theta) = L_e(x \rightarrow \Theta) + \tau L(x \rightarrow \Theta)$$
$$\tau L(x \rightarrow \Theta) = \int_{\Omega_x}f_r(x, \Phi \leftrightarrow \Theta)L(r(x, \Theta) \rightarrow -\Phi) cos(N_x, \Phi)d\omega_{\Phi}$$

Similarly, we can also write incident importance function $W^{\leftarrow}$ with a linear operation, denoted by $\varrho$.

$$W(x \leftarrow \Theta) = w_e(x \leftarrow \Theta) + \varrho W(x \leftarrow \Theta)$$

$$\varrho W(x \leftarrow \Theta) = \int_{\Omega_{r(x, \Theta)}} f_r(r(x, \Theta), \Phi \leftrightarrow -\Theta)W(r(x, \Theta) \leftarrow \Phi) cos(N_{r(x, \Theta)}, \Phi) d \omega_{\Phi}$$

Then we will get the following things:  

$$L^{\rightarrow} = L_e^{\rightarrow} + \tau L^{\rightarrow}$$
$$L^{\leftarrow} = L_e^{\leftarrow} + \varrho L^{\leftarrow}$$
$$W^{\leftarrow} = W_e^{\leftarrow} + \varrho W^{\leftarrow}$$
$$W^{\rightarrow} = W_e^{\rightarrow} + \tau W^{\rightarrow}$$

## Global Reflectance Distribution Function

The **GRDF** describes one point-direction pair $(x, \Theta)$'s radiance contribution to another pair $(y, \Phi)$. Then we will get the following formula:  

$$L(y \rightarrow \Phi) = \int_{A}\int_{\Omega_x} L_e(x \rightarrow \Theta)G_r(x \leftarrow \Theta, y \rightarrow \Phi)cos(N_x, \Phi)d \omega_{\Theta}dA_x$$

As a result, we can use a four-dimension integration to calculate flux in $S$:  

$$\Phi(S) = \int_{A}\int_{\Omega_x}\int_{A}\int_{\Omega_y} L_e(x \rightarrow \Theta) G_r(x \leftarrow \Theta, y \rightarrow \Phi)W_e(y \leftarrow \Phi) cos(N_x, \Phi) cos(N_y, \Phi) d\omega{\Phi} dA_y d\omega_{\Theta} dA_x$$

It is fairly complex to get an analytical solution for this integration function, we usually use **Monte Carlo techniques** to do this integration.  