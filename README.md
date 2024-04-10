# Typical load profile MV CIGRE benchmark

This repository contains consumption and generation profiles test cases for the [CIGRE MV network (European Configuration)](https://www.e-cigre.org/publications/detail/575-benchmark-systems-for-network-integration-of-renewable-and-distributed-energy-resources.html). This network has residential and commercial loads at the nodes, whose unit profiles (for a given time period) are scaled by the rated power indicated in the report. Network parameters are also available in [Pandapower](https://pandapower.readthedocs.io/en/v2.1.0/networks/cigre.html)

These residential and commercial consumption profiles, as well as the total consumption per node, are based on the per-season profiles described in the article ["Modelling and Optimization in Microgrids"](https://www.mdpi.com/1996-1073/10/4/523), published in Energies by Tobias Porsinger, Przemyslaw Janik, Zbigniew Leonowicz, and Radomir Gono. It shows profiles for weekdays, Saturday and Sunday for winter, summer and transition seasons. The unit profiles for each load type and season used are shown in the figure below:


<p align="center" width="100%">
    <img src="https://github.com/CarlosGS20/Typical-load-profile-MV-CIGRE-benchmark/blob/main/Profiles_consumption_disaggregation.jpg" width="400" height="400">
</p>


### Directory Content

This repository contains:

- [5-days test cases](https://github.com/CarlosGS20/Typical-load-profile-MV-CIGRE-benchmark/tree/main/5-days%20test%20case): This case is based on winter consumption profiles. It consists of 5 days formed by the sequence of two weekdays, Saturday, Sunday and another weekday.

