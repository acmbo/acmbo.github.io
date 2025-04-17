## Geometry transformations in 3D Space

Transformation in 3D Geometry (Euclidean Space)

In 3D geometry, transformations are operations that modify the position, orientation, or shape of objects in Euclidean space. These include:

1. Translation – Moving an object along a vector.
2. Rotation – Turning an object around an axis.
3. Scaling – Resizing an object uniformly or non-uniformly.
4. Shearing – Distorting an object along an axis.
5. Reflection – Mirroring an object across a plane.

These transformations are represented using matrices (linear algebra) for efficiency and composability.

### What is Euclidean Space?

Euclidean space is the "standard" mathematical playground for geometry—the world of points, lines, and shapes where the rules feel intuitive. At its core, it’s built on Cartesian coordinates (like familiar (x, y) in 2D or (x, y, z) in 3D), but it’s more than just axes and grids.

Key Properties:
1. Flat and Rigid – No curves or warping: distances and angles follow Euclid’s ancient axioms. Think graph paper, not a globe.
2. Pythagorean Distance – The straight-line distance between two points (like √(x² + y² + z²) in 3D) is the gold standard.
3. Uniform Scaling – Shapes stay congruent when moved or rotated—no stretching weirdly (thanks to rigid transformations).
4. Parallel Lines Stay Parallel – Unlike curved spaces (e.g., planetary surfaces), parallel lines never meet.

With a more mathematical approach to Euclidean space (denoted as ℝ³ for 3D)  you can derive the following properties:
- Points are defined by coordinates (e.g., (x,y,z)(x,y,z)).
- Distances follow the Pythagorean theorem: $\ d(P_1, P_2) = \sqrt{(x_2 - x_1)^2 + (y_2 - y_1)^2 + (z_2 - z_1)^2}$
- Angles and straight lines behave as in classical geometry.
- It is flat (no curvature, unlike non-Euclidean spaces).
Mathematical Notation for 3D Transformations

## Mathematical Notation for 3D Transformations  
Transformations are represented using **4×4 matrices** (homogeneous coordinates) to combine translation with linear transformations.

### 1. Translation by $\((t_x, t_y, t_z)\)$  
$$
T = \begin{bmatrix}
1 & 0 & 0 & t_x \\
0 & 1 & 0 & t_y \\
0 & 0 & 1 & t_z \\
0 & 0 & 0 & 1 \\
\end{bmatrix}
$$  

**Effect:**  

$$
\begin{pmatrix} x' \\ y' \\ z' \\ 1 \end{pmatrix} = T \cdot \begin{pmatrix} x \\ y \\ z \\ 1 \end{pmatrix}
$$

### 2. Rotation (around Z-axis by angle θ)  

$$
R_z = \begin{bmatrix}
\cosθ & -\sinθ & 0 & 0 \\
\sinθ & \cosθ & 0 & 0 \\
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1 \\
\end{bmatrix}
$$  

*(Similar for %\(R_x\)% and $\(R_y\)$.)*

####  2.1 Rodriguez Formula

The Rodriguez formula offers a compact and elegant way to rotate a vector around a given axis by a specified angle, without dealing with full rotation matrices or quaternions.

Given:
- A vector $v$ that we want to rotate.
- A unit axis vector $k$ (the rotation axis).
- An angle $θ$ (the rotation angle in radians).

The rotated vector v' is given by:

$$
\mathbf{v'} = v \cosθ + (\mathbf{k} \times \mathbf{v}) \sinθ + \mathbf{k} (\mathbf{k} \cdot \mathbf{v}) (1 - \cosθ)
$$


##### How to Use the Rodriguez Formula (Step-by-Step)

Let’s rotate 
- vector $ v = \begin{bmatrix} 1 \\ 0 \\ 0 \end{bmatrix}$ (x-axis) 
- by 
    $$
    \theta = 90^\circ
    $$ 
    ($\pi/2$ radians) 
- around axis

    $$
    k = \begin{bmatrix} 0 \\ 0 \\ 1 \end{bmatrix}
    $$ 
    
    (z-axis).

###### **Step 1: Ensure $\(\mathbf{k}\)$ is a unit vector**
$$
\|\mathbf{k}\| = \sqrt{0^2 + 0^2 + 1^2} = 1 \quad \text{(already normalized)}
$$

###### **Step 2: Compute $\(\mathbf{k} \times \mathbf{v}\)$ (cross product)**
$$
\mathbf{k} \times \mathbf{v} = 
\begin{vmatrix}
\mathbf{i} & \mathbf{j} & \mathbf{k} \\
0 & 0 & 1 \\
1 & 0 & 0 \\
\end{vmatrix} = \begin{bmatrix} 0 \\ 1 \\ 0 \end{bmatrix}
$$

###### **Step 3: Compute $\(\mathbf{k} \cdot \mathbf{v}\)$ (dot product)**
$$
\mathbf{k} \cdot \mathbf{v} = (0)(1) + (0)(0) + (1)(0) = 0
$$

###### **Step 4: Plug into the Rodriguez formula**

$$
\mathbf{v'} = \mathbf{v} \cos \theta + (\mathbf{k} \times \mathbf{v}) \sin \theta + \mathbf{k} (\mathbf{k} \cdot \mathbf{v}) (1 - \cos \theta)
$$

Substitute values $\(\cos 90^\circ = 0\)$, $\(\sin 90^\circ = 1\)$:

$$
\mathbf{v'} = \begin{bmatrix} 1 \\ 0 \\ 0 \end{bmatrix} \cdot 0 + \begin{bmatrix} 0 \\ 1 \\ 0 \end{bmatrix} \cdot 1 + \begin{bmatrix} 0 \\ 0 \\ 1 \end{bmatrix} \cdot 0 \cdot (1 - 0)
$$

Simplify:

$$
\mathbf{v'} = \begin{bmatrix} 0 \\ 1 \\ 0 \end{bmatrix}
$$



### 3. Scaling by $\((s_x, s_y, s_z)\)$  

$$
S = \begin{bmatrix}
s_x & 0 & 0 & 0 \\
0 & s_y & 0 & 0 \\
0 & 0 & s_z & 0 \\
0 & 0 & 0 & 1 \\
\end{bmatrix}
$$

### 4. Composition of Transformations  
Multiple transformations are combined via **matrix multiplication**:  

$$
M = T \cdot R \cdot S
$$  

*(Order matters: e.g., "Translate then Rotate" ≠ "Rotate then Translate".)*
