# Lecture 3 <div style="text-align:right;"> 12/01/2024 </div>

## Other Components of the HVS
- The eye can see EM waves with wavelengths from 380 to 780 nm - visible spectrum
- Depth Perception
    * Oculomotor - Vergence (eyeball rotation) Accomodation (focus change)
    * inocular - Stereopsis, Retinal Disparity
    * Moncular - Motion Parallax, perspective, size
- Color Opponency
- Color Constancy

## Light
- EM radiation
- Speed of light in vacuume is `c = 299,792,458 m/s`
- Exhibits dual nature
    * of a wave - waelength, frequency, amplitude
    * of a particle - photons
    * Explained by QED (Quantum Electro Dynamics)

## Measurement of Light
- Radiometry
    * Measurement of EM radiation
    * Radian Energy of a Photon is $h\mu = \frac{hc}{\lambda}$
- Photometry
    * Measurement of EM Radiation as percieved by the human eye.

## Tristimulus Color Theory
- Cones are of 3 types
    * Each of S(hort), M(edium) and L(ong) cones are differently sesitive to different wavelengths
- Suggests we should be able to use 3 parameters to describe all perceivable colors
- Spectral Color
    * Color evoked by monochromatic light
- Spectral power distribution (SPD) - power per unit area per unit wavelength

## Metamers
- Two different SPDs can be percieved as the same color.
- This is crucial for perceptual color matching by additive mixing

Color Model 
- RGB
    * used additive color mixing
    * what kind of light needs to be emitted to produce a given color
- CMYK
    * uses subtractive color mixing
    * what kind of inks need to be applied, so that reflected light from the substrate, and through the inks  produces the color

## Perceptual Color Matching (CIE RGB)
- Represent the target color in the basis of primary manochromatic colors
- Standardized by the Commision of illuminatino Engineers (CIE)
    * 700nm, 546.1nm, 435.8nm
    * 2 degree standard observer
- Color perception is linear ( __Grassman's Law__ )
    * Beam 1 has color (R1, G1, B1)
    * Beam 2 has color(R2, G2, B2)
    * Beam 3 is additive mix of Beam 1 and Beam 2 with weights w1 and w2 then
        + R3 = w1 R1 + w2 R2
        + G3 = w1 G1 + w2 G2
        + B3 = w1 B1 + w2 B2

## CIE XYZ Color space
- CIE RGB to XYZ is a linear mapping to have all coffecient as positive
- The XYZ primaries are imaginary colors
- Y is luminance (luminous intensity per unit area of light in given direction ) or brightness
- X and Z are components measure chromaticity
- XYZ is a 3D colorspace
- xyY chromaticity luminancy colorspace (projection on the x + y + Z = 1 plane)
    $$x = \frac{X}{X + Y + Z}, y = \frac{Y}{X + Y + Z}$$

## Non Linear RGB Color Space
- R, G, B chromaticity coordinates
- Chromaticity of the white point
