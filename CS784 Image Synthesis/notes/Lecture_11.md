# lecture 11 <div style="text-align"> 13/02/2024 </div>

## Photon Mapping

$$
    L_0(p,\omega_0) = L_e(p, \omega_0) + \int_\Omega f_r(p, \omega_0, \omega_i)L_i(p, \omega_i)cos\theta_id\omega_i
$$

photons mapping algorithm
- Emit photons
- Trace photons
- store photons
    * caustic photon map
    * global photon map
- gather photons

### Reflected Radiance Estimate
- *Read Slides for equations* 

### KD Tree
- Take objects x cooridnates and then divide along the x axis
- Then for each peice take y coordinates and choose the median 
- Very good for k-nearest neighbour queries

## Point based GI
- Divide scene into surfels
- Each surfel is a small disk - point, radius, normal, outgoing radiance
- Record direct illumination on these surfels
- Splat these on the hemisphere around a point in the gather phase and add to compute GI
- on every disk calculate the direct illumination
- To compute global illumination, consider the hemisphere at the surfel
- project all the surfels you can see on the hemisphere
- add them up
- fast by rasterization from the required surfel

# Volume Graphics
- Rendering hair, Grass
- *See Slides* 
