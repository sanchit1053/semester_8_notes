# Lecture 4 <div style='text-align:right;'> 16/01/2023 </div>

## Raster Image
- binary - 0 and 1 value
- Grayscale, Single value floating point or byte (8 bit Image)
- Color - Triplet of values, 24 bit image

### Resolution, Bit Depth (bits per pixel), Transperancy

## Hydanamic Range Image 
- Dynamic Range ~ ratio of luminance of brightest and darkest regiono fan image
- Capture, Display, Transmission, storage

##### Exposure
- Low exposure: Assume that the whole picture is well lit 
- High exposure: Assume whole photo is inside, causes the windows to become saturates
- Exposure_fission

##### Tone Mapping
- Tone mapped back to low dynamic range of devices
- Higher bit depths can represent tmore dynamic range

---------------------------------------

# Ray Tracing

## Rendering Image
- Drawing images on the computer sreen
- We have seen one redering method already (Rasterization)
- Issues
    * Visiblity
        + Whatparts of a scene are visible?
            + Clipping
            + CUlling (backface and occlusion)
    * Illumination
        + Reflection, Refraction, Shadows

## RECAP
- There is a near plane, far plane, And view frustum
- Part of world that lies outside the view frustum is removed (Clipping)
- If we do in 2d then clipping, if we do in 3d then it is called culling

## Ray tracing
- Tracing the rays of light to model the interactin of light with objects
- (ideally called linear ray tracing)
- (We will disregard the wave nature of light)
- Light comes from source, reflects from objects and fall on camera
- Many rays will not contribute to the image (as they will not fall on camera)

## camera model 
- Pin hole camera model, 
- there is the position of camera
- There is direction in which it is pointing
- Up-Vector, The direction that is up
- focal-length, field of view(specify horizontol, vertical or one and aspect ratio)
- near-plane becomes default image-plane

## Basic Idea
- For every pixel in the image
    * Shoot a ray
    * Find closest intersection with object
    * find normal at teh point of intersection
    * compute illumination at point of intersection
    * Assign pixel color
- Reflection
    * Shoot a ray
    * Find closest intersection with object
    * find normal at teh point of intersection
    * compute direct iluumination at point of intersection
    * Shoot secondary rays and collect indirect illumination (mulitple secondary colors by factory)
    * return pixel color as sum of direct and indirect illumination
- Shadow Rays
    * Shoot a ray toward a light source,
    * If it does not hit any opaque object in its path then the object contributes to the color
- Ray Casting
    * The first ray from the camera (no secondary rays)

## To Be Viable
- Visibility
    * Ray- Object intersections
- Illumination
    *

## Ray Representation
- $R_0 = [x_0 y_0 z_0]$ Ray Origins


# __TODO__
