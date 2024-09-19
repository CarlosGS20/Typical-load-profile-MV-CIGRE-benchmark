# 15-days typical year test case


This directory contains:

- [Scenario](https://github.com/CarlosGS20/Typical-load-profile-MV-CIGRE-benchmark/tree/main/5-days%20test%20case/Scenario%20B): The objective of this scenario is to analyse the congestion problem in a scenario consisting of 15 representative days. The total number of days is divided into three periods: the transition season between winter and summer, five days of winter, and finally, five days of summer. In this scenario, with the load profiles used, there are both occasional problems (lasting one or two hours) and prolonged problems (lasting up to four hours). These issues occur during the transition season  and the winter season.
- Network parameters.

The test network used is shown in the figure below, with a modification for simplicity in the modeling: the substations are replaced by two branches, 0-1 and 0-12, whose parameters are defined in the network data. 

<p align="center" width="100%">
    <img src="https://github.com/CarlosGS20/Typical-load-profile-MV-CIGRE-benchmark/blob/main/5-days%20test%20case/MV_CIGRE_grid.jpg" width="400" height="400">
</p>


\begin{table}[htb]
\caption{Value of currents (A) above the limit for each hour in overloaded lines.}
\label{Table:overload_violation}
\centering
%\scriptsize
\begin{tabular}{c c c c c c c}
\hline
Branch & t43  & t44 & t91  & t108 & t161 & t162 \\ \hline
0-1  & 29.20 & 5.71 & 52.35 & 55.55 & 60.21 & 46.63\\
3-4 & 13.97 & 11.27 & -- & -- & -- & --\\ 
3-8 & 23.30 & 23.60 & -- & -- & 14.19 & 13.60 \\ \hline
Branch & t163  & t164 & t211  & t212 & t228 & t229 \\ \hline
0-1  & 4.52  & 95.62 & 96.97 & 87.53 & 46.92 & 29.49\\
3-4 & -- & -- & 20.09 & 13.17 & -- & -- \\ 
3-8 & 11.32 & 18.12 & -- & -- & -- & --\\ \hline
\end{tabular}
\end{table}


