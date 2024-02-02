# Lecture 5 <div style="text-align:right;"> 19/01/2024 </div>

## Setting up
##### Viewing

If a point P has coordinates `(x, y, z)` in World coordinate system (WCS)
`(a , b, c)` in View coordinate system (VCS)

$$\begin{bmatrix} x \\ y \\ z \end{bmatrix} = M . \begin{bmatrix} a \\ b \\ c \end{bmatrix} + R$$
where   
$$M = \begin{bmatrix} u_x & v_x & n_x \\u_y & v_y & n_y \\u_z & v_z & n_z \end{bmatrix}$$

- Specify the view reference point (VRP) with respect to the WCS and then specify camera with respect to the WCS
- Define VRP `R(r_x, r_y, r_z)`
- Compute M from u, v, n
- define eye in VCS
    $E(u_e,v_e, n_e) = (0, 0, -e)$
- in WCS the eye becomes $E_{WCS} = M.E + R$
- Join the eye with every pixel on the image plane (UV plane)

##### Window 
- Define window size `W_l, W_r, W_t, W_b`
- For pixel(i, j) where $u_i^* = W_l + i\Delta u$ and $v_j^* = W_t - j\Delta v$
- Thus coordinates of pixel (i, j) are  
    $\Delta u = (W_r - W_l) / \text{MAXCOLS}$  
    $\Delta v = (W_t - W_b) / \text{MAXROWS}$
- MAXROWS and MAXCOLS can be used to control the resolution of the image  
    $P_{ij}^* = (u_i^*, v_j^*, 0)$ pixel coordinates
- $E_{WCS} = M.E + R = M.[0 0 -n_e]^T + R$
- Direction of the ray from the eye through pixel at (i, j) in WCS 
- __TODO__

##### Basic Idea
- For every pixel in the image
    * Shoot a ray
    * Find closest intersection with object
    * Find normal at the point of intersection
    * Shoot secondary ray

###### Transforming objects
- ray `s + ct`
- Objects : Sphere, COne, CYlinder, Box
- We assume the objects to be normalized so that the ray-object intersection is easier
- For e.g Sphere:  
     $x^2 + y^2 + z^2 = 1$
- For each object has its own coordinate origin (OBJECT/MODELLING coordinate system)
- Transform M that takes from object space to world space
- If M includes a scaling then c isnot a unit vector after the transformation
- if c is renomalized then scale the value t accordingly

##### Side note on transformations
- Projective
    * **Affine**
        + **Similarity / Conformal**
            + isotropic scaling
            + Rigid / Euclidean
                + Translation
                + Identity 
                + Rotation
        + **Linear**
            + Identity
            + Rotation
            + isotropic scaling
            + scaling
            + reflection
            + Shear
    * perspective

Can be represented 4x4 matrices

#### Normals
- Transforming normals - think about tangents instead
- If V_T is an vector in the tangent plane then after transformtion it becomes $V_T' = M.V_T$
- the correct 

$$N^TV_T = 0$$  
$$N^T(M^{-1}M)V_T = 0$$  
$$(N^TM^{-1})(M.V_T) = 0$$  
$$(N^TM^{-1})(V_T') = 0$$  
__MORE ON SLIDES__


### Recursive Ray Tracing
- Primary Rays - from the eye
- Secondary Rays - Reflection, Refraction
- Shadow rays
- ((Ray Tree)) From eye where ray meets, then where the reflected and refracted ray meets

#### Reflected ray
- I Incident ray
- R Reflected ray
- N Suface Normal
- $R = I - 2(I.N)N$

## Illumination model
#### Types of surfaces
- Specular : bounce in the general mirror Direction (GLOSSY)
````

        \  |  /  -/
         \ | / -/
          \|/-/
        --------------
````
- Diffused : insted of light reflecting in a specific direction, light can reflect in any direction (LAMBERTIAN)
#### Phong model
- For a single light source total illumination at any point is given by;
- $$I = k_aI_a + k_bI_b +k_cI_c$$
- ambient, diffuse, specular
