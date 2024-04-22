# Lecture 20 <div style="text-align:right"> 05/04/2024 </div>

## 3d Gaussian Splatting for Radiance Field Rendering

Get a volume and figure where radiance field is what

## EULERIAN vs LAGRANGIAN

## Surface Splatting
- We define a continous function on the surface represented by a set of points {Pk} as 
 
$$
\begin{align*}
    f_c(u) = \sum_{k \in N} w_k r_k (u - u_k)
\end{align*}
$$

- Further given a mapping from object surface to screen space  

$$
\begin{align*}
    x = m(u); \mathbb R^2 \rightarrow \mathbb R^2
\end{align*}
$$

- Rendering involves the following
    * Warp $f_c(u)$ to screen space $g_c(x) = f_c(m^{-1}(u))$
    * Bandlimit screen space signal $g'_c(x) = \int_{\mathbb R^2} G_c(\xi)h(x - \xi) \;d\xi$

**READ FROM SLIDES** 


#### Orthographic Projection

$$
\begin{align*}
    \begin{bmatrix} 
        1 & 0 & 0 & 0 \\
        0 & 1 & 0 & 0 \\
        0 & 0 & 0 & 0 \\
        0 & 0 & 0 & 1 \\
    \end{bmatrix}
\end{align*}
$$

#### Perspective Projection

$$
\begin{align*}
    \begin{bmatrix} 
        1 & 0 & 0 & 0 \\
        0 & 1 & 0 & 0 \\
        0 & 0 & 0 & 0 \\
        0 & 0 & r & 1 \\
    \end{bmatrix}
\end{align*}
$$

So the perspecive becomes

$$
\begin{align*}
    \begin{bmatrix} \frac{X}{1 + rz} & \frac{Y}{1 + rz} & 0 \end{bmatrix}
\end{align*}
$$



