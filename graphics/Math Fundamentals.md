# Math Fundamental of Modeling

## Some concepts

- Point: Location representation
- Vector: Movement representation
- Normal: Orientation representation
- Coordinates: Numerical representation of **point, vector, normal** in a given coordinate system.

## Matrix

We use matrices mainly have 2 purposes:

- Transform things: Points in the same coordinte system, but location changed.
- Coordinate system changes: represent locations in two coordinate system.

## Vectors(Linear space)

- We can use a basis to produce all vectors in the space.

$$v = \sum_i{c_ib_i}$$

The properties of a linear transformation L.
$$L(v+u) = L(v) + L(u)$$
$$L(\alpha v) = \alpha L(v)$$

We can do something magic using the properties above:  
$$L(v) = L(\sum_i{c_ib_i}) = \sum_i{c_iL(b_i)}$$

So we know for any vector in a linear space, we can calculate any transformations on them based on the transformation on the basis.

## Frames

- A **frame** is an origin o plus a basis b.
- Any point in the space can be described as following:  

$$p = o + \sum_i{c_i b_i}$$

We like to have this representation in matrix form:  

$$
p = 
\begin{bmatrix}
b_1 & b_2 & b_3 & o
\end{bmatrix}
\begin{bmatrix}
c_1 \\ 
c_2 \\ 
c_3 \\
1
\end{bmatrix}
= f^tc
$$

## Afine transformations
- Include all linear transformation
- Translation

## Notation properties

- If the fourth coordinate is zero, we get a vector.

- A **frame** is an origin o plus a basis b.
- Any point in the space can be described as following:  

$$p = o + \sum_i{c_i b_i}$$

We like to have this representation in matrix form:  

$$
p = 
\begin{bmatrix}
b_1 & b_2 & b_3 & o
\end{bmatrix}
\begin{bmatrix}
c_1 \\ 
c_2 \\ 
c_3 \\
1
\end{bmatrix}
= f^tc
$$

## Afine transformations
- Include all linear transformation
- Translation

## Notation properties

- If the fourth coordinate is zero, we get a vector.
- If the fourth coordinate is 1, then we get a point.(A point plus a vector).

## Homogeneous Coordinates

- Add an extra dimension
  - For 2D, we use 3-vectors and 3*3 matrices...

- The extra coordinate is now an arbitrary value, w.
