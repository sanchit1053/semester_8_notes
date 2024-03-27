# lecture 16 <div style="text-align:right"> 19/03/2024 </div>

## Instant Neural Graphics Primitives with Multiresoultion Hash Encoding
- Not Nerfs as it made other things faster too

#### Rendering Training Algorithm (not in class)
- Did Task Specific GPU implementation
- eg on :- radiance caching field
- 10-100 times fewer steps

#### Small Neural Network
- Only one layer deep for density and two layers for color
- Entire network in cuda kernel
- fully fused implementation 
- 5-10 times faster than TensorFlow

#### Multiresoultion Hash Encoding
- better speed vs quality tradeoff than prior work
- Task agnostic

## Fully Fused Neural Networ
- Standard MLP with 
    * __READ FROM SLIDES__

CUDA
+ Entire nerual Network implemented as a single CUDA kernel

```mermaid
graph LR
    a["Stream of Vertices"] --> GPU["GPU <hr> series of <br> Streaming media"] --> b["Stream of pixels"]
```
+ CUDA has a hardware abstraction, programmer needs only cuda, not hardware
+ kernel is just a piece of code function
+ say 
    + f1 : 3 blocks
    + f2 : 2 blocks
    + f3 : 2 blocks
    + If 10 SMs then 6 f1, 2 f2, 2 f3 can run 
+ warp, each thread run same instruction instead of blocks where different instructions can be running
+ much faster than tensorflow

## input Encoding
- Replace large neural network with samaller network conditioned on a different feature representation

##### Uniform Grids
Create a uniform grid and for points not on grid interpolate from nearest grid point
- pros:
    * Easy to implement
    * Algorithmically fast access O(1)
    * Estabilished operations like convulations
    * simple topology
- cons:
    * Expensive in memory an dbandwidth
    * limited by Nyquist

##### Sparse Grids
No vertices for cells which are empty
- pros:
    * memory efficient
    * Algorithmically efficient access O(log(n))
    * GPU compatible data structures
    * Estabilished operations like sparse 3d convulation
- cons:
    * Need to manage a complex data strucutre
    * __MORE ON SLIDES__


##### Point Clouds (irregular Grids)
create random points, for any point take a gaussian on it and  take points falling in the gaussian
- pros:
    * Non limited by Nyquist
    * can be densely supported in space (more points in denser region)
    * Expressive
- cons:
    * often needs complex data structres for fast access and interpolation of kernel
    * heavily affected by choice of kernel

##### Multiresoultion Grids
Point expressed in terms of multiple resolution of points, interpolating from grid vertices  
Causes smoothing of points 


##### hash grid
Instead of storing point, store the hash of the points
- If code book is small then all memory can fit, making it fast
- But it may lead to collisions
- featrures from different place might hash into same entry

## Multiresoultion hash Encoding
- Hashing for different resolutions
