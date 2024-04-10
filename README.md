# Typical load profile MV CIGRE benchmark

This repository contains consumption and generation profiles test cases for the [CIGRE MV network (European Configuration)](https://www.e-cigre.org/publications/detail/575-benchmark-systems-for-network-integration-of-renewable-and-distributed-energy-resources.html). This network has residential and commercial loads at the nodes, whose unit profiles (for a given time period) are scaled by the rated power indicated in the report.

These residential and commercial consumption profiles, as well as the total consumption per node, are based on the per-season profiles described in the article ["Modelling and Optimization in Microgrids"](https://www.mdpi.com/1996-1073/10/4/523), published in Energies by Tobias Porsinger, Przemyslaw Janik, Zbigniew Leonowicz, and Radomir Gono. It shows profiles for weekdays, Saturday and Sunday for winter, summer and transition seasons.



<p align="center" width="100%">
    <img src="https://github.com/CarlosGS20/Typical-load-profile-MV-CIGRE-benchmark/blob/main/Profiles_consumption_disaggregation.jpg" width="400" height="400">
    <figcaption>{{ include.description }}</figcaption>
</p>

<figure>
  <img src="{{site.url}}/assets/image.jpg" alt="my alt text"/>
  <figcaption>This is my caption text.</figcaption>
</figure>

Once this data is available in a numerical and fully accessible form, the total consumption at each node for each typical day can be calculated by multiplying by the nominal power of the loads of each type indicated in the CIGRE report. It is also possible to manipulate this data to perform various analyses, such as creating voltage problems at some nodes or current problems on the lines. 

[1] CIGRE Task Force C6.04: Benchmark Systems for Network Integration of Renewable and Distributed Energy Resources, May 2013. ISBN: 978-285-873-270-8.
