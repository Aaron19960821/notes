# Shading & Material Appearance

## Light sources

- Linearity

$$I(a+b) = I(a) + I(b)$$
$$I(sa) = sI(a)$$

- Intensity as Function of Distance

$$I = \frac{1}{ar^2 + br + c}$$

- Intensity as Function of incoming irradiance

$$I_{in} = I_{light}cos\theta / r^2$$
$I_{in}$: light intensity at the surface
$I_{light}$: light intensity

## Quantifying Reflection

- BRDF(Birirectional Reflectance Distribution Function)
- Ratio of light coming from one direction that gets reflected in another direction.  

We can write BRDF as the following function:  

$$BRDF = f_r(l, v)$$
$l$: light direction
$v$: view direction

As a result, we compute output light intensity as:  

$$I_{out}(v) = I_{in}(l)f_r(l, v)$$

Isotropic: Keeping l and v fixed, rotation around the normal does not change the reflection.  

### How to compute BRDFs

- BRDFs can be measured from real data
- Parametric BRDFs:

  - Ideal Diffuse Reflectance:
    - The surface reflects equally in all directions.  

  - Non-ideal Diffuse Reflectors:
    - Phong Specular Model:
    $$L_o = k_s(cos\alpha)^q \frac{L_i}{r^2}$$
    $\alpha$: The angle between the ideal reflection direction r and viewer direction v.
