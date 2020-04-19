# Stochastic Path-Tracing Algorithms

## Overview

When we try to render a picture, we are trying to compute the incident radiance of each pixel. In rendering equation, we divide the incident radiance into 2 parts, self-emitted and reflected. Firstly, we write the reflected term as **exitant radiance** below:  

$$\begin{aligned} L_r(x \rightarrow \Theta) 
&= \int_{\Omega_x}L(x \leftarrow \Phi)f_r(x, \Theta \leftrightarrow \Phi)cos(\Phi, N_x)d \omega_{\Phi} \\  
&= \int_{\Omega_x}L(r(x, \Phi) \rightarrow -\Phi)f_r(x, \Theta \leftrightarrow \Phi)cos(\Phi, N_x)d \omega_{\Phi}  \end{aligned}$$

Then we rewrite this term as a sum of **direct illumination** and **indirect illumination**.  

$$\begin{aligned} L_r(x \to \Theta)
&= \int_{\Omega_x}L_e(r(x, \Phi) \to -\Phi)f_r(x, \Theta \leftrightarrow \Phi)cos(\Phi, N_x)d \omega_{\Phi} \\
&+ \int_{\Omega_x}L_r(r(x, \Phi) \to -\Phi)f_r(x, \Theta \leftrightarrow \Phi)cos(\Phi, N_x)d \omega_{\Phi} \\
&= L_{direct}(x \to \Theta) + L_{indirect}(x \to \Theta)
\end{aligned}$$

## Direct illumination

In direct illumination, we intent to solve the following integral:  

$$L_{direct}(x \to \Theta) = \int_A{sources} L_e(y \to xy)G(x, y)V(x, y)dA_y$$

When there is only one emitter in the scene, then $L_{direct}$ will be:  

$$L_{direct}(x \to \Theta) = \frac{1}{N_s}\sum_1^{N_s} \frac{L_e(y_i \to y_ix)f_r(x, \Theta \leftrightarrow xy_i)G(x, y_i)V(x, y_i)}{p(y_i)}$$

Note that $N_s$ is the number of samples.  

When there is multiple emitters in the scene, note that the number of emitters is $l$, then direct illumination will be solved by **Bayesian Equation**.  

$$L_{direct}(x \to \Theta) = \frac{1}{N}\sum_1^{N} \frac{L_e(y_i \to y_ix)f_r(x, \Theta \leftrightarrow xy_i)G(x, y_i)V(x, y_i)}{p(y_i|j)p_l(j)}$$

## Light-Tracing Algorithm

As we know, **Ray-Tracing** algorithms are going from a pixel in **film** and find a path from this pixel to the emitter(light source). However, this order is different from actual light transport order. Lights come from a light source and travel through a path to a pixel in our **film**. So we have **Light-Tracing Algorithm** to do the exact the same thing.  

The **Weight Function** of **Light-Tracing** Algorithms can be written in the following form:  

$$W(x \rightarrow \Theta) = W_e(x \rightarrow \Theta) + \int_{\Omega_x}W(x \leftarrow \Phi)f_r(x, \Theta \leftrightarrow \Phi)cos(\Phi, N_x)d \omega_{\Phi}$$

And for each pixel, we just integrate over all emitters(light sources).  

$$P = \int_{sources} W(x \rightarrow \Phi)L_e(x \rightarrow \Phi)cos(N_x, \Phi)dA_xd\omega_{\Phi}$$