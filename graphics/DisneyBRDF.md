# Disney Principled BRDF

Disney Pricipled BRDF is a BRDF model based on microfacet theory. It is proposed by Disney in Siggraph 2012. It uses some intuitive parameters rather than some physical parameters to express the BRDF model. The parameter includes:  

- baseColor: The surface color.
- subSurface: 
- metallic: The metallic-ness.
- specular: Incident speclar amount.
- specularTint
- roughness
- anisotropic
- sheen
- sheenTint
- clearCoat
- clearCoatGloss

The effect of each parameter is here below:  
[](./pic/disney_brdf)

## Microfacet Models

The Microfacet theory thought that if a surface reflection is between a given light vector **l** and view vector **v**, then there should be some portion of surface, or microfacet, with a normal aligned halfway between the **l** and **v** vectors. The half vector is defined as $h = normalize(l+v)$.

Then a general form of microfacet BRDFs is like below:  

$$f(l, v) = diffuse + \frac{D(\theta_h)F(\theta_d)G(\theta_l, \theta_v)}{4cos\theta_lcos\theta_v}$$

According to **Bruce Walter**'s work on ESR2007, the specular term contains the following things:

- **D**: Microfacet distribution function, the statistical distribution of surface normals over the microsurface.
- **G**: Bidirectional shadowing-masking function, means that visible fraction of microsurface with normal **m** in both directions **i** and **o**.
- **F**: 

### Diffuse model

Disney Principled BRDF uses the Schlick Fresnel approximation with some modifications. The diffuse model is here below:  

$$f_d = \frac{baseColor}{\pi}\left(1 + (F_{D90}-1)(1-cos \theta_l)^5\right) \left(1+(F_{D90}-1)(1-cos \theta_v)^5\right)$$
$$F_{D90} = 0.5 + 2*cos \theta_d^2 \text{ roughness}$$

And we also have subsurface BRDF based on the ideas from **Hanrahan-Krueger subsurface BRDF**. And the function is:
$$f_{subsurface} = \frac{1.25}{\pi}(F_{ss}*(\frac{1.0}{cos\theta_i + cos\theta_o}-0.5)+0.5)$$
$$F_{ss} = (1 + (F_{ss90}-1)(1-cos\theta_i)^5)(1+(F_{ss90}-1)(1-cos\theta_o)^5)$$
$$F_{ss90} = cos\theta_d^2 * roughness$$

In Disney Principled BRDF, we use **subSurface** to put everything together, that is:  
$$f = (1.0-subsurface)*f_d + subsurface*f_{subsurface}$$