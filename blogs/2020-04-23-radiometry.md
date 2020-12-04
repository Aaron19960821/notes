---
layout: post
title: "Radiometry"
date: 2020-04-23 15:55:04
tags: ['rendering','physics','graphics']
comments: false
# Does not change and does not remove 'script' variable.
script: [post.js]
---

<!-- Write from here your post !!! -->

# Radiometry

**Radiometry** is the basic of light transport simulation. It explains how light transports and how to do realistic light transport simulation.  

## Solid Angle

Before getting to know concepts of light transport, we have to know **Solid angle** first.  

We know that a point in a 3-D area can be expressed as a tuple: $(r, \theta, \phi)$. Like the figure below:  

![](../../assets/images/posts/solid_angle.jpg)

**Solid Angle** is defined as the following way:  

$$\omega = \frac{A}{r^2}$$

Where $A$ is the corresponding surface area on sphere. When we do differentiation on it, it becomes:  

$$d \omega = \frac{dA}{r^2} = sin \theta d \theta d \phi$$

We can integrate solid angle over a sphere:  

$$\int_S d \omega = \int_0^{2 \pi} \int_0^{\pi} sin \theta d \theta d \phi = 4 \pi$$

## Radiometry

Firstly we introduce some concepts in **Radiometry**.  

**Flux**: note as $\Phi$, expressed in Watts. Expressing how much energy flows from/to/through a surface per unit time.  

**Irradiance**: The incident radiant power on a surface, per unit surface area. Noted as $E$, expressed as:  
$$E = \frac{d \Phi}{dA}$$

**Radiant intensity**: Expressing the radiant power per solid angle, expressed as:  
$$I = \frac{d \Phi}{d \omega}$$

**Radiance**: Flux per unit solid angle per unit surface area, can be expressed:  
$$L = \frac{d^2 \Phi}{d \omega d A^{\perp}} = \frac{d^2 \Phi}{d \omega dA cos\theta}$$

## Bidirectional Reflectance Distribution Function(BRDF)

**Reflectance** can be explained in the following way: Energy flows from incident directions and absorbed by differential surface area $dA$ and emits to different solid angles.  

The incident irradiance can be expressed as:  

$$dE(\omega_i) = L(\omega_i) cos \theta_i d \omega$$

The exitant radiance:  

$$dL_r(\omega_o)$$

Thus, we denote **BRDF** as the following thing:  

$$f_r(\omega_i, \omega_o) = \frac{dL_r(\omega_o)}{dE(\omega_i)}$$

Note that the differential surface can also emitted randiance itself, we express it as $L_e(\omega)$. Thus exitance radiance of surface can be expressed as:  

$$L(x \rightarrow \omega_o) = L_e(x \rightarrow \omega_o) + \int_S L(x \leftarrow \omega_i) f_r(\omega_i, \omega_o)cos \theta_i d \omega$$

This is famous **rendering equation** published by *James Kajiya* in 1986.

## The Rendering Equation

We can rewrite **Rendering Equation** in the following form:  

$$L(x \rightarrow \omega_o) = L_e(x \rightarrow \omega_o) + \int_{A}L(x, \omega_o)f_r(\omega_i, \omega_o)V(x, y)G(x, y)dA_y$$

Note that $V(x,y)$ is the visibility function and $G(x,y)$ is the geometry term between $x$ and $y$.  

Next, we define the kernel function of rendering equation as:  

$$K(x, y) = V(x,y)G(x,y)f_r(\omega_i, \vec{xy})$$

Then we use **linear operator** to rewrite **rendering function**, we will get that:  

$$
\begin{aligned}
L &= E + KL \\
(I-K)L &= E \\
L &= (I-K)^{-1}E
\end{aligned}
$$

Then we use **taylor expansion** on linear operators, we will get:  

$$L = E + KE + K^2E+ ...$$

We call $E$ as the emitted radiance in $x$, $KE$ as the direct illumination in $x$ and others are indirect illumination.  
