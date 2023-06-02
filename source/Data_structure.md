# Data structure

File naming and structure are ordered under the following protocol:

/DATA/WRF/{mode}/{year}/{month}/{day}/{inicialization}/WRFDETAR_{frequency}\_{year}{month}{day}\_{inicialization}_{fhr}.nc

where fields between curly brackets are defined as: <br />
{mode} = 3 capital letters indicating the scheme used, either deterministic or ensemble (DET) <br />
{year} = 4-digit number <br />
{month} = 2-digit number <br />
{day} = 2-digit number <br />
{initialization} = 2-digit number indicating the time of the model run (00, 06, 12 or 18) <br />
{frequency} = 2-digit number indicating the temporal resolution and one letter indicating the time unit. For example, for data with 10-min frequency it takes the value 10M, for hourly data it takes the value 01H, and for daily data 24H. <br />
{fhr} = 3-digit number for lead time. For hourly data, takes values from 0 to 73 and the unit is hours. For daily data, takes values of 000, 001, 002 or 003 and the unit is days.

All times are considered in relation to Universal Time Coordinated (UTC).

Examples:
* /DATA/WRF/DET/2022/03/14/00/WRFDETAR_10M_20220314_00_012.nc corresponds to forecasts initialized on March 14, 2022 at 00 UTC for the 12-hour lead time  with a 10-min frequency. This file contains 6 times valid from 12:00UTC to 12:50UTC. 
* /DATA/WRF/DET/2022/03/14/00/WRFDETAR_01H_20220314_00_005.nc corresponds to forecasts initialized on March 14, 2022 at 00 UTC for the 05-hour lead time with 1-hour frequency. This file contains only 1 time valid for 05:00UTC.
* /DATA/WRF/DET/2022/03/14/00/WRFDETAR_24H_20220314_00_001.nc corresponds to forecasts initialized on March 14, 2022 at 00 UTC for the 05-hour lead time 
with daily frequency. This file contains only 1 time valid for March 15, 2022. 
