# Lecture 7 <div style="text-align:right"> 30/01/2024 </div>

## Vitae Ray Tracing
- cannot do everything with only reflected ray 
- Such as hazy mirror or frosted glass

CHECK BRDF Mirror, glossy, transparent, translucent (glossy transparent)

## Distributed Ray Tracing
- Have 4 Distributed reflection

- Soft Shadows
 
    $$\sum s_i (\text{DIRECT-ILLUM})_i + \text{INDIRECT}$$
 
    * s_i is the percentage of points that are incident on light source
- Depth Perception
    * Move the camera front and back to have clear image only for certain depth
- Motion Blur
    * shoot different rays for different frames of an animation

## Rendering Equation
$$L_0(x, \omega, \lambda, t) = L_e(x, \omega, \lambda, t) + \int_\omega f_r(x, \omega', \omega, \lambda, t) L_i(x, \omega', \lambda, t)(-\omega \cdot n)d\omega'$$
- L_0 
    * Is the total amount of light of wavelentth $\lambda$ directed outward along direction $\omega$ at time $t$, from a particular position $x$
- L_e
    * is the emitted light
- L_i
    * is the light of wavelentth $\lambda$ coming inward toward x from direction $\omega'$ at time t
- f_r
    * is the BRDF. It is the proportion of light reflected from $\omega'$ to $\omega$ at position x, at time t and wavelentgh $\lambda$
- $-\omega \cdot n$
    * **TODO** 

# Radiometry
- Self Shadows
    * Things like grass or hair should have shodow on itself
- Subsurface Scatterring
    * Light goes inside the object and does not reflect directly from point of incidence

## Ground Rules for Global Illumination
- Geometric Optics
    * not considering liht as oscillating EM fields, not quantum properties
- Radiative transfer
    * linearity, energy conservation, steady state
- No mention of polarization, phospohoresence

## Basic Radiometry

- Radiant Flux $\Phi$
    * Total amount of energy passing through a surface/ region of space per unit time
    * has units of power (watts (W) or joules/second($Js^{-1}$))
- Irradiance E (incident) and Radiant Exitance M (out of surface)
    * Area density of flux arriving/ leaving a surface
    * has units $Wm^{-2}$
    * irradiance at a point on the outer sphere is less than irradiance at a point on the inner one
    * Energy recieved from a light source falls off with squared distance from it
        $$E = \frac{\Phi}{4\pi r^2}$$
    * Origin of Lamberts Law
        + Light arriving at a surface is proportional to the cosine of the angle between the light direction and surface normal
            $$
        \begin{align} 
                E_1 =& \frac{\Phi}{A_1} =& \frac{\Phi}{A} \\ 
                E_2 =& \frac{\Phi}{A_2} =& \frac{\Phi}{A/cos\theta}
        \end{align}$$

- Intensity
    * Flux density per unit solid angle $I = \frac{d\Phi}{d\omega}$
    * Has units of $Wsr^{-1}$
    * A steradian is defined as teh solid 
    * __TODO__

- Radiance L
    * flux density per unit area per unit solid angle $L = \frac{d\Phi}{d\omega dA^{\perp}}$
    * $A^{\perp}$ is the projected area on the surface perpendicular to $\omega$
    * Measured in $Wm^{-2}sr^{-1}$
    * Radiance remains constant along rays of light through empty space

## Photometry
- THe human eye is more sensitive to some wavelengths of teh visible light than other
- The spectral response curve $V(\lambda)$
- blue light has to be 5 times stronger to have same brightness as green
- For every radiometry quantity a corresponding photometry quantity

## Luminance and Radiance
$$ 
\begin{align*}
L_v &= \int L(\lambda) V(\lambda) d\lambda \\
L_v &= 683\int L(\lambda) Y(\lambda) d\lambda \\
\end{align*}
$$
where Y i sthe standard CIE spectral response curve

## Radiometric computations
$L_i(p, \omega)$ is incident radiance at p coming from a direction $\omega$
Notice $\omega
