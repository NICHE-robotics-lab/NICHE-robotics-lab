---
layout: post
title: "Fourier Birds: Drawing a Hummingbird with Harmonics"
date: 2025-03-25 10:30:00 -0700
inline: false
related_posts: false
---

Sometimes art and engineering meet — and when they do, Fourier harmonics can help us draw elegant curves from complex shapes. In this tutorial, we’ll reconstruct a hummingbird from its image silhouette using the **Fourier descriptor method**.

### Step-by-step

We start by:
- Converting the image to a binary silhouette
- Extracting the largest contour (the bird)
- Uniformly sampling boundary points
- Applying a Fourier Transform and filtering to smooth it
- Reconstructing the shape with limited harmonics

Let’s dive in.

---

### Python code

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

# Step 1: Load and preprocess the image
img = cv2.imread('humming2.jpg')
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
_, bw = cv2.threshold(gray, 0, 255, cv2.THRESH_BINARY + cv2.THRESH_OTSU)
bw = cv2.bitwise_not(bw)

# Step 2: Find largest contour
contours, _ = cv2.findContours(bw, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_NONE)
contour = max(contours, key=cv2.contourArea)
pts = contour[:, 0, :]
x, y = pts[:, 0], pts[:, 1]
z = x + 1j * y

# Step 3: Resample uniformly
n = 3000
t = np.linspace(0, 1, len(z))
tq = np.linspace(0, 1, n)
z_uniform = np.interp(tq, t, z.real) + 1j * np.interp(tq, t, z.imag)

# Step 4: Apply Fourier transform and keep a few harmonics
Z = np.fft.fft(z_uniform)
m = 50
Z_filtered = np.zeros_like(Z)
Z_filtered[:m] = Z[:m]
Z_filtered[-m:] = Z[-m:]
z_smooth = np.fft.ifft(Z_filtered)

# Step 5: Plot
plt.figure(figsize=(6, 6))
plt.plot(z_smooth.real - np.mean(z_smooth.real),
         -(z_smooth.imag - np.mean(z_smooth.imag)),
         color='firebrick', linewidth=2)
plt.axhline(0, color='gray', linestyle='--')
plt.axvline(0, color='gray', linestyle='--')
plt.text(10, 0, "x-axis", verticalalignment='bottom')
plt.text(0, 10, "y-axis", horizontalalignment='left')
plt.title("Hummingbird Reconstructed with Fourier Harmonics")
plt.axis('equal')
plt.axis('off')
plt.show()

```