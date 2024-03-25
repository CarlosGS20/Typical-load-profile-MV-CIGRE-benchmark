# Typical load profile MV CIGRE benchmark

This document describes how to obtain the MV CIGRE network consumption data described in an article for use in power system research studies. The motivation for this repository is to describe a clear method for obtaining data to replicate articles or methods in a transparent way when data is difficult to find in database form. The procedure described is also applicable to other work where data is required and displayed on graphs. 

The first step is to identify the data to be collected. In this case, Figure 9 of the article ["Modelling and Optimization in Microgrids"](https://www.mdpi.com/1996-1073/10/4/523), published in Energies by Tobias Porsinger, Przemyslaw Janik, Zbigniew Leonowicz, and Radomir Gono.

![Image|100](https://github.com/CarlosGS20/Typical-load-profile-MV-CIGRE-benchmark/blob/main/typical_profile.JPG)

The next step is to use computer vision software to help extract numerical data from the plot images, such []WebPlotDigitilizer(https://apps.automeris.io/wpd/). Thanks to this, it is possible to identify the points of the profiles to be extracted. The process is simple, as described below:

1. Load image and select 2D (X-Y) Plot.
2. Select the X-values and Y-values. In this case, Y-values are 0 and 40 MW. If the hourly sample is considered, being three consecutive days, X-value are 0 and 72 hours.
3. Select manual extraction and mark the points of the profile to be extracted: winter, transition or summer. The more points selected, the more accurate the extracted profile. 
4. Click on view data and then in download .csv.
5. A csv file with the data is now available. Perform this operation for each station separately to get all the data.


The data in this file still needs to be processed before it can be used in optimisation algorithms or for network analysis, as the intervals are not regular due to the manual process of marking points. For example, we may have one data point at hour 1, another at 1.14 and at 2.2. Thus, it is essential to interpolate to obtain the power in hour one and hour 2. Python is used for this interpolation process. Although the full code is provided for use, the steps are explained below in case a user feels more comfortable with another programming language and can see the similarities. 

```python
#Read csv file with pandas
Summer = pd.read_csv('Summer.csv', skiprows=0)
Winter = pd.read_csv('Winter.csv', skiprows=0)
Inter = pd.read_csv('Inter.csv', skiprows=0)
#
#Transformation into an array for easy manipulation
Summer=np.array(Summer.loc[:,:])
Winter=np.array(Winter.loc[:,:])
Inter=np.array(Inter.loc[:,:])
#
#Create arrays of length equal to the number of hours set for the three days: 72 components and 2 row for hour and power data.
datasummer = np.zeros([72,2])
datawinter = np.zeros([72,2])
datainter = np.zeros([72,2])
```

To simplify data storage, three separate vectors are defined. In them, the time and the power value obtained in that hour are stored as a table. To obtain the values in a fixed step interval, it is necessary to interpolate. For this purpose, the function [np.interp](https://numpy.org/doc/stable/reference/generated/numpy.interp.html) is used. This function returns the one-dimensional piecewise linear interpolant to a function with given discrete data points (xp, fp), evaluated at x. 


```python
for i in range(0,72):
    y_interp = np.interp(i, Summer[:,0], Summer[:,1])
    datasummer[i,0] =  i
    datasummer[i,1] = y_interp
    y_interp = np.interp(i, Winter[:,0], Winter[:,1])
    datawinter[i,0] =  i
    datawinter[i,1] = y_interp
    y_interp = np.interp(i, Inter[:,0], Inter[:,1])
    datainter[i,0] =  i
    datainter[i,1] = y_interp    
```

Representing the winter variable (without interpolation) and the winter data interpolated at hourly intervals, the following results are obtained:

![Image|100](https://github.com/CarlosGS20/Typical-load-profile-MV-CIGRE-benchmark/blob/main/Profiles_consumption_comparison.jpg)

Thus the data of the graph is now available for use. A further step is the disaggregation of this general profile into commercial and residential profiles.


# Disaggregation of general profile into commercial and residential load type

In this section a disaggregation according to typical daily profiles is proposed, related to the example 24-hour profile shown in the data of Figure 6.4 in ![MV CIGRE report](https://www.e-cigre.org/publications/detail/575-benchmark-systems-for-network-integration-of-renewable-and-distributed-energy-resources.html). This proposed disaggregation aims to identify profiles by residential and commercial load per season, because are located on the network and are given in nominal power. This is essential in order to carry out simulations and studies with coherent profiles for different seasons.  The same process described above is used to obtain the data for the 24-hour evolution figure. 

![texto cualquiera por si no carga la imagen](https://github.com/CarlosGS20/Typical-load-profile-MV-CIGRE-benchmark/blob/main/typical_profile3.JPG)

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
        Inter_residencial[i*24+j] = datainter[i*24+j,1]/max(datainter[:,1])*Porce_P_hour[0,j]
        Inter_comercial[i*24+j] = datainter[i*24+j,1]/max(datainter[:,1])*Porce_P_hour[1,j]      
```

Once these profiles have been obtained, they can be scaled by a certain coefficient to improve the evolution as desired (due to the digitalisation process, some minor errors or deviations may have occurred). As an example, for the proposed case, the winter and summer profiles are slightly increased and the transition season is reduced in order to obtain, in general, evolutions as similar as possible to the article ["Modelling and Optimization in Microgrids"](https://www.mdpi.com/1996-1073/10/4/523). The results are as follows:

![texto cualquiera por si no carga la imagen](https://github.com/CarlosGS20/Typical-load-profile-MV-CIGRE-benchmark/blob/main/Profiles_consumption_disaggregation.jpg)

Once this data is available in a numerical and fully accessible form, the total consumption at each node for each typical day can be calculated by multiplying by the nominal power of the loads of each type indicated in the CIGRE report. It is also possible to manipulate this data to perform various analyses, such as creating voltage problems at some nodes or current problems on the lines. 

