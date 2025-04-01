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

Euclidean space (denoted as ℝ³ for 3D) is a mathematical space where:
- Points are defined by coordinates (e.g., (x,y,z)(x,y,z)).
- Distances follow the Pythagorean theorem:
    ```d(P1,P2)=sqrt ((x2−x1)^2+(y2−y1)^2+(z2−z1)^2)
       d(P1​,P2​)=sqrt( (x2​−x1​)^2+(y2​−y1​)^2+(z2​−z1​)^2)```

- Angles and straight lines behave as in classical geometry.
- It is flat (no curvature, unlike non-Euclidean spaces).
Mathematical Notation for 3D Transformations

## Mathematical Notation for 3D Transformations  
Transformations are represented using **4×4 matrices** (homogeneous coordinates) to combine translation with linear transformations.

### 1. Translation by \((t_x, t_y, t_z)\)  
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
*(Similar for \(R_x\) and \(R_y\).)*

### 3. Scaling by \((s_x, s_y, s_z)\)  
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
