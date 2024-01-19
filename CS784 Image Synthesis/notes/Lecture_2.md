# CS 784 Lecture 2 <div style="text-align: right;"> 09/01/2024 </div>
## Digital Light
Book by Alby Ray Smith, History of Pixel

#### Joseph Fourier
- All funcitons of a variable are made of a combination of sine waves.
- The Fourier Transform
    * $G(u) = F\{g\}(u) = \int_{-\infty}^{\infty}g(x)e^{-i2\pi u x}dx$
- The Inverse Fourier Transform
    * $g(u) = F\{G\}(u) = \int_{-\infty}^{\infty}G(x)e^{i2\pi u x}dx$

Take a wave and "bind" it along a circle, that is run the wave on a circle, 
If the binding frequency is equal to the frequency to the given wave then the centroid of the binded one will have a peak 


You can form any image by a combination of suitably modulated sin images

| Spatial domain             | Frequency domain                            |
|-----------------           | -------------------                         |
| Impulse                    | uniform                                     |
| rectangle                  | Sync                                        |
| Sin                        | two pulses at freq and -freq                |
| comb(pulses with dist T)   | comb(pulses with distances $\frac{1}{T}$)   |

## Vladimir Kotelnikov 
- Sampling Theorem
    * If the highest frequency in a functino of a variable is $f_{max}$ cycles per second, then it can be completely reconstructed from its samples spadd no more than $\frac{1}{2f_{max}}$ seconds apart
- By Shannon and Nyquist

## Convolutions 
- Convultion Operator
- $r(x) = \{g * h\}(x) = \int_{-\infty}^{\infty}g(\alpha)h(x - \alpha)d\alpha$
- Convulotion Theorem
- __TODO__

## Pixel is Born
- A PIXEL or picture elemetn is a discrete, point (visual or light) sample of the continuoius real world.
- It has no size, 
- It has no shape
- We can (re)construct views of the (real) world from pixels.
- Digital Light 

## Capturing Light
- Bayers Filter, 2 the number of green filters than red and blue filters as eye is more sensitive to light in the green wavelenth
- Interpolation is done on the intensity of individual colors, (this is called Demosaicing)
- __Aliasing__

## Displaying Light - Monitors
- Crts
- leds

## Color Model

- RGB
    * Uses additive color mixing
    * What kind of light needs to be emitted to produce a given color.
- CMYK
    * Uses subtractive color mixing
    * What kind of inks need to be applied, so that reflected light from the substrate throuht the inks produces the color

Maximum color perception on fovia
## COlor Spaces
- Spectral Color
    * Color evoked by monochromatic light
    * $X=\int_\lambda L_{e, \omega, \lambda}(\lambda)\bar{x}(\lambda)d\lambda$
    * $Y=\int_\lambda L_{e, \omega, \lambda}(\lambda)\bar{y}(\lambda)d\lambda$
    * $Z=\int_\lambda L_{e, \omega, \lambda}(\lambda)\bar{z}(\lambda)d\lambda$
- Standard color space is called CIE RGB color scpace
- Projected a color from a projector, he can vary R, G, B dials, he needs to match the color to the target color

## RBG Color Spaces
- R, G, B chromaticity coordinates
- Chromaticity of the White Point
- Tone response curve or gamma
    * Used to model human perception of brightness under common illumination conditions
    * Greater Sensitivity to changes in brightness in dark regions than highlights
    * if non-linear mapping is not done, too many bits are allocated to highlights, and too few to dark regions
