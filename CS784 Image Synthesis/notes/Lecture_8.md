# Lecture 8 <div style="text-align:right"> 02/02/2024 </div>

# THE BRDF
- differential Irradiance at p is $dE(p, \omega_i) = L_i(p,\omega_i)cos\theta_id\omega_i$
- Reflected differential readiance is then given by $dL_0(p, \omega_o) \propto dE(p, \omega_i)$
- $$f_r(p, \omega_o, \omega_i) = \frac{dL_o(p, \omega_o)}{dE(p, \omega_i)}$$
- Convention, Rays point outside out of the surface

1. Reciprocity
    $$f_r(p, \omega_o, \omega_i) = f_r(p, \omega_i, \omega_o)$$
    Rays from one side is same as rays from the other side
2. Energy Conservation
    $$\int f_r(p, \omega_o, \omega')cos\theta'd\omega' \le 1$$
    integrate over all angles then it has to be less than one as outgoing energy cannot be more than incoming energy
3. consider a general f() over the sphere of all directions and we get the BSDF(BRDF + BTDF)
    $$L_o(p, \omega_o) = \int_\Omega f(p, \omega_o, \omega_i)L_i(p, \omega_i)|cos\theta_i)|d\omega_i$$

#### Sources
- Measured Data ()
- Phenomenological models (cos theta ^ n)
- Simulations ()
- Physical (wave) Optics (frenel reflection)
- Geometric optics (angle of incidence = reflection)

##### Types of surfaces
- Diffuse
- Glossy Specular
- Perfect Specular
- Retro reflective

### Ideal Diffuse BRDF
 $$\text{Let } f_r(p, \omega_o, \omega_i) = k_d$$
- Assume BRDF reflects a fraction p of the incoming light

    $$
    \begin{align}
        \int f(p, \omega_o, \omega_i)cos\theta_id\omega_i &= p \\ 
        k_d \int \int cos\theta_isin\theta_id\theta_id\phi_i &= p \\
        2 \pi k_d \int cos\theta_isin\theta_id\theta_i &= p \\
    \end{align}
    $$


### Ideal Mirror BRDF
- CHeck slides from formula

### Fresnel Reflectance
- Slides
- Schlik Approximation
    $$F_r = F_o + (1 - F_o)(1 - cos\theta)^5$$
    $$F_o = \left(\frac{\eta_1 - \eta_2}{\eta_1 + \eta_2}\right)^2$$

### Specular Transmittance
- BTDF is zero 

### Glossy BRDF
$$f_{phong} = k_s (\omega_o.R(\omega_i, \hat{n}))^g$$
Phenomenological

$$f_{bling_phong} = k_s' (\omega_{half} . \hat{n}))^h$$
also, Phenomenological but gives less error

## Microfacet BRDF
- Described by a function giving the distribution of microfacet normals, $\vec{n_f}$ with respect to surface normal $\vec{n}$greater variation indicates a rougher surface.
- Also necessary to describe teh BRDF for the individual factes
- First Described by Torrance-Sparrow
- in BLinn-phong, the distibution of microfacet normals is approximated by an exponential falloff

$$ 
\begin{align}
    D(\omega_h) &\propto (\omega_h . \hat{n})^h \\
    D(\omega_h) &= \frac{h + 2}{2\pi}(\omega_h . \hat{n})^h \\
\end{align}
$$

**Check slides** 
