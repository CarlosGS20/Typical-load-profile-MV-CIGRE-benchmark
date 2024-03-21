# Typical load profile MV CIGRE benchmark

This document describes how to obtain the MV CIGRE network consumption data described in an article for use in power system research studies. The motivation for this repository is to describe a clear method for obtaining data to replicate articles or methods in a transparent way when data is difficult to find in database form. The procedure described is also applicable to other work where data is required and displayed on graphs. 

The first step is to identify the data to be collected. In this case, Figure 9 of the article ["Modelling and Optimization in Microgrids"](https://www.mdpi.com/1996-1073/10/4/523), published in Energies by Tobias Porsinger, Przemyslaw Janik, Zbigniew Leonowicz, and Radomir Gono.

![texto cualquiera por si no carga la imagen](https://github.com/CarlosGS20/Typical-load-profile-MV-CIGRE-benchmark/blob/main/typical_profile.JPG)

The next step is to use computer vision software to help extract numerical data from the plot images, such []WebPlotDigitilizer(https://apps.automeris.io/wpd/). Thanks to this, it is possible to identify the points of the profiles to be extracted. The process is simple, as described below:

1. Load image and select 2D (X-Y) Plot.
2. Select the X-values and Y-values. In this case, Y-values are 0 and 40 MW. If the hourly sample is considered, being three consecutive days, X-value are 0 and 72 hours.
3. Select manual extraction and mark the points of the profile to be extracted: winter, transition or summer. The more points selected, the more accurate the extracted profile. 
4. Click on view data and then in download .csv.
5. A csv file with the data is now available. Perform this operation for each station separately to get all the data.


