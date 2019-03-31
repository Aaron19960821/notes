# Ray Casting

## Rendering

- **Rendering**: Takes a set of objects and produces its output as a matrix of pixels.
- **Rendering** have two types, **object-order rendering** and **image-order rendering**. The first one is 
considering each object in turn and the second one is taking each pixel in turn.

- **Ray tracing** and **ray casting** are image-order algorithms for making renderings of 3-D scenes.

## Ray casting

The basic of **Ray casting** algorithm can be shown below:  

```c++
For every pixel
  Constructa ray from the eye
  For every object in the scene
    Find intersection with the ray
    Keep if closest
```

So we have the following questions to answer:  

### How to represent a ray

A **ray** have the following properties:  

- Origin - Point
- Direction - Vector
- Parametric line: $P(t) = origin + t*direction$

### How to define a **Camera**

See the following picture, we focus on the following things of a camera when
we do ray-casting algorithms.  

![Camera][./pic/ray_casting/ray_casting_camera.png]

- The point of Camera **e**
- The Orthobasis **u, v, w**(horizontal, up, direction)
- Field of view angle
- Image rectangle aspect ratio

Practice: Compute the ray from a camera to an image-plane.

### Find the intersection from a camera and a plane

#### A ray and a plane intersection

- Ray definition $P(t) = R_0 + t * R_d$
- Plane definition: A plane can be refined by a point and a normal vector

![Plane][./pic/ray_casting/ray_casting_plane.png]

Let's have the following definitions:
$$P_0 = (x_0, y_0, z_0)$$
$$n = (A, B, C)$$
Then we can get the implicit function of the plane:  

$$n * P + D = 0$$

And it is very easy to compute **t** here:  

$$t = \frac{-D-nR_0}{nR_d}$$

#### A ray and a sphare intersection

- Ray definition: $P(t) = R_0 + t * R_d$
- Sphare representation:  

Generally, a sphare can be represented as follwoing:  

$$(x-x_c)^2 + (y-y_c)^2 + (z-z_c)^2 - R^2 = 0$$

Written the function in vector form:  

$$c = (x_c, y_c, z_c)$$
$$(P-c)*(P-c) - R^2 = 0$$

#### A ray and a triangle intersection

- triangle definition: (a, b, c)
- Fact: For every point on the plane same as the trangle, the point can be written as the 
following form:  

$$P(\alpha, \beta, \gamma) = \alpha a + \beta b + \gamma c$$
where $\alpha + \beta + \gamma = 1$
And then, we have the following equation:  

$$P(\beta, \gamma) = a + \beta(b-a) + \gamma(c-a)$$
It is called the **Barycentric definition of a plane**

To compute the value of $\alpha, \beta, \gamma$, we just need a simple trick in linear algebra.  
$$P - a - \alpha e_1 - \beta e_2 = 0$$
$$<e_1, P - a - \alpha e_1 - \beta e_2> = 0$$
$$<e_2, P - a - \alpha e_1 - \beta e_2> = 0$$
$$e_1 = (b-a), e_2 = (c-a)$$

Then compute **t**, we just solve the following linear system:  
$$R_0 + t*R_d = a + \alpha (b-a) + \beta(c - a)$$

## Constructive Solid Geometry

- A neat way to build complex objects from simple parts using Boolean operations.

Focus the **entry** and **exit** point for a ray to a set of objects.  



