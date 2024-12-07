---
title: "Constraining the Cosmology with Void Size Function based on Delaunay Triangulation"
collection: research
permalink: /research/DTVoid
excerpt: "still ongoing..."
date: 2024-11-01  # this is only for sorting the pages
---

Collaborators: Cheng Zhao, Yu Liu (both from Tsinghua University)

**Background:** Cosmic voids are the areas where the matter density is significantly lower than galaxy areas. Various methods have been proposed to find voids. [Zhao et al. 2016](https://ui.adsabs.harvard.edu/abs/2016MNRAS.459.2670Z/abstract) proposed a way to find voids using galaxy / halo catalogs with Delaunay Triangulation, which could find far more voids than other methods such as ZOBOV, and exhibits the potential of significantly reducing the statistical uncertainty of void-related statistics ([Zhao et al. 2020](https://ui.adsabs.harvard.edu/abs/2020MNRAS.491.4554Z/abstract)).

In this work, we plan to use the size (radius) function of the above void to constrain the cosmological parameters. As there is no analytical model for the Delaunay triangulation We will first train an emulator using Quijote simulation, and them apply the emulator to the real observation data.

1. We measure the void size function for halo catalogs from BSQ simulations of Quijote, which contains ~32,000 different sets of cosmological parameters. Due to the low resolution of Quijote, the void size function at small radius end is not accurate. However, the large radius end is accurate, and we may use a simple gaussian function to describe the large radius end of void size function (**Figure 1**). ![DTVoid1](/images/DTVoid1.png)
2. We extract the gaussian parameter (i.e. the mean and the standard deviation) for the BSQ simulations. By ploting the parameter response, we discover that the void size function is the most sensitive to $$\Omega_m$$ and $$\sigma_8$$ (**Figure 2**). ![DTVoid2](/images/DTVoid2.png) ![DTVoid3](/images/DTVoid3.png)
3. We train a MLP to map the cosmological parameters to gaussian parameters. The response of our emulator is consistent with the data (red lines in **Figure 2**).
4. Using the Fiducial simulations of Quijote, we get the preliminary constraining power. Although the statistical error seems promising for $$\Omega_m$$ and $$\sigma_8$$, severe bias still exists (**Figure 3**). ![DTVoid4](/images/DTVoid4.png)
5. Delaunay triangulation is highly sensitive to the precise position of every point, thus causing severe shot noise. To reduse the shot noise, we try the bootstrap method: we sample the halo catalog with replacement, exclude the repeative points, and measure the void size function. We do this for 30 times for a single set of cosmological parameters, and take the average of all void size functions. After applying this correction, the bias is significantly reduced, although the statistical uncertainty increases (**Figure 4**). However, as the bootstrap procedure consumes lots of computing power (30 times!), this is the result only for 4,000 sets of parameter out of 32,000 BSQ simulations. We believe the result will get improved if we use the full BSQ simulations. ![DTVoid5](/images/DTVoid5.png)

**Future work:**

1. Improve the way we extract gaussian parameters.
2. Run the bootstrap code for all ~32,000 BSQ simulations.
3. Hopefully we can apply to the BOSS data! 😀
