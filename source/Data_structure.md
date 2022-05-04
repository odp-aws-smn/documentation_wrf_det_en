# Data structure

File naming and structure are ordered under the following protocol:

/DATA/WRF/{mode}/{year}/{month}/{day}/{inicialization}/WRFDETAR_{frequency}H_{year}{month}{day}\_{inicialization}_{fhr}.nc

where fields between curly brackets are defined as: <br />
{mode} = 3 capital letters indicating the scheme used, either deterministic or ensemble (DET) <br />
{year} = 4-digit number <br />
{month} = 2-digit number <br />
{day} = 2-digit number <br />
{initialization} = 2-digit number indicating the time of the model run (00 or 12) <br />
{frequency} = 2-digit number indicating the temporal resolution. For hourly data it takes the value 01, and for daily data 24. <br />
{fhr} = 3-digit number for lead time. For hourly data, takes values from 0 to 73 and the unit is hours. For daily data, takes values of 000, 001, 002 or 003 and the unit is days.

All times are considered in relation to Universal Time Coordinated (UTC).

Examples:
* /DATA/WRF/DET/2022/03/14/00/WRFDETAR_01H_20220314_00_005.nc corresponds to forecasts of hourly data initialized on 14th March 2022 00 UTC for lead time hours 05. 
* /DATA/WRF/DET/2022/03/14/00/WRFDETAR_24H_20220314_00_001.nc corresponds to forecasts of daily data initialized on 14th March 2022 00 UTC for lead time day 01. 
