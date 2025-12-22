---
title: "Linking Digital Image Operations to Physics"
date: 2025-12-22T22:25:00+05:30
draft: false
math: true
---

What we perceive as color is electromagnetic radiation coming off a surface as a spectral power distribution. A tomato appears red because its surface reflects radiation mostly around 700 nm.

The human eye has three kinds of color‑sensitive cells for perceiving color: short, medium, and long wavelength cones, each sensitive to wavelengths that correspond roughly to blue, green, and red channels.

We mathematically model this for digital display by projecting the spectrum onto a three‑dimensional color space. Projecting an infinite‑dimensional spectrum onto a three‑dimensional space results in the loss of information and leads to **metamers** (different spectra with the same RGB).

In 1931, the CIE established color spaces that define this relation.

The trichromatic values from spectral data are calculated as follows:

\[
X = \int R(\lambda)\,\bar{x}(\lambda)\,d\lambda,\quad
Y = \int R(\lambda)\,\bar{y}(\lambda)\,d\lambda,\quad
Z = \int R(\lambda)\,\bar{z}(\lambda)\,d\lambda
\]

```python 
    delta_lambda = wavelengths[1] - wavelengths[0]
    S = reflectance * illuminant  # effective spectrum under D65

    X = np.sum(S * xbar) * delta_lambda
    Y = np.sum(S * ybar) * delta_lambda
    Z = np.sum(S * zbar) * delta_lambda
    XYZ = np.array([X, Y, Z])

```

Here \(R(\lambda)\) is the spectral power distribution, and \(\bar{x}, \bar{y}, \bar{z}\) are the color matching functions published in CIE 1931 based on color matching experiments. Y represents luminance, and Z is roughly equivalent to the blue of the CIE RGB curves.

RGB is computed by a linear transform of \([X\;Y\;Z]^T\).

```python 
    M = np.array([
        [ 3.2406, -1.5372, -0.4986],
        [-0.9689,  1.8758,  0.0415],
        [ 0.0557, -0.2040,  1.0570],
    ])
    RGB = M @ XYZ

    # normalize by D65 white
    white_reflect = np.ones_like(reflectance)
    S_white = white_reflect * illuminant
    Xw = np.sum(S_white * xbar) * delta_lambda
    Yw = np.sum(S_white * ybar) * delta_lambda
    Zw = np.sum(S_white * zbar) * delta_lambda
    XYZ_white = np.array([Xw, Yw, Zw])
    RGB_white = M @ XYZ_white

    RGB_normalized = RGB / RGB_white.max()
```