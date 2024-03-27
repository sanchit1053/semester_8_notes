# lecture 13 <div style="text-align:right"> 05/03/2024 </div>

## Image Based Rendering
- Multiple images of the object from varying angles
- Using this creating a point cloud
- Made it work on a few GPUS (Rome built in cloudless day)
- Image of object that we see is exactly is the radiance carried by the image
- use images to model readiance carried by a ray through a point in any direction

## Model to Images
    
    Only Images                                                                                     Only Geometry
    ------------------------------------------------------------------------------------------------------------
    LightField    Panaromas  View          Planar Geometry with Textures      meshes            meshes with 
    Lumigraph                Morphing      Layered    Sprites   Billboards     with textures     vertex colors
                                            Depth
                                            Image

- Model the geometry as piecewise planar approximation and place textures on the planes

Example
- Given a front view of an image where the real geometry has 2 protrusions in the side view
- In front view cannot tell and it will just put texture on a wall

#### Billboard (gaming)
- Flat texture that is always pointing towards the camera so the 

#### sprites (gaming)
- They don't rotate to face the player

#### Layered Depth Images (graphics)
- Divide a image into different layers depending on percieved depth

#### View Morphing
- Transform the images I0 and I1 to parallel views
- Can then linearly interpolate between images to get any view

#### Panaromas
- Assume a environment shape such as cube, sphere
- stitch images on the surface of these models

## radiance along a ray
- Is constant of free space
- All possible rays - represented by a 7D Plenoptic function
- $L_{out} = f(x, y, z, \theta, \phi, \lambda, t)$
- This is too complicated to work with
- So we work with a 4D parametrization instead - Light Field
- Don't want $\lambda$ and $t$ that is the environment will remain the same, ignore their effects

### Lighfield Rendering
- Called the light slab representation
- Assume thier are two planes
- can get any ray between the planes as $L(u, v, s, t)$
- first p
