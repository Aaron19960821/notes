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