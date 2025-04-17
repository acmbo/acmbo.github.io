## Distance Functions

### Distance between two points

**Formula:**

$$ 
d = \sqrt{(x_2 - x_1)^2 + (y_2 - y_1)^2 + (z_2 - z_1)^2}
$$ 

**Where:** 
- $\( P_1(x_1, y_1, z_1) \)$ and $\( P_2(x_2, y_2, z_2) \)$ are 3D Points coordiantes:


### Distance from Point to Line 

**Formula:**

$$ \text{Distance} = \frac{\| (P - A) \times \vec{v} \|}{\| \vec{v} \|} $$ 

**Where:** 
- $\ A$ = Line start point 
- $\ \vec{v}$ = Line direction vector (End - Start) 
- $\ P$ = Query point


### Distance from a point to a plane (3D)

**Formula:**

$$
d = \frac{|ax_0 + by_0 + cz_0 + d|}{\sqrt{a^2 + b^2 + c^2}}
$$

**Where:** 
- $\( ax + by + cz + d = 0 \)$ is a Plane given in Parametric Form,
- $\( P(x_0, y_0, z_0) \)$ is Point in 3d Space: