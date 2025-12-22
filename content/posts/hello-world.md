---
title: "Linking Digital Image Observations to Physics"
date: 2025-12-22T22:25:00+05:30
draft: false
math: true
---

Color is a **perceptual** phenomenon. The perception of color involves both physics and the brain.

What we perceive as color is electromagnetic radiation coming off a surface as a spectral power distribution. A tomato appears red because its surface reflects radiation mostly around 700 nm.

The human eye has three kinds of color‑sensitive cells for perceiving color: short, medium, and long wavelength cones, each sensitive to wavelengths that correspond roughly to blue, green, and red channels.

We mathematically model this by projecting the spectrum to a three‑dimensional color space. Projecting an infinite‑dimensional spectrum onto a three‑dimensional space results in the loss of information and leads to **metamers** (different spectra with the same RGB).

In 1931, the CIE established color spaces that define this relation.

The trichromatic values from spectral data are calculated as follows:

\[
X = \int R(\lambda)\,\bar{x}(\lambda)\,d\lambda,\quad
Y = \int R(\lambda)\,\bar{y}(\lambda)\,d\lambda,\quad
Z = \int R(\lambda)\,\bar{z}(\lambda)\,d\lambda
\]

Here \(R(\lambda)\) is the spectral power distribution, and \(\bar{x}, \bar{y}, \bar{z}\) are the color matching functions published in CIE 1931 based on color matching experiments. Y represents luminance, and Z is roughly equivalent to the blue of the CIE RGB curves.

RGB is computed by a linear transform of \([X\;Y\;Z]^T\).
