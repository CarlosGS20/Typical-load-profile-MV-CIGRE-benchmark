# Typical load profile MV CIGRE benchmark

This repository contains consumption and generation profiles test cases for the [CIGRE MV network (European Configuration)](https://www.e-cigre.org/publications/detail/575-benchmark-systems-for-network-integration-of-renewable-and-distributed-energy-resources.html). This network has residential and commercial loads at the nodes, whose unit profiles (for a given time period) are scaled by the rated power indicated in the report.

These residential and commercial consumption profiles, as well as the total consumption per node, are based on the per-season profiles described in the article ["Modelling and Optimization in Microgrids"](https://www.mdpi.com/1996-1073/10/4/523), published in Energies by Tobias Porsinger, Przemyslaw Janik, Zbigniew Leonowicz, and Radomir Gono. It shows profiles for weekdays, Saturday and Sunday for winter, summer and transition seasons.


# Disaggregation of general profile into commercial and residential load type

In this section a disaggregation according to typical daily profiles is proposed, related to the example 24-hour profile shown in the data of Figure 6.4 in ![MV CIGRE report](https://www.e-cigre.org/publications/detail/575-benchmark-systems-for-network-integration-of-renewable-and-distributed-energy-resources.html). This proposed disaggregation aims to identify profiles by residential and commercial load per season, because are located on the network and are given in nominal power. This is essential in order to carry out simulations and studies with coherent profiles for different seasons.  The same process described above is used to obtain the data for the 24-hour evolution figure. 



<p align="center" width="100%">
    <img src="https://github.com/CarlosGS20/Typical-load-profile-MV-CIGRE-benchmark/blob/main/typical_profile3.JPG" width="680" height="400">
</p>


The winter, summer and transition profiles are normalised according to the highest consumption, which is winter. This results in a total annual consumption profile per unit, descomposed into the 72 hours of winter, summer and transition seasons.  This profile is multiplied by the residential and commercial load per unit from the CIGRE report, resulting in the evolution of load types for typical days of the seasons. 


```python
#Read pu profile of CIGRE report
Porce_P_hour = pd.read_csv('Porce_P_hour.csv', skiprows=0) #residencial y debajo comercial
#
Porce_P_hour = np.array(Porce_P_hour)
#
#Create arrays of length equal to the number of hours set for the three days: 72 components (three days per 24 hours).
Winter_residencial = np.zeros(3*24)
Winter_comercial = np.zeros(3*24)
Summer_residencial = np.zeros(3*24)
Summer_comercial = np.zeros(3*24)
Inter_residencial = np.zeros(3*24)
Inter_comercial = np.zeros(3*24)
#
for i in range(0,3):
    for j in range(0,24):
        Winter_residencial[i*24+j] = datawinter[i*24+j,1]/max(datawinter[:,1])*Porce_P_hour[0,j]
        Winter_comercial[i*24+j] = datawinter[i*24+j,1]/max(datawinter[:,1])*Porce_P_hour[1,j]
        Summer_residencial[i*24+j] = datasummer[i*24+j,1]/max(datawinter[:,1])*Porce_P_hour[0,j]
        Summer_comercial[i*24+j] = datasummer[i*24+j,1]/max(datawinter[:,1])*Porce_P_hour[1,j]        
        Inter_residencial[i*24+j] = datainter[i*24+j,1]/max(datawinter[:,1])*Porce_P_hour[0,j]
        Inter_comercial[i*24+j] = datainter[i*24+j,1]/max(datawinter[:,1])*Porce_P_hour[1,j]      
```

Once these profiles have been obtained, they can be scaled by a certain coefficient to improve the evolution as desired (due to the digitalisation process, some minor errors or deviations may have occurred). with this, the consumption profiles are more similar to the article ["Modelling and Optimization in Microgrids"](https://www.mdpi.com/1996-1073/10/4/523). The results are as follows:


<p align="center" width="100%">
    <img src="https://github.com/CarlosGS20/Typical-load-profile-MV-CIGRE-benchmark/blob/main/Profiles_consumption_disaggregation.jpg" width="680" height="680">
</p>

Once this data is available in a numerical and fully accessible form, the total consumption at each node for each typical day can be calculated by multiplying by the nominal power of the loads of each type indicated in the CIGRE report. It is also possible to manipulate this data to perform various analyses, such as creating voltage problems at some nodes or current problems on the lines. 

[1] CIGRE Task Force C6.04: Benchmark Systems for Network Integration of Renewable and Distributed Energy Resources, May 2013. ISBN: 978-285-873-270-8.
