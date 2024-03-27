# Lecture 18 <div style="text-align:right"> 26/03/2024 </div>


## Image Synthesis for MR(Mixed Reality AR+VR)

### Monte Carlo Path Tracing
- choosing a random sample location in a pixel
- Trace ray from the eye through the pixel location
- Sample BRDF to find bounce direction at hit surface
- Iterate

## Issue that affect MR
- Latency : Motion to Photon Latency has to be of the order of 20ms
    * Motion Detection
    * Visual processing
    * Display
- Vergence-Accomodation Conflict
    * Vergence an accomodatin mechanisms
- Coherent Rendering for AR
    * Occlusion beween real and virtual elements
    * Illumination from the real used to light the virtual

## Two Sides of learning how to render

#### VR
- Learning how to render a good purely synthetic image
    * Application to virtual reality(VR)
    * More realistic reandreing gives better immersion
    * We want good images in less time with less noise

#### AR
- Learning how the real world looks so that we can add synthetic elements to it 
- __READ SLIDES

## Learning how to render for Virtual Reality

### Strategy 1 : Removing the noise
### Strategy 2 : Better quality where gaze is
### Strategy 3 : Make it easier to see

Kinect camera produces a RGBD image, one image with color and one with depth
