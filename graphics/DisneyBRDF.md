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

## BRDF Models

According to **Bruce Walter**'s work on ESR2007, the Microfacet model BRDFs mainly have the following parts:  

- **D**: Microfacet distribution function, the statistical distribution of surface normals over the microsurface.
- **G**: Bidirectional shadowing-masking function, means that visible fraction of microsurface with normal **m** in both directions **i** and **o**.
- **F**: 

### Diffuse model

Disney Principled BRDF uses the Schlick Fresnel approximation with some modifications. The diffuse model is here below:  

$$f_d = \frac{baseColor}{\pi}\left(1 + (F_{D90}-1)(1-cos \theta_l)^5\right) \left(1+(F_{D90}-1)(1-cos \theta_v)^5\right)$$
$$F_{D90} = 0.5 + 2*cos \theta_d^2 \text{ roughness}$$