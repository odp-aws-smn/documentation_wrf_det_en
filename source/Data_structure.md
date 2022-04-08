# Data structure

File naming and structure are ordered under the following protocol:

/DATA/WRF/{mode}/{year}/{month}/{day}/{cycle}/WRFDETAR_{frequency}H_{year}{month}{day}\_{cycle}_{fhr}.nc

Where fields between curly brackets are defined as: <br />

{mode} = 3 capital letters indicating the scheme used, either deterministic or ensemble (DET o ENS) <br />
{year} = 4-digit number <br />
{month} = 2-digit number <br />
{day} = 2-digit number <br />
{cycle} = 2-digit number indicating the model run <br />
{frequency} = 2-digit number indicating the temporal resolution. For hourly data it takes the value 01, and for daily data 24. <br />
{fhr} = 3-digit number for lead time. If frequency is 01H the lead time is in hours, if frequency is 24H is in days. 

Examples:
* /DATA/WRF/DET/2022/03/14/00/WRFDETAR_01H_20220314_00_005.nc corresponds to forecasts of hourly data initialized on 14th March 2022 00 UTC for lead time hours 05. 
* /DATA/WRF/DET/2022/03/14/00/WRFDETAR_24H_20220314_00_001.nc corresponds to forecasts of daily data initialized on 14th March 2022 00 UTC for lead time day 01. 
