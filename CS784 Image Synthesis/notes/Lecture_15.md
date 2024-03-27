# lecture 15 <div style="text-align:right"> 15/03/2024 </div>

## Neural Fields
Coordinate Sampling   
→ Neural Network   
→ Reconstruction Domain(Radiance field , signed distance field)  
→ forward maps   
→ sensor domain

Distance field, inside or outside of a object  
Want neural network to output the values of the current field

Bridge between the reconstruction and the measurement is forward maps(sphere tracing, volume rendering)

## Neural Radiance Field (NeRF)
- input a ray $x, y, z, \theta, \phi$
- Output a radiance estimate (color $c$) and a transmittance estimate (density $\sigma$)
- A parameter value inside the volume but no object then background color and density is 0
- If falls on a object then the density is 1

### Rendering Scene Volumes
- Volume Rendering Integral 

$$
\begin{align*}
    I(D) = I_oe^{\tau(0, D)} + \int_0^Dc(t)e^{-\tau(0, t)}dt
\end{align*}
$$

- Assume $I_0 = 0$
- if ray $r(o,d) = o + td$ sampled from $t_n$ to $t_f$
- __READ FROM SLIDES__
- $t_n$ is the near value 
- Multiple samples are taken along the ray at different t values, the colour at each sample is $c(r(t), d)$
- Then the aggregate color along the ray is obtained as 

$$
\begin{align*}
    C(r) &= \int_{t_n}^{t_f}T(t)\sigma(r(t))c(r(t), d)dt \\
    \text{where } T(t) &= e^{-\int_{t_n}^t\sigma(r(s))ds}
\end{align*}
$$

- $T(t)$ is probability of not hitting anything from $t_n$ to $t$
-----------
- For Homogeneous media with constant colour $C_a$ and density $\sigma_a$ over some interval [a, b] aggregate color over the interval is 
- __READ FROM SLIDES__
- If $\sigma_a$ is 0 then it is transparent and if it is 1 then there is fall off
- Discretize the aggregation


$$
\begin{align*}
    T_i &= e^{\sum_{k =1}^{n-1}\sigma_k\delta_k} \\ 
    \alpha_i &= (1 - e^{-\sigma_i\delta_i}) \\
    T_i &= \prod_{k = 1}^{i}(1 - \alpha_i)
\end{align*}
$$

- **Alpha Composting**  
- The final equation is just sum of $T_i\alpha_ic_i$ which is differentiable over both c and $\sigma$ which are the outputs

#### Architecture
- 9 layers with 256 values in each
- input collection of images (for each image we know the position and orientation of camera)
- create ray from camera center through pixel
- sample ray at equal distance
- for each sample we get ($x, y, z, \theta, \phi$)
- Neural network give $RGB\sigma$
- photometric consistency, same point from multiple views then color value is consistent

## Hierarchical Sampling
- one MLP given the Coarse set of samples which return the (color, density)
- other MLP take the fine and coarse samples and return (color, density)

+ if the whole data is given at once then neural network does not work well as the network has the power to change
+ Give it the point coordinate at start and take density, then feed the direction, which will give the RGB
