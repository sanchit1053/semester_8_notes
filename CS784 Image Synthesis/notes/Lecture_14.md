# lecture 14 <div style="text-align:right"> 12/03/2024 </div>

## Radiance along a Ray
- is constant in free space
- All possible rays - represented by a 7D plenoptic Function
- $L_{7D} = f(x, t, z, \theta, \phi, \lambda, t)$
- This is too complicated to work with
- So we work with a 4D parameterization instead - LightField

## Lightfields

- A 4d parameterization of rays using 2 planes
    * LightField rendering
    * Lumigraph

parameterizing the lightfield
- Any ray can be parameterized with 4 parameters - indexes on th uv and st plane
- The discretization on the uv plane is denser than on th est plane - objects is on/near the uv plane - which is the focal surface

example
- one objects
- 4 cameras say each having 64 samples
- we will get 4 images with 64x64 sample

## Lightfield Rendering
- Aliasing happens during reconstruction
    * low pass filter interpolation
    * etween nearest 16 points
- for each ray from (s,t) to (u,v)
- find nearest camera on st and nearest points on uv, interpolate

## Reparameterizing the lightfield

-Every ray $r = (s,t,u,v)$ is reparameterized as $r = (s,t,f,g)$ corresponding to a focal surface

## aperture
- smaller aperture give large view of field
- If too large a aperture we can even remove the foreground

