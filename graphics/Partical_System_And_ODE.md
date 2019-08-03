# Particle Systems and ODEs

## Physical-based Animation

- Assign physical properties to objects
- Type of Dynamics: Point, Rigid body, deformable body.

### Partical system overview

- **Emitters** generate tons of "particles"
- Describe external **forces** with a force field.
- **Integrate** the laws of mechanics.
- Apply **randomness** to get nice effects.

Partical-based methods can range from pure heuristics to "real" simulation.  

An example: Sprinkler

```
PL: linked list of particle = empty
spread = 0.1
colorSpread = 0.1
for each time step:
  Generate k particles
  p = new particle();
  p->position=(0, 0, 0)
  // Apply randomness to this system
  p->velocity=(0,0,1) + spread * (rnd(), rnd(), rnd())
  p->color = (0,0,1) + colorSpread*(rnd(), rnd(), rnd())
  PL->add(p)
  
  for each particle p in PL:
    p->position += p->velocity*dt
    p->velocity -= g * dt //Apply physical properties
    glColor(p.color)
    glVertex(p->position)
```

### Numerical integration

#### Newtonian Mechanics

- Point mass: $2^{nd} order ODE$
$$ F = ma$$
$$F = m\frac{d^2x}{dt^2}$$

Note that position x and force F are vectors. We know F and m, we want to solve for x.

We reduce a 2-order ODE to 1-order:  

$$
  \begin{cases}
    \frac{dv}{dt} = F/m \\
    \frac{dx}{dt} = v
  \end{cases}
$$

So we let:

$$
X =
\begin{pmatrix}
x_1 \\
v_1 \\
... \\
x_n \\
v_n
\end{pmatrix}
$$

Then we will get:  

$$
f(x, t) = \frac{dX}{dt} = 
\begin{pmatrix}
v_1 \\
F1/m \\
... \\
v_n \\
F_n/m
\end{pmatrix}
$$

#### How to integrate ODE?

What we want to do in graphics is to compute the state of the whole system **X(t)**. The simplest way to do is **Euler's Method**.

```
h: step
X: The state of partical system
for each step:
  t = t + h
  X = X + h*f(x, t)
```

The problem of **Euler method**:  
- Euler method is not accurate. For example, if a function is a circle and we use euler method, then we will turn it to spiral of our choice.
- The euler method is not stable. 

Analyse the error provided by **Euler method**: We use **Taylor series**

$$x(t_0+h) = x(t_0) + hx'(t_0) + \frac{h^2}{2!}x''(t_0) + ... + \frac{h^n}{n!}x^{(n)}$$

We recognise that the error term is here below:  

$$error = \frac{h^2}{2!}x''(t_0) + ... + \frac{h^n}{n!}x^{(n)}$$

An easy approach: Take smaller step(smaller h) and we will get a better answer but more computation worked should be done by us.

**Midpoint Method**: We realise that if we compute $x'(t)$, then we will shrink the error to $O(h^3)$, which is much better.  
In order to avoid computing second derivative of a function, we will use Taylor series again:  

$$f(x_0 + \Delta x) = f(x_0) + \Delta xf'(x_0) + O(\Delta x^2)$$


















