# Lecture 6 <div style="text-align:right"> 23/01/2024 </div>

## Illumination model 
The PHONG model

    1) Reality
    2) best known modle of reality in Science
    ┆
    N) Phong Model (Ambient + Diffuse + Specular) Ka*Ia

## surfaces
- Diffuse (Rough)
- Specular (Smooth)

## Whitted Ray Tracing
- At most 2 secondary rays, (reflected and refracted) per ray-object intersection
- Point light source

## Ambient Reflection
- Makes the whole scene a little brighter
- Represent the reflection of all indirect illumination 
- has the same  value everywhere
- is an approximation to computing global illumination

## PATHS
- LSE (Light Specular Eye)
- LSDE(Light Specular Diffuse Eye)
- LDE(Light Diffuse Eye)
- In whitted, paths are not possible if light bounces from diffused 

## diffused illumiation
- Color Bleeding (light bouncing from one diffused surface to other diffused surface)
- $I_d = I_lcos\theta_l$
- Reflection light according to lamberts cosine law
- Assumes ideal diffuse
- __TODO__  FROM SLIDES
- light that appear at more grazing angle(higher angle with normal) have lower illumination

## Specular 
- $I_s = I_Lcos^n\alpha_v =I_L(R.V)^n$
- Ideal Specular surface reflects only along one direction
- Reflected intensity is view dependent Mostly it is along the reflected ray but as we move away some of the reflection is slightly offset from the reflected ray due to microscopic surface irregularities
- alpha is coefficient of shininess and gives the size of bright spot on a surface
- $I_L = \frac{I_t}{r^2}$ $I_t$ is the intensity of the light source and r is distance from source
 
## BRDF (Bi-Directional Reflectance Distribution Function)
- Lambertian BRDF
- Cosine Lobe

## OTHER MODELS
- Local/Direct Illumination Model
    * $I_{local} = k_aI_a + \sum_{1\le i\le m}(k_dI_{di} + k_sI_{si})$
- Global Illumination Model
    * $I_{global} = I_local + k_rI_{reflected} + K_tI_{transmitted}$
- Reflected an transmitedd components may also be attenuated based on distance the ray travels

## Surface material properties
### Colors 
- for each object there can be a 
    * Diffuse color, specular color, reflected color and tranmitted color
    * Remember differently colored light is at different wavelength so

## Recursive ray tracing
> complexity = h * w * N<sub>objects</sub> * 
            intersection cost * depth of recursion * N<sub>shadow rays</sub> * ...

## Stopping recursion
- When ray leaves the scene
- Whenever calculating the K_r an K_t if it falls below threshold
- Number of bounces

## Optimization
- Bound (MaxMin x, y, z) each object in a bounding box
- check if ray hits bigger bounding box, if it hits then check if it hits children 
- This is called bounding volume hierarchy (from class of algorithm called space subdivision algorithms)
> other space subdivision algorithm include octree in 3d and quadtree in 2d or even a regular grid, Brassenham algorithm
- Aliasing - Discrete samples of continuous world
- anti-aliasing - shoot more rays per pixel 
    * super sampling:
        + regular
        + adaptive ( shoot some rays, check where intensity varied, do more sampling there)
        + stochastic or jittered(shoot rays in random direction)
