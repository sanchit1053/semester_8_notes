# CS 784 Lecture 1 <div style="text-align: right;"> 05/01/2024 </div>

## What is Image Synthesis
- Study the methods to synthesize images using a computer
- What kind of images
    - Photorealistic vs. Non-photorealistic
    - Algorithmically generated vs. Manually generated 
    - neurally generated vs. non-neurally generated
    - Real-time vs. Offline

## How is this subject different from...
- Image Processing
- Computer Vision
- Computational/Medicinal imaging
- Computer Graphics

## what is rendering
- Create a discrete view of a continuous world
- color the pixels (The render image is discrete so smallest part has a homogenious color)
- Methods 
    - Real time → Rasterization (small patches arranged in a grid, if a object in a pixel then color pixel or not)
    - Ray tracing  

### Ray Tracing
- geometry and a light source, light from source and bounces on object in scene, some of them fall on the camera
- This is wasteful as many rays do not fall on camera
- follow the path of the rays that pass through the camera i.e. shoot rays from the camera (__Direct or Local Illumination__)
- Light rays can bounce multiple times and then the sample becomes combination of all (__indirect Illumination__)
- Together direct and indirect illumination become __global illumination__
- In what direction to bounce 
    * Depends on properties of the surface (Bidirectional Reflectance Distribuition Function BRDF)

## Image Based Rendering
- Panaroma
- LightField Rendering
