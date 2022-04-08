# Data format

Files follow a format much used to organize multi-dimensional scientific data, the **NetCDF** (Network Common Data Form). In particular, this data follow the [CF](http://cfconventions.org/) convention. For more information on this format see this [link](https://docs.unidata.ucar.edu/netcdf-c/current/index.html).

**Map projection:** <br />
Model grid is represented in a [*Lambert conformal*](https://www2.mmm.ucar.edu/wrf/users/docs/user_guide_V3/user_guide_V3.9/users_guide_chap3.html)  projection. The center of the model grid is located at -35° latitude and -65° longitude, and the spatial resolution is approximately 4 km.

**Dimensions:**<br />
|Dimension   |Value   |
|---|---|
| time  |1   |
|y   |1249   |
|x   |999   |

**Variables:**<br />
|Variable   |Description   |Unit   |Precision   |
|---|---|---|---|
|PP   |Accumulated precipitation in a given time period   |mm   |float32   |
|HR2   |2-meter relative humidity   |%   |float32   |
|T2   |2-meter temperature (\*)   |°C   |float32   |
|dirViento10   |10-meter wind direction    |°   |float32   |
|magViento10   |10-meter wind speed (\*)   |m/s   |float32   |
|Tmax   |Daily maximum temperature (\*)   |°C   |float32   |
|Tmin   |Daily minimum temperature (\*)   |°C   |float32   |

(\*) Variables debiased using surface observations. For more information about the methodology see [Cutraro y otros, 2020](http://hdl.handle.net/20.500.12160/1405). In case of failure in the debiasing procedure, raw data will be presented instead.

For the minimum temperature (Tmin) of a given day, the value corresponds to a temperature registered between 00 and 12 UTC. For the maximum temperature (Tmax) of a given day, the value corresponds to a temperature registered between 12 and 00 UTC of the following day.

For example, the file WRFDETAR_24H_20220314_00_001.nc includes data from the 00 UTC forecasting cycle for the first forecast period (001 here represents the first day) and contains the forecast minimum temperature for the day 20220315 between 00 and 12 UTC,and the forecast maximum temperature between 12 and 00 UTC of the same day.

Precipitation PP for a given day at time P corresponds to the amount accumulated between times P-1 and P. 

For example, the file WRFDETAR_01H_20220314_00_036.nc contains data from the 00 UTC forecasting cycle for the 36th forecast hour with accumulated precipitation for day 20220315 between 11 and 12 UTC.


**Coordinate variables:**<br />
|Variable   |Description   |Unit   |Precision   |
|---|---|---|---|
|time   |Time   |Hours since the beginnig of the forecast cycle   |int   |
|y   |y coordinate  |Meters from the center of the grid   |float32   |
|x   |x coordinate  |Meters from the center of the grid   |float32   |
|lat   |Latitude   |° (between 90° y -90°)   |float32   |
|lon   |Longitude   |° (between -180° y 180°)   |float32   |
